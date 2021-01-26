---
title: Créer un package NuGet à l’aide de l’interface CLI dotnet
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 4771a30ee2ff73e68154d05f1c84efd90b584162
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774484"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="708b6-103">Créer un package NuGet à l’aide de l’interface CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="708b6-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="708b6-104">Quel que soit la fonction de votre package ou le code qu’il contient, vous utilisez l’un des outils CLI, `nuget.exe` ou `dotnet.exe`, pour empaqueter cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="708b6-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="708b6-105">Cet article décrit comment créer un package à l’aide de l’interface CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="708b6-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="708b6-106">Pour installer l’interface CLI `dotnet`, consultez [Installer les outils clients NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="708b6-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="708b6-107">À compter de Visual Studio 2017, l’interface CLI dotnet est incluse dans les charges de travail .NET Core.</span><span class="sxs-lookup"><span data-stu-id="708b6-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="708b6-108">Pour les projets .NET Core et .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md), et tout autre projet de style SDK, NuGet utilise les informations dans le fichier projet directement pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="708b6-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="708b6-109">Pour des didacticiels pas à pas, consultez [Créer des packages .NET Standard avec l’interface CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ou [Créer des packages .NET Standard avec Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="708b6-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="708b6-110">`msbuild -t:pack` est fonctionnellement équivalent à `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="708b6-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="708b6-111">Pour générer avec MSBuild, consultez [Créer un package NuGet avec MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="708b6-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="708b6-112">Cette rubrique s’applique aux projets [SDK-style](../resources/check-project-format.md), qui sont généralement des projets .net Core et .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="708b6-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="708b6-113">Définir des propriétés</span><span class="sxs-lookup"><span data-stu-id="708b6-113">Set properties</span></span>

<span data-ttu-id="708b6-114">Les propriétés suivantes sont requises pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="708b6-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="708b6-115">`PackageId`, l’identificateur du package, qui doit être unique dans toute la galerie qui héberge le package.</span><span class="sxs-lookup"><span data-stu-id="708b6-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="708b6-116">Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="708b6-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="708b6-117">`Version`, un numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [versions préliminaires](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="708b6-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="708b6-118">Si elle n’est pas spécifiée, la valeur par défaut est 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="708b6-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="708b6-119">Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)</span><span class="sxs-lookup"><span data-stu-id="708b6-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="708b6-120">`Authors`, informations sur l’auteur et le propriétaire.</span><span class="sxs-lookup"><span data-stu-id="708b6-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="708b6-121">Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="708b6-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="708b6-122">`Company`, le nom de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="708b6-122">`Company`, your company name.</span></span> <span data-ttu-id="708b6-123">Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="708b6-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="708b6-124">Dans Visual Studio, vous pouvez définir ces valeurs dans les propriétés du projet (cliquez avec le bouton droit sur le projet dans Explorateur de solutions, choisissez **Propriétés**, puis sélectionnez l’onglet **Package**).</span><span class="sxs-lookup"><span data-stu-id="708b6-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="708b6-125">Vous pouvez aussi définir directement ces propriétés dans les fichiers projet (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="708b6-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="708b6-126">Donnez au package un identificateur unique sur nuget.org ou dans la source de package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="708b6-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="708b6-127">L’exemple suivant montre un fichier projet simple et complet avec ces propriétés incluses.</span><span class="sxs-lookup"><span data-stu-id="708b6-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="708b6-128">(Vous pouvez créer un nouveau projet par défaut à l’aide de la commande `dotnet new classlib`.)</span><span class="sxs-lookup"><span data-stu-id="708b6-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="708b6-129">Vous pouvez également définir les propriétés optionnelles, telles que `Title`, `PackageDescription` et `PackageTags`, comme cela est décrit dans [les cibles de packages MSBuild](../reference/msbuild-targets.md#pack-target), [Contrôle des ressources de dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) et [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="708b6-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="708b6-130">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="708b6-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="708b6-131">Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) et [Gestion des versions de package](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="708b6-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="708b6-132">Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `<IncludeAssets>` et `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="708b6-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="708b6-133">Pour plus d’informations, consultez [contrôle des ressources de dépendance](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="708b6-133">For more information, see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="708b6-134">Ajouter un champ de description facultatif</span><span class="sxs-lookup"><span data-stu-id="708b6-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="708b6-135">Choisir un identificateur de package unique et définir le numéro de version</span><span class="sxs-lookup"><span data-stu-id="708b6-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="708b6-136">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="708b6-136">Run the pack command</span></span>

<span data-ttu-id="708b6-137">Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `dotnet pack`, qui génère également le projet automatiquement :</span><span class="sxs-lookup"><span data-stu-id="708b6-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="708b6-138">La sortie affiche le chemin d’accès du fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="708b6-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="708b6-139">Générer automatiquement le package à la création</span><span class="sxs-lookup"><span data-stu-id="708b6-139">Automatically generate package on build</span></span>

<span data-ttu-id="708b6-140">Pour exécuter automatiquement `dotnet pack` pendant l’exécution de `dotnet build`, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="708b6-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="708b6-141">Quand vous exécutez `dotnet pack` sur une solution, cela compresse tous les projets de la solution qui peuvent être représentables (la [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) propriété a la valeur `true` ).</span><span class="sxs-lookup"><span data-stu-id="708b6-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="708b6-142">Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="708b6-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="708b6-143">Tester l’installation de package</span><span class="sxs-lookup"><span data-stu-id="708b6-143">Test package installation</span></span>

<span data-ttu-id="708b6-144">Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test.</span><span class="sxs-lookup"><span data-stu-id="708b6-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="708b6-145">Les tests permettent de s’assurer que les fichiers nécessaires se trouvent tous dans leurs emplacements corrects dans le projet.</span><span class="sxs-lookup"><span data-stu-id="708b6-145">The tests make sure that the necessary files all end up in their correct places in the project.</span></span>

<span data-ttu-id="708b6-146">Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="708b6-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="708b6-147">Les packages sont immuables.</span><span class="sxs-lookup"><span data-stu-id="708b6-147">Packages are immutable.</span></span> <span data-ttu-id="708b6-148">Si vous remédiez à un problème, modifiez le contenu du package et compressez-le à nouveau. Si vous répétez un test, vous utiliserez l’ancienne version du package tant que vous n’aurez pas [effacé votre dossier de packages globaux](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="708b6-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="708b6-149">C’est particulièrement utile lorsque vous testez des packages qui n’utilisent pas une étiquette de version préliminaire unique sur chaque build.</span><span class="sxs-lookup"><span data-stu-id="708b6-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="708b6-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="708b6-150">Next Steps</span></span>

<span data-ttu-id="708b6-151">Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="708b6-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="708b6-152">Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="708b6-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="708b6-153">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="708b6-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="708b6-154">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="708b6-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="708b6-155">Icône Ajouter un package</span><span class="sxs-lookup"><span data-stu-id="708b6-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="708b6-156">Transformations de fichiers sources et de configuration</span><span class="sxs-lookup"><span data-stu-id="708b6-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="708b6-157">Localisation</span><span class="sxs-lookup"><span data-stu-id="708b6-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="708b6-158">Versions préliminaires</span><span class="sxs-lookup"><span data-stu-id="708b6-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="708b6-159">Définir un type de package</span><span class="sxs-lookup"><span data-stu-id="708b6-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="708b6-160">Créer des packages avec des assemblys COM Interop</span><span class="sxs-lookup"><span data-stu-id="708b6-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="708b6-161">Enfin, il existe d’autres types de package à connaître :</span><span class="sxs-lookup"><span data-stu-id="708b6-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="708b6-162">Packages natifs</span><span class="sxs-lookup"><span data-stu-id="708b6-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="708b6-163">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="708b6-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
