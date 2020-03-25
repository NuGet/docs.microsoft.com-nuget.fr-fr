---
title: Notes de publication de NuGet 5,5
description: Notes de publication de NuGet 5,5, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148296"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="d43ac-103">Notes de publication de NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="d43ac-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="d43ac-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="d43ac-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d43ac-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="d43ac-105">NuGet version</span></span> | <span data-ttu-id="d43ac-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d43ac-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d43ac-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d43ac-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d43ac-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="d43ac-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d43ac-109">Visual Studio 2019 version 16,5</span><span class="sxs-lookup"><span data-stu-id="d43ac-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d43ac-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d43ac-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="d43ac-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="d43ac-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="d43ac-112">Résumé : nouveautés de 5,5</span><span class="sxs-lookup"><span data-stu-id="d43ac-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="d43ac-113">Amélioration de l’accessibilité et du lecteur d’écran pour l’interface utilisateur du gestionnaire de package NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d43ac-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="d43ac-114">Problèmes d’accessibilité dans l’expérience du lecteur d’écran, altText et nom accessible manquants pour la zone de texte installée, etc.,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="d43ac-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="d43ac-115">Problèmes d’accessibilité dans les expériences de lecteur d’écran dans la liste des packages- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="d43ac-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="d43ac-116">Problèmes d’accessibilité dans les environnements de lecteur d’écran liés aux onglets « parcourir », « installer », « mettre à jour »- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="d43ac-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="d43ac-117">Le narrateur n’annonce pas « vide », « aucune Dependencies","NuGet. org », étiquette de lien « MIT » [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="d43ac-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="d43ac-118">Prise en charge de l’apprentissage des icônes autonomes dans l’interface utilisateur du gestionnaire de package Visual Studio pour les packages hébergés sur des flux locaux- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="d43ac-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="d43ac-119">Amélioration significative des performances de restauration sans opération à l’aide de `RestoreUseStaticGraphEvaluation` qui accélèrent les évaluations en appelant les API Graph statiques MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="d43ac-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="d43ac-120">Amélioration de la fiabilité de dotnet. exe avec les plug-ins d’authentification multiplateforme</span><span class="sxs-lookup"><span data-stu-id="d43ac-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="d43ac-121">échec de dotnet restore avec TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="d43ac-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="d43ac-122">Plug-in : « une tâche a été annulée »-problème avec l’authentification ADO en raison de cette erreur.</span><span class="sxs-lookup"><span data-stu-id="d43ac-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="d43ac-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="d43ac-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="d43ac-124">[#4126](https://github.com/NuGet/Home/issues/4126) de commande Add `dotnet nuget <add|remove|update|disable|enable|list> source`</span><span class="sxs-lookup"><span data-stu-id="d43ac-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="d43ac-125">Prises en `--skip-duplicate` à l’aide de dotnet NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="d43ac-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="d43ac-126">Prise en charge `packages.config` avec MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="d43ac-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d43ac-127">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="d43ac-127">Issues fixed in this release</span></span>

<span data-ttu-id="d43ac-128">**Bogues**</span><span class="sxs-lookup"><span data-stu-id="d43ac-128">**Bugs**</span></span>

* <span data-ttu-id="d43ac-129">Réutilisation de l’Auto-Updater avec les API V3- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="d43ac-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="d43ac-130">Version de dépendance de package incorrecte si la version de dépendance de package est définie sur « \* »- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="d43ac-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="d43ac-131">Le message d’erreur ErrorUnsafePackageEntry ne pointe pas vers la source du problème- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="d43ac-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="d43ac-132">Le fichier de verrouillage n’est pas respecté dans les scénarios « \* »- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="d43ac-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="d43ac-133">NuGet. exe ne résout pas la version la plus récente d’un package lors de l’utilisation de \* dans PackageReference (MSBuild/dotnet/VS Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="d43ac-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="d43ac-134">package de liste dotnet avec multi-ciblage de projets WPF- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="d43ac-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="d43ac-135">Améliorer les ConcurrencyUtilities (réduire l’utilisation de l’UC)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="d43ac-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="d43ac-136">Les spécifications de la DG pour les scénarios de projets déchargés ne doivent pas être écrites dans les restaurations d’aperçu- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="d43ac-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="d43ac-137">Les packages NuGet de Visual Studio (RestoreManagerPackage) doivent être chargés automatiquement sur les événements de build de solution- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="d43ac-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="d43ac-138">Blocage dans VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="d43ac-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="d43ac-139">La boîte à outils de VisualStudio n’est pas remplie à partir d’un package NuGet si un projet est placé dans un dossier de solution- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="d43ac-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="d43ac-140">VS : la restauration de solution a échoué en raison d’une condition de concurrence critique [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="d43ac-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="d43ac-141">Constante « chargement en cours.. » sur l’onglet installé et «recherche</span><span class="sxs-lookup"><span data-stu-id="d43ac-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="d43ac-142">..» sous l’onglet mises à jour- [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="d43ac-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="d43ac-143">Icônes incorporées manquantes dans l’interface utilisateur de VS PM après expiration du cache- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="d43ac-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="d43ac-144">Démarrage de l’interface utilisateur FireAndForget PM- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="d43ac-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="d43ac-145">Restauration : l’implémentation de IncludeExcludeFiles. Equals (...) est incorrecte- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="d43ac-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="d43ac-146">Restauration : PackageSpec. Clone () crée une [#9211](https://github.com/NuGet/Home/issues/9211) de clonage inégale</span><span class="sxs-lookup"><span data-stu-id="d43ac-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="d43ac-147">Liste d’erreurs affichée bien que « toujours afficher Liste d’erreurs si la génération se termine avec des erreurs » n’est pas vérifiée- [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="d43ac-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="d43ac-148">La restauration du graphique statique ne doit pas passer un SolutionPath vide- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="d43ac-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="d43ac-149">Restauration : fermeture calculée pour chaque projet 4 fois- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="d43ac-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="d43ac-150">Restauration : DependencyGraphSpec. Load (...) n’a pas besoin de JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="d43ac-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="d43ac-151">Restauration : chaînes volumineuses créées sur le tas d’objets volumineux (LOH)- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="d43ac-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="d43ac-152">Le fichier NuGet. exe personnalisé sur un mono plus récent peut s’arrêter en raison du programme de résolution du SDK MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="d43ac-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="d43ac-153">la restauration échoue quand NuGet. DGSPEC. JSON est « utilisé par un autre processus »- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="d43ac-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="d43ac-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="d43ac-154">**DCRs**</span></span>

* <span data-ttu-id="d43ac-155">La logique de _GetRestoreProjectStyle doit se trouver dans une tâche [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="d43ac-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="d43ac-156">Ajoutez les informations d’obsolescence par défaut sous l’onglet installé- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="d43ac-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="d43ac-157">**[Liste de tous les problèmes résolus dans cette version-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="d43ac-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
