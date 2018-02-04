---
title: Commandes pack et restore NuGet comme cibles MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+."
keywords: NuGet et MSBuild, cible pack NuGet, cible restore NuGet
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Commandes pack et restore NuGet comme cibles MSBuild

*NuGet 4.0+*

Avec le format PackageReference, NuGet 4.0 + peut stocker des métadonnées du manifeste tout directement dans un fichier projet au lieu d’utiliser un distinct `.nuspec` fichier.

Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous. Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild. (Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../tools/cli-ref-pack.md) et [restore](../tools/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)

## <a name="target-build-order"></a>Ordre de génération des cibles

Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail. Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression. Pour ce faire, ajoutez le code suivant dans votre fichier projet :

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.

## <a name="pack-target"></a>Cible pack

Lors de l’utilisation de la cible de pack, autrement dit, `msbuild /t:pack`, MSBuild dessine ses entrées dans le fichier projet. Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier de projet dans le premier `<PropertyGroup>` nœud. Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel. Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../reference/nuspec.md).

Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.

| Valeur d’attribut/NuSpec | Propriété MSBuild | Par défaut | Notes |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) de MSBuild |
| Version | PackageVersion | Version | Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 » |
| VersionPrefix | PackageVersionPrefix | vide | La définition de PackageVersion remplace PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | vide | $(VersionSuffix) de MSBuild. La définition de PackageVersion remplace PackageVersionSuffix |
| Auteurs | Auteurs | Nom de l’utilisateur actuel | |
| Propriétaires | N/A | Ne figure pas dans NuSpec | |
| Titre | Titre | PackageId| |
| Description | Description | « Description du package » | |
| Copyright | Copyright | vide | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| LicenseUrl | PackageLicenseUrl | vide | |
| ProjectUrl | PackageProjectUrl | vide | |
| IconUrl | PackageIconUrl | vide | |
| Balises | PackageTags | vide | Les balises sont séparées par un point-virgule. |
| ReleaseNotes | PackageReleaseNotes | vide | |
| RepositoryUrl | RepositoryUrl | vide | |
| RepositoryType | RepositoryType | vide | |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Récapitulatif | Non pris en charge | | |

### <a name="pack-target-inputs"></a>entrées de cible pack

- IsPackable
- PackageVersion
- PackageId
- Auteurs
- Description
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>Scénarios avec pack

### <a name="packageiconurl"></a>PackageIconUrl

Dans le cadre du changement lié au [problème NuGet 2582](https://github.com/NuGet/Home/issues/2582), la propriété `PackageIconUrl` sera finalement remplacée par `PackageIconUri` et peut être un chemin relatif vers un fichier icône qui sera inclus à la racine du package obtenu.

### <a name="output-assemblies"></a>Assemblys de sortie

`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`. Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.

Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :

- `IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.
- `BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés. Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.

### <a name="package-references"></a>Références de package

Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Références entre projets

Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Ajout de contenu dans un package

Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`. Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier. Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.

`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule. La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package. Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`. Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.

D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.

> [!Note]
> Outre les éléments de contenu, le `<Pack>` et `<PackagePath>` métadonnées peuvent également être définies sur les fichiers avec une action de génération de la compilation, EmbeddedResource, ApplicationDefinition, Page, ressources, écran de démarrage, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.
>
> Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.

### <a name="includesymbols"></a>IncludeSymbols

Quand vous utilisez `MSBuild /t:pack /p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.

### <a name="includesource"></a>IncludeSource

Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`. Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu. La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.

Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Lors de l’utilisation de `MSBuild /t:pack /p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`. Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.

### <a name="packing-using-a-nuspec"></a>Compression à l’aide d’un fichier .nuspec

Vous pouvez utiliser un fichier `.nuspec` pour compresser votre projet à condition que vous ayez un fichier projet pour importer `NuGet.Build.Tasks.Pack.targets` afin que la tâche de compression puisse être exécutée. Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :

1. `NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.
1. `NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule. En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath` : chemin de base pour le fichier `.nuspec`.

Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a>Cible restore

`MSBuild /t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :

1. Lire toutes les références entre projets
1. Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework
1. Passer des données msbuild à NuGet.Build.Tasks.dll
1. Exécuter la restauration
1. Télécharger les packages
1. Écrire le fichier de ressources, les cibles et les propriétés

### <a name="restore-properties"></a>Propriétés de restauration

Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet. Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `/p:` (consultez Exemples ci-dessous).

| Propriété | Description |
|--------|--------|
| RestoreSources | Liste de sources de packages séparées par un point-virgule. |
| RestorePackagesPath | Chemin du dossier de packages de l’utilisateur. |
| RestoreDisableParallel | Limite les téléchargements à un à la fois. |
| RestoreConfigFile | Chemin à un fichier `Nuget.Config` à appliquer. |
| RestoreNoCache | Si la valeur est true, permet d’éviter l’utilisation du cache web. |
| RestoreIgnoreFailedSources | Si la valeur est true, ignore les sources de packages défectueuses ou manquantes. |
| RestoreTaskAssemblyFile | Chemin d’accès à `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus. |
| RestoreOutputPath | Dossier de sortie qui est par défaut le dossier `obj`. |

#### <a name="examples"></a>Exemples

Ligne de commande :

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

Fichier projet :

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>Sorties de restauration

La restauration crée les fichiers suivants dans le dossier `obj` de build :

| Fichier | Description |
|--------|--------|
| `project.assets.json` | Précédemment `project.lock.json` |
| `{projectName}.projectFileExtension.nuget.g.props` | Références à des propriétés MSBuild contenues dans des packages |
| `{projectName}.projectFileExtension.nuget.g.targets` | Références à des cibles MSBuild contenues dans des packages |

### <a name="packagetargetfallback"></a>PackageTargetFallback

L’élément `PackageTargetFallback` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages. Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../reference/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet. Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.

Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue. Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`. Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Remplacement d’une bibliothèque à partir d’un graphique de restauration

Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix. Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
