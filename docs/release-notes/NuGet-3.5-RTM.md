---
title: Notes de mise à jour de NuGet 3.5 bêta
description: Notes de publication pour 3.5 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="e3075-103">Notes de version 3.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="e3075-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="e3075-104">[Notes de publication NuGet 3.5 RC](../release-notes/nuget-3.5-RC.md) | [Notes de version RC de NuGet 4.0](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="e3075-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e3075-105">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="e3075-105">Bug Fixes</span></span>

* <span data-ttu-id="e3075-106">Pack n’utilise pas MSBuild 14,1 sur mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="e3075-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="e3075-107">Onglet de mise à jour ne sélectionne pas la dernière version disponible pour mettre à jour au lieu de cela, sélectionnez la version installée en cours - [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="e3075-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="e3075-108">Résoudre l’incident après l’authentification d’un v2 privé MyGet flux et en cliquant sur « Afficher x plus de résultats »- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="e3075-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="e3075-109">Messages du journal semblent être dans l’ordre inverse pour l’interface utilisateur - [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="e3075-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="e3075-110">V3.4.4 - Nuget restore lève « format du chemin d’accès donné n’est pas pris en charge » - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="e3075-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="e3075-111">NuGet cmdLine 3.6 bêta ne tient pas compte - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="e3075-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="e3075-112">IKVM NuGet lente installer sur un grand projet - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="e3075-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="e3075-113">NuGet.exe mise à jour - Self conserve sur la mise à jour lui-même - [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="e3075-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="e3075-114">3.5 installation/restauration à partir de partage UNC a régression des performances de 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="e3075-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="e3075-115">Erreur lors de l’installation Moq à partir de l’interface utilisateur de gestion de Package pour un projet net451 - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="e3075-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="e3075-116">Onglet installation au niveau de la solution n’affiche une version du package - [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="e3075-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="e3075-117">xproj `project.json` mise à jour à partir de l’onglet installé perd l’état - [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="e3075-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="e3075-118">Pack de NuGet sur `.csproj` ignore l’élément de fichiers vides dans `.nuspec` fichier - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="e3075-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="e3075-119">Les projets de site Web hébergés dans IIS ne devraient pas provoquer l’échec - restauration [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="e3075-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="e3075-120">Informations d’identification ne pas récupérées à partir de Nuget.Config lorsque le point de terminaison v3 redirige vers v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="e3075-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="e3075-121">Pack de NuGet ne parvient pas à résoudre l’assembly lors de la récupération des métadonnées de l’assembly portable - [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="e3075-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="e3075-122">Impossible de trouver NuGet `msbuild.exe` sur Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="e3075-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="e3075-123">pack de NuGet.exe n’autorise pas une balise en version préliminaire qui commence par nombres - [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="e3075-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="e3075-124">installation du package NuGet échoue sur VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="e3075-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="e3075-125">allowedVersions de filtre de travail au niveau de la solution - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="e3075-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="e3075-126">Restauration échoue de manière aléatoire avec un élément avec la même clé a déjà été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="e3075-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="e3075-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="e3075-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="e3075-128">Impossible d’installer Nuget.Common dans `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="e3075-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="e3075-129">Lorsque vous utilisez l’interface utilisateur pour rechercher une source V2, FindPackagesById est appelée deux fois pour chaque ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="e3075-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="e3075-130">Les packages ne peuvent pas dépendre de projets - [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="e3075-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="e3075-131">pack de NuGet.exe - Exclude est documentée, mais pas pris en charge - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="e3075-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="e3075-132">Problèmes avec l’erreur messages lorsque section 'fichiers' `.nuspec` n’est pas valide - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="e3075-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="e3075-133">Push envoie toujours le package entier à deux reprises avec des sources de package - authentifié [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="e3075-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="e3075-134">Aucune information n’a été donnée lors de l’appel \*.csproj de mise à jour de nuget.exe lors du projet n’a pas un `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="e3075-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="e3075-135">`packages.config` restauration de ne pas de nouvelle tentative sur les codes d’état 5xx à partir de sources de V2 - [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="e3075-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="e3075-136">Deux points dans l’attribut src de fichier dans `.nuspec` ne fonctionne pas - [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="e3075-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="e3075-137">Restauration de CoreCLR doit ignorer les flux avec chiffrement - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="e3075-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="e3075-138">NuGet.exe push gestion 403 - incorrectement demander des informations d’identification - [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="e3075-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="e3075-139">Mise à jour de NuGet via le Gestionnaire de package supprime des propriétés à partir de la `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="e3075-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="e3075-140">NuGet.PackageManagement.VisualStudio tente de charger « NuGet.TeamFoundationServer14 », mais que le nom de la DLL changé de « NuGet.TeamFoundationServer » - [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="e3075-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="e3075-141">Gestionnaire de package n’affiche pas l’interface utilisateur qui vient d’être mis à jour la version - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="e3075-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="e3075-142">Essayez d’utiliser l’ID de package, du package de mise à jour version au lieu de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="e3075-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="e3075-143">NuGet restore csproj doit erreur si le projet n’est pas à l’aide de nuget (`packages.config` ou `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="e3075-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="e3075-144">Erreur de TFS » [fichier] est introuvable dans votre espace de travail, ou vous n’êtes pas autorisé à y accéder » au cours de mise à niveau ou désinstaller en cas de solution/projet est lié au contrôle de code source TFS - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="e3075-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="e3075-145">package de mise à jour n’obtenir les dépendances pour les packages non cibles - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="e3075-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="e3075-146">Il n’existe aucun moyen de définir le niveau de détail des journaux pour les actions de l’interface utilisateur du Gestionnaire de package de Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="e3075-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="e3075-147">la configuration NuGet n’est pas valide - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="e3075-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="e3075-148">DefaultPushSource dans `NuGetDefaults.Config` (`ProgramData\NuGet`) ne fonctionne pas - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="e3075-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="e3075-149">version de NuGet 3.4.3 - mise en route de la valeur ne peut pas être null lors de la build du package - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="e3075-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="e3075-150">restauration n’utilise pas les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="e3075-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="e3075-151">[dotnet restauration]--configfile est relatif au répertoire de projet au lieu de la commande dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="e3075-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="e3075-152">Allocations excessives dans le code de comparaison de version - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="e3075-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="e3075-153">Plusieurs instances de nuget.exe tente d’installer le même package en parallèle provoque une double écriture - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="e3075-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="e3075-154">Informations de dépendance ne sont pas mis en cache pour les opérations de plusieurs projets - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="e3075-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="e3075-155">Installer et mettre à jour les packages de téléchargement sans vérifier le dossier packages tout d’abord - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="e3075-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="e3075-156">Si la liste des sources de package est vide, ne peut pas ajouter la source du package via l’interface utilisateur (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="e3075-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="e3075-157">Induire des erreurs lorsque vous tentez d’installer le package dépend au moment du design façades - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="e3075-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="e3075-158">Installation d’un package à partir de la console PackageManager avec le paramètre « All » tente uniquement de première source - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="e3075-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="e3075-159">Dernière version bêta ne pas décompresser ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="e3075-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="e3075-160">Panne de VS2015 au démarrage avec NuGet automatique intégrée 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="e3075-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="e3075-161">Commande de mise à jour peut être un peu plus détaillée si i lui demander d’être plus.. - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="e3075-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="e3075-162">VSIX généré localement doit avoir les mêmes fichiers DLL et que la build de l’élément de configuration.</span><span class="sxs-lookup"><span data-stu-id="e3075-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="e3075-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="e3075-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="e3075-164">Résoudre les avertissements vers une version antérieure de NuGet dans la build - [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="e3075-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="e3075-165">Authentifie source du package (3 fois) est bloquée toujours - [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="e3075-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="e3075-166">Contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un v3.3 nuget + flux avec l’argument - NoCache lorsque le package contient `.nupkg` fichiers - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="e3075-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="e3075-167">Échec de l’installation de NuGet avec toutes les Sources de Package, mais de package manquant à partir de la source de 1, - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="e3075-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="e3075-168">[PerfWatson] UIDelay : nuget.packagemanagement.visualstudio.dll ! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt ; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="e3075-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="e3075-169">Installer des blocs si une seule source échoue autorisation - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="e3075-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="e3075-170">`.nuspec` version plage doit substituer IncludeReferencedProjects - version - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="e3075-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="e3075-171">Package de mise à jour lente super - « tentative de collecte des informations de dépendance » - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="e3075-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="e3075-172">Rétrogradations furtives de NuGet package quand lot mise à jour de ses dépendances - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="e3075-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="e3075-173">mise à jour de NuGet.exe supprime le nom fort d’assembly et l’attribut privé.</span><span class="sxs-lookup"><span data-stu-id="e3075-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="e3075-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="e3075-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="e3075-175">Chemin d’accès relatif pour « DefaultPushSource » - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="e3075-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="e3075-176">Améliorer les messages d’échec de résolution - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="e3075-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="e3075-177">package de mise à jour v3 échoue avec des packages pas dans la source spécifiée - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="e3075-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="e3075-178">À l’aide de chemins d’accès relatifs pour les sources de package peut être problématique pour utiliser - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="e3075-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="e3075-179">Pas de dépendance dans le fichier NUPKG généré à partir de projet si la dépendance indirecte existe déjà avec une spécification de version inférieure - [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="e3075-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="e3075-180">Suppression d’un projet ferme la fenêtre de l’interface utilisateur correspondante, mais renommer un projet ne renomme pas la fenêtre de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3075-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="e3075-181">Notez que PMC écoute pour renommer le projet et les événements de suppression de projet - [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="e3075-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="e3075-182">[Salix charge de travail Web] Création de Razor v3 WSP se bloque - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="e3075-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="e3075-183">Installation/la restauration d’un package particulier échoue avec « Le Package contient plusieurs fichiers nuspec. »</span><span class="sxs-lookup"><span data-stu-id="e3075-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="e3075-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="e3075-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="e3075-185">ID de minuscules & `packages.config` scénarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="e3075-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="e3075-186">[3.5 à la bêta 2] Restauration des packages ne parvient pas à restaurer les packages « hérités » - [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="e3075-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="e3075-187">NuGet pack ajoute forcer les fichiers .tt au dossier de contenu quelle - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="e3075-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="e3075-188">package de mise à jour de l’application web ASP.NET génère l’avertissement lié au fichier : source - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="e3075-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="e3075-189">NuGet pack csproj (avec `project.json`) se bloque si aucun packOptions et le propriétaire du fichier JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="e3075-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="e3075-190">pack de NuGet pour `project.json` ignore les balises packOptions comme résumé, les auteurs, les propriétaires, etc. - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="e3075-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="e3075-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="e3075-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="e3075-192">Pack de NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="e3075-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="e3075-193">Mise à jour de plusieurs packages avec restauration laisse le projet dans un état interrompu - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="e3075-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="e3075-194">Les fichiers associés ne sont pas ajoutés pour les projets de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="e3075-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="e3075-195">Ne peut pas empaqueter bibliothèque ciblant .net Standard correctement - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="e3075-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="e3075-196">Fichier -> Nouveau projet -> Échec de projet de bibliothèque de classes (Portable) dans VS2015 et Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="e3075-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="e3075-197">Erreur de nuGet - 1.0.0-\* n’est pas une chaîne de version valide - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="e3075-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="e3075-198">Find-Package ne parvient pas à l’affichage mais works d’Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="e3075-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="e3075-199">Erreur lors de la « Install-Package jquery.validation » sur dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="e3075-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="e3075-200">par défaut pour le chemin d’accès de la cible non valide - pack NuGet de xproj [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="e3075-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="e3075-201">Lorsque installé Visual Studio 2015 update 3 sur un VS par NuGet version 3.5.0 erreur - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="e3075-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="e3075-202">« Bloqué par packages.config » `project.json` (UWP, build ou intégré) projet - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="e3075-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="e3075-203">mettre à jour cli dotnet installé par le script de compilation preview2-003121, qui est la build preview2 officiel.</span><span class="sxs-lookup"><span data-stu-id="e3075-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="e3075-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="e3075-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="e3075-205">Interface utilisateur du Gestionnaire de package : n’affiche pas nouvelle version après mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="e3075-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="e3075-206">-ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoyé dans 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="e3075-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="e3075-207">Chaîne incorrect : version finale d’un package ne doit pas avoir sur une dépendance de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="e3075-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="e3075-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="e3075-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="e3075-209">OptimizedZipPackage cache laisse les dossiers vides - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="e3075-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="e3075-210">Création de get de projet de bibliothèque de classes portables (net46 et windows 10) NullRef exception.</span><span class="sxs-lookup"><span data-stu-id="e3075-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="e3075-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="e3075-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="e3075-212">Mise à jour de NuGet doit fournir de message d’information lorsqu’une version plus récente est restreinte par la contrainte d’allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="e3075-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="e3075-213">Problèmes de restauration v3 NuGet - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="e3075-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="e3075-214">Plug-in d’informations d’identification s’est arrêté avec l’erreur -1 / erreur téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="e3075-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="e3075-215">`project.json` NuGet restore entraîne une recompilation en l’absence de modification - [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="e3075-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="e3075-216">Les packages de symboles ne doivent pas être déjà utilisé dans l’installation ou de mise à jour - [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="e3075-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="e3075-217">Visual Studio ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe fait) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="e3075-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="e3075-218">Les éléments d’interface utilisateur sans étiquette dans le Gestionnaire de Package UI d’étiquette pour l’accessibilité - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="e3075-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="e3075-219">Les infrastructures portables avec des profils de trait d’union sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="e3075-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="e3075-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="e3075-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="e3075-221">Gestionnaire de package NuGet doit indiquer clairement que liste d’options dans les packages de détail ne s’applique pas aux `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="e3075-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="e3075-222">push de NuGet.exe/delete ne sont pas utiliser la clé API - [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="e3075-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="e3075-223">Supprimez la propriété verrouillée le fichier de verrouillage - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="e3075-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="e3075-224">Échec de la mise à jour de NuGet 3.3.0 avec ' une contrainte supplémentaire... défini dans packages.config empêche cette opération. »</span><span class="sxs-lookup"><span data-stu-id="e3075-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="e3075-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="e3075-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="e3075-226">L’installation du package à partir d’une source locale qui n’existe pas lève un message erroné - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="e3075-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="e3075-227">Filtre de « Mise à niveau disponible » affiche les mises à niveau qui violent la contrainte de version - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="e3075-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="e3075-228">Impossible de mettre à jour les packages natives - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="e3075-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="e3075-229">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="e3075-229">Features</span></span>

* <span data-ttu-id="e3075-230">Prend en charge le paramètre CopyLocal false sur les références ajoutées par NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="e3075-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="e3075-231">prise en charge de NuGet.exe pour MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="e3075-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="e3075-232">Pack prise en charge.`csproj`</span><span class="sxs-lookup"><span data-stu-id="e3075-232">Pack support for .`csproj`</span></span><span data-ttu-id="e3075-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="e3075-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="e3075-234">Désactiver l’action de l’utilisateur lorsqu’il existe des actions de l’utilisateur en cours d’exécution- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="e3075-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="e3075-235">NuGet doit prendre en charge les `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="e3075-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="e3075-236">Ajouter des compatibilités framework manquant dans NuGet 2.x (qui sont déjà dans 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="e3075-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="e3075-237">Prise en charge des dossiers de package de secours - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="e3075-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="e3075-238">Concevoir et implémenter une notion de type de package pour prendre en charge les packages de l’outil - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="e3075-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="e3075-239">Ajouter une API pour obtenir le chemin d’accès au dossier packages global - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="e3075-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="e3075-240">Activer SemVer 2.0.0 Pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="e3075-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="e3075-241">DCR</span><span class="sxs-lookup"><span data-stu-id="e3075-241">DCRs</span></span>

* <span data-ttu-id="e3075-242">push de NuGet.exe - paramètre de délai d’attente ne fonctionne pas - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="e3075-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="e3075-243">Texte de Description de package doit-elle être sélectionnés - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="e3075-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="e3075-244">Activer nuget.exe produire `.props` et `.targets` pour les fichiers `.nuproj` projets [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="e3075-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="e3075-245">Ajouter à comparer les infrastructures des importations - API d’extensibilité [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="e3075-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="e3075-246">Masquer les options de dépendance lors de l’utilisation `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="e3075-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="e3075-247">Impression nuget.exe en-tête de version dans une sortie détaillée - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="e3075-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="e3075-248">NuGet a besoin informer les utilisateurs que la mise à niveau/installation dans un tfm dotnet basé PCL peut entraîner des problèmes - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="e3075-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="e3075-249">Avertir l’installation/mise à niveau incorrect pour le projet avec tfm = « dotnet » - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="e3075-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="e3075-250">Résoudre les problèmes de performances avec ReShaper et NuGet pour la mise à jour - [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="e3075-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="e3075-251">Ajouter la prise en charge netcoreapp11 et netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="e3075-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="e3075-252">Attribut de AssemblyMetadata tirent parti de `.nuspec` jeton remplacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="e3075-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
