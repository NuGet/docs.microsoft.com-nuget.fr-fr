---
title: Créer un package NuGet à l’aide de l’interface CLI dotnet
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 87b38d7a707d6175eb3347280784d9dfefd9c17d
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "89359645"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Créer un package NuGet à l’aide de l’interface CLI dotnet

Quel que soit la fonction de votre package ou le code qu’il contient, vous utilisez l’un des outils CLI, `nuget.exe` ou `dotnet.exe`, pour empaqueter cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs. Cet article décrit comment créer un package à l’aide de l’interface CLI dotnet. Pour installer l’interface CLI `dotnet`, consultez [Installer les outils clients NuGet](../install-nuget-client-tools.md). À compter de Visual Studio 2017, l’interface CLI dotnet est incluse dans les charges de travail .NET Core.

Pour les projets .NET Core et .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md), et tout autre projet de style SDK, NuGet utilise les informations dans le fichier projet directement pour créer un package. Pour des didacticiels pas à pas, consultez [Créer des packages .NET Standard avec l’interface CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ou [Créer des packages .NET Standard avec Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` est fonctionnellement équivalent à `dotnet pack`. Pour générer avec MSBuild, consultez [Créer un package NuGet avec MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Cette rubrique s’applique aux projets [SDK-style](../resources/check-project-format.md), qui sont généralement des projets .net Core et .NET Standard.

## <a name="set-properties"></a>Définir des propriétés

Les propriétés suivantes sont requises pour créer un package.

- `PackageId`, l’identificateur du package, qui doit être unique dans toute la galerie qui héberge le package. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.
- `Version`, un numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [versions préliminaires](prerelease-packages.md). Si elle n’est pas spécifiée, la valeur par défaut est 1.0.0.
- Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)
- `Authors`, informations sur l’auteur et le propriétaire. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.
- `Company`, le nom de votre entreprise. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.

Dans Visual Studio, vous pouvez définir ces valeurs dans les propriétés du projet (cliquez avec le bouton droit sur le projet dans Explorateur de solutions, choisissez **Propriétés**, puis sélectionnez l’onglet **Package**). Vous pouvez aussi définir directement ces propriétés dans les fichiers projet (`.csproj`).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Donnez au package un identificateur unique sur nuget.org ou dans la source de package que vous utilisez.

L’exemple suivant montre un fichier projet simple et complet avec ces propriétés incluses. (Vous pouvez créer un nouveau projet par défaut à l’aide de la commande `dotnet new classlib`.)

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Vous pouvez également définir les propriétés optionnelles, telles que `Title`, `PackageDescription` et `PackageTags`, comme cela est décrit dans [les cibles de packages MSBuild](../reference/msbuild-targets.md#pack-target), [Contrôle des ressources de dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) et [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.

Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) et [Gestion des versions de package](../concepts/package-versioning.md). Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `<IncludeAssets>` et `<ExcludeAssets>`. Pour plus d’informations, consultez [contrôle des ressources de dépendance](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Ajouter un champ de description facultatif

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Choisir un identificateur de package unique et définir le numéro de version

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Exécuter la commande pack

Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `dotnet pack`, qui génère également le projet automatiquement :

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

La sortie affiche le chemin d’accès du fichier `.nupkg`.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Générer automatiquement le package à la création

Pour exécuter automatiquement `dotnet pack` pendant l’exécution de `dotnet build`, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Quand vous exécutez `dotnet pack` sur une solution, cela compresse tous les projets de la solution qui peuvent être représentables (la [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) propriété a la valeur `true` ).

> [!NOTE]
> Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.

### <a name="test-package-installation"></a>Tester l’installation de package

Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test. Les tests permettent de s’assurer que les fichiers nécessaires se trouvent tous dans leurs emplacements corrects dans le projet.

Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Les packages sont immuables. Si vous remédiez à un problème, modifiez le contenu du package et compressez-le à nouveau. Si vous répétez un test, vous utiliserez l’ancienne version du package tant que vous n’aurez pas [effacé votre dossier de packages globaux](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). C’est particulièrement utile lorsque vous testez des packages qui n’utilisent pas une étiquette de version préliminaire unique sur chaque build.

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../nuget-org/publish-a-package.md).

Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :

- [Gestion des versions de package](../concepts/package-versioning.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/multiple-target-frameworks-project-file.md)
- [Icône Ajouter un package](../reference/nuspec.md#icon)
- [Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md)
- [Localisation](../create-packages/creating-localized-packages.md)
- [Versions préliminaires](../create-packages/prerelease-packages.md)
- [Définir un type de package](../create-packages/set-package-type.md)
- [Créer des packages avec des assemblys COM Interop](../create-packages/author-packages-with-COM-interop-assemblies.md)

Enfin, il existe d’autres types de package à connaître :

- [Packages natifs](../guides/native-packages.md)
- [Packages de symboles](../create-packages/symbol-packages-snupkg.md)
