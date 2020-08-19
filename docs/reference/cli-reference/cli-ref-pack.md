---
title: Commande du Pack de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622952"
---
# <a name="pack-command-nuget-cli"></a>commande Pack (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge** pour la création de package : 2.7 +

Crée un package NuGet basé sur le fichier [. NuSpec](../nuspec.md) ou le fichier projet spécifié. La `dotnet pack` commande (consultez les [commandes dotnet](../dotnet-Commands.md)) et `msbuild -t:pack` (voir [cibles MSBuild](../msbuild-targets.md)) peut être utilisée comme variantes.

> [!Important]
> Utilisez [`dotnet pack`](../dotnet-Commands.md) ou [`msbuild -t:pack`](../msbuild-targets.md) pour les projets basés sur [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> Sous mono, la création d’un package à partir d’un fichier projet n’est pas prise en charge. Vous devez également ajuster les chemins non locaux dans le `.nuspec` fichier aux chemins de style UNIX, car nuget.exe ne convertit pas les chemins Windows eux-mêmes.

## <a name="usage"></a>Usage

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

où `<nuspecPath>` et `<projectPath>` spécifient `.nuspec` respectivement le fichier projet ou.

## <a name="options"></a>Options
- **`-BasePath`**

   Définit le chemin d’accès de base des fichiers définis dans le fichier [. NuSpec](../nuspec.md) .

- **`-Build`**

  Spécifie que le projet doit être généré avant de générer le package.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-Exclude`**

  Spécifie un ou plusieurs modèles de caractères génériques à exclure lors de la création d’un package. Pour spécifier plusieurs modèles, répétez l’indicateur-Exclude. Voir l’exemple ci-dessous.

- **`-ExcludeEmptyDirectories`**

  Empêche l’inclusion de répertoires vides lors de la génération du package.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-IncludeReferencedProjects`**

  Indique que le package généré doit inclure des projets référencés en tant que dépendances ou dans le cadre du package. Si un projet référencé a un fichier correspondant `.nuspec` portant le même nom que le projet, ce projet référencé est ajouté en tant que dépendance. Dans le cas contraire, le projet référencé est ajouté dans le cadre du package.

- **`-InstallPackageToOutputPath`**

  Spécifiez si la commande doit préparer le répertoire de sortie du package pour prendre en charge le partage en tant que flux.

- **`-MinClientVersion`**

  Définissez l’attribut *minClientVersion* pour le package créé. Cette valeur remplace la valeur de l’attribut *minClientVersion* existant (le cas échéant) dans le `.nuspec` fichier.

- **`-MSBuildPath`**

  *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande, prioritaire sur `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild.

- **`-NoDefaultExcludes`**

  Empêche l’exclusion par défaut des fichiers de package NuGet et des fichiers et dossiers commençant par un point, comme `.svn` et `.gitignore` .

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-NoPackageAnalysis`**

  Spécifie que le pack ne doit pas exécuter d’analyse du package après sa génération.

- **`-OutputDirectory`**

  Spécifie le dossier dans lequel le package créé est stocké. Si aucun dossier n’est spécifié, le dossier actif est utilisé.

- **`-OutputFileNamesWithoutVersion`**

  Spécifiez si la commande doit préparer le nom de la sortie du package sans la version.

- **`-PackagesDirectory`**

  Spécifie le dossier Packages.

- **`-p|-Properties`**

  Doit apparaître en dernier sur la ligne de commande après d’autres options. Spécifie une liste de propriétés qui remplacent les valeurs du fichier projet ; consultez les [Propriétés communes des projets MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) pour les noms de propriété. L’argument Properties ici est une liste de paires jeton = valeur, séparées par des points-virgules, où chaque occurrence de `$token$` dans le `.nuspec` fichier sera remplacée par la valeur donnée. Les valeurs peuvent être des chaînes entre guillemets. Notez que, pour la propriété « configuration », la valeur par défaut est « Debug ». Pour passer à une configuration Release, utilisez `-Properties Configuration=Release` . **En général**, les propriétés doivent être identiques à celles utilisées lors de la génération du projet correspondant, afin d’éviter un comportement potentiellement étrange.

- **`-SolutionDirectory`**

  Spécifie le répertoire de la solution.

- **`-Suffix`**

  *(3.4.4 +)* Ajoute un suffixe au numéro de version généré en interne, généralement utilisé pour ajouter la build ou d’autres identificateurs de préversion. Par exemple, l’utilisation de `-suffix nightly` crée un package avec un numéro de version comme `1.2.3-nightly` . Les suffixes doivent commencer par une lettre pour éviter les avertissements, les erreurs et les incompatibilités potentielles avec les différentes versions de NuGet et du gestionnaire de package NuGet.

- **`-SymbolPackageFormat`**

  Lorsque vous créez un package de symboles, permet de choisir entre le `snupkg` `symbols.nupkg` format et.

- **`-Symbols`**

  Spécifie que le package contient des sources et des symboles. Lorsqu’il est utilisé avec un `.nuspec` fichier, cela crée un fichier de package NuGet standard et le package de symboles correspondant. Par défaut, il crée un [package de symboles hérité](../../create-packages/Symbol-Packages.md). Le nouveau format recommandé pour les packages de symboles est .snupkg. Consultez [Création de packages de symboles (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).

- **`-Tool`**

   Spécifie que les fichiers de sortie du projet doivent être placés dans le `tool` dossier.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

- **`-Version`**

  Remplace le numéro de version du `.nuspec` fichier.

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Exclusion des dépendances de développement

Certains packages NuGet sont utiles en tant que dépendances de développement, qui vous aident à créer votre propre bibliothèque, mais qui ne sont pas nécessairement nécessaires en tant que dépendances de package réelles.

La `pack` commande ignore les `package` entrées dans `packages.config` dont l' `developmentDependency` attribut a la valeur `true` . Ces entrées ne sont pas incluses en tant que dépendances dans le package créé.

Par exemple, considérez le `packages.config` fichier suivant dans le projet source :

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Pour ce projet, le package créé par `nuget pack` aura une dépendance sur `jQuery` et, `microsoft-web-helpers` mais pas sur `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Suppression des avertissements de Pack

Bien qu’il soit recommandé de résoudre tous les avertissements NuGet au cours de vos opérations de Pack, il est justifié, dans certains cas, de les supprimer.

Vous pouvez obtenir cela de la façon suivante : 

> Package nuget.exe Pack. NuSpec-Properties nowarn = NU5104

## <a name="examples"></a>Exemples

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
