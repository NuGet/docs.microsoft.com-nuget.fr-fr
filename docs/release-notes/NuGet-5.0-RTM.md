---
title: Notes de publication de NuGet 5.0 RTM
description: Notes de publication pour 5.0 NuGet, y compris les problèmes connus, les correctifs de bogues, les nouvelles fonctionnalités et les dcr.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921583"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="89e0a-103">Notes de publication NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="89e0a-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="89e0a-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="89e0a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="89e0a-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="89e0a-105">NuGet version</span></span> | <span data-ttu-id="89e0a-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89e0a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="89e0a-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="89e0a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [**<span data-ttu-id="89e0a-108">5.0.0</span><span class="sxs-lookup"><span data-stu-id="89e0a-108">5.0.0</span></span>**](https://nuget.org/downloads) | [<span data-ttu-id="89e0a-109">Visual Studio 2019 version 16.0</span><span class="sxs-lookup"><span data-stu-id="89e0a-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="89e0a-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="89e0a-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="89e0a-111"><sup>1</sup>installées avec Visual Studio 2019 par charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="89e0a-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="89e0a-112"><sup>2</sup>disponible en tant qu’option installation avec Visual Studio 2019 avec la charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="89e0a-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="89e0a-113">Résumé : Quelles sont les nouveautés dans 5.0</span><span class="sxs-lookup"><span data-stu-id="89e0a-113">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="89e0a-114">Prise en charge pour la restauration [filtré solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) dans Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="89e0a-114">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* `BuildTransitive` <span data-ttu-id="89e0a-115">dossier permet de packages de manière transitive contribuer cibles/propriétés au projet hôte - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="89e0a-115">folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="89e0a-116">Meilleure prise en charge pour les scénarios de PackageReference dans NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="89e0a-116">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* `nuget.exe pack project.json` <span data-ttu-id="89e0a-117">a été déconseillé - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="89e0a-117">has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="89e0a-118">Plug-in du fournisseur d’informations d’identification de génération 1 a été remplacée par [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) et sera bientôt dépréciée - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="89e0a-118">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="89e0a-119">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="89e0a-119">Issues fixed in this release</span></span>

**<span data-ttu-id="89e0a-120">Bogues</span><span class="sxs-lookup"><span data-stu-id="89e0a-120">Bugs</span></span>**

* <span data-ttu-id="89e0a-121">Lorsque vous effectuez une restauration NoOp, éviter \*. écriture dgspec.json dans le répertoire obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="89e0a-121">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="89e0a-122">Autorisations sur les fichiers créés à l’intérieur de ~/.nuget sont trop ouverts - [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="89e0a-122">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* `dotnet list package --outdated` <span data-ttu-id="89e0a-123">ne fonctionne pas avec les sources nécessitant une authentification - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="89e0a-123">doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="89e0a-124">NuGet.VisualStudio.IVsPackageInstaller - appel sur un projet avec aucun package fait référence à toujours utilise packages.config, même si la valeur par défaut est définie sur PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="89e0a-124">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="89e0a-125">PMC : Package de mise à jour réinstaller échoue (« Impossible de trouver le package ») sur les packages delisted.</span><span class="sxs-lookup"><span data-stu-id="89e0a-125">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="89e0a-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="89e0a-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="89e0a-127">Ajouter des avis de tiers dans notre référentiel et le VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="89e0a-127">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="89e0a-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage devez installer la version la plus récente lorsque aucune version donnée - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="89e0a-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="89e0a-129">--prise en charge interactive pour dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="89e0a-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="89e0a-130">Lors de la restauration avec le fichier de verrouillage, NU1603 avertissement ne doit pas être déclenché.</span><span class="sxs-lookup"><span data-stu-id="89e0a-130">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="89e0a-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="89e0a-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="89e0a-132">NuGet ne doit pas imprimer le chemin d’accès pendant la restauration avec une journalisation minimale - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="89e0a-132">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="89e0a-133">--la prise en charge interactive pour dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="89e0a-133">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="89e0a-134">Ajouter nouveau NuGet.Packaging.Core avec TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="89e0a-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="89e0a-135">plugins_cache a besoin d’un chemin plus court pour un fonctionnement optimal - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="89e0a-135">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="89e0a-136">Préférez le chemin d’accès pour la découverte de msbuild si l’utilisateur n’a pas demander une version de msbuild spécifiques - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="89e0a-136">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* `nuget.exe /?` <span data-ttu-id="89e0a-137">doit répertorier les versions de msbuild correct - [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="89e0a-137">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="89e0a-138">NuGet.targets(498,5) : erreur : Impossible de trouver une partie du chemin d’accès « / tmp/NuGetScratch - sur mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="89e0a-138">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="89e0a-139">restauration énumère inutilement le contenu de toutes les versions de package référencé dans le cache de l’ordinateur - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="89e0a-139">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="89e0a-140">La détection automatique de MSBuild sélectionne toujours 16.0 après l’installation de VS 2019 affiché un aperçu - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="89e0a-140">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="89e0a-141">package de liste dotnet sur une solution génère des entrées en double pour le framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="89e0a-141">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="89e0a-142">Exception « nom de chemin d’accès vide n’est pas légale » lorsque IVsPackageInstaller.InstallPackage appelante sur l’ancien projets et packages dossier n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="89e0a-142">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="89e0a-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="89e0a-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="89e0a-144">niveau de détail MSBuild/t : Restore minimal doit être plus minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="89e0a-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="89e0a-145">Visual Studio de 16.0 NuGet UI comporte des onglets illisibles en raison de problèmes de couleur - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="89e0a-145">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="89e0a-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="89e0a-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="89e0a-147">Restauration énumère inutilement le dossier de package global dans la tentative de déterminer le type - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="89e0a-147">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="89e0a-148">Erreurs de mise en œuvre du fichier de verrouillage doivent apparaître dans la fenêtre liste d’erreurs - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="89e0a-148">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="89e0a-149">Résoudre les problèmes de NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="89e0a-149">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="89e0a-150">Adapter à MSBuild de la mise à jour son installation emplacement - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="89e0a-150">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="89e0a-151">NuGet.Build.Tasks.Pack doit être une dépendance de développement - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="89e0a-151">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="89e0a-152">Ajouter le point d’extension pack pour inclure des symboles - de débogage [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="89e0a-152">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* `dotnet pack` <span data-ttu-id="89e0a-153">doit conserver la plage de versions de dépendance dans le package NuGet créé (même si une version flottante est utilisée) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="89e0a-153">should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* `dotnet restore` <span data-ttu-id="89e0a-154">ne fonctionne pas pour une source authentifiée lors de la configuration de niveau de l’utilisateur a également source - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="89e0a-154">fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="89e0a-155">Pack ne doit pas restreindre l’ensemble des BuildActions pour les fichiers de contenu - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="89e0a-155">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="89e0a-156">À l’aide d’un ProjectReference nécessitant AssetTargetFallback réussisse, doit émettre un avertissement.</span><span class="sxs-lookup"><span data-stu-id="89e0a-156">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="89e0a-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="89e0a-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="89e0a-158">Blocage en raison de problèmes liés aux threads lors de l’appel dans le CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="89e0a-158">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* `dotnet add package` <span data-ttu-id="89e0a-159">n’utilise pas les informations d’identification à partir de la configuration globale pour une source spécifiée dans la configuration locale - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="89e0a-159">doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="89e0a-160">Problèmes liés aux threads grâce à MEF, appelé sur async code chemins d’accès - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="89e0a-160">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="89e0a-161">Signature : erreur signalée à deux reprises et sans la pile des appels - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="89e0a-161">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="89e0a-162">Installation d’un package signé avec un certificat de signature non approuvé doit afficher l’erreur - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="89e0a-162">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="89e0a-163">La restauration NuGet incorrectement commandes NOOP lorsque 2 projets partagent répertoire obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="89e0a-163">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="89e0a-164">Impossible d’utiliser PAT avec `dotnet restore` sur Linux avec des packages à partir de flux authentifié - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="89e0a-164">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="89e0a-165">restauration de dotnet échoue en raison de la machine désactivé large flux - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="89e0a-165">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

**<span data-ttu-id="89e0a-166">DCR</span><span class="sxs-lookup"><span data-stu-id="89e0a-166">DCRs</span></span>**

* <span data-ttu-id="89e0a-167">Avertir de la suppression ultérieure des « project.json du pack dotnet - » [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="89e0a-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="89e0a-168">Ajoute un avertissement de désapprobation pour plug-in des informations d’identification Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="89e0a-168">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="89e0a-169">Signature : Référentiel est activée pour exiger la vérification du client de chaque package en tant que référentiel signée--via RepositorySignatures/5.0.0 ressource - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="89e0a-169">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="89e0a-170">limiter le nombre de demande http par source via NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="89e0a-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="89e0a-171">NuGet doit cibler Net472 (ce qui permet le nettoyage de la build 16.0 de l’extension VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="89e0a-171">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="89e0a-172">PMC : Supprimer la commande de OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="89e0a-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="89e0a-173">Mappage de NetCoreApp 3.0 marque à la version 2.1 de NetStandard - [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="89e0a-173">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="89e0a-174">Ajouter la prise en charge netstandard2.0 aux packages de NuGet.\* - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="89e0a-174">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="89e0a-175">Permettre aux auteurs de package définir le comportement transitive de build actifs - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="89e0a-175">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="89e0a-176">Prend en charge la fonctionnalité de filtre de Solution VS 2019.</span><span class="sxs-lookup"><span data-stu-id="89e0a-176">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="89e0a-177">Prend également en charge projet pas de solution ou les projets déchargés.</span><span class="sxs-lookup"><span data-stu-id="89e0a-177">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="89e0a-178">Avez besoin de restaurer une solution complète (via l’interface CLI ou VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="89e0a-178">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="89e0a-179">Assemblys de NuGet 5.0 nécessitent .NET 4.7.2 (via la modification du moniker du Framework cible) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="89e0a-179">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="89e0a-180">NuGetLicenseData de NuGet.Packaging doit être un type public.</span><span class="sxs-lookup"><span data-stu-id="89e0a-180">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="89e0a-181">Mettre à jour les métadonnées de licence reçues à partir de spdx.</span><span class="sxs-lookup"><span data-stu-id="89e0a-181">Update license metadata ingested from spdx.</span></span><span data-ttu-id="89e0a-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="89e0a-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="89e0a-183">Supprimer les paramètres des API obsolètes - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="89e0a-183">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="89e0a-184">Délais d’attente de restauration de solution de contournement sur les systèmes avec 1 processeur - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="89e0a-184">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="89e0a-185">NuGet préfère l’authentification NTLM, même s’il existe des informations d’identification dans NuGet.config : ajouter l’option de configuration pour filtrer les types d’authentification pour les informations d’identification - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="89e0a-185">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="89e0a-186">Activer EmbedInteropTypes pour PackageReference (fonctionnalité Packages.Config de correspondance) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="89e0a-186">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

**[<span data-ttu-id="89e0a-187">Liste de tous les problèmes résolus dans cette version - 5.0 RTM</span><span class="sxs-lookup"><span data-stu-id="89e0a-187">List of all issues fixed in this release - 5.0 RTM</span></span>](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a><span data-ttu-id="89e0a-188">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="89e0a-188">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="89e0a-189">Les packages dans FallbackFolders ont été installés de façon personnalisée par le kit SDK .NET Core et la validation de la signature échoue.</span><span class="sxs-lookup"><span data-stu-id="89e0a-189">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="89e0a-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="89e0a-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="89e0a-191">Problème</span><span class="sxs-lookup"><span data-stu-id="89e0a-191">Issue</span></span>
<span data-ttu-id="89e0a-192">Si vous utilisez dotnet.exe 2.x pour restaurer un projet qui cible netcoreapp 1.x et netcoreapp 2.x, le dossier de secours est traité comme un flux de fichier.</span><span class="sxs-lookup"><span data-stu-id="89e0a-192">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="89e0a-193">Cela signifie que, lors de la restauration, NuGet sélectionnera le package dans le dossier de secours et essaiera de l’installer dans le dossier de packages globaux, et la validation de signature habituelle échouera.</span><span class="sxs-lookup"><span data-stu-id="89e0a-193">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="89e0a-194">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="89e0a-194">Workaround</span></span>
<span data-ttu-id="89e0a-195">Désactiver l’utilisation du dossier de secours en définissant le `RestoreAdditionalProjectSources` Nothing :</span><span class="sxs-lookup"><span data-stu-id="89e0a-195">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="89e0a-196">Utilisez-le avec précaution comme des packages seraient restaurés à partir du dossier de secours est maintenant téléchargés à partir de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="89e0a-196">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
