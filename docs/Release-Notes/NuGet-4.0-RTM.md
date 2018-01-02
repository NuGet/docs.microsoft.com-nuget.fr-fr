---
title: Notes de publication de NuGet 4.0 RC | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: "Notes de publication pour NuGet 4.0 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR."
keywords: "notes de publication de NuGet 4.0 RTM, correctifs de bogues, problèmes connus, fonctionnalités ajoutées, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a><span data-ttu-id="ed73d-104">Notes de publication de la version 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="ed73d-104">4.0 RTM Release Notes</span></span>

<span data-ttu-id="ed73d-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.0, qui ajoute la prise en charge de .NET Core, intègre un ensemble de correctifs de qualité et améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="ed73d-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="ed73d-106">Cette version offre aussi plusieurs améliorations telles que la prise en charge de PackageReference, des commandes NuGet comme cibles MSBuild, la restauration des packages en arrière-plan, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="ed73d-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ed73d-107">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="ed73d-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="ed73d-108">La restauration NuGet peut échouer quand plusieurs projets référencent un autre projet dans une solution</span><span class="sxs-lookup"><span data-stu-id="ed73d-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="ed73d-109">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-109">Issue:</span></span>
<span data-ttu-id="ed73d-110">La restauration NuGet peut ne pas fonctionner si, dans une solution, vous avez des références de projet au projet même avec une casse différente ou avec différents chemins relatifs.</span><span class="sxs-lookup"><span data-stu-id="ed73d-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="ed73d-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="ed73d-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="ed73d-112">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-112">Workaround:</span></span>
<span data-ttu-id="ed73d-113">Corrigez les casses ou les chemins relatifs pour qu’ils soient identiques pour toutes les références de projet.</span><span class="sxs-lookup"><span data-stu-id="ed73d-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="ed73d-114">Lors de l’utilisation de la Console du Gestionnaire de Package, la touche « Entrée » peut ne pas fonctionner</span><span class="sxs-lookup"><span data-stu-id="ed73d-114">While using Package Manager Console, 'Enter' key may not work</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-115">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-115">Issue:</span></span>
<span data-ttu-id="ed73d-116">Parfois, la touche Entrée ne fonctionne pas dans la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="ed73d-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="ed73d-117">Si cela se produit, vérifiez l’évolution du correctif et spécifiez les éventuelles informations supplémentaires utiles dans les étapes de reproduction du problème.</span><span class="sxs-lookup"><span data-stu-id="ed73d-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="ed73d-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="ed73d-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="ed73d-119">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-119">Workaround:</span></span>
<span data-ttu-id="ed73d-120">Redémarrez Visual Studio et ouvrez la console de gestion des packages avant d’ouvrir la solution.</span><span class="sxs-lookup"><span data-stu-id="ed73d-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="ed73d-121">Vous pouvez aussi tenter de supprimer le `project.lock.json` et de réeffectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="ed73d-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="ed73d-122">Dans les projets .NET Core, vous pouvez vous retrouver avec une boucle de restauration infinie quand vous utilisez un package qui contient un assembly avec une signature non valide</span><span class="sxs-lookup"><span data-stu-id="ed73d-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-123">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-123">Issue:</span></span>
<span data-ttu-id="ed73d-124">Parfois, quand vous utilisez un package qui contient un assembly avec une signature non valide, ou quand la version du package est définie avec 'DateTime', la restauration automatique de package s’exécute dans une boucle infinie.</span><span class="sxs-lookup"><span data-stu-id="ed73d-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="ed73d-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="ed73d-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="ed73d-126">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-126">Workaround:</span></span>
<span data-ttu-id="ed73d-127">Il n’existe aucune solution de contournement pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="ed73d-127">There is no workaround at this time.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="ed73d-128">Vous ne pouvez pas afficher, ajouter ou mettre à jour DotNetCLITools à l’aide du Gestionnaire de package Nuget</span><span class="sxs-lookup"><span data-stu-id="ed73d-128">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-129">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-129">Issue:</span></span>
<span data-ttu-id="ed73d-130">Le Gestionnaire de package NuGet ne s’affiche pas et n’autorise pas l’ajout/mise à jour de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="ed73d-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="ed73d-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="ed73d-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a><span data-ttu-id="ed73d-132">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-132">Workaround:</span></span>
<span data-ttu-id="ed73d-133">Vous devez modifier manuellement DotNetCLIToolReferences dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="ed73d-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="ed73d-134">La restauration NuGet échoue quand vous définissez la propriété PackageId pour des projets</span><span class="sxs-lookup"><span data-stu-id="ed73d-134">NuGet restore will fail when you set PackageId property for projects</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-135">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-135">Issue:</span></span>
<span data-ttu-id="ed73d-136">Pour les projets .NET Core, la restauration NuGet dans Visual Studio ne respecte pas la propriété PackageId des projets.</span><span class="sxs-lookup"><span data-stu-id="ed73d-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="ed73d-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="ed73d-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="ed73d-138">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-138">Workaround:</span></span>
<span data-ttu-id="ed73d-139">Exécutez la restauration à l’aide de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="ed73d-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="ed73d-140">Quand votre projet n’a pas de dossier « obj », la restauration du package peut échouer</span><span class="sxs-lookup"><span data-stu-id="ed73d-140">When your project does not have 'obj' folder, package restore may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-141">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-141">Issue:</span></span>
<span data-ttu-id="ed73d-142">Visual Studio ne parvient pas à restaurer PackageReferences quand le dossier « obj » a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="ed73d-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="ed73d-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="ed73d-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="ed73d-144">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-144">Workaround:</span></span>
<span data-ttu-id="ed73d-145">Créez manuellement le dossier « obj » ; la restauration devrait alors fonctionner.</span><span class="sxs-lookup"><span data-stu-id="ed73d-145">Create 'obj' folder manually and the restore should work.</span></span> 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="ed73d-146">La mise à jour manuelle des packages à l’aide de Update-Package dans la console peut échouer</span><span class="sxs-lookup"><span data-stu-id="ed73d-146">Manually updating packages using Update-Package in console may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-147">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-147">Issue:</span></span>
<span data-ttu-id="ed73d-148">L’utilisation manuelle d’Update-Package dans la console ne fonctionne qu’une seule fois pour les projets PackageReferences qui viennent d’être convertis.</span><span class="sxs-lookup"><span data-stu-id="ed73d-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="ed73d-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="ed73d-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="ed73d-150">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-150">Workaround:</span></span>
<span data-ttu-id="ed73d-151">Il n’existe aucune solution de contournement pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="ed73d-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="ed73d-152">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes</span><span class="sxs-lookup"><span data-stu-id="ed73d-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>
#### <a name="issue"></a><span data-ttu-id="ed73d-153">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-153">Issue:</span></span>
<span data-ttu-id="ed73d-154">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed73d-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="ed73d-155">Cela se produit quand vous utilisez PackageReferences comme format de gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="ed73d-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="ed73d-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="ed73d-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="ed73d-157">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-157">Workaround:</span></span>
<span data-ttu-id="ed73d-158">Effectuez une restauration manuelle.</span><span class="sxs-lookup"><span data-stu-id="ed73d-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="ed73d-159">`msbuild /t:restore` échoue quand un projet ciblant .NET461 référence un autre projet ciblant .NETStandard</span><span class="sxs-lookup"><span data-stu-id="ed73d-159">`msbuild /t:restore` fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="ed73d-160">Problème :</span><span class="sxs-lookup"><span data-stu-id="ed73d-160">Issue:</span></span>
<span data-ttu-id="ed73d-161">msbuild /t:restore échoue quand un projet basé sur PackageReference ciblant .NET461 référence un autre projet basé sur PackageReference ciblant .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="ed73d-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="ed73d-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="ed73d-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="ed73d-163">Solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="ed73d-163">Workaround:</span></span>
<span data-ttu-id="ed73d-164">Il n’existe aucune solution de contournement pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="ed73d-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="ed73d-165">Problèmes résolus dans NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="ed73d-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="ed73d-166">[Notes de publication de NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) : répertorie tous les problèmes résolus dans NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="ed73d-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

<span data-ttu-id="ed73d-167">**Bogues :**</span><span class="sxs-lookup"><span data-stu-id="ed73d-167">**Bug:**</span></span>

* <span data-ttu-id="ed73d-168">La restauration NuGet dans Visual Studio ne respecte pas la propriété PackageId des projets - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="ed73d-168">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

* <span data-ttu-id="ed73d-169">Erreur NuGet ProjectSystemCache lors de l’ajout d’un package dans un package vsix - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="ed73d-169">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

* <span data-ttu-id="ed73d-170">Le pack lève une exception si IncludeSource est utilisé dans un projet avec plusieurs TFM - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="ed73d-170">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

* <span data-ttu-id="ed73d-171">VS 2017 RC3 se bloque lors de l’utilisation de la mise à jour à partir de la gestion de package à l’échelle de la solution - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="ed73d-171">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

* <span data-ttu-id="ed73d-172">Impossible de désinstaller un package nouvellement installé - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="ed73d-172">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

* <span data-ttu-id="ed73d-173">Lors de la migration vers PackageRef, les solutions hybrides ont un comportement de restauration étrange - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="ed73d-173">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

* <span data-ttu-id="ed73d-174">La génération peu après le démarrage d’une opération NuGet (installation, mise à jour, restauration) peut provoquer le blocage de VS - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="ed73d-174">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

* <span data-ttu-id="ed73d-175">Blocage de l’interface utilisateur : interblocage lors de l’initialisation de NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="ed73d-175">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

* <span data-ttu-id="ed73d-176">La commande add package doit ajouter la version en tant qu’attribut au lieu d’élément - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="ed73d-176">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

* <span data-ttu-id="ed73d-177">Dotnet Restore foo.sln -- échoue quand des configurations dans SLN provoquent la présence de projets en double (mais avec des configurations différentes) dans le graphique de restauration - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="ed73d-177">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

* <span data-ttu-id="ed73d-178">Packages de contenu uniquement - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="ed73d-178">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

* <span data-ttu-id="ed73d-179">Par défaut, ignorer l’option de sélection du format de package - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="ed73d-179">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

* <span data-ttu-id="ed73d-180">Performances : Le projet CreateUAP_CSharp_VS.01.1.Create a diminué Duration_TotalElapsedTime de 3 153,570 ms (149,1 %).</span><span class="sxs-lookup"><span data-stu-id="ed73d-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="ed73d-181">Ligne de base 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="ed73d-181">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

* <span data-ttu-id="ed73d-182">Performances : La solution ManagedLangs_CS_DDRIT.0300.Rebuild a diminué Duration_TotalElapsedTime de 1,5 seconde.</span><span class="sxs-lookup"><span data-stu-id="ed73d-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="ed73d-183">Ligne de base de 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="ed73d-183">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

* <span data-ttu-id="ed73d-184">La nomination échoue dans les projets multi-TFM - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="ed73d-184">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

* <span data-ttu-id="ed73d-185">Performances : La solution WebForms_DDRIT.1200.Close a diminué VM_ImagesInMemory_Total_devenv de 3,000 (0,5 %).</span><span class="sxs-lookup"><span data-stu-id="ed73d-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="ed73d-186">Ligne de base 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="ed73d-186">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

* <span data-ttu-id="ed73d-187">vsfeedback - Avertissements de pack lors du ciblage de netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="ed73d-187">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

* <span data-ttu-id="ed73d-188">PathTooLongException lors de la tentative d’ajout d’un package NuGet à une application web ASP.NET Core vide - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="ed73d-188">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

* <span data-ttu-id="ed73d-189">Le pack s’exécute trop souvent -- Échec de dotnet pack avec l’erreur Il existe une dépendance circulaire dans le graphique de dépendance cible qui implique la cible « Pack » - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="ed73d-189">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

* <span data-ttu-id="ed73d-190">Le pack s’exécute trop souvent -- La génération de package NuGet n’inclut pas toutes les configurations - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="ed73d-190">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

* <span data-ttu-id="ed73d-191">NullReferenceException : ajout de nuget avec packageref dans le projet C++ - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="ed73d-191">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

* <span data-ttu-id="ed73d-192">Accessibilité : Le narrateur n’effectue pas la narration de la case à cocher pour sélectionner les projets dans lesquels installer le package- [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="ed73d-192">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

* <span data-ttu-id="ed73d-193">NuGet VS17 ne parvient pas toujours à se connecter aux flux VSO/VSTS - Bogue VS 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="ed73d-193">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

* <span data-ttu-id="ed73d-194">contentFiles envoie la sortie vers un emplacement incorrect si PackagePath spécifie « contentFiles » comme chemin - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="ed73d-194">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

* <span data-ttu-id="ed73d-195">La cible de pack ajoute la propriété PackageVersion avec VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="ed73d-195">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

* <span data-ttu-id="ed73d-196">La spécification du chemin du package ne fonctionne pas avec dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="ed73d-196">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

* <span data-ttu-id="ed73d-197">NuGet génère un ensemble d’avertissements à propos des importations en double pendant la restauration - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="ed73d-197">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

* <span data-ttu-id="ed73d-198">Le choix de la boîte de dialogue « Format du Gestionnaire de Package NuGet » semble incorrect dans le thème sombre - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="ed73d-198">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

* <span data-ttu-id="ed73d-199">Blocage de Visual Studio lors de la restauration de la build - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="ed73d-199">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

* <span data-ttu-id="ed73d-200">Interblocages de Visual Studio si vous ajoutez TFM dans targetframeworks, enregistrez, puis générez.</span><span class="sxs-lookup"><span data-stu-id="ed73d-200">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="ed73d-201">10 % du temps - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="ed73d-201">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

* <span data-ttu-id="ed73d-202">nuget pack ne génère pas de message de réussite en cas d’empaquetage correct d’un projet - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="ed73d-202">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

* <span data-ttu-id="ed73d-203">PackTask échoue car System.IO.Compression 4.1 est introuvable - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="ed73d-203">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

* <span data-ttu-id="ed73d-204">Le pack s’exécute trop souvent -- PackTask échoue souvent avec un conflit d’accès aux fichiers - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="ed73d-204">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

* <span data-ttu-id="ed73d-205">NuGet ouvre la fenêtre de sortie pendant la restauration en arrière-plan - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="ed73d-205">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

* <span data-ttu-id="ed73d-206">Éliminer ServiceProvider en tant que modèle de codage dangereux (susceptible de provoquer des blocages) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="ed73d-206">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

* <span data-ttu-id="ed73d-207">Performances/blocage de l’interface utilisateur - Améliorer les lectures DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="ed73d-207">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

* <span data-ttu-id="ed73d-208">Interblocage de Visual Studio si vous essayez de fermer un projet avant la fin de la restauration NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="ed73d-208">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

* <span data-ttu-id="ed73d-209">Problèmes liés à PackTask et à l’empaquetage `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="ed73d-209">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

* <span data-ttu-id="ed73d-210">[vsfeedback] Impossible de résoudre les packages nuget sur un nouveau projet (nécessité de redémarrer visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="ed73d-210">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

* <span data-ttu-id="ed73d-211">[vsfeedback] La liste déroulante « Version » qui affiche les versions de package disponibles a du mal à rester synchronisée avec le package nuGet sélectionné... - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="ed73d-211">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

* <span data-ttu-id="ed73d-212">Nuget.Client doit utiliser CPS JoinableTaskFactory lors de l’interaction avec CPS pour éviter les interblocages - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="ed73d-212">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

* <span data-ttu-id="ed73d-213">NuGet 3.5.0 ne décompresse pas `.targets` à partir du package - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="ed73d-213">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

* <span data-ttu-id="ed73d-214">dotnet pack ne prend pas en charge le titre dans `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="ed73d-214">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

* <span data-ttu-id="ed73d-215">Install-Package génère une boîte de dialogue d’erreur dans VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="ed73d-215">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

* <span data-ttu-id="ed73d-216">La mise à jour d’un package pour un projet .net core semble ne pas fonctionner, car l’interface utilisateur n’obtient pas la mise à jour CPS à partir de la nomination.</span><span class="sxs-lookup"><span data-stu-id="ed73d-216">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="ed73d-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="ed73d-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

* <span data-ttu-id="ed73d-218">Améliorer l’avertissement de référence non résolue - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="ed73d-218">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

* <span data-ttu-id="ed73d-219">dotnet pack - ProjectReference perd les informations de version - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="ed73d-219">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

* <span data-ttu-id="ed73d-220">Création d’application UWP - régressions de durée totale écoulée pour la création de projet et la régénération - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="ed73d-220">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

* <span data-ttu-id="ed73d-221">Un message de fin de restauration s’affiche même après une erreur pendant la restauration.</span><span class="sxs-lookup"><span data-stu-id="ed73d-221">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="ed73d-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="ed73d-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

* <span data-ttu-id="ed73d-223">Republier Nuget.CommandLine 3.4.4 sur Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="ed73d-223">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

* <span data-ttu-id="ed73d-224">Lors de la migration, le projet change de `project.json` à `.csproj` --- la restauration échoue - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="ed73d-224">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

* <span data-ttu-id="ed73d-225">Échec de restauration en cas de projet de test xunit nouvellement créé - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="ed73d-225">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

* <span data-ttu-id="ed73d-226">Les projets Core peuvent se bloquer, verrouiller l’interface utilisateur à l’ouverture - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="ed73d-226">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

* <span data-ttu-id="ed73d-227">Corriger le fichier de cibles pour les tâches de génération - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="ed73d-227">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

* <span data-ttu-id="ed73d-228">La liste d’erreurs contient une erreur après la génération d’une solution qui décharge le projet référencé - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="ed73d-228">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

* <span data-ttu-id="ed73d-229">MSB4057 : L’objet « _GenerateRestoreGraphProjectEntry » cible n’existe pas dans le projet.</span><span class="sxs-lookup"><span data-stu-id="ed73d-229">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="ed73d-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="ed73d-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

* <span data-ttu-id="ed73d-231">vsfeedback : l’interface utilisateur du gestionnaire nuget pour la solution se bloque quand vous sélectionnez tous les projets - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="ed73d-231">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

* <span data-ttu-id="ed73d-232">nuget.exe msbuildpath échoue quand il y a une barre oblique de fin - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="ed73d-232">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

* <span data-ttu-id="ed73d-233">vsfeedback : NuGet restore génère plusieurs avertissements de référence de projet pour un projet LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="ed73d-233">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

* <span data-ttu-id="ed73d-234">Le pack de `.csproj` n’inclut pas l’attribut minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="ed73d-234">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

* <span data-ttu-id="ed73d-235">NuGet.Build.Tasks.Pack.dll fournie est signée avec retard dans VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="ed73d-235">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

* <span data-ttu-id="ed73d-236">VSFeedback : Échec de restauration d’un projet VS 2015 généré avec CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="ed73d-236">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

* <span data-ttu-id="ed73d-237">VSFeedback : Des erreurs de restauration peuvent masquer des messages d’erreur plus complets que la build pourrait donner - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="ed73d-237">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

* <span data-ttu-id="ed73d-238">[VSFeedback] Une erreur s’est produite lors de la restauration des packages NuGet pour le projet de site web : la valeur ne peut pas être null.</span><span class="sxs-lookup"><span data-stu-id="ed73d-238">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="ed73d-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="ed73d-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

* <span data-ttu-id="ed73d-240">La migration lève « Exception de référence d’objet » dans NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="ed73d-240">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

* <span data-ttu-id="ed73d-241">dotnet pack doit empaqueter les outils avec les versions par rapport auxquelles le package a été créé - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="ed73d-241">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

* <span data-ttu-id="ed73d-242">Une nouvelle restauration en arrière-plan écrit des millisecondes dans la barre d’état alors que la restauration prend plusieurs secondes - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="ed73d-242">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

* <span data-ttu-id="ed73d-243">Faute de frappe lors d’un échec de résolution de toutes les références de projet - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="ed73d-243">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

* <span data-ttu-id="ed73d-244">Activer les flux de travail PCM dans les scénarios de référence de package - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="ed73d-244">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

* <span data-ttu-id="ed73d-245">Packages installés introuvables dans l’interface utilisateur du Gestionnaire de package - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="ed73d-245">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

* <span data-ttu-id="ed73d-246">dotnet pack échoue quand PackagePath est vide - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="ed73d-246">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

* <span data-ttu-id="ed73d-247">La tâche de restauration échoue dans un scénario à plusieurs utilisateurs - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="ed73d-247">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

* <span data-ttu-id="ed73d-248">Impossible de modifier le type de contenu lors de l’empaquetage à l’aide de la tâche NuGet Pack - [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="ed73d-248">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

* <span data-ttu-id="ed73d-249">La copie par défaut de ContentFiles est incorrecte pour MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="ed73d-249">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

* <span data-ttu-id="ed73d-250">La restauration de package d’installation enregistre deux fois le message de restauration de packages - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="ed73d-250">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

* <span data-ttu-id="ed73d-251">Supprimer Guardrails - La restauration de la section « runtimes » doit s’appliquer uniquement au projet actif - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="ed73d-251">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

* <span data-ttu-id="ed73d-252">La tâche Pack place les fichiers de contenu à la fois dans « content/ » et dans « contentFiles/ » - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="ed73d-252">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

* <span data-ttu-id="ed73d-253">dotnet pack3 effectue un fractionnement de balise supplémentaire - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="ed73d-253">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

* <span data-ttu-id="ed73d-254">dotnet pack : L’empaquetage d’un projet avec des références de package génère un avertissement d’importation en double - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="ed73d-254">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

* <span data-ttu-id="ed73d-255">La journalisation de restauration dans Visual Studio ne s’affiche pas toujours - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="ed73d-255">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

* <span data-ttu-id="ed73d-256">Le texte d’aide de nuget locals mentionnait encore le cache des packages - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="ed73d-256">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

* <span data-ttu-id="ed73d-257">Restore3 associe PackageReferences à TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="ed73d-257">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="ed73d-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="ed73d-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

* <span data-ttu-id="ed73d-259">NuGet récupère une version inattendue de MSBuild dans VS « 15 » Preview 4 dev.</span><span class="sxs-lookup"><span data-stu-id="ed73d-259">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="ed73d-260">invite de commandes - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="ed73d-260">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

* <span data-ttu-id="ed73d-261">Écrire des cibles/fichiers de propriétés lors de l’échec de restauration - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="ed73d-261">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

* <span data-ttu-id="ed73d-262">NuGet pendant la restauration ne respecte pas les mêmes shims de compatibilité que MSBuild lors de l’exécution dans l’invite de commandes de Visual Studio 15 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="ed73d-262">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

* <span data-ttu-id="ed73d-263">Réactiver PackFromProjectWithDevelopmentDependencySet pour VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="ed73d-263">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

* <span data-ttu-id="ed73d-264">Fusionner des problèmes avec NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="ed73d-264">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

* <span data-ttu-id="ed73d-265">Intégrer 4.0.0.2067 dans les dépôts CLI et SDK pour livrer avec RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="ed73d-265">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

* <span data-ttu-id="ed73d-266">Blocage de Visual Studio quand vous créez une application de console Core, fermez la solution, ouvrez la solution puis fermez la solution - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="ed73d-266">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

* <span data-ttu-id="ed73d-267">Blocage lors de l’ouverture de projet contre d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="ed73d-267">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

* <span data-ttu-id="ed73d-268">Corriger le message d’aide/documentation dotnet/nuget.exe locals - [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="ed73d-268">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

* <span data-ttu-id="ed73d-269">Inspecter PackTask à la recherche des problèmes avec les espaces blancs de début ou de fin - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="ed73d-269">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

* <span data-ttu-id="ed73d-270">dotnet pack empaquète à partir d’obj et non bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="ed73d-270">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

* <span data-ttu-id="ed73d-271">dotnet pack semble toujours définir la version de ProjectReference sur 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="ed73d-271">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

* <span data-ttu-id="ed73d-272">dotnet pack échoue avec les références de projet et <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="ed73d-272">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

* <span data-ttu-id="ed73d-273">LockRecursionException dans ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="ed73d-273">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

* <span data-ttu-id="ed73d-274">Supprimer les espaces blancs des propriétés MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="ed73d-274">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

* <span data-ttu-id="ed73d-275">Consolider les deux événements de projets déclenchés lors du chargement du projet - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="ed73d-275">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

* <span data-ttu-id="ed73d-276">Les bibliothèques P2P dans le fichier `project.assets.json` ont une version incorrecte - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="ed73d-276">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

* <span data-ttu-id="ed73d-277">Blocage de la restauration car un flux ne répond pas et un package est indisponible - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="ed73d-277">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

* <span data-ttu-id="ed73d-278">nuget.exe pourrait se bloquer en cas de sortie d’erreur MSBuild volumineuse - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="ed73d-278">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

* <span data-ttu-id="ed73d-279">La restauration au moment de la génération pour Blend échoue la première fois, réussit la deuxième fois (scénario VS corrigé) - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="ed73d-279">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

<span data-ttu-id="ed73d-280">**DCR :**</span><span class="sxs-lookup"><span data-stu-id="ed73d-280">**DCR:**</span></span>

* <span data-ttu-id="ed73d-281">migrer vsix de v2 vsix vers v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="ed73d-281">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

* <span data-ttu-id="ed73d-282">NuGet devrait avoir un mécanisme permettant d’obtenir le chemin du fichier de verrouillage dans MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="ed73d-282">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

* <span data-ttu-id="ed73d-283">Ajouter des ressources de build au contrôle de compatibilité TFM et au fichier de ressources - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="ed73d-283">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

* <span data-ttu-id="ed73d-284">Définir un nouveau « Pack » ProjectCapability dans les cibles Pack pour l’activation des fonctionnalités liées au package - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="ed73d-284">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

* <span data-ttu-id="ed73d-285">Exécuter le pack en tant que cible post-build sous réserve de propriété MSBuild « GeneratePackageOnBuild » - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="ed73d-285">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

* <span data-ttu-id="ed73d-286">Utiliser la propriété NuGet RestoreProjectStyle pour créer un projet NuGet spécifique - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="ed73d-286">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

* <span data-ttu-id="ed73d-287">Adapter la restauration pour changement de références de projet transitives - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="ed73d-287">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

* <span data-ttu-id="ed73d-288">Ajouter des propriétés NuGet dans le fichier cible pour les projets non UWP - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="ed73d-288">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

* <span data-ttu-id="ed73d-289">Prise en charge UWP TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="ed73d-289">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

* <span data-ttu-id="ed73d-290">Communiquer les métadonnées de référence de projet au système de projet NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="ed73d-290">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

* <span data-ttu-id="ed73d-291">Ajouter une interface utilisateur pour le mode d’empaquetage - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="ed73d-291">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

* <span data-ttu-id="ed73d-292">`.csproj` hérité a besoin de NugetTargetMoniker et RuntimeIdentifiers définis dans le projet/les cibles - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="ed73d-292">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

* <span data-ttu-id="ed73d-293">L’installation de package peut chevaucher la restauration automatique - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="ed73d-293">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

* <span data-ttu-id="ed73d-294">Le menu contextuel QueryStatus ne se produit pas quand VSPackage n’est pas chargé - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="ed73d-294">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

* <span data-ttu-id="ed73d-295">La restauration de solution et la restauration de build continuent à afficher des boîtes de dialogue - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="ed73d-295">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

* <span data-ttu-id="ed73d-296">Isoler la version VSSDK dans la build de solution NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="ed73d-296">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

<span data-ttu-id="ed73d-297">**Fonctionnalité :**</span><span class="sxs-lookup"><span data-stu-id="ed73d-297">**Feature:**</span></span>

* <span data-ttu-id="ed73d-298">Localiser les chaînes dans NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="ed73d-298">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

* <span data-ttu-id="ed73d-299">NuGet force le chargement des projets d’application web en mode LSL - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="ed73d-299">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

* <span data-ttu-id="ed73d-300">Prise en charge d’AutoReferenced PackageReference pour bloquer les changements de version dans l’interface utilisateur pour les packages à « sdk installé » - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="ed73d-300">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

* <span data-ttu-id="ed73d-301">Communiquer correctement PackageSpec.Version pour toutes les dépendances de projet (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="ed73d-301">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

* <span data-ttu-id="ed73d-302">Prise en charge de la suppression des références dans `.csproj` à partir de la ligne de commande - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="ed73d-302">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

* <span data-ttu-id="ed73d-303">Prise en charge de la restauration pour les projets PackageReference (normaux et xplat) et le chargement de solution allégé - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="ed73d-303">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

* <span data-ttu-id="ed73d-304">Prise en charge de l’ajout des références dans `.csproj` à partir de la ligne de commande - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="ed73d-304">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

* <span data-ttu-id="ed73d-305">Prise en charge de la restauration NuGet pour le chargement de solution allégé pour `packages.config` ou `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="ed73d-305">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

* <span data-ttu-id="ed73d-306">Prise en charge de contentFiles dans le fichier de cibles généré nuget - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="ed73d-306">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

* <span data-ttu-id="ed73d-307">Établir un Mono CI pour la validation nuget.exe sur Mac à l’aide de MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="ed73d-307">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

* <span data-ttu-id="ed73d-308">Déplacer NuGet hors des dépendances v2 NuGet.Core - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="ed73d-308">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>


## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="ed73d-309">Liens vers les problèmes GitHub corrigés dans la version RTM</span><span class="sxs-lookup"><span data-stu-id="ed73d-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="ed73d-310">Liste des problèmes 1</span><span class="sxs-lookup"><span data-stu-id="ed73d-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="ed73d-311">Liste des problèmes 2</span><span class="sxs-lookup"><span data-stu-id="ed73d-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="ed73d-312">Liste des problèmes 3</span><span class="sxs-lookup"><span data-stu-id="ed73d-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="ed73d-313">Liste des problèmes 4</span><span class="sxs-lookup"><span data-stu-id="ed73d-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="ed73d-314">Liste des problèmes 5</span><span class="sxs-lookup"><span data-stu-id="ed73d-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

