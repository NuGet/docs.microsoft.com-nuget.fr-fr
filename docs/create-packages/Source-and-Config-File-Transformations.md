---
title: Transformations de fichiers sources et de configuration pour les packages NuGet
description: Informations sur la possibilité pour les packages NuGet de transformer des fichiers de code source et de configuration (XML) à l’installation.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 7d011e9924f37175815efa70f5ae1947fb256912
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817643"
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformation de fichiers de code source et de configuration

Pour les projets utilisant `packages.config`, NuGet offre la possibilité d’effectuer des transformations sur les fichiers de code source et de configuration au moment de l’installation et de la désinstallation des packages. Seules les transformations du code source sont appliquées en cas d’installation d’un package dans un projet avec [PackageReference](../consume-packages/package-references-in-project-files.md).

Une **transformation de code source** applique un remplacement unilatéral des jetons aux fichiers inclus dans le dossier `content` ou `contentFiles` (`content` pour les clients utilisant `packages.config` et `contentFiles` pour `PackageReference`) au moment où le package est installé, où les jetons font référence aux [propriétés de projet](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) Visual Studio. Ainsi, vous pouvez insérer un fichier dans l’espace de noms du projet, ou bien personnaliser du code qui irait normalement dans `global.asax` dans un projet ASP.NET.

Une **transformation de fichier de configuration** vous permet de modifier des fichiers qui existent déjà dans un projet cible, comme `web.config` et `app.config`. Par exemple, votre package peut avoir besoin d’ajouter un élément à la section `modules` dans le fichier de configuration. Cette transformation est effectuée en incluant des fichiers spéciaux dans le package qui décrivent les sections à ajouter aux fichiers de configuration. Lorsqu’un package est désinstallé, ces mêmes modifications sont alors annulées, ce qui en fait une transformation bidirectionnelle.

## <a name="specifying-source-code-transformations"></a>Spécification de transformations de code source

1. Les fichiers que vous voulez insérer à partir du package dans le projet doivent se trouver dans les dossiers `content` et `contentFiles` du package. Par exemple, si vous voulez installer un fichier appelé `ContosoData.cs` dans un dossier `Models` du projet cible, il doit se trouver à l’intérieur des dossiers `content\Models` et `contentFiles\{lang}\{tfm}\Models` dans le package.

1. Pour demander à NuGet d’appliquer un remplacement des jetons au moment de l’installation, ajoutez `.pp` au nom du fichier de code source. Après l’installation, le fichier ne porte pas l’extension `.pp`.

    Par exemple, pour effectuer des transformations dans `ContosoData.cs`, nommez le fichier dans le package `ContosoData.cs.pp`. Après l’installation, il s’affiche en tant que `ContosoData.cs`.

1. Dans le fichier de code source, utilisez des jetons ne respectant pas la casse sous la forme `$token$` pour indiquer les valeurs que NuGet doit remplacer par les propriétés de projet :

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Lors de l’installation, NuGet remplace `$rootnamespace$` par `Fabrikam` en supposant que le projet cible a pour espace de noms racine `Fabrikam`.

Le jeton `$rootnamespace$` est la propriété de projet la plus souvent utilisée ; toutes les autres sont listés dans la documentation sur les [propriétés de projet](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). N’oubliez pas, évidemment, que certaines propriétés peuvent être spécifiques du type de projet.

## <a name="specifying-config-file-transformations"></a>Spécification de transformations de fichiers de configuration

Comme décrit dans les sections qui suivent, les transformations de fichiers de configuration peuvent être effectuées de deux manières :

- Incluez des fichiers `app.config.transform` et `web.config.transform` dans le dossier `content` de votre package, où l’extension `.transform` indique à NuGet que ces fichiers contiennent le code XML à fusionner avec les fichiers de configuration existants lors de l’installation du package. Lorsqu’un package est désinstallé, ce même code XML est supprimé.
- Incluez les fichiers `app.config.install.xdt` et `web.config.install.xdt` dans le dossier `content` de votre package en utilisant la [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx) pour décrire les changements souhaités. Avec cette option, vous pouvez également inclure un fichier `.uninstall.xdt` pour annuler ces modifications lorsque le package est supprimé d’un projet.

> [!Note]
> Les transformations ne sont pas appliquées aux fichiers `.config` référencés sous forme de lien dans Visual Studio.

L’avantage d’utiliser la syntaxe XDT est qu’au lieu de simplement fusionner deux fichiers statiques, elle permet de manipuler la structure d’un DOM XML en faisant correspondre éléments et attributs à l’aide d’une prise en charge XPath complète. La syntaxe XDT permet alors d’ajouter, de mettre à jour ou de supprimer des éléments, de placer de nouveaux éléments à un emplacement spécifique ou de remplacer/supprimer des éléments (y compris des nœuds enfants). La création de transformations de désinstallation qui reviennent sur toutes les transformations effectuées pendant l’installation du package est ainsi facilitée.

### <a name="xml-transforms"></a>Transformations XML

Les fichiers `app.config.transform` et `web.config.transform` du dossier `content` d’un package contiennent uniquement les éléments à fusionner dans les fichiers `app.config` et `web.config` existants du projet.

Par exemple, supposons que le projet contienne initialement ce qui suit dans `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Pour ajouter un élément `MyNuModule` à la section `modules` lors de l’installation d’un package, créez un fichier `web.config.transform` dans le dossier `content` du package qui ressemble à ceci :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Une fois que NuGet a installé le package, `web.config` apparaît comme suit :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Notez que NuGet n’a pas remplacé la section `modules`, mais y a simplement fusionné la nouvelle entrée en ajoutant uniquement de nouveaux éléments et attributs. NuGet ne modifie pas les éléments ou attributs existants.

Lorsque le package est désinstallé, NuGet réexamine les fichiers `.transform` et supprime les éléments qu’ils contiennent provenant des fichiers `.config` appropriés. Notez que ce processus n’affecte pas les lignes du fichier `.config` que vous modifiez après l’installation du package.

Comme un exemple plus complet, le package [Gestionnaires et modules d’enregistrement des erreurs (ELMAH) pour ASP.NET](https://www.nuget.org/packages/elmah/) ajoute de nombreuses entrées dans `web.config`, qui sont de nouveau supprimées lors de la désinstallation d’un package.

Pour examiner son fichier `web.config.transform`, téléchargez le package ELMAH à partir du lien ci-dessus, remplacez l’extension du package `.nupkg` par `.zip`, puis ouvrez `content\web.config.transform` dans ce fichier ZIP.

Pour voir l’effet de l’installation et de la désinstallation du package, créez un projet ASP.NET dans Visual Studio (le modèle est disponible sous **Visual C# > Web** dans la boîte de dialogue Nouveau projet), puis sélectionnez une application ASP.NET vide. Ouvrez `web.config` pour voir son état initial. Ensuite, cliquez sur le projet, sélectionnez **Gérer les packages NuGet**, recherchez ELMAH sur nuget.org et installez la version la plus récente. Remarquez toutes les modifications apportées à `web.config`. Désinstallez maintenant le package : `web.config` reviendra à son état antérieur.

### <a name="xdt-transforms"></a>Transformations XDT

Vous pouvez modifier des fichiers de configuration en utilisant la [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx). Vous pouvez également demander à NuGet de remplacer les jetons par des [propriétés de projet](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) en plaçant leur nom entre les délimiteurs `$` (sans respecter la casse).

Par exemple, le fichier `app.config.install.xdt` suivant insère un élément `appSettings` dans `app.config` qui contient les valeurs `FullPath`, `FileName` et `ActiveConfigurationSettings` du projet :

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Autre exemple, supposons que le projet contienne initialement ce qui suit dans `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Pour ajouter un élément `MyNuModule` à la section `modules` pendant l’installation du package, le fichier `web.config.install.xdt` du package doit contenir ce qui suit :

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Après avoir installé le package, `web.config` ressemble à ceci :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Pour supprimer uniquement l’élément `MyNuModule` pendant la désinstallation du package, le fichier `web.config.uninstall.xdt` doit contenir ce qui suit :

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
