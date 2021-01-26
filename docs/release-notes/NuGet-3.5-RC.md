---
title: Notes de publication de 3,5 RC
description: Notes de publication de NuGet 3,5 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780204"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="1ee92-103">Notes de publication de NuGet 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="1ee92-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="1ee92-104">Notes de publication [de NuGet 3,5-bêta2](../release-notes/nuget-3.5-Beta2.md)  |  [Notes de publication de NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="1ee92-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="1ee92-105">la version 3,5 est axée sur l’amélioration de la qualité et des performances des clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="1ee92-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="1ee92-106">En outre, nous avons fourni quelques fonctionnalités telles que la prise en charge des [dossiers de secours](https://github.com/NuGet/Home/issues/2899), la prise en charge de [PackageType](https://github.com/NuGet/Home/issues/2476) dans `.nuspec` et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="1ee92-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="1ee92-107">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="1ee92-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="1ee92-108">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="1ee92-108">Bug Fixes</span></span>

* <span data-ttu-id="1ee92-109">L’installation/la restauration d’un package échoue avec « le package contient plusieurs `.nuspec` fichiers ».</span><span class="sxs-lookup"><span data-stu-id="1ee92-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="1ee92-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="1ee92-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="1ee92-111">le Pack NuGet ajoute `.tt` de force aux fichiers dans le dossier de contenu, quelle que soit la [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="1ee92-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="1ee92-112">NuGet Pack csproj (avec `project.json` ) se bloque s’il n’existe aucun packOptions et propriétaire dans le fichier JSON- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="1ee92-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="1ee92-113">le Pack NuGet pour `project.json` ignore les balises packOptions comme Summary, Authors, Owners, etc. [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="1ee92-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="1ee92-114">le Pack NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="1ee92-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="1ee92-115">La mise à jour de plusieurs packages avec la restauration laisse le projet dans un État rompu, [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="1ee92-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="1ee92-116">Les ContentFiles sous n’importe lequel ne sont pas ajoutés pour les projets netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="1ee92-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="1ee92-117">Impossible de regrouper correctement la bibliothèque .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="1ee92-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="1ee92-118">Fichier > nouveau projet de bibliothèque de classes de > (portable) échoue dans VS2015 et Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="1ee92-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="1ee92-119">Erreur NuGet-1.0.0-\* n’est pas une chaîne de version valide- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="1ee92-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="1ee92-120">Find-Package ne parvient pas à s’afficher mais Install-Package Works [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="1ee92-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="1ee92-121">Erreur lorsque « Install-Package jQuery. validation » sur dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="1ee92-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="1ee92-122">Lors de l’installation de VS 2015 Update 3 sur un VS qui utilise une erreur NuGet version 3.5.0 se produit- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="1ee92-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="1ee92-123">Interface utilisateur du gestionnaire de package : n’affiche pas la nouvelle version après la mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="1ee92-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="1ee92-124">-ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoi dans 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="1ee92-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="1ee92-125">Chaîne incorrecte : une version stable d’un package ne doit pas avoir une dépendance de préversion.</span><span class="sxs-lookup"><span data-stu-id="1ee92-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="1ee92-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="1ee92-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="1ee92-127">Création d’une exception de NullRef de projet PCL (net46 et Windows 10).</span><span class="sxs-lookup"><span data-stu-id="1ee92-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="1ee92-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="1ee92-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="1ee92-129">La mise à jour NuGet doit fournir un message informatif quand une version supérieure est limitée par la contrainte allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="1ee92-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="1ee92-130">[#2885](https://github.com/NuGet/Home/issues/2885) le plug-in des informations d’identification s’est arrêté avec l’erreur 1/erreur lors du téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources</span><span class="sxs-lookup"><span data-stu-id="1ee92-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="1ee92-131">Pack NuGet-Newtonsoft.Jsmanquant sur la dépendance du package- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="1ee92-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="1ee92-132">Bogue dans ExecuteSynchronizedCore sur Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="1ee92-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="1ee92-133">VS ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="1ee92-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="1ee92-134">Résoudre les problèmes d’accessibilité- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="1ee92-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="1ee92-135">Les infrastructures portables avec des profils avec trait d’Union sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="1ee92-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="1ee92-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="1ee92-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="1ee92-137">Le gestionnaire de package NuGet doit faire en sorte qu’il soit clair que les options Lister les détails des packages ne s’appliquent pas à `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="1ee92-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="1ee92-138">La mise à jour NuGet 3.3.0 échoue avec «une contrainte supplémentaire... défini dans packages.config empêche cette opération.»</span><span class="sxs-lookup"><span data-stu-id="1ee92-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1ee92-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1ee92-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1ee92-140">L’installation d’un package à partir d’une source locale qui n’existe pas lève une fausse [#1674](https://github.com/NuGet/Home/issues/1674) de messages</span><span class="sxs-lookup"><span data-stu-id="1ee92-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="1ee92-141">Le filtre « mettre à niveau une mise à jour » affiche des mises à niveau qui violent la contrainte de version- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="1ee92-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="1ee92-142">Optimisation des performances</span><span class="sxs-lookup"><span data-stu-id="1ee92-142">Performance Improvements</span></span>

* <span data-ttu-id="1ee92-143">Performances : améliorer l’analyse du Framework cible ContentModel- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="1ee92-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="1ee92-144">Performances : Évitez `runtime.json` de lire des fichiers pour les restaurations qui n’ont pas de rid [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="1ee92-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="1ee92-145">Sur les machines CI, la restauration d’un exemple d’application Web ASP.NET est réduite de plus de 15 secondes à 3 secondes.</span><span class="sxs-lookup"><span data-stu-id="1ee92-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="1ee92-146">Performances : la console du gestionnaire de package init.ps1 temps de chargement [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="1ee92-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="1ee92-147">La durée d’ouverture de PackageManagerConsole a été améliorée dans certains cas, de 132s à 10s.</span><span class="sxs-lookup"><span data-stu-id="1ee92-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="1ee92-148">Résolvez les problèmes de performances resharpers dans NuGet Update- [#3044](https://github.com/NuGet/Home/issues/3044): sur un exemple de projet, temps nécessaire pour installer les packages réduits de 140s à 68s.</span><span class="sxs-lookup"><span data-stu-id="1ee92-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="1ee92-149">DCR</span><span class="sxs-lookup"><span data-stu-id="1ee92-149">DCRs</span></span>

* <span data-ttu-id="1ee92-150">NuGet doit permettre aux utilisateurs de savoir que la mise à niveau/installation dans un PCL basé sur dotnet TFM peut provoquer des problèmes [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="1ee92-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="1ee92-151">Signaler une installation/mise à niveau incorrecte pour le projet w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="1ee92-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="1ee92-152">Ajouter la prise en charge de netcoreapp11 et netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="1ee92-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="1ee92-153">Imprimer le contenu de l’en-tête NuGet-Warning sur la console dans nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="1ee92-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="1ee92-154">Tirer parti de l’attribut AssemblyMetadata pour les `.nuspec` remplacements de jetons- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="1ee92-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="1ee92-155">Supprimez la propriété locked du fichier de verrouillage- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="1ee92-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="1ee92-156">Les packages de symboles ne doivent jamais être utilisés dans l’installation ou la mise à jour #2807</span><span class="sxs-lookup"><span data-stu-id="1ee92-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="1ee92-157">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="1ee92-157">Features</span></span>

* <span data-ttu-id="1ee92-158">Prise en charge des dossiers de package de secours- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="1ee92-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="1ee92-159">Concevez et implémentez une notion de type de package pour prendre en charge les packages d’outils- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="1ee92-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="1ee92-160">API permettant d’accéder au dossier des packages globaux- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="1ee92-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="1ee92-161">Prise en charge des mises à jour des packages natifs- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="1ee92-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
