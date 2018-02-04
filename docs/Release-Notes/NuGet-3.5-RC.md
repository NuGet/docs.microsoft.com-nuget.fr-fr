---
title: 3.5 Notes de publication RC | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour RC 3.5 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 3.5 RC, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="a187b-104">Notes de version RC de NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="a187b-104">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="a187b-105">[Notes de version 3.5 à la bêta 2 de NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM de Notes de publication](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="a187b-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="a187b-106">version 3.5 met l’accent sur l’amélioration de la qualité et les performances des clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="a187b-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="a187b-107">En outre, nous vous avons envoyé certaines fonctionnalités comme la prise en charge de [dossiers secours](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) prise en charge dans `.nuspec` et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="a187b-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="a187b-108">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="a187b-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="a187b-109">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="a187b-109">Bug Fixes</span></span>

* <span data-ttu-id="a187b-110">Installation/restauration d’un package échoue avec « Package contient plusieurs `.nuspec` fichiers. »</span><span class="sxs-lookup"><span data-stu-id="a187b-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="a187b-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="a187b-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="a187b-112">pack de NuGet ajoute force `.tt` fichiers au dossier de contenu quelle - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="a187b-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="a187b-113">NuGet pack csproj (avec `project.json`) se bloque si aucun packOptions et le propriétaire du fichier JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="a187b-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="a187b-114">pack de NuGet pour `project.json` ignore les balises packOptions comme résumé, les auteurs, les propriétaires, etc. - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="a187b-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="a187b-115">pack de NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="a187b-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="a187b-116">Mise à jour de plusieurs packages avec restauration laisse le projet dans un état interrompu - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="a187b-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="a187b-117">Les fichiers associés ne sont pas ajoutés pour les projets de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="a187b-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="a187b-118">Ne peut pas empaqueter bibliothèque ciblant .net Standard correctement - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="a187b-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="a187b-119">Fichier -> Nouveau projet -> Échec de projet de bibliothèque de classes (Portable) dans VS2015 et Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="a187b-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="a187b-120">Erreur de nuGet - 1.0.0-\* n’est pas une chaîne de version valide - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="a187b-120">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="a187b-121">Find-Package ne parvient pas à l’affichage mais works d’Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="a187b-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="a187b-122">Erreur lors de la « Install-Package jquery.validation » sur dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="a187b-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="a187b-123">Lorsque installé Visual Studio 2015 update 3 sur un VS par NuGet version 3.5.0 erreur - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="a187b-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="a187b-124">Interface utilisateur du Gestionnaire de package : n’affiche pas nouvelle version après mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="a187b-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="a187b-125">-ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoyé dans 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="a187b-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="a187b-126">Chaîne incorrect : version finale d’un package ne doit pas avoir sur une dépendance de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="a187b-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="a187b-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="a187b-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="a187b-128">Création de get de projet de bibliothèque de classes portables (net46 et windows 10) NullRef exception.</span><span class="sxs-lookup"><span data-stu-id="a187b-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="a187b-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="a187b-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="a187b-130">Mise à jour de NuGet doit fournir de message d’information lorsqu’une version plus récente est restreinte par la contrainte d’allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="a187b-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="a187b-131">Plug-in d’informations d’identification s’est arrêté avec l’erreur -1 / erreur téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="a187b-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="a187b-132">pack de NuGet - dépendance de package manquant de Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="a187b-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="a187b-133">Bogue dans ExecuteSynchronizedCore sur Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="a187b-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="a187b-134">Visual Studio ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe fait) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="a187b-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="a187b-135">Résoudre les problèmes d’accessibilité - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="a187b-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="a187b-136">Les infrastructures portables avec des profils de trait d’union sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="a187b-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="a187b-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="a187b-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="a187b-138">Gestionnaire de package NuGet doit indiquer clairement que liste d’options dans les packages de détail ne s’applique pas aux `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="a187b-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="a187b-139">Échec de la mise à jour de NuGet 3.3.0 avec ' une contrainte supplémentaire... défini dans packages.config empêche cette opération. »</span><span class="sxs-lookup"><span data-stu-id="a187b-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="a187b-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="a187b-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="a187b-141">L’installation du package à partir d’une source locale qui n’existe pas lève un message erroné - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="a187b-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="a187b-142">Filtre de « Mise à niveau disponibles » affiche les mises à niveau qui violent la contrainte de version - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="a187b-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="a187b-143">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="a187b-143">Performance Improvements</span></span>

* <span data-ttu-id="a187b-144">Performances : Améliorer les ContentModel framework cible analyse - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="a187b-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="a187b-145">Performances : Éviter la lecture `runtime.json` fichiers pour les restaurations qui n’ont pas d’identificateurs RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="a187b-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="a187b-146">Sur les ordinateurs de l’élément de configuration, restauration d’un exemple de Qu'application Web ASP.NET réduite plus de 15 secondes à 3 secondes.</span><span class="sxs-lookup"><span data-stu-id="a187b-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="a187b-147">Performances : Temps de chargement Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="a187b-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="a187b-148">Temps nécessaire pour ouvrir PackageManagerConsole améliorées dans certains cas de 132s à 10 s.</span><span class="sxs-lookup"><span data-stu-id="a187b-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="a187b-149">Résoudre les problèmes de performances ReSharper de mise à jour de NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): sur un exemple de projet, temps nécessaire pour installer des packages réduite de 140s à 68s.</span><span class="sxs-lookup"><span data-stu-id="a187b-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="a187b-150">DCR</span><span class="sxs-lookup"><span data-stu-id="a187b-150">DCRs</span></span>

* <span data-ttu-id="a187b-151">NuGet a besoin informer les utilisateurs que la mise à niveau/installation dans un tfm dotnet basé PCL peut entraîner des problèmes - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="a187b-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="a187b-152">Avertir l’installation/mise à niveau incorrect pour le projet avec tfm = « dotnet » - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="a187b-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="a187b-153">Ajouter la prise en charge netcoreapp11 et netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="a187b-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="a187b-154">Imprimer le contenu d’en-tête NuGet-avertissement dans la console de nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="a187b-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="a187b-155">Attribut de AssemblyMetadata tirent parti de `.nuspec` jeton remplacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="a187b-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="a187b-156">Supprimez la propriété verrouillée le fichier de verrouillage - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="a187b-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="a187b-157">Packages de symboles ne doivent pas déjà utilisés dans l’installation ou mettre à jour #2807</span><span class="sxs-lookup"><span data-stu-id="a187b-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="a187b-158">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="a187b-158">Features</span></span>

* <span data-ttu-id="a187b-159">Prise en charge des dossiers de package de secours - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="a187b-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="a187b-160">Concevoir et implémenter une notion de type de package pour prendre en charge les packages de l’outil - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="a187b-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="a187b-161">Pour obtenir le chemin d’accès au dossier packages global - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="a187b-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="a187b-162">Prise en charge - mettre à jour les packages natifs [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="a187b-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
