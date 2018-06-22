---
title: Notes de publication de la version NuGet 4.0 RC
description: Notes de publication de NuGet 4.0 RC, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821884"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="4de5a-103">Notes de publication de la version NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="4de5a-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="4de5a-104">Notes de publication de NuGet 3.5 RTM</span><span class="sxs-lookup"><span data-stu-id="4de5a-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="4de5a-105">[NuGet 4.0 RC pour Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) ajoute la prise en charge des scénarios .NET Core, répond aux principaux commentaires des clients et améliore les performances dans de nombreux scénarios.</span><span class="sxs-lookup"><span data-stu-id="4de5a-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="4de5a-106">Cette version offre plusieurs améliorations telles que la prise en charge de PackageReference, des commandes NuGet comme cibles MSBuild, la restauration des packages en arrière-plan, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="4de5a-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4de5a-107">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="4de5a-107">Bug Fixes</span></span>

- <span data-ttu-id="4de5a-108">Changements de comportement dans `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="4de5a-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="4de5a-109">Échec de la restauration de nuget.exe sur les ordinateurs VS « 15 » uniquement - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="4de5a-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="4de5a-110">Un nouveau projet de fichier .NETCore doit bloquer la build pendant la restauration - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="4de5a-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="4de5a-111">Impossible de restaurer une application web ASP.NET Core migrée de VS2015 vers VS « 15 ».</span><span class="sxs-lookup"><span data-stu-id="4de5a-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="4de5a-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="4de5a-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="4de5a-113">[Échec de test] Le package « jQuery Validation » ne peut pas être désinstallé par l’interface utilisateur du Gestionnaire de package - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="4de5a-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="4de5a-114">Quand un package est installé dans un fichier `project.json` UWP, les projets parents doivent également être restaurés - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="4de5a-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="4de5a-115">Modifiez les cibles NuGet pour enregistrer dans le journal les sources de package avec un niveau de détail élevé plutôt que normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="4de5a-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="4de5a-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="4de5a-116">dotnet</span></span>
  - <span data-ttu-id="4de5a-117">dotnetcore pack3 doit inclure la documentation XML par défaut - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="4de5a-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="4de5a-118">La mise à jour par lots échoue à partir de l’interface utilisateur quand la source sans le package est en premier que et Tout est sélectionné comme source - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="4de5a-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="4de5a-119">La commande Nuget pack n’inclut pas tous les fichiers - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="4de5a-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="4de5a-120">Problème d’insuffisance de mémoire - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="4de5a-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="4de5a-121">La section ProjectFileDependencyGroups du fichier de ressources doit utiliser des noms de bibliothèques pour les projets - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="4de5a-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="4de5a-122">« dotnet restore » et sous-répertoires récursifs - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="4de5a-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="4de5a-123">Les échecs Restore3 sont enregistrés en tant qu’avertissements plutôt qu’en tant qu’erreurs - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="4de5a-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="4de5a-124">Problème TFS : « [fichier] introuvable dans votre espace de travail, ou vous n’êtes pas autorisé à y accéder » - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="4de5a-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="4de5a-125">Le fait de taper « nuget <packagename>» dans la zone de recherche de lancement rapide de Visual Studio conserve le préfixe « nuget » - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="4de5a-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="4de5a-126">System.Xml.XmlException : Élément racine non reconnu dans le composant Core Properties.</span><span class="sxs-lookup"><span data-stu-id="4de5a-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="4de5a-127">Ligne 2, position 2.</span><span class="sxs-lookup"><span data-stu-id="4de5a-127">Line 2, position 2.</span></span><span data-ttu-id="4de5a-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="4de5a-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="4de5a-129">`.nuspec` avec &lt; ou &gt; placé dans une séquence d’échappement dans des champs de texte n’est plus généré - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="4de5a-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="4de5a-130">La suppression nuget.exe n’invite pas à fournir d’informations d’identification (elle est en mode non interactif) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="4de5a-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="4de5a-131">La suppression nuget.exe fournit un avertissement concernant la Clé API pour les sources locales, alors que cela n’est pas justifié - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="4de5a-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="4de5a-132">Expérience d’erreur médiocre lors de l’installation de package -pre EF - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="4de5a-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="4de5a-133">Visual Studio s’est arrêté de manière anormale après un changement de sélection dans le Gestionnaire de package - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="4de5a-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="4de5a-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="4de5a-134">dotnet</span></span>
  - <span data-ttu-id="4de5a-135">dotnetcore restore effectue des recherches d’ID respectant la casse sur des dépôts locaux à liste plate quand des versions flottantes sont utilisées - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="4de5a-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="4de5a-136">La suppression nuget.exe est rompue pour le flux V2 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="4de5a-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="4de5a-137">Le délai d’attente de push de nuget.exe a besoin d’un meilleur message d’erreur - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="4de5a-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="4de5a-138">La restauration d’outil sans importations correctes échoue de manière silencieuse.</span><span class="sxs-lookup"><span data-stu-id="4de5a-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="4de5a-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="4de5a-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="4de5a-140">NuGet vous invite à entrer des informations d’identification quand il y a un flux privé, même lors de l’installation à partir de nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="4de5a-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="4de5a-141">Un package ApplicationInsights 2.0 est répertorié alors qu’il n’existe pas encore - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="4de5a-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="4de5a-142">UIDelay dans la branche 5 de Visual Studio « 15 » Preview - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="4de5a-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="4de5a-143">Le premier événement OnBuild est ignoré pour la restauration lors de la génération pour UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="4de5a-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="4de5a-144">PowerShell5 rompt l’installation d’EntityFramework ?</span><span class="sxs-lookup"><span data-stu-id="4de5a-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="4de5a-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="4de5a-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="4de5a-146">Ajouter la source à la journalisation détaillée (à prendre en compte pour 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="4de5a-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="4de5a-147">Paramètre NoCache non respecté dans la version 3.4+ du client nuget - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="4de5a-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="4de5a-148">Quand le chargement d’un fournisseur d’informations d’identification dans Visual Studio échoue, ne rompez pas NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="4de5a-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="4de5a-149">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="4de5a-149">Features</span></span>

- <span data-ttu-id="4de5a-150">Configurer CI pour exécuter x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="4de5a-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="4de5a-151">Restauration automatique 3/3 : interface utilisateur non bloquante - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="4de5a-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="4de5a-152">Restauration automatique 2/3 : restauration en arrière-plan sur nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="4de5a-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="4de5a-153">Restaurer les références de projet pour qu’elles correspondent au comportement de build (récursivité) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="4de5a-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="4de5a-154">Prise en charge de DPL dans Visual Studio « 15 » - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="4de5a-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="4de5a-155">Déplacement du fichier de paramètres vers Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="4de5a-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="4de5a-156">Les cibles et les propriétés de restauration générées ont besoin d’une prise en charge de la participation au ciblage croisé - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="4de5a-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="4de5a-157">Prise en charge de la restauration NuGet pour PackageTargetFallback (fonctionnalité Importations) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="4de5a-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="4de5a-158">Implémentation de ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="4de5a-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="4de5a-159">Restore3 pour un RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="4de5a-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="4de5a-160">Prise en charge de l’ajout/suppression/mise à jour de PackageRefs dans l’interface utilisateur de NuGet - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="4de5a-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="4de5a-161">Restauration automatique 1/3 : Implémentation de l’API de nomination par le biais de la mise en cache des informations de restauration de projet - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="4de5a-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="4de5a-162">[0] Tâches et cibles de restauration NuGet - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="4de5a-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="4de5a-163">[1] Activation de la restauration au niveau de la solution dans MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="4de5a-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="4de5a-164">Prise en charge de l’extensibilité publique du fournisseur d’informations d’identification dans Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="4de5a-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="4de5a-165">Restauration nuget récursive - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="4de5a-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="4de5a-166">Impossible de charger Microsoft.TeamFoundation.Client sur dev15. Nécessité de mettre à jour Microsoft.TeamFoundation.Client vers la version 15.0 pour Visual Studio « 15 » Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="4de5a-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="4de5a-167">Impossible d’installer un package C++ dans un projet UWP C++ dans Visual Studio « 15 » Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="4de5a-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="4de5a-168">Nupkg doit prendre en charge le dossier \buildCrossTargeting\ et importer `.targets` / `.props` pour le « ciblage croisé » de l’étendue MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4de5a-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="4de5a-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="4de5a-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="4de5a-170">Conception de ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="4de5a-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="4de5a-171">Correction de l’interface utilisateur de NuGet pour prendre en charge la restauration avec PackageReferences dans `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="4de5a-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="4de5a-172">Ajout du bouton Effacer le cache aux paramètres du Gestionnaire de package VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="4de5a-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="4de5a-173">DCR</span><span class="sxs-lookup"><span data-stu-id="4de5a-173">DCRs</span></span>

- <span data-ttu-id="4de5a-174">La restauration de solution doit être bloquée pendant la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="4de5a-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="4de5a-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="4de5a-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="4de5a-176">L’installation de NetCore à partir de l’interface utilisateur du Gestionnaire de Package NuGet effectue une installation sur chaque TFM, au lieu de ceux pris en charge par le package - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="4de5a-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="4de5a-177">L’API de nominateur de restauration doit aussi prendre en charge DotNetCliToolsReferences.</span><span class="sxs-lookup"><span data-stu-id="4de5a-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="4de5a-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="4de5a-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="4de5a-179">Marquer notre vsix Visual Studio « 15 » en tant que systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="4de5a-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="4de5a-180">Migrer du référencement de MS.VS.Services.Client vers MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="4de5a-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="4de5a-181">$(RestoreLegacyPackagesDirectory) doit être respecté au niveau du projet par la restauration - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="4de5a-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="4de5a-182">La restauration dans un projet avec TargetFramework unique ne doit pas conditionner les propriétés - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="4de5a-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="4de5a-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="4de5a-183">dotnet</span></span>
  - <span data-ttu-id="4de5a-184">dotnetcore restore3 foo.csproj doit suivre les dépendances projectref et les restaurer aussi.</span><span class="sxs-lookup"><span data-stu-id="4de5a-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="4de5a-185">Comme la build.</span><span class="sxs-lookup"><span data-stu-id="4de5a-185">Like build.</span></span><span data-ttu-id="4de5a-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="4de5a-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="4de5a-187">Dépendances « type » : « plateforme » représentées en tant que « type » : « package » dans le fichier de verrouillage - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="4de5a-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="4de5a-188">Le mode détaillé NuGet.exe doit afficher l’URL de téléchargement - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="4de5a-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="4de5a-189">Déplacer NuGet xplat vers Microsoft.NetCore.App et netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="4de5a-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="4de5a-190">Push - Il devrait être possible de remplacer le serveur de symboles lors d’une opération Push à partir de la ligne de commande - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="4de5a-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="4de5a-191">Consolider le code pour la recherche du chemin de packages global - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="4de5a-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="4de5a-192">Il faut un meilleur nom que suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="4de5a-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="4de5a-193">Déterminer le nom de la dépendance `project.json` à utiliser pour les projets MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="4de5a-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="4de5a-194">Ajout de la prise en charge de SemVer 2.0.0 à NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="4de5a-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="4de5a-195">Autoriser la disponibilité de la dépendance transitive NuPkgs avec `.targets` dans MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="4de5a-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="4de5a-196">La restauration NuGet à partir de la ligne de commande est beaucoup plus lente que VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="4de5a-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="4de5a-197">Faire en sorte que la comparaison de version et d’ID de package respecte la casse - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="4de5a-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="4de5a-198">L’option NoCache ne fonctionne pas pour la restauration/installation basée sur `packages.config` (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="4de5a-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="4de5a-199">Les ressources FindPackageByIdResource ont besoin d’un enregistreur d’événements et d’un contexte de cache par défaut - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="4de5a-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
