---
title: Créer un package NuGet avec MSBuild
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9512899a4086d17d2584f16833aba33efb321eae
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380688"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="2bf14-103">Créer un package NuGet avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="2bf14-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="2bf14-104">Lorsque vous créez un package NuGet à partir de votre code, vous compressez cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="2bf14-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="2bf14-105">Cet article décrit comment créer un package à l’aide de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="2bf14-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="2bf14-106">MSBuild est préinstallé avec chaque charge de travail Visual Studio qui contient NuGet.</span><span class="sxs-lookup"><span data-stu-id="2bf14-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="2bf14-107">Vous pouvez également utiliser MSBuild via l’interface CLI dotnet avec [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span><span class="sxs-lookup"><span data-stu-id="2bf14-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span></span>

<span data-ttu-id="2bf14-108">Pour les projets .NET Core et .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md), et tout autre projet de style SDK, NuGet utilise les informations dans le fichier projet directement pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="2bf14-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="2bf14-109">Pour un projet de style non SDK qui utilise `<PackageReference>`, NuGet utilise également le fichier projet pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="2bf14-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="2bf14-110">La fonctionnalité de compression est disponible par défaut dans les projets de style SDK.</span><span class="sxs-lookup"><span data-stu-id="2bf14-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="2bf14-111">Pour les projets PackageReference de style non SDK, vous devez ajouter le package NuGet.Build.Tasks.Pack aux dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="2bf14-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="2bf14-112">Pour plus d’informations sur les cibles de pack MSBuild, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="2bf14-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="2bf14-113">La commande qui crée un package, `msbuild -t:pack`, est équivalente à `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="2bf14-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bf14-114">Cette rubrique concerne les projets de [style SDK](../resources/check-project-format.md), en général les projets .NET Core et .NET Standard, et aux projets de style non SDK qui utilisent PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2bf14-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="2bf14-115">Définir les propriétés</span><span class="sxs-lookup"><span data-stu-id="2bf14-115">Set properties</span></span>

<span data-ttu-id="2bf14-116">Les propriétés suivantes sont requises pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="2bf14-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="2bf14-117">`PackageId`, l’identificateur du package, qui doit être unique dans toute la galerie qui héberge le package.</span><span class="sxs-lookup"><span data-stu-id="2bf14-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="2bf14-118">S’il n’est pas spécifié, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="2bf14-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="2bf14-119">`Version`, un numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [versions préliminaires](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="2bf14-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="2bf14-120">Si elle n’est pas spécifiée, la valeur par défaut est 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="2bf14-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="2bf14-121">Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)</span><span class="sxs-lookup"><span data-stu-id="2bf14-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="2bf14-122">`Authors`, informations sur l’auteur et le propriétaire.</span><span class="sxs-lookup"><span data-stu-id="2bf14-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="2bf14-123">S’il n’est pas spécifié, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="2bf14-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="2bf14-124">`Company`, le nom de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="2bf14-124">`Company`, your company name.</span></span> <span data-ttu-id="2bf14-125">S’il n’est pas spécifié, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="2bf14-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="2bf14-126">Dans Visual Studio, vous pouvez définir ces valeurs dans les propriétés du projet (cliquez avec le bouton droit sur le projet dans Explorateur de solutions, choisissez **Propriétés**, puis sélectionnez l’onglet **Package**).</span><span class="sxs-lookup"><span data-stu-id="2bf14-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="2bf14-127">Vous pouvez également définir directement ces propriétés dans les fichiers projet ( *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="2bf14-127">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="2bf14-128">Donnez au package un identificateur unique sur nuget.org ou dans la source de package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="2bf14-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="2bf14-129">L’exemple suivant montre un fichier projet simple et complet avec ces propriétés incluses.</span><span class="sxs-lookup"><span data-stu-id="2bf14-129">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="2bf14-130">Vous pouvez également définir les propriétés optionnelles, telles que `Title`, `PackageDescription` et `PackageTags`, comme cela est décrit dans [les cibles de packages MSBuild](../reference/msbuild-targets.md#pack-target), [Contrôle des ressources de dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) et [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="2bf14-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="2bf14-131">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="2bf14-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="2bf14-132">Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) et [Gestion des versions de package](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2bf14-132">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="2bf14-133">Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `<IncludeAssets>` et `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="2bf14-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="2bf14-134">Pour plus d’informations, consultez [Contrôle des ressources des dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="2bf14-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="2bf14-135">Choisir un identificateur de package unique et définir le numéro de version</span><span class="sxs-lookup"><span data-stu-id="2bf14-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="2bf14-136">Ajouter le package NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="2bf14-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="2bf14-137">Si vous utilisez MSBuild avec un projet de style non SDK et PackageReference, ajoutez le package NuGet.Build.Tasks.Pack à votre projet.</span><span class="sxs-lookup"><span data-stu-id="2bf14-137">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="2bf14-138">Ouvrez le fichier projet et ajoutez ce qui suit après l’élément `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="2bf14-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="2bf14-139">Ouvrez une invite de commandes développeur (dans la zone **Rechercher**, saisissez **Invite de commandes développeur**).</span><span class="sxs-lookup"><span data-stu-id="2bf14-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="2bf14-140">Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu **Démarrer**, car elle est configurée avec tous les chemins nécessaires pour MSBuild.</span><span class="sxs-lookup"><span data-stu-id="2bf14-140">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="2bf14-141">Basculez vers le dossier contenant le fichier projet et saisissez la commande suivante pour installer le package NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="2bf14-141">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="2bf14-142">Assurez-vous que la sortie MSBuild indique que la génération s’est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="2bf14-142">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="2bf14-143">Exécuter la commande msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="2bf14-143">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="2bf14-144">Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `msbuild -t:pack`, qui génère également le projet automatiquement :</span><span class="sxs-lookup"><span data-stu-id="2bf14-144">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="2bf14-145">Dans l’invite de commandes Développeur pour Visual Studio, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2bf14-145">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="2bf14-146">La sortie affiche le chemin d’accès du fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="2bf14-146">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="2bf14-147">Générer automatiquement le package à la création</span><span class="sxs-lookup"><span data-stu-id="2bf14-147">Automatically generate package on build</span></span>

<span data-ttu-id="2bf14-148">Pour exécuter automatiquement `msbuild -t:pack` pendant la création ou la restauration du projet, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="2bf14-148">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="2bf14-149">Lorsque vous exécutez `msbuild -t:pack` sur une solution, cela compresse tous les projets de la solution qui peuvent être compressés (la propriété [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) a la valeur `true`).</span><span class="sxs-lookup"><span data-stu-id="2bf14-149">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="2bf14-150">Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="2bf14-150">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="2bf14-151">Tester l’installation de package</span><span class="sxs-lookup"><span data-stu-id="2bf14-151">Test package installation</span></span>

<span data-ttu-id="2bf14-152">Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test.</span><span class="sxs-lookup"><span data-stu-id="2bf14-152">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="2bf14-153">Les tests permettent de s’assurer que les fichiers nécessaires se placent tous au bon endroit dans le projet.</span><span class="sxs-lookup"><span data-stu-id="2bf14-153">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="2bf14-154">Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="2bf14-154">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bf14-155">Les packages sont immuables.</span><span class="sxs-lookup"><span data-stu-id="2bf14-155">Packages are immutable.</span></span> <span data-ttu-id="2bf14-156">Si vous remédiez à un problème, modifiez le contenu du package et compressez-le à nouveau. Si vous répétez un test, vous utiliserez l’ancienne version du package tant que vous n’aurez pas [effacé votre dossier de packages globaux](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="2bf14-156">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="2bf14-157">C’est particulièrement utile lorsque vous testez des packages qui n’utilisent pas une étiquette de version préliminaire unique sur chaque build.</span><span class="sxs-lookup"><span data-stu-id="2bf14-157">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bf14-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bf14-158">Next Steps</span></span>

<span data-ttu-id="2bf14-159">Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="2bf14-159">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="2bf14-160">Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="2bf14-160">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="2bf14-161">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="2bf14-161">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="2bf14-162">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="2bf14-162">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="2bf14-163">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="2bf14-163">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="2bf14-164">Transformations de fichiers sources et de configuration</span><span class="sxs-lookup"><span data-stu-id="2bf14-164">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="2bf14-165">Localisation</span><span class="sxs-lookup"><span data-stu-id="2bf14-165">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2bf14-166">Préversions</span><span class="sxs-lookup"><span data-stu-id="2bf14-166">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="2bf14-167">Définir un type de package</span><span class="sxs-lookup"><span data-stu-id="2bf14-167">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="2bf14-168">Créer des packages avec des assemblys COM Interop</span><span class="sxs-lookup"><span data-stu-id="2bf14-168">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="2bf14-169">Enfin, il existe d’autres types de package à connaître :</span><span class="sxs-lookup"><span data-stu-id="2bf14-169">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="2bf14-170">Packages natifs</span><span class="sxs-lookup"><span data-stu-id="2bf14-170">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="2bf14-171">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="2bf14-171">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
