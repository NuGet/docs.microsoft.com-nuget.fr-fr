---
title: Créer un package NuGet avec MSBuild
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231316"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Créer un package NuGet avec MSBuild

Lorsque vous créez un package NuGet à partir de votre code, vous compressez cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs. Cet article décrit comment créer un package à l’aide de MSBuild. MSBuild est préinstallé avec chaque charge de travail Visual Studio qui contient NuGet. En outre, vous pouvez également utiliser MSBuild à travers le CLI dotnet avec [msbuild dotnet](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).

Pour les projets .NET Core et .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md), et tout autre projet de style SDK, NuGet utilise les informations dans le fichier projet directement pour créer un package.  Pour un projet de style non SDK qui utilise `<PackageReference>`, NuGet utilise également le fichier projet pour créer un package.

La fonctionnalité de compression est disponible par défaut dans les projets de style SDK. Pour les projets PackageReference de style non SDK, vous devez ajouter le package NuGet.Build.Tasks.Pack aux dépendances du projet. Pour plus d’informations sur les cibles de pack MSBuild, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).

La commande qui crée un package, `msbuild -t:pack`, est équivalente à `dotnet pack`.

> [!IMPORTANT]
> Cette rubrique concerne les projets de [style SDK](../resources/check-project-format.md), en général les projets .NET Core et .NET Standard, et aux projets de style non SDK qui utilisent PackageReference.

## <a name="set-properties"></a>Définir des propriétés

Les propriétés suivantes sont requises pour créer un package.

- `PackageId`, l’identificateur du package, qui doit être unique dans toute la galerie qui héberge le package. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.
- `Version`, un numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [versions préliminaires](prerelease-packages.md). Si elle n’est pas spécifiée, la valeur par défaut est 1.0.0.
- Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)
- `Authors`, informations sur l’auteur et le propriétaire. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.
- `Company`, le nom de votre entreprise. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.

En outre, si vous emballez des projets non-SDK-style qui utilisent PackageReference, ce qui suit est nécessaire:

- `PackageOutputPath`, le dossier de sortie pour le paquet généré lors du pack d’appels.

Dans Visual Studio, vous pouvez définir ces valeurs dans les propriétés du projet (cliquez avec le bouton droit sur le projet dans Explorateur de solutions, choisissez **Propriétés**, puis sélectionnez l’onglet **Package**). Vous pouvez également définir directement ces propriétés dans les fichiers projet (*.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Donnez au package un identificateur unique sur nuget.org ou dans la source de package que vous utilisez.

L’exemple suivant montre un fichier projet simple et complet avec ces propriétés incluses.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Vous pouvez également définir les propriétés optionnelles, telles que `Title`, `PackageDescription` et `PackageTags`, comme cela est décrit dans [les cibles de packages MSBuild](../reference/msbuild-targets.md#pack-target), [Contrôle des ressources de dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) et [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.

Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) et [Gestion des versions de package](../concepts/package-versioning.md). Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `<IncludeAssets>` et `<ExcludeAssets>`. Pour plus d’informations, consultez [Contrôle des ressources des dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Ajouter un champ de description facultatif

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Choisir un identificateur de package unique et définir le numéro de version

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Ajouter le package NuGet.Build.Tasks.Pack

Si vous utilisez MSBuild avec un projet de style non SDK et PackageReference, ajoutez le package NuGet.Build.Tasks.Pack à votre projet.

1. Ouvrez le fichier projet et ajoutez ce qui suit après l’élément `<PropertyGroup>` :

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Ouvrez une invite de commandes développeur (dans la zone **Rechercher**, saisissez **Invite de commandes développeur**).

   Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu **Démarrer**, car elle est configurée avec tous les chemins nécessaires pour MSBuild.

3. Basculez vers le dossier contenant le fichier projet et saisissez la commande suivante pour installer le package NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Assurez-vous que la sortie MSBuild indique que la génération s’est terminée avec succès.

## <a name="run-the-msbuild--tpack-command"></a>Exécuter la commande msbuild -t:pack

Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `msbuild -t:pack`, qui génère également le projet automatiquement :

Dans l’invite de commandes Développeur pour Visual Studio, tapez la commande suivante :

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

La sortie affiche le chemin d’accès du fichier `.nupkg`.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Générer automatiquement le package à la création

Pour exécuter automatiquement `msbuild -t:pack` pendant la création ou la restauration du projet, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Lorsque vous `msbuild -t:pack` exécutez sur une solution, cela emballe tous les[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) projets `true`dans la solution qui sont emballés (la propriété est définie à ).

> [!NOTE]
> Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.

### <a name="test-package-installation"></a>Tester l’installation de package

Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test. Les tests permettent de s’assurer que les fichiers nécessaires se placent tous au bon endroit dans le projet.

Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Les packages sont immuables. Si vous remédiez à un problème, modifiez le contenu du package et compressez-le à nouveau. Si vous répétez un test, vous utiliserez l’ancienne version du package tant que vous n’aurez pas [effacé votre dossier de packages globaux](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). C’est particulièrement utile lorsque vous testez des packages qui n’utilisent pas une étiquette de version préliminaire unique sur chaque build.

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../nuget-org/publish-a-package.md).

Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :

- [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md)
- [Contrôle de version des packages](../concepts/package-versioning.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md)
- [Localisation](../create-packages/creating-localized-packages.md)
- [Versions pré-version](../create-packages/prerelease-packages.md)
- [Définir un type de package](../create-packages/set-package-type.md)
- [Créer des packages avec des assemblys COM Interop](../create-packages/author-packages-with-COM-interop-assemblies.md)

Enfin, il existe d’autres types de package à connaître :

- [Packages natifs](../guides/native-packages.md)
- [Paquets de symboles](../create-packages/symbol-packages-snupkg.md)
