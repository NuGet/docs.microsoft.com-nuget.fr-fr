---
title: Notes de publication de NuGet 4.3 RTM
description: Notes de publication de NuGet 4.4 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822654"
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="a98b0-103">Notes de publication de NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="a98b0-103">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="a98b0-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.3 RTM, qui ajoute la prise en charge de nouveaux scénarios tels que .NET Standard 2.0/.NET Core 2.0, contient de nombreux correctifs de qualité et améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="a98b0-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="a98b0-105">Cette version offre également plusieurs améliorations comme la prise en charge de la Gestion sémantique de version 2.0.0, l’intégration MSBuild des avertissements et erreurs NuGet, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="a98b0-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a98b0-106">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="a98b0-106">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="a98b0-107">La restauration NuGet peut dans certains cas traiter des sources de packages désactivées comme étant activées</span><span class="sxs-lookup"><span data-stu-id="a98b0-107">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="a98b0-108">Problème</span><span class="sxs-lookup"><span data-stu-id="a98b0-108">Issue</span></span>

<span data-ttu-id="a98b0-109">Les techniques des lignes de commande de restauration suivantes traitent les sources de packages désactivées comme étant activées.</span><span class="sxs-lookup"><span data-stu-id="a98b0-109">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="a98b0-110">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="a98b0-110">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="a98b0-111">`dotnet restore` (concerne le dotnet.exe fourni avec Visual Studio ou la version livrée avec le SDK NetCore 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="a98b0-111">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a98b0-112">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="a98b0-112">Workaround</span></span>

1. <span data-ttu-id="a98b0-113">Utilisez Visual Studio (2017 15.3 ou ultérieur) ou NuGet.exe (v4.3.0 ou ultérieur)</span><span class="sxs-lookup"><span data-stu-id="a98b0-113">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="a98b0-114">Supprimez votre source désactivée, puis continuez à utiliser msbuild ou dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="a98b0-114">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="a98b0-115">Pour votre solution, vous pouvez utiliser « Clear » dans NuGet.config puis définir les sources nécessaires pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="a98b0-115">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="a98b0-116">Lors de l’utilisation de la Console du Gestionnaire de Package, la touche « Entrée » peut ne pas fonctionner</span><span class="sxs-lookup"><span data-stu-id="a98b0-116">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="a98b0-117">Problème</span><span class="sxs-lookup"><span data-stu-id="a98b0-117">Issue</span></span>

<span data-ttu-id="a98b0-118">Parfois, la touche Entrée ne fonctionne pas dans la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="a98b0-118">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="a98b0-119">Si cela se produit, vérifiez l’évolution du correctif et spécifiez les éventuelles informations supplémentaires utiles dans les étapes de reproduction du problème.</span><span class="sxs-lookup"><span data-stu-id="a98b0-119">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="a98b0-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="a98b0-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a98b0-121">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="a98b0-121">Workaround</span></span>

<span data-ttu-id="a98b0-122">Redémarrez Visual Studio et ouvrez la console de gestion des packages avant d’ouvrir la solution.</span><span class="sxs-lookup"><span data-stu-id="a98b0-122">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="a98b0-123">Vous pouvez aussi tenter de supprimer le `project.lock.json` et de réeffectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="a98b0-123">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="a98b0-124">Impossible d’afficher, d’ajouter ou de mettre à jour DotNetCLITools à l’aide du Gestionnaire de package NuGet</span><span class="sxs-lookup"><span data-stu-id="a98b0-124">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="a98b0-125">Problème</span><span class="sxs-lookup"><span data-stu-id="a98b0-125">Issue</span></span>

<span data-ttu-id="a98b0-126">Le Gestionnaire de package NuGet ne s’affiche pas et n’autorise pas l’ajout/mise à jour de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="a98b0-126">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="a98b0-127">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="a98b0-127">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="a98b0-128">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="a98b0-128">Workaround</span></span>

<span data-ttu-id="a98b0-129">Vous devez modifier manuellement DotNetCLIToolReferences dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="a98b0-129">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="a98b0-130">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes</span><span class="sxs-lookup"><span data-stu-id="a98b0-130">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="a98b0-131">Problème</span><span class="sxs-lookup"><span data-stu-id="a98b0-131">Issue</span></span>

<span data-ttu-id="a98b0-132">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a98b0-132">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="a98b0-133">Cela se produit quand vous utilisez PackageReferences comme format de gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="a98b0-133">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="a98b0-134">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="a98b0-134">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="a98b0-135">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="a98b0-135">Workaround</span></span>

<span data-ttu-id="a98b0-136">Effectuez une restauration manuelle.</span><span class="sxs-lookup"><span data-stu-id="a98b0-136">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="a98b0-137">Problèmes résolus dans NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="a98b0-137">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="a98b0-138">[Notes de publication de NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md) : répertorie tous les problèmes résolus dans NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="a98b0-138">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="a98b0-139">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="a98b0-139">Features</span></span>

- <span data-ttu-id="a98b0-140">Amélioration des performances de restauration NuGet - Implémentation de NoOp plus intelligent pour les restaurations sur la ligne de commande et VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="a98b0-140">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="a98b0-141">NET Core 2.0 : l’interface de ligne de commande VS/Dotnet doit commencer à utiliser les fonctionnalités existantes de NuGet : dossiers de secours - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="a98b0-141">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="a98b0-142">NET Core 2.0 : Permet aux utilisateurs d’ignorer des avertissements de restauration spécifiques (ou de les promouvoir en erreur) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="a98b0-142">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="a98b0-143">NET Core 2.0 : assemblys CLI localisés - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="a98b0-143">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="a98b0-144">NET Core 2.0 : inscription de tous les avertissements/erreurs dans le fichier de ressources (notamment PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="a98b0-144">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="a98b0-145">Activation de la prise en charge TFM : NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="a98b0-145">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="a98b0-146">Réduction du nombre de projets NuGet.Core et NuGet.Client (et donc de DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="a98b0-146">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="a98b0-147">Ajout de la possibilité de marquer des avertissements nuget comme des erreurs - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="a98b0-147">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="a98b0-148">Bogues</span><span class="sxs-lookup"><span data-stu-id="a98b0-148">Bugs</span></span>

- <span data-ttu-id="a98b0-149">msbuild /t:pack échoue avec l’erreur Le paramètre « DevelopmentDependency » n’est pas pris en charge par la tâche « PackTask » - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="a98b0-149">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="a98b0-150">La structure de répertoires des fichiers de contenu est aplatie si vous n’ajoutez pas de séparateur de répertoire Windows à la fin de PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="a98b0-150">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="a98b0-151">Les projets netcore ne prennent pas en charge le paramétrage en tant que developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="a98b0-151">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="a98b0-152">RestoreManagerPackage chargé de façon synchrone, ce qui bloquait le thread d’interface utilisateur et provoquait un interblocage de VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="a98b0-152">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="a98b0-153">dotnet</span><span class="sxs-lookup"><span data-stu-id="a98b0-153">dotnet</span></span>
  - <span data-ttu-id="a98b0-154">dotnetcore restore (et par conséquent msbuild /t:restore) ignore les projets avec une dépendance de projet de solution explicite [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="a98b0-154">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="a98b0-155">Si votre solution a des références de projet qui référencent le même projet avec une casse différente, la restauration risque de ne pas fonctionner.</span><span class="sxs-lookup"><span data-stu-id="a98b0-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="a98b0-156">Cela affecte également les chemins relatifs différents sans différence de casse - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="a98b0-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="a98b0-157">Les fichiers exécutables restaurés à partir de packages NuGet ne sont plus exécutables avec .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="a98b0-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="a98b0-158">NuGet.exe avale les détails d’exception lors de l’analyse du fichier de solution - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="a98b0-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="a98b0-159">Le pack place les fichiers de contenu à un emplacement incorrect si ContentTargetFolders contient un chemin qui se termine par « / » sur Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="a98b0-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="a98b0-160">Impossible de restaurer un DotNetCliToolReference pour un package d’outils qui cible netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="a98b0-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="a98b0-161">L’interface de ligne de commande de mise à jour de NuGet laisse l’ancienne condition de version de package dans le fichier de projet (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="a98b0-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a98b0-162">DCR</span><span class="sxs-lookup"><span data-stu-id="a98b0-162">DCRs</span></span>

- <span data-ttu-id="a98b0-163">Lecture de DotnetCliToolTargetFramework à partir de la nomination CPS - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="a98b0-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="a98b0-164">La vérification TPMinV doit fonctionner pour les applications UWP de style pj - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="a98b0-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="a98b0-165">Amélioration de la description de l’interface utilisateur pour les packages AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="a98b0-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="a98b0-166">NuGet restore sélectionne des ressources de compilation à partir de la section de runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b0-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="a98b0-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="a98b0-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="a98b0-168">Placement des diagnostics de dépendances dans le fichier de verrouillage - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="a98b0-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="a98b0-169">Liens vers les problèmes GitHub corrigés dans RTM 4.3</span><span class="sxs-lookup"><span data-stu-id="a98b0-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="a98b0-170">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="a98b0-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
