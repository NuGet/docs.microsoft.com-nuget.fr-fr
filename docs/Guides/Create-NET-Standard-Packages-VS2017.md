---
title: "Créer des packages NuGet .NET Standard 2.0 avec Visual Studio 2017 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard 2.0 à l’aide de NuGet 4.x et Visual Studio 2017."
keywords: "créer un package, packages .NET Standard, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="b9607-104">Créer des packages .NET Standard 2.0 avec Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b9607-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="b9607-105">*S’applique à NuGet 4.x+ et MSBuild 15.3+ tels que fournis avec Visual Studio 2017 Update 3. Pour les versions antérieures de Visual Studio 2017, ces instructions s’appliquent à .NET Standard versions 1.4 à 1.6 sous réserve de modifier la propriété \<TargetFramework\>. Consultez également [Créer des packages .NET Standard avec Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) si vous envisagez d’utiliser NuGet 3.x+.*</span><span class="sxs-lookup"><span data-stu-id="b9607-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="b9607-106">La [bibliothèque .NET Standard](/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET.</span><span class="sxs-lookup"><span data-stu-id="b9607-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="b9607-107">La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="b9607-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="b9607-108">Elle permet aux développeurs de produire des bibliothèques de classes portables qui sont utilisables à travers tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.</span><span class="sxs-lookup"><span data-stu-id="b9607-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="b9607-109">Ce guide vous explique comment créer un package nuget ciblant .NET Standard Library 2.0 avec Visual Studio 2017 Update 3 et NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="b9607-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="b9607-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b9607-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="b9607-111">Créer le projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="b9607-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="b9607-112">Modifier les métadonnées dans le fichier .csproj</span><span class="sxs-lookup"><span data-stu-id="b9607-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="b9607-113">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="b9607-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="b9607-114">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="b9607-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="b9607-115">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b9607-115">Pre-requisites</span></span>

<span data-ttu-id="b9607-116">Cette procédure pas à pas nécessite Visual Studio 2017 Update 3 avec la charge de travail **Développement multiplateforme .Net Core**.</span><span class="sxs-lookup"><span data-stu-id="b9607-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="b9607-117">Vous pouvez installer l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser les éditions Professional et Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b9607-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="b9607-118">La charge de travail requise s’affiche comme suit dans le programme d’installation de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="b9607-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Charge de travail Développement multiplateforme .Net Core dans le programme d’installation de Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="b9607-120">Créer le projet de bibliothèque de classes .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b9607-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="b9607-121">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez **Bibliothèque de classes (.NET Standard)**, changez le nom en AppLogger et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="b9607-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Créer un projet de bibliothèque de classes](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="b9607-123">Définissez la configuration de build sur **Release**.</span><span class="sxs-lookup"><span data-stu-id="b9607-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="b9607-124">Cliquez avec le bouton droit sur le projet `AppLogger` dans l’Explorateur de solutions, sélectionnez **Propriétés**, sélectionnez l’onglet **Générer**, cochez la case **Fichier de documentation XML**, puis définissez le nom de fichier simplement sur `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="b9607-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="b9607-125">Ensuite, enregistrez le projet.</span><span class="sxs-lookup"><span data-stu-id="b9607-125">Then save the project.</span></span>

1. <span data-ttu-id="b9607-126">Ajoutez votre code au composant, à l’image du code suivant (qui se contente d’afficher des messages dans la console) :</span><span class="sxs-lookup"><span data-stu-id="b9607-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="b9607-127">Générez le projet (avec la configuration Release) et vérifiez que les fichiers DLL et XML sont produits dans le dossier `bin\Release\netstandard2.0`.</span><span class="sxs-lookup"><span data-stu-id="b9607-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="b9607-128">Modifier les métadonnées dans le fichier .csproj</span><span class="sxs-lookup"><span data-stu-id="b9607-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="b9607-129">Avec les projets NuGet 4.0 et .NET Core, les métadonnées des packages se trouvent directement dans le fichier `.csproj` au lieu de fichiers externes, tels qu’un fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b9607-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="b9607-130">Une description complète de ces métadonnées est disponible dans [Cibles NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="b9607-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="b9607-131">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, sélectionnez **Modifier AppLogger.csproj**, puis modifiez le premier groupe de propriétés pour inclure les informations de package telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b9607-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="b9607-132">Enregistrez le projet, puis cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour regénérer tous les fichiers du package, cette fois avec les métadonnées correctes.</span><span class="sxs-lookup"><span data-stu-id="b9607-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="b9607-133">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="b9607-133">Package the component</span></span>

<span data-ttu-id="b9607-134">NuGet 4.0 prend en charge une cible pack à l’aide de MSBuild version 15,1+ (MSBuild 15.3 dans le cadre de Visual Studio 2017 Update 3) quand le projet contient les métadonnées de package nécessaires, ajoutées dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="b9607-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="b9607-135">Pour appeler MSBuild de cette manière, spécifiez simplement la cible pack sur la ligne de commande dans le même dossier que le fichier `.csproj` :</span><span class="sxs-lookup"><span data-stu-id="b9607-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="b9607-136">Pour d’autres options avec `msbuild /t:pack`, telles que l’inclusion de fichiers de contenu, de symboles et de code source, consultez [Cibles NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="b9607-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="b9607-137">Dans tous les cas, la commande ci-dessus génère `AppLogger.YOUR_NAME.1.0.0.nupkg` dans le dossier `bin\Release` par défaut, car elle génère cette configuration.</span><span class="sxs-lookup"><span data-stu-id="b9607-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="b9607-138">Si vous omettez le commutateur `/p`, la configuration par défaut est `Debug`.</span><span class="sxs-lookup"><span data-stu-id="b9607-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="b9607-139">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="b9607-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet Package Explorer affichant le package AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="b9607-141">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="b9607-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="b9607-142">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b9607-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="b9607-143">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b9607-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="b9607-144">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="b9607-144">Related topics</span></span>

- <span data-ttu-id="b9607-145">[Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) explique comment décrire votre package directement dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="b9607-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="b9607-146">[Cibles NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md) décrit toutes les options de création d’un package à l’aide de `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="b9607-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="b9607-147">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b9607-147">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b9607-148">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b9607-148">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
