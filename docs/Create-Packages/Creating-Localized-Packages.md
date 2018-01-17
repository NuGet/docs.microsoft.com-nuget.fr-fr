---
title: "Guide pratique pour créer un package NuGet localisé | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 824c3f45-c6c2-4c82-9d6d-62a19bfdc4a4
description: "Informations sur les deux façons de créer des packages NuGet localisés, soit en incluant tous les assemblys dans un package unique, soit en publiant des assemblys séparés."
keywords: "Localisation de packages NuGet, assemblys satellites NuGet, création de packages localisés, conventions de localisation NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aa48e77bd0e64cf45292687a2d4cada198ff5749
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-localized-nuget-packages"></a>Création de packages NuGet localisés

Il existe deux façons de créer des versions localisées d’une bibliothèque :

1. Incluez tous les assemblys de ressources localisés dans un package unique.
2. Créez des packages satellites localisés distincts (NuGet 1.8 et version ultérieure), en suivant un ensemble strict de conventions.

Les deux méthodes ont leurs avantages et leurs inconvénients, comme décrit dans les sections suivantes.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Assemblys de ressources localisés dans un package unique

L’inclusion des assemblys de ressources localisés dans un package unique constitue généralement l’approche la plus simple. Pour cela, créez des dossiers dans `lib` pour la langue prise en charge autre que celle par défaut du package (supposée être en-us). Dans ces dossiers, vous pouvez placer des assemblys de ressources et des fichiers XML IntelliSense localisés.

Par exemple, la structure de dossiers suivante prend en charge l’allemand (de), l’italien (it), le japonais (ja), le russe (ru), le chinois simplifié (zh-Hans) et le chinois traditionnel (zh-Hant) :

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Vous pouvez voir que les langues sont toutes répertoriées sous le dossier de la version cible de .Net Framework `net40`. Si vous [prenez en charge plusieurs frameworks](../create-packages/supporting-multiple-target-frameworks.md), vous avez un dossier sous `lib` pour chaque variante.

Avec ces dossiers en place, vous allez ensuite référencer tous les fichiers dans votre `.nuspec` :

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

[Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0) est un exemple de package qui utilise cette approche.

### <a name="advantages-and-disadvantages"></a>Avantages et inconvénients

Le regroupement de toutes les langues dans un package unique présente quelques inconvénients :

1. **Métadonnées partagées** : étant donné qu’un package NuGet peut uniquement contenir un seul fichier `.nuspec`, vous pouvez fournir les métadonnées d’une seule langue. Autrement dit, NuGet ne prend pas encore en charge les métadonnées localisées.
2. **Taille du package** : selon le nombre de langues que vous prenez en charge, la bibliothèque peut devenir très volumineuse, ce qui ralentit l’installation et la restauration du package.
3. **Versions simultanées** : le regroupement des fichiers localisés dans un package unique exige la publication simultanée de toutes les ressources dans ce package, au lieu de la publication de chaque localisation séparément. De plus, toute mise à jour d’une localisation exige une nouvelle version de la totalité du package.

Toutefois, il a également quelques avantages :

1. **Simplicité** : les consommateurs du package obtiennent toutes les langues prises en charge dans une installation unique, au lieu de devoir installer chaque langue séparément. Un package unique est également plus facile à trouver sur nuget.org.
2. **Versions couplées** : étant donné que tous les assemblys de ressources se trouvent dans le même package que l’assembly principal, ils partagent tous le même numéro de version et ne courent pas le risque d’être découplés par erreur.


## <a name="localized-satellite-packages"></a>Packages satellites localisés

Semblable à la manière dont .NET Framework prend en charge les assemblys satellites, cette méthode sépare les ressources localisées et les fichiers XML IntelliSense dans des packages satellites.

Pour cela, votre package principal utilise la convention de nommage `{identifier}.{version}.nupkg` et contient l’assembly de la langue par défaut (par exemple, en-US). Par exemple, `ContosoUtilities.1.0.0.nupkg` contiendrait la structure suivante :

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Un assembly satellite utilise alors la convention de nommage `{identifier}.{language}.{version}.nupkg`, comme `ContosoUtilities.de.1.0.0.nupkg`. L’identificateur **doit** correspondre exactement à celui du package principal.

Comme il s’agit d’un package distinct, il possède son propre fichier `.nuspec` qui contient des métadonnées localisées. N’oubliez pas que la langue dans le fichier `.nuspec` **doit** correspond à celle utilisée dans le nom de fichier.

L’assembly satellite **doit** également déclarer une version exacte du package principal en tant que dépendance, à l’aide de la notation de version [] \(consultez [Gestion des versions de package](../reference/package-versioning.md)). Par exemple, `ContosoUtilities.de.1.0.0.nupkg` doit déclarer une dépendance vis-à-vis de `ContosoUtilities.1.0.0.nupkg` à l’aide de la notation `[1.0.0]`. Le package satellite peut, bien entendu, avoir un numéro de version différent de celui du package principal.

La structure du package satellite doit alors inclure l’assembly de ressources et le fichier XML IntelliSense dans un sous-dossier qui correspond à `{language}` dans le nom de fichier du package :

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Remarque** : sauf si des sous-cultures spécifiques comme `ja-JP` sont nécessaires, utilisez toujours l’identificateur de langue le plus général, comme `ja`.

Dans un assembly satellite, NuGet reconnaît **uniquement** les fichiers inclus dans le dossier qui correspond à `{language}` dans le nom de fichier. Tous les autres sont ignorés.

Lorsque toutes ces conventions sont respectées, NuGet reconnaît le package en tant que package satellite et installe les fichiers localisés dans le dossier `lib` du package principal, comme s’ils avaient été regroupés à l’origine. La désinstallation du package satellite permet de supprimer ses fichiers de ce même dossier.

Vous créez d’autres assemblys satellites de la même façon pour chaque langue prise en charge. Pour obtenir un exemple, examinez l’ensemble de packages MVC ASP.NET :

* [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (anglais principal)
* [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (allemand)
* [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonais)
* [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chinois (simplifié))
* [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chinois (traditionnel))

### <a name="summary-of-required-conventions"></a>Résumé des conventions obligatoires

- Le package principal doit être nommé `{identifier}.{version}.nupkg`.
- Un package satellite doit être nommé `{identifier}.{language}.{version}.nupkg`.
- Le fichier `.nuspec` d’un package satellite doit spécifier sa langue pour correspondre au nom de fichier.
- Un package satellite doit déclarer une dépendance vis-à-vis d’une version exacte du package principal à l’aide de la notation [] dans son fichier `.nuspec`. Les plages ne sont pas prises en charge.
- Un package satellite doit placer des fichiers dans le dossier `lib\[{framework}\]{language}` qui correspondent exactement à `{language}` dans le nom de fichier.

### <a name="advantages-and-disadvantages"></a>Avantages et inconvénients

L’utilisation de packages satellites présente quelques avantages :

1. **Taille du package** : l’encombrement global du package principal est réduit et les consommateurs payent uniquement les coûts de chaque langue qu’ils souhaitent utiliser.
2. **Métadonnées distinctes** : chaque package satellite possède son propre fichier `.nuspec` et, par conséquent, ses propres métadonnées localisées. Cela peut permettre à certains consommateurs de trouver plus facilement des packages sur nuget.org en utilisant des termes localisés.
3. **Versions découplées** : il est possible de publier les assemblys satellites progressivement, plutôt que tous en même temps, ce qui vous permet d’étaler vos efforts de localisation.

Néanmois, les packages satellites présentent aussi quelques inconvénients :

1. **Multiplicité** : au lieu d’un package unique, vous avez de nombreux packages pouvant engendrer des résultats de recherche confus sur nuget.org et une longue liste de références dans un projet Visual Studio.
2. **Conventions strictes**. Les packages satellites doivent suivre les conventions à la lettre sans quoi les versions localisées ne sont pas correctement sélectionnées.
3. **Gestion de versions** : chaque package satellite doit avoir une dépendance de version exacte vis-à-vis du package principal. Cela signifie que la mise à jour du package principal peut nécessiter celle de tous les packages satellites également, même si les ressources n’ont pas changé.
