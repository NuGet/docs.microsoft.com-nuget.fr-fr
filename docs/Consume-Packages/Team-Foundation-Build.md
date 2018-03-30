---
title: Procédure pas à pas pour la restauration des packages NuGet avec Team Foundation Build | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Procédure pas à pas expliquant comment restaurer des packages avec Team Foundation Build (Visual Studio Team Services et TFS).
keywords: Restauration des packages NuGet, NuGet et TFS, NuGet et VSTS, systèmes de génération NuGet, Team Foundation Build, projets MSBuild personnalisés, Cloud Build, intégration continue
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f46a7402214bf965918a5195605027913a8c60c2
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="85951-104">Configuration de la restauration de packages avec Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="85951-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="85951-105">Cet article explique pas à pas comment restaurer des packages dans [Team Services Build](/vsts/build-release/index) pour la gestion de version Team Services et Git.</span><span class="sxs-lookup"><span data-stu-id="85951-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="85951-106">Cette procédure pas à pas est propre au scénario où Team Foundation Services est utilisé. Toutefois, les mêmes concepts s’appliquent aussi à d’autres systèmes de gestion de versions et de build.</span><span class="sxs-lookup"><span data-stu-id="85951-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="85951-107">S’applique aux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="85951-107">Applies To:</span></span>

- <span data-ttu-id="85951-108">Projets MSBuild personnalisés exécutés sur n’importe quelle version de TFS</span><span class="sxs-lookup"><span data-stu-id="85951-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="85951-109">Team Foundation Server 2012 ou version antérieure</span><span class="sxs-lookup"><span data-stu-id="85951-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="85951-110">Modèles de processus Team Foundation Build personnalisés migrés vers TFS 2013 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="85951-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="85951-111">Modèles de processus de génération sans la fonctionnalité de restauration Nuget</span><span class="sxs-lookup"><span data-stu-id="85951-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="85951-112">Si vous utilisez Visual Studio Team Services ou Team Foundation Server 2013 avec ses modèles de processus de génération, une restauration automatique des packages est effectuée dans le cadre du processus de génération.</span><span class="sxs-lookup"><span data-stu-id="85951-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="85951-113">Approche générale</span><span class="sxs-lookup"><span data-stu-id="85951-113">The general approach</span></span>

<span data-ttu-id="85951-114">L’utilisation de NuGet vous permet d’éviter l’archivage des fichiers binaires dans votre système de gestion de versions.</span><span class="sxs-lookup"><span data-stu-id="85951-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="85951-115">Ceci est particulièrement intéressant si vous utilisez un [système de gestion de versions distribué](http://en.wikipedia.org/wiki/Distributed_revision_control) tel que git, car les développeurs ont besoin de cloner l’intégralité du référentiel, y compris l’historique complet, avant de pouvoir travailler en local.</span><span class="sxs-lookup"><span data-stu-id="85951-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="85951-116">L’archivage des fichiers binaires peut provoquer l’encombrement du référentiel, puisqu’ils sont généralement stockés sans compression delta.</span><span class="sxs-lookup"><span data-stu-id="85951-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="85951-117">NuGet prend en charge la [restauration des packages](../consume-packages/package-restore.md) dans le cadre de la génération depuis longtemps.</span><span class="sxs-lookup"><span data-stu-id="85951-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="85951-118">L’implémentation précédente avait un problème du type « l’œuf ou la poule » pour les packages qui devaient étendre le processus de génération, car NuGet restaurait les packages lors de la génération du projet.</span><span class="sxs-lookup"><span data-stu-id="85951-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="85951-119">Toutefois, MSBuild ne permet pas d’étendre la génération pendant la génération. Certains pourraient dire qu’il s’agit d’un problème MSBuild, mais je pense qu’il s’agit plutôt d’un problème inhérent.</span><span class="sxs-lookup"><span data-stu-id="85951-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="85951-120">Selon ce que vous avez besoin d’étendre, vous ne pourrez plus inscrire votre package une fois la restauration effectuée.</span><span class="sxs-lookup"><span data-stu-id="85951-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="85951-121">Pour remédier à ce problème, la première étape du processus de génération est de vérifier que les packages sont restaurés :</span><span class="sxs-lookup"><span data-stu-id="85951-121">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="85951-122">Lorsque votre processus de génération restaure des packages avant de générer le code, vous n’avez pas à archiver les fichiers `.targets`.</span><span class="sxs-lookup"><span data-stu-id="85951-122">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="85951-123">Les packages doivent être associés à leur auteur afin de permettre leur chargement dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85951-123">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="85951-124">Dans le cas contraire, vous pouvez toujours archiver les fichiers `.targets` pour que les autres développeurs puissent ouvrir la solution sans avoir à restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="85951-124">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="85951-125">Le projet de démonstration suivant montre comment configurer la génération de sorte que les dossiers `packages` et les fichiers `.targets` n’aient pas à être archivés.</span><span class="sxs-lookup"><span data-stu-id="85951-125">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="85951-126">Il montre également comment configurer une génération automatique dans Team Foundation Service pour cet exemple de projet.</span><span class="sxs-lookup"><span data-stu-id="85951-126">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="85951-127">Structure du référentiel</span><span class="sxs-lookup"><span data-stu-id="85951-127">Repository structure</span></span>

<span data-ttu-id="85951-128">Notre projet de démonstration est un outil en ligne de commande simple qui utilise l’argument de ligne de commande pour interroger Bing.</span><span class="sxs-lookup"><span data-stu-id="85951-128">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="85951-129">Il cible .NET Framework 4 et utilise une grande partie des [packages BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) et [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="85951-129">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="85951-130">La structure du référentiel se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="85951-130">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="85951-131">Vous pouvez voir que nous n’avons pas archivé le dossier `packages` ni les fichiers `.targets`.</span><span class="sxs-lookup"><span data-stu-id="85951-131">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="85951-132">Nous avons, toutefois, archivé le fichier `nuget.exe`, car il est nécessaire pour le processus de génération.</span><span class="sxs-lookup"><span data-stu-id="85951-132">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="85951-133">En suivant les conventions couramment utilisées, nous l’avons archivé dans un dossier `tools` partagé.</span><span class="sxs-lookup"><span data-stu-id="85951-133">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="85951-134">Le code source se trouve dans le dossier `src`.</span><span class="sxs-lookup"><span data-stu-id="85951-134">The source code is under the `src` folder.</span></span> <span data-ttu-id="85951-135">Notre démonstration utilise une seule solution. Toutefois, ce dossier pourrait tout à fait contenir plusieurs solutions.</span><span class="sxs-lookup"><span data-stu-id="85951-135">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="85951-136">Ignorer les fichiers</span><span class="sxs-lookup"><span data-stu-id="85951-136">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="85951-137">Il existe actuellement un [bogue connu dans le client NuGet](https://nuget.codeplex.com/workitem/4072), à cause duquel le client continue d’ajouter le dossier `packages` à la gestion de versions.</span><span class="sxs-lookup"><span data-stu-id="85951-137">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="85951-138">Pour contourner ce problème, désactivez l’intégration du contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="85951-138">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="85951-139">Vous aurez besoin pour cela d’un fichier `Nuget.Config ` dans le dossier `.nuget`, parallèle à votre solution.</span><span class="sxs-lookup"><span data-stu-id="85951-139">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="85951-140">Si ce dossier n’existe pas encore, créez-le.</span><span class="sxs-lookup"><span data-stu-id="85951-140">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="85951-141">Dans [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), ajoutez le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="85951-141">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="85951-142">Pour informer la gestion de version que notre intention n’est pas d’archiver les dossiers des **packages**, nous avons également ajouté une option « ignorer les fichiers » pour la gestion de version git (`.gitignore`) et Team Foundation (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="85951-142">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="85951-143">Ces fichiers décrivent les modèles des fichiers que vous ne souhaitez pas archiver.</span><span class="sxs-lookup"><span data-stu-id="85951-143">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="85951-144">Le fichier `.gitignore` se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="85951-144">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="85951-145">Le fichier `.gitignore` est [très puissant](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="85951-145">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="85951-146">Par exemple, si vous ne souhaitez pas archiver le contenu du dossier `packages`, mais souhaitez archiver les fichiers `.targets`, vous pouvez utiliser la règle suivante :</span><span class="sxs-lookup"><span data-stu-id="85951-146">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="85951-147">Cela exclut tous les dossiers `packages`, mais inclut de nouveau tous les fichiers `.targets` contenus.</span><span class="sxs-lookup"><span data-stu-id="85951-147">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="85951-148">Pour obtenir un modèle de fichier `.gitignore` conçu spécialement pour les besoins des développeurs Visual Studio, [cliquez ici](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="85951-148">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="85951-149">La gestion de versions Team Foundation prend en charge un mécanisme très similaire via le fichier [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control).</span><span class="sxs-lookup"><span data-stu-id="85951-149">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="85951-150">La syntaxe est pratiquement la même :</span><span class="sxs-lookup"><span data-stu-id="85951-150">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="85951-151">build.proj</span><span class="sxs-lookup"><span data-stu-id="85951-151">build.proj</span></span>

<span data-ttu-id="85951-152">Pour notre démonstration, nous présentons un processus de génération relativement simple.</span><span class="sxs-lookup"><span data-stu-id="85951-152">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="85951-153">Nous allons créer un projet MSBuild qui génère toutes les solutions en veillant à ce que les packages soient restaurés avant la génération des solutions.</span><span class="sxs-lookup"><span data-stu-id="85951-153">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="85951-154">Ce projet aura trois cibles conventionnelles (`Clean`, `Build` et `Rebuild`), ainsi qu’une nouvelle cible (`RestorePackages`).</span><span class="sxs-lookup"><span data-stu-id="85951-154">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="85951-155">Les cibles `Build` et `Rebuild` dépendent toutes les deux de `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="85951-155">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="85951-156">Vous avez ainsi la garantie de pouvoir exécuter `Build` et `Rebuild`, et de compter sur les packages en cours de restauration.</span><span class="sxs-lookup"><span data-stu-id="85951-156">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="85951-157">`Clean`, `Build` et `Rebuild` appellent la cible MSBuild correspondante dans tous les fichiers solution.</span><span class="sxs-lookup"><span data-stu-id="85951-157">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="85951-158">La cible `RestorePackages` appelle `nuget.exe` pour chaque fichier solution.</span><span class="sxs-lookup"><span data-stu-id="85951-158">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="85951-159">Pour cela, utilisez la [fonctionnalité de traitement par lots de MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="85951-159">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="85951-160">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="85951-160">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="85951-161">Configuration de Team Build</span><span class="sxs-lookup"><span data-stu-id="85951-161">Configuring Team Build</span></span>

<span data-ttu-id="85951-162">Team Build propose divers modèles de processus.</span><span class="sxs-lookup"><span data-stu-id="85951-162">Team Build offers various process templates.</span></span> <span data-ttu-id="85951-163">Pour cette démonstration, nous utilisons Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="85951-163">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="85951-164">Les installations locales de TFS sont cependant très similaires.</span><span class="sxs-lookup"><span data-stu-id="85951-164">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="85951-165">Les modèles Team Build sont différents pour Git et pour la gestion de versions Team Foundation. Par conséquent, les étapes suivantes vont varier selon le système de gestion de versions que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="85951-165">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="85951-166">Dans les deux cas, vous avez seulement à sélectionner le fichier build.proj comme le projet que vous souhaitez générer.</span><span class="sxs-lookup"><span data-stu-id="85951-166">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="85951-167">Tout d’abord, examinons le modèle de processus pour git.</span><span class="sxs-lookup"><span data-stu-id="85951-167">First, let's look at the process template for git.</span></span> <span data-ttu-id="85951-168">Dans le modèle git, la génération est sélectionnée via la propriété `Solution to build` :</span><span class="sxs-lookup"><span data-stu-id="85951-168">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Processus de génération pour git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="85951-170">Notez que cette propriété est un emplacement de votre référentiel.</span><span class="sxs-lookup"><span data-stu-id="85951-170">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="85951-171">Étant donné que notre `build.proj` se trouve à la racine, nous avons simplement utilisé `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="85951-171">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="85951-172">Si vous placez le fichier de build dans un dossier appelé `tools`, la valeur sera `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="85951-172">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="85951-173">Dans le modèle de gestion de versions Team Foundation, le projet est sélectionné via la propriété `Projects` :</span><span class="sxs-lookup"><span data-stu-id="85951-173">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Processus de génération pour la gestion de versions Team Foundation](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="85951-175">Contrairement au modèle git, le modèle de gestion de versions Team Foundation prend en charge les sélecteurs (le bouton situé à droite des trois points).</span><span class="sxs-lookup"><span data-stu-id="85951-175">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="85951-176">Par conséquent, afin d’éviter les éventuelles erreurs de frappe, nous vous suggérons de les utiliser pour sélectionner le projet.</span><span class="sxs-lookup"><span data-stu-id="85951-176">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
