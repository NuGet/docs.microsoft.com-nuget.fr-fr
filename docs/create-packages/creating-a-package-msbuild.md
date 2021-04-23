---
title: Créer un package NuGet avec MSBuild
description: Guide détaillé du processus de conception et de création d’un package NuGet à l’aide de MSBuild, y compris les points de décision clés comme les fichiers et le contrôle de version.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 18e0da335f65fde99d035388b95f35160757ee84
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901458"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="60a28-103">Créer un package NuGet avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a28-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="60a28-104">Lorsque vous créez un package NuGet à partir de votre code, vous compressez cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="60a28-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="60a28-105">Cet article décrit comment créer un package à l’aide de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="60a28-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="60a28-106">MSBuild est préinstallé avec chaque charge de travail Visual Studio qui contient NuGet.</span><span class="sxs-lookup"><span data-stu-id="60a28-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="60a28-107">En outre, vous pouvez également utiliser MSBuild à l’aide de l’interface CLI dotnet avec [dotnet MSBuild](/dotnet/core/tools/dotnet-msbuild).</span><span class="sxs-lookup"><span data-stu-id="60a28-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="60a28-108">Pour les projets .NET Core et .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md), et tout autre projet de style SDK, NuGet utilise les informations dans le fichier projet directement pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="60a28-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="60a28-109">Pour un projet de style non SDK qui utilise `<PackageReference>`, NuGet utilise également le fichier projet pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="60a28-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="60a28-110">La fonctionnalité de compression est disponible par défaut dans les projets de style SDK.</span><span class="sxs-lookup"><span data-stu-id="60a28-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="60a28-111">Pour les projets PackageReference de style non SDK, vous devez ajouter le package NuGet.Build.Tasks.Pack aux dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="60a28-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="60a28-112">Pour plus d’informations sur les cibles de pack MSBuild, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="60a28-113">La commande qui crée un package, `msbuild -t:pack`, est équivalente à `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="60a28-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60a28-114">Cette rubrique concerne les projets de [style SDK](../resources/check-project-format.md), en général les projets .NET Core et .NET Standard, et aux projets de style non SDK qui utilisent PackageReference.</span><span class="sxs-lookup"><span data-stu-id="60a28-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="60a28-115">Définir des propriétés</span><span class="sxs-lookup"><span data-stu-id="60a28-115">Set properties</span></span>

<span data-ttu-id="60a28-116">Les propriétés suivantes sont requises pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="60a28-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="60a28-117">`PackageId`, l’identificateur du package, qui doit être unique dans toute la galerie qui héberge le package.</span><span class="sxs-lookup"><span data-stu-id="60a28-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="60a28-118">Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="60a28-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="60a28-119">`Version`, un numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [versions préliminaires](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="60a28-120">Si elle n’est pas spécifiée, la valeur par défaut est 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="60a28-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="60a28-121">Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)</span><span class="sxs-lookup"><span data-stu-id="60a28-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="60a28-122">`Authors`, informations sur l’auteur et le propriétaire.</span><span class="sxs-lookup"><span data-stu-id="60a28-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="60a28-123">Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="60a28-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="60a28-124">`Company`, le nom de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="60a28-124">`Company`, your company name.</span></span> <span data-ttu-id="60a28-125">Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="60a28-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="60a28-126">En outre, si vous compressez des projets de type non-SDK qui utilisent PackageReference, les conditions suivantes sont requises :</span><span class="sxs-lookup"><span data-stu-id="60a28-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="60a28-127">`PackageOutputPath`, le dossier de sortie du package généré lors de l’appel à Pack.</span><span class="sxs-lookup"><span data-stu-id="60a28-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="60a28-128">Dans Visual Studio, vous pouvez définir ces valeurs dans les propriétés du projet (cliquez avec le bouton droit sur le projet dans Explorateur de solutions, choisissez **Propriétés**, puis sélectionnez l’onglet **Package**).</span><span class="sxs-lookup"><span data-stu-id="60a28-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="60a28-129">Vous pouvez également définir directement ces propriétés dans les fichiers projet (*.csproj*).</span><span class="sxs-lookup"><span data-stu-id="60a28-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="60a28-130">Donnez au package un identificateur unique sur nuget.org ou dans la source de package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="60a28-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="60a28-131">L’exemple suivant montre un fichier projet simple et complet avec ces propriétés incluses.</span><span class="sxs-lookup"><span data-stu-id="60a28-131">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="60a28-132">Vous pouvez également définir les propriétés optionnelles, telles que `Title`, `PackageDescription` et `PackageTags`, comme cela est décrit dans [les cibles de packages MSBuild](../reference/msbuild-targets.md#pack-target), [Contrôle des ressources de dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) et [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="60a28-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="60a28-133">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="60a28-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="60a28-134">Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) et [Gestion des versions de package](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="60a28-135">Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `<IncludeAssets>` et `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="60a28-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="60a28-136">Pour plus d’informations, consultez [Contrôle des ressources des dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="60a28-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="60a28-137">Ajouter un champ de description facultatif</span><span class="sxs-lookup"><span data-stu-id="60a28-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="60a28-138">Choisir un identificateur de package unique et définir le numéro de version</span><span class="sxs-lookup"><span data-stu-id="60a28-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="60a28-139">Ajouter le package NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="60a28-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="60a28-140">Si vous utilisez MSBuild avec un projet de style non SDK et PackageReference, ajoutez le package NuGet.Build.Tasks.Pack à votre projet.</span><span class="sxs-lookup"><span data-stu-id="60a28-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="60a28-141">Ouvrez le fichier projet et ajoutez ce qui suit après l’élément `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="60a28-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="60a28-142">Ouvrez une invite de commandes développeur (dans la zone **Rechercher**, saisissez **Invite de commandes développeur**).</span><span class="sxs-lookup"><span data-stu-id="60a28-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="60a28-143">Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu **Démarrer**, car elle est configurée avec tous les chemins nécessaires pour MSBuild.</span><span class="sxs-lookup"><span data-stu-id="60a28-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="60a28-144">Basculez vers le dossier contenant le fichier projet et saisissez la commande suivante pour installer le package NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="60a28-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="60a28-145">Assurez-vous que la sortie MSBuild indique que la génération s’est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="60a28-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="60a28-146">Exécuter la commande msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="60a28-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="60a28-147">Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `msbuild -t:pack`, qui génère également le projet automatiquement :</span><span class="sxs-lookup"><span data-stu-id="60a28-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="60a28-148">Dans l’invite de commandes Développeur pour Visual Studio, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="60a28-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="60a28-149">La sortie affiche le chemin d’accès du fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="60a28-149">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="60a28-150">Générer automatiquement le package à la création</span><span class="sxs-lookup"><span data-stu-id="60a28-150">Automatically generate package on build</span></span>

<span data-ttu-id="60a28-151">Pour exécuter automatiquement `msbuild -t:pack` pendant la création ou la restauration du projet, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="60a28-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="60a28-152">Quand vous exécutez `msbuild -t:pack` sur une solution, cela compresse tous les projets de la solution qui peuvent être représentables (la [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) propriété a la valeur `true` ).</span><span class="sxs-lookup"><span data-stu-id="60a28-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="60a28-153">Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="60a28-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="60a28-154">Tester l’installation de package</span><span class="sxs-lookup"><span data-stu-id="60a28-154">Test package installation</span></span>

<span data-ttu-id="60a28-155">Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test.</span><span class="sxs-lookup"><span data-stu-id="60a28-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="60a28-156">Les tests permettent de s’assurer que les fichiers nécessaires se placent tous au bon endroit dans le projet.</span><span class="sxs-lookup"><span data-stu-id="60a28-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="60a28-157">Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="60a28-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60a28-158">Les packages sont immuables.</span><span class="sxs-lookup"><span data-stu-id="60a28-158">Packages are immutable.</span></span> <span data-ttu-id="60a28-159">Si vous remédiez à un problème, modifiez le contenu du package et compressez-le à nouveau. Si vous répétez un test, vous utiliserez l’ancienne version du package tant que vous n’aurez pas [effacé votre dossier de packages globaux](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="60a28-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="60a28-160">C’est particulièrement utile lorsque vous testez des packages qui n’utilisent pas une étiquette de version préliminaire unique sur chaque build.</span><span class="sxs-lookup"><span data-stu-id="60a28-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60a28-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60a28-161">Next Steps</span></span>

<span data-ttu-id="60a28-162">Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="60a28-163">Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="60a28-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="60a28-164">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="60a28-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="60a28-165">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="60a28-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="60a28-166">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="60a28-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="60a28-167">Transformations de fichiers sources et de configuration</span><span class="sxs-lookup"><span data-stu-id="60a28-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="60a28-168">Localisation</span><span class="sxs-lookup"><span data-stu-id="60a28-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="60a28-169">Versions préliminaires</span><span class="sxs-lookup"><span data-stu-id="60a28-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="60a28-170">Définir un type de package</span><span class="sxs-lookup"><span data-stu-id="60a28-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="60a28-171">Créer des packages avec des assemblys COM Interop</span><span class="sxs-lookup"><span data-stu-id="60a28-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="60a28-172">Enfin, il existe d’autres types de package à connaître :</span><span class="sxs-lookup"><span data-stu-id="60a28-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="60a28-173">Packages natifs</span><span class="sxs-lookup"><span data-stu-id="60a28-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="60a28-174">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="60a28-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)