---
title: Notes de publication de NuGet 4.4 RTM
description: Notes de publication de NuGet 4.4 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498701"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="aa6c4-103">Notes de publication de NuGet 4.4</span><span class="sxs-lookup"><span data-stu-id="aa6c4-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="aa6c4-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="aa6c4-105">Résumé: Quoi de neuf en 4.4.0</span><span class="sxs-lookup"><span data-stu-id="aa6c4-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="aa6c4-106">Résumé: Quoi de neuf en 4.4.2</span><span class="sxs-lookup"><span data-stu-id="aa6c4-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="aa6c4-107">Correctif de sécurité : Les autorisations sur les fichiers créés à l’intérieur de l’adresse suivante [: les #7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="aa6c4-108">Résumé: Quoi de neuf en 4.4.3</span><span class="sxs-lookup"><span data-stu-id="aa6c4-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="aa6c4-109">Correctif de sécurité: Les fichiers à l’intérieur des NUPKGs peuvent avoir un chemin relatif au-dessus de l’annuaire NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="aa6c4-110">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="aa6c4-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="aa6c4-111">Problèmes liés à .NET Standard 2.0 avec .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="aa6c4-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="aa6c4-112">.NET Standard et ses outils ont été conçus de façon à ce que les projets qui ciblent le .NET Framework 4.6.1 puissent consommer les projets et les packages NuGet ciblant .NET Standard 2.0 ou antérieur.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="aa6c4-113">[Ce document](https://github.com/dotnet/standard/issues/481) récapitule les problèmes liés à ce scénario et propose des solutions de contournement que vous pouvez déployer avec les outils actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="aa6c4-114">Lors de l’utilisation de la Console du Gestionnaire de Package, la touche « Entrée » peut ne pas fonctionner</span><span class="sxs-lookup"><span data-stu-id="aa6c4-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="aa6c4-115">Problème</span><span class="sxs-lookup"><span data-stu-id="aa6c4-115">Issue</span></span>

<span data-ttu-id="aa6c4-116">Parfois, la touche Entrée ne fonctionne pas dans la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="aa6c4-117">Si cela se produit, vérifiez l’évolution du correctif et spécifiez les éventuelles informations supplémentaires utiles dans les étapes de reproduction du problème.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="aa6c4-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="aa6c4-119">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="aa6c4-119">Workaround</span></span>

<span data-ttu-id="aa6c4-120">Redémarrez Visual Studio et ouvrez la console de gestion des packages avant d’ouvrir la solution.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="aa6c4-121">Vous pouvez aussi tenter de supprimer le `project.lock.json` et de réeffectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="aa6c4-122">Impossible d’afficher, d’ajouter ou de mettre à jour DotNetCLITools à l’aide du Gestionnaire de package NuGet</span><span class="sxs-lookup"><span data-stu-id="aa6c4-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="aa6c4-123">Problème</span><span class="sxs-lookup"><span data-stu-id="aa6c4-123">Issue</span></span>

<span data-ttu-id="aa6c4-124">Le Gestionnaire de package NuGet ne s’affiche pas et n’autorise pas l’ajout/mise à jour de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="aa6c4-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="aa6c4-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="aa6c4-126">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="aa6c4-126">Workaround</span></span>

<span data-ttu-id="aa6c4-127">Vous devez modifier manuellement DotNetCLIToolReferences dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="aa6c4-128">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes</span><span class="sxs-lookup"><span data-stu-id="aa6c4-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="aa6c4-129">Problème</span><span class="sxs-lookup"><span data-stu-id="aa6c4-129">Issue</span></span>

<span data-ttu-id="aa6c4-130">Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="aa6c4-131">Cela se produit quand vous utilisez PackageReferences comme format de gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="aa6c4-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="aa6c4-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="aa6c4-133">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="aa6c4-133">Workaround</span></span>

<span data-ttu-id="aa6c4-134">Effectuez une restauration manuelle.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="aa6c4-135">Un package dans un projet .NET Core qui contient un assembly avec une signature non valide peut déclencher une boucle de restauration infinie</span><span class="sxs-lookup"><span data-stu-id="aa6c4-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="aa6c4-136">Problème</span><span class="sxs-lookup"><span data-stu-id="aa6c4-136">Issue</span></span>

<span data-ttu-id="aa6c4-137">Parfois, quand vous utilisez un package qui contient un assembly avec une signature non valide ou quand la version du package est définie avec le symbole « DateTime », la restauration automatique du package s’exécute dans une boucle infinie (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="aa6c4-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="aa6c4-138">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="aa6c4-138">Workaround</span></span>

<span data-ttu-id="aa6c4-139">Il n’existe aucune solution de contournement pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="aa6c4-140">Problèmes résolus dans NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="aa6c4-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="aa6c4-141">[Notes de publication de NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) : répertorie tous les problèmes résolus dans NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="aa6c4-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="aa6c4-142">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="aa6c4-142">Features</span></span>

- <span data-ttu-id="aa6c4-143">Prise en charge du chargement de solution allégé dans les scénarios d’interface utilisateur de Gestionnaire de package NuGet et PMC - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="aa6c4-144">La cible de pack msbuild doit avoir un raccordement public pour l’exécution des cibles utilisateur avant elle-même - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="aa6c4-145">Fonctionnalité : Ajout du commutateur dependencyVersion à nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="aa6c4-146">uap10.0.TODO.0 doit mapper à .NET Standard 2.0 pour NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="aa6c4-147">Prise en charge du SKU Visual Studio Build Tools avec msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="aa6c4-148">Pendant la restauration, générer une erreur si la prise en charge de .NET 4.6.1 pour .NET 2.0 Standard est nécessaire mais pas installée - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="aa6c4-149">Interface utilisateur de client de réservation de préfixe d’ID de package - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="aa6c4-150">Remise de composants nuget localisés pour prendre en charge la localisation de dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="aa6c4-151">Bogues</span><span class="sxs-lookup"><span data-stu-id="aa6c4-151">Bugs</span></span>

- <span data-ttu-id="aa6c4-152">Différentes casses de chemin de projet peuvent entraîner la perte de PackageReferences par la restauration - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="aa6c4-153">Déplacement des codes d’erreur avec numéros d’avertissement vers la plage d’erreurs - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="aa6c4-154">Erreur trompeuse quand la version de .NET Standard n’est pas connue pour être compatible avec le framework cible - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="aa6c4-155">Fichiers texte avec licences prêtant à confusion - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="aa6c4-156">En-têtes de licence manquants dans les modèles tests EndToEnd - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="aa6c4-157">packages.config restore affiche les erreurs comme NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="aa6c4-158">nuget.exe install doit avoir DisableParallelProcessing sur mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="aa6c4-159">nuget.exe install désactive incorrectement la mise en cache - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="aa6c4-160">Visual Studio : l’exécution de la commande restore pour packages.config quand la restauration est désactivée provoque l’affichage d’un message incorrect - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="aa6c4-161">Visual Studio : l’exécution de la commande restore quand la restauration est désactivée provoque l’affichage d’un message prêtant à confusion : [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="aa6c4-162">GetRestoreDotnetCliToolsTask échoue quand les métadonnées de version sont manquantes - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="aa6c4-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="aa6c4-163">dotnet</span></span>
  - <span data-ttu-id="aa6c4-164">dotnetcore add package peut effacer les lignes vides d’un csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="aa6c4-165">Les noms de sources des paramètres d’informations d’identification dans NuGet.Config respectent la casse - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="aa6c4-166">L’activation de GeneratePackageOnBuild a supprimé tout mon historique des packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="aa6c4-167">Restauration ne restaure pas les packages mono.cecil ou semver, mais tous les autres packages sont restaurés.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="aa6c4-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="aa6c4-169">Erreurs et avertissements - erreur incorrecte quand une source n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="aa6c4-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="aa6c4-171">[Cohérence de conception] Le texte d’état d’installation de NuGet ne semble pas correct actuellement sur le thème sombre.</span><span class="sxs-lookup"><span data-stu-id="aa6c4-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="aa6c4-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="aa6c4-173">Mise à jour des packages lors des mises à jour/installations de solution pour tous les projets - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="aa6c4-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="aa6c4-174">dotnet</span></span>
  - <span data-ttu-id="aa6c4-175">dotnetcore pack se comporte différemment pour TargetFramework et TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="aa6c4-176">Les DLL incluses dans le dossier Tools génèrent des avertissements - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="aa6c4-177">NuGet.ContentModel consomme trop de mémoire pour les opérations de chaîne - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="aa6c4-178">RuntimeEnvironmentHelper.IsLinux retourne la valeur true pour OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="aa6c4-179">« dotnet pack » place nuspec sous obj au lieu d’obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="aa6c4-180">NuGet : mise à niveau de package extrêmement lente - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="aa6c4-181">CPS non synchronisé avec la restauration avec les solutions plus grandes pour lesquelles la restauration de solution allégée (LSL) n’est pas activée - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="aa6c4-182">SemVer 2.0 - nuget pack avec version fournie ignore les métadonnées (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="aa6c4-183">Le package d’installation NuGet.exe (3 +) avec numéro de version et indicateur ExcludeVersion n’effectue pas la mise à jour du package vers une version plus récente [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="aa6c4-184">La restauration Project.json doit émettre un avertissement quand des packages de niveau supérieur enfreignent des contraintes - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="aa6c4-185">-ConfigFile ne définit pas la configuration personnalisée sur la commande install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="aa6c4-186">nuget.exe install n’honore pas le commutateur « -DisableParallelProcessing » - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="aa6c4-187">Sources désactivées encore utilisées par DotNet.exe ou msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="aa6c4-188">Corriger les blocages dans un scénario LSL - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="aa6c4-189">DCR</span><span class="sxs-lookup"><span data-stu-id="aa6c4-189">DCRs</span></span>

- <span data-ttu-id="aa6c4-190">Prise en charge du framework cible avec nuget.exe install - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="aa6c4-191">Ajout de différentes chaînes UserAgent de tâche msbuild (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="aa6c4-192">PackagePathResolver.GetPackageDirectoryName doit être virtuel - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="aa6c4-193">[Cohérence de conception] Message prêtant à confusion lors de l’ajout d’un package NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="aa6c4-194">[Avertissements et erreurs] NoWarn n’est pas transmis de manière transitive à travers les références P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="aa6c4-195">Charge de solution légère : noyau commun pour l’interface utilisateur de PM, PMC, et IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="aa6c4-196">Chargement de solution allégé : Prise en charge - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="aa6c4-197">Ajouter la prise en charge de la cible MSBuild de pré-restauration déclenchée par Visual Studio - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="aa6c4-198">Ajouter une cible publique à NuGet.targets qui peut être référencée à l’aide de BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="aa6c4-199">La cible Pack ne peut pas créer correctement de contentFiles avec des actions de génération - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="aa6c4-200">RestoreOperationLogger.Do bloque les threads de pool de threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="aa6c4-201">Docs</span><span class="sxs-lookup"><span data-stu-id="aa6c4-201">Docs</span></span>

- <span data-ttu-id="aa6c4-202">Documentation pour les indicateurs DependencyVersion et Framework de la commande Install - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="aa6c4-203">Mise à jour de la documentation sur les avertissements et erreurs NuGet - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="aa6c4-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="aa6c4-204">Liens vers les problèmes GitHub corrigés dans RTM 4.4</span><span class="sxs-lookup"><span data-stu-id="aa6c4-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="aa6c4-205">Liste des questions 1</span><span class="sxs-lookup"><span data-stu-id="aa6c4-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="aa6c4-206">Liste des questions 2</span><span class="sxs-lookup"><span data-stu-id="aa6c4-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="aa6c4-207">Liste des questions 3</span><span class="sxs-lookup"><span data-stu-id="aa6c4-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
