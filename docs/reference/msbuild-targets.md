---
title: Commandes pack et restore NuGet comme cibles MSBuild
description: Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: e922da94a02450d4ea476c828209fa0cd4305725
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Commandes pack et restore NuGet comme cibles MSBuild

*NuGet 4.0+*

Avec le format PackageReference, NuGet 4.0+ peut stocker toutes les métadonnées du manifeste directement dans un fichier projet, au lieu d’utiliser un fichier `.nuspec` distinct.

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

Pour les projets .NET Standard en utilisant le format PackageReference, à l’aide de `msbuild /t:pack` dessine des entrées à partir du fichier de projet à utiliser pour créer un package NuGet.

Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier projet au sein du premier nœud `<PropertyGroup>`. Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel. Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../reference/nuspec.md).

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
| Description | PackageDescription | « Description du package » | |
| Copyright | Copyright | vide | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| LicenseUrl | PackageLicenseUrl | vide | |
| ProjectUrl | PackageProjectUrl | vide | |
| IconUrl | PackageIconUrl | vide | |
| Balises | PackageTags | vide | Les balises sont séparées par un point-virgule. |
| ReleaseNotes | PackageReleaseNotes | vide | |
| Url du référentiel / | RepositoryUrl | vide | URL de référentiel permettant de cloner ou extraire le code source. Exemple : *https://github.com/NuGet/NuGet.Client.git* |
| / Type de référentiel | RepositoryType | vide | Type de référentiel. Exemples : *git*, *tfs*. |
| Branche du référentiel / | RepositoryBranch | vide | Informations de branche de référentiel facultatif. *RepositoryUrl* doit également être spécifié pour cette propriété à inclure. Exemple : *master* (NuGet 4.7.0+) |
| Référentiel/validation | RepositoryCommit | vide | Validation du référentiel facultatif ou l’ensemble de modifications pour indiquer le package de la source qui a été généré. *RepositoryUrl* doit également être spécifié pour cette propriété à inclure. Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
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
- RepositoryBranch
- RepositoryCommit
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

Dans le cadre de la modification de [NuGet problème 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sera modifiée par la suite en `PackageIconUri` et peut être un chemin relatif à un fichier d’icône qui seront inclus à la racine du package qui en résulte.

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
> Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.
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

Vous pouvez utiliser un `.nuspec` fichier de pack de votre projet si vous disposez d’un fichier de projet de kit de développement logiciel pour importer `NuGet.Build.Tasks.Pack.targets` afin que la tâche pack peut être exécutée. Vous devez toujours restaurer le projet avant que vous pouvez choisir un fichier nuspec. Le framework cible du fichier projet n’est pas pertinent et pas utilisé lors de la livraison d’un nuspec. Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :

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

Notez qu’un nuspec de livraison à l’aide de dotnet.exe ou msbuild d’accéder à générer le projet par défaut. Cela peut être évité en passant ```--no-build``` dotnet.exe, qui est l’équivalent du paramètre de propriété ```<NoBuild>true</NoBuild> ``` dans votre fichier projet, en même temps que le paramètre ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` dans le fichier projet

Un exemple d’un fichier csproj compresser un fichier nuspec est :

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Avancée des points d’extension pour créer le package personnalisé

Le `pack` cible fournit deux points d’extension qui s’exécutent dans cette build spécifique du framework cible interne. Les points d’extension prise en charge de contenu spécifique du framework cible et d’assemblys dans un package :

- `TargetsForTfmSpecificBuildOutput` cible : utilisation de fichiers à l’intérieur du `lib` dossier ou un dossier spécifié à l’aide de `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` cible : utilisation de fichiers en dehors de la `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Écrire une cible personnalisée et le spécifier en tant que la valeur de la `$(TargetsForTfmSpecificBuildOutput)` propriété. Pour tous les fichiers qui doivent passer dans le `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans l’élément ItemGroup `BuildOutputInPackage` et définir les deux valeurs de métadonnées suivantes :

- `FinalOutputPath`: Le chemin d’accès absolu du fichier ; Si n’est fourni, l’identité est utilisée pour évaluer le chemin d’accès source.
- `TargetPath`: (Facultatif) définir lorsque le fichier doit aller dans un sous-dossier dans `lib\<TargetFramework>` , telles que les assemblys satellites vont sous leurs dossiers de culture respectifs. Par défaut, le nom du fichier.

Exemple :

```
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Écrire une cible personnalisée et le spécifier en tant que la valeur de la `$(TargetsForTfmSpecificContentInPackage)` propriété. Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans l’élément ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes :

- `PackagePath`: Chemin d’accès où le fichier doit être la sortie dans le package. NuGet émet un avertissement si plus d’un fichier est ajouté à la même chemin d’accès du package.
- `BuildAction`: Obligatoire l’action de génération à assigner au fichier, uniquement si le chemin d’accès du package est dans le `contentFiles` dossier. Valeur par défaut est « None ».

Voici un exemple :
```
<PropertyGroup>
    <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
    <ItemGroup>
      <TfmSpecificPackageFile Include=""abc.txt"">
        <PackagePath>mycontent/$(TargetFramework)</PackagePath>
      </TfmSpecificPackageFile>
      <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
        <PackagePath>net46content</PackagePath>
      </TfmSpecificPackageFile>  
    </ItemGroup>
  </Target>  
```

## <a name="restore-target"></a>Cible restore

`MSBuild /t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :

1. Lire toutes les références entre projets
1. Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework
1. Passer des données msbuild à NuGet.Build.Tasks.dll
1. Exécuter la restauration
1. Télécharger les packages
1. Écrire le fichier de ressources, les cibles et les propriétés

Le `restore` cible fonctionne **uniquement** pour les projets en utilisant le format PackageReference. Il effectue **pas** fonctionnent pour les projets à l’aide de la `packages.config` format ; utilisez [restauration nuget](../tools/cli-ref-restore.md) à la place.

### <a name="restore-properties"></a>Propriétés de restauration

Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet. Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `/p:` (consultez Exemples ci-dessous).

| Propriété | Description |
|--------|--------|
| RestoreSources | Liste de sources de packages séparées par un point-virgule. |
| RestorePackagesPath | Chemin du dossier de packages de l’utilisateur. |
| RestoreDisableParallel | Limite les téléchargements à un à la fois. |
| RestoreConfigFile | Chemin à un fichier `Nuget.Config` à appliquer. |
| RestoreNoCache | Si la valeur est true, permet d’éviter l’utilisation de packages de mise en cache. Consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
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
</PropertyGroup>
```

### <a name="restore-outputs"></a>Sorties de restauration

La restauration crée les fichiers suivants dans le dossier `obj` de build :

| Fichier | Description |
|--------|--------|
| `project.assets.json` | Contient le graphique de dépendance de toutes les références de package. |
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
