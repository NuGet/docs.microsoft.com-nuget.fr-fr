---
title: Notes de publication de NuGet 3.5 RTM
description: Notes de publication de NuGet 3,5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776357"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="3a219-103">Notes de publication de NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="3a219-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="3a219-104">Notes de publication [de NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Notes de publication de NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="3a219-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3a219-105">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="3a219-105">Bug Fixes</span></span>

* <span data-ttu-id="3a219-106">Pack n’utilise pas MSBuild 14,1 sur mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="3a219-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="3a219-107">L’onglet mettre à jour ne sélectionne pas la dernière version disponible pour la mise à jour, à la place sélectionnez version installée actuelle- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="3a219-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="3a219-108">Correction du blocage après l’authentification d’un flux MyGet privé v2 et en cliquant sur « Afficher x plus de résultats »- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="3a219-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="3a219-109">Les messages de journal semblent être dans l’ordre inverse pour les [#3446](https://github.com/NuGet/Home/issues/3446) d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="3a219-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="3a219-110">v 3.4.4-la restauration NuGet lève « le format du chemin d’accès spécifié n’est pas pris en charge »- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="3a219-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="3a219-111">NuGet cmdLine 3,6 Beta ne respecte pas-prop configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="3a219-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="3a219-112">Installation lente de NuGet IKVM sur un grand projet- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="3a219-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="3a219-113">nuget.exe Update-continue à se mettre à jour automatiquement- [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="3a219-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="3a219-114">3,5 l’installation/la restauration à partir d’un partage UNC présente une régression des performances de 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="3a219-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="3a219-115">Erreur lors de l’installation de MOQ à partir de l’interface utilisateur de gestion des packages pour un projet net451- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="3a219-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="3a219-116">L’onglet installation au niveau de la solution n’affiche pas la version du package- [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="3a219-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="3a219-117">la `project.json` mise à jour xproj à partir de l’onglet installé perd l’état- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="3a219-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="3a219-118">L’élément NuGet Pack on `.csproj` ignore les fichiers vides dans le `.nuspec` fichier- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="3a219-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="3a219-119">Les projets de site Web hébergés dans IIS ne doivent pas provoquer l’échec de la restauration [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="3a219-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="3a219-120">Les informations d’identification ne sont pas récupérées à partir de Nuget.Config lorsque le point de terminaison v3 redirige vers v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="3a219-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="3a219-121">Le Pack NuGet ne parvient pas à résoudre l’assembly lors de la récupération des métadonnées de l’assembly portable- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="3a219-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="3a219-122">NuGet ne peut pas trouver `msbuild.exe` sur mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="3a219-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="3a219-123">nuget.exe Pack n’autorise pas une balise de préversion qui commence par des chiffres- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="3a219-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="3a219-124">échec de l’installation du package NuGet sur VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="3a219-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="3a219-125">le filtre allowedVersions ne fonctionne pas au niveau de la solution- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="3a219-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="3a219-126">La restauration échoue de façon aléatoire avec un élément avec la même clé a déjà été ajouté.</span><span class="sxs-lookup"><span data-stu-id="3a219-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="3a219-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="3a219-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="3a219-128">Impossible d’installer NuGet. common dans `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="3a219-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="3a219-129">Lorsque vous utilisez l’interface utilisateur pour rechercher une source v2, FindPackagesById est appelé deux fois pour chaque ID- [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="3a219-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="3a219-130">Les packages ne peuvent pas dépendre de projets- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="3a219-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="3a219-131">nuget.exe Pack-Exclude est documenté, mais n’est pas pris en charge- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="3a219-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="3a219-132">Problèmes liés aux messages d’erreur quand la section’contentFiles’de `.nuspec` n’est pas valide- [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="3a219-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="3a219-133">Push envoie toujours le package entier à deux reprises avec des sources de packages authentifiés- [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="3a219-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="3a219-134">Aucune information n’a été fournie lors de l’appel de nuget.exe Update \*. csproj tant que le projet n’a pas de `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="3a219-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="3a219-135">`packages.config` la restauration ne réessaye pas sur les codes de statut 5xx à partir des sources v2- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="3a219-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="3a219-136">Le double point dans le fichier src `.nuspec` ne fonctionne pas [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="3a219-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="3a219-137">La restauration de CoreCLR doit ignorer les flux avec le chiffrement- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="3a219-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="3a219-138">nuget.exe de la gestion Push 403-demande d’informations d’identification incorrectes- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="3a219-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="3a219-139">La mise à jour NuGet via le gestionnaire de package supprime les propriétés du `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="3a219-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="3a219-140">NuGet. PackageManagement. VisualStudio essayez de charger « NuGet. TeamFoundationServer14 », mais ce nom de DLL a été remplacé par « NuGet. TeamFoundationServer »- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="3a219-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="3a219-141">L’interface utilisateur du gestionnaire de package n’affiche pas la version [#2828](https://github.com/NuGet/Home/issues/2828) récemment mise à jour</span><span class="sxs-lookup"><span data-stu-id="3a219-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="3a219-142">Update : package essayant d’utiliser PackageID, version au lieu de package. version- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="3a219-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="3a219-143">NuGet Restore csproj doit être erroné si le projet n’utilise pas NuGet ( `packages.config` ou `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="3a219-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="3a219-144">L’erreur TFS « [fichier] est introuvable dans votre espace de travail, ou vous n’êtes pas autorisé à y accéder » lors de la mise à niveau ou de la désinstallation quand la solution/le projet est lié au contrôle de code source TFS- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="3a219-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="3a219-145">le package de mise à jour n’obtient pas de dépendances pour les packages non cibles- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="3a219-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="3a219-146">Il n’existe aucun moyen de définir le niveau de détail des journaux pour les actions de l’interface utilisateur du gestionnaire de package NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="3a219-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="3a219-147">la configuration NuGet n’est pas valide-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="3a219-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="3a219-148">DefaultPushSource dans `NuGetDefaults.Config` ( `ProgramData\NuGet` ) ne fonctionne pas- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="3a219-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="3a219-149">la version de NuGet 3.4.3-l’obtention de la valeur ne peut pas être null dans la génération du package- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="3a219-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="3a219-150">la restauration n’utilise pas les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="3a219-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="3a219-151">[dotnet restore]--ConfigFile est relatif au répertoire du projet au lieu du Rép cmd- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="3a219-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="3a219-152">Allocations excessives dans le code d’analyse de version- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="3a219-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="3a219-153">Plusieurs instances de nuget.exe tentant d’installer le même package en parallèle entraînent une double écriture [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="3a219-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="3a219-154">Les informations de dépendance ne sont pas mises en cache pour les opérations à plusieurs projets- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="3a219-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="3a219-155">Installer et mettre à jour les packages de téléchargement sans vérifier le dossier Packages en premier [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="3a219-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="3a219-156">Si la liste source du package est vide, impossible d’ajouter la source du package via l’interface utilisateur (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="3a219-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="3a219-157">Erreur trompeuse lors de la tentative d’installation du package qui dépend des façades au moment du design- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="3a219-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="3a219-158">L’installation d’un package à partir de la console PackageManager avec le paramètre « All » essaie uniquement la première source [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="3a219-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="3a219-159">La dernière version bêta ne décompresse pas ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="3a219-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="3a219-160">VS2015 crash au démarrage avec NuGet auto-intégré NuGet- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="3a219-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="3a219-161">La commande de mise à jour peut être un peu plus détaillée si je l’ai demandée...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="3a219-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="3a219-162">L’extension VSIX générée localement doit avoir les mêmes dll et fichiers que la build CI.</span><span class="sxs-lookup"><span data-stu-id="3a219-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="3a219-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="3a219-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="3a219-164">Corriger les avertissements de rétrogradation NuGet dans le [#2396](https://github.com/NuGet/Home/issues/2396) de build</span><span class="sxs-lookup"><span data-stu-id="3a219-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="3a219-165">L’échec de l’authentification de la source du package (3 fois) est bloqué indéfiniment [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="3a219-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="3a219-166">Le contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un flux NuGet v 3.3 + avec l’argument-NoCache quand le package contient `.nupkg` des fichiers- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="3a219-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="3a219-167">Installation de NuGet avec toutes les sources de package, mais le package est absent de 1 source, Fail- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="3a219-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="3a219-168">[PerfWatson] UIDelay : nuget.packagemanagement.visualstudio.dll ! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt ; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="3a219-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="3a219-169">Installer les blocs si une seule source ne parvient pas à obtenir l’autorisation- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="3a219-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="3a219-170">`.nuspec` la plage de versions doit remplacer-IncludeReferencedProjects version- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="3a219-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="3a219-171">Update-Package super lent-« tentative de collecte des informations sur les dépendances »- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="3a219-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="3a219-172">Package NuGet Stealth rétrogrades lors de la mise à jour par lots de ses dépendances- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="3a219-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="3a219-173">nuget.exe mise à jour supprime le nom fort et l’attribut privé de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="3a219-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="3a219-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="3a219-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="3a219-175">Chemin de fichier relatif pour « DefaultPushSource »- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="3a219-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="3a219-176">Améliorer les messages d’échec du programme de résolution- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="3a219-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="3a219-177">échec de la mise à jour du package dans v3 avec des packages qui ne sont pas dans le [#1013](https://github.com/NuGet/Home/issues/1013) source spécifié</span><span class="sxs-lookup"><span data-stu-id="3a219-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="3a219-178">L’utilisation de chemins d’accès relatifs pour les sources de package pose problème à l’utilisation de- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="3a219-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="3a219-179">Dépendance manquante dans NUPKG-fichier généré à partir du projet si la dépendance indirecte existe déjà avec une spécification de version antérieure- [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="3a219-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="3a219-180">La suppression d’un projet ferme la fenêtre de l’interface utilisateur correspondante, mais le fait de renommer un projet ne renomme pas la fenêtre de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a219-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="3a219-181">Notez que PMC écoute les événements renommer le projet et supprimer le projet- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="3a219-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="3a219-182">[Willow Web Workload] Création de blocages de la préversion de Razor v3- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="3a219-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="3a219-183">L’installation/la restauration d’un package particulier échoue avec « le package contient plusieurs fichiers NuSpec ».</span><span class="sxs-lookup"><span data-stu-id="3a219-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="3a219-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="3a219-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="3a219-185">ID en minuscules & `packages.config` scénarios- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="3a219-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="3a219-186">[3,5-bêta2] La restauration du package ne parvient pas à restaurer les packages « hérités »- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="3a219-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="3a219-187">le Pack NuGet ajoute de force aux fichiers. TT dans le dossier de contenu, quelle que soit la [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="3a219-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="3a219-188">Update-le package de l’application Web ASP.NET génère un avertissement lié au fichier : source- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="3a219-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="3a219-189">NuGet Pack csproj (avec `project.json` ) se bloque s’il n’existe aucun packOptions et propriétaire dans le fichier JSON- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="3a219-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="3a219-190">le Pack NuGet pour `project.json` ignore les balises packOptions comme Summary, Authors, Owners, etc. [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="3a219-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="3a219-191">NullReferenceException via NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="3a219-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="3a219-192">Le Pack NuGet ignore les dépendances dans la sortie `.nuspec` pour `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="3a219-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="3a219-193">La mise à jour de plusieurs packages avec la restauration laisse le projet dans un État rompu, [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="3a219-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="3a219-194">Les ContentFiles sous n’importe lequel ne sont pas ajoutés pour les projets netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="3a219-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="3a219-195">Impossible de regrouper correctement la bibliothèque .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="3a219-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="3a219-196">Fichier > nouveau projet de bibliothèque de classes de > (portable) échoue dans VS2015 et Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="3a219-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="3a219-197">erreur nuGet-1.0.0-\* n’est pas une chaîne de version valide- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="3a219-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="3a219-198">Find-Package ne parvient pas à s’afficher mais Install-Package Works [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="3a219-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="3a219-199">Erreur lorsque « Install-Package jQuery. validation » sur dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="3a219-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="3a219-200">le Pack NuGet de xproj est défini par défaut sur un chemin cible non valide- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="3a219-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="3a219-201">Lors de l’installation de VS 2015 Update 3 sur un VS qui utilise une erreur NuGet version 3.5.0 se produit- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="3a219-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="3a219-202">« Bloqué par packages.config » dans le `project.json` projet (UWP, a. k. a Build intégré)- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="3a219-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="3a219-203">Mettez à jour l’interface CLI dotnet installée par le script de compilation dans preview2-003121, qui est la build preview2 officielle.</span><span class="sxs-lookup"><span data-stu-id="3a219-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="3a219-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="3a219-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="3a219-205">Interface utilisateur du gestionnaire de package : n’affiche pas la nouvelle version après la mise à jour d’un package- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="3a219-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="3a219-206">-ApiKey sur la ligne de commande de suppression n’est pas en lecture/envoi dans 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="3a219-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="3a219-207">Chaîne incorrecte : une version stable d’un package ne doit pas avoir une dépendance de préversion.</span><span class="sxs-lookup"><span data-stu-id="3a219-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="3a219-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="3a219-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="3a219-209">Le cache OptimizedZipPackage conserve les dossiers vides- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="3a219-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="3a219-210">Création d’une exception de NullRef de projet PCL (net46 et Windows 10).</span><span class="sxs-lookup"><span data-stu-id="3a219-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="3a219-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="3a219-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="3a219-212">La mise à jour NuGet doit fournir un message informatif quand une version supérieure est limitée par la contrainte allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="3a219-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="3a219-213">Problèmes de restauration NuGet v3- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="3a219-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="3a219-214">[#2885](https://github.com/NuGet/Home/issues/2885) le plug-in des informations d’identification s’est arrêté avec l’erreur 1/erreur lors du téléchargement du package lors de l’utilisation de fournisseurs d’informations d’identification avec plusieurs sources</span><span class="sxs-lookup"><span data-stu-id="3a219-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="3a219-215">`project.json` la restauration NuGet provoque une recompilation lorsque rien n’est modifié- [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="3a219-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="3a219-216">Les packages de symboles ne doivent jamais être utilisés dans Install ou UPDATE- [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="3a219-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="3a219-217">VS ne prend pas en charge les variables d’environnement dans repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="3a219-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="3a219-218">Étiqueter les UIElements sans étiquette dans l’interface utilisateur du gestionnaire de package pour l’accessibilité- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="3a219-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="3a219-219">Les infrastructures portables avec des profils avec trait d’Union sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="3a219-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="3a219-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="3a219-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="3a219-221">Le gestionnaire de package NuGet doit faire en sorte qu’il soit clair que les options Lister les détails des packages ne s’appliquent pas à `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="3a219-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="3a219-222">nuget.exe Push/Delete n’utilise pas de clé API- [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="3a219-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="3a219-223">Supprimez la propriété locked du fichier de verrouillage- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="3a219-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="3a219-224">La mise à jour NuGet 3.3.0 échoue avec «une contrainte supplémentaire... défini dans packages.config empêche cette opération.»</span><span class="sxs-lookup"><span data-stu-id="3a219-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="3a219-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="3a219-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="3a219-226">L’installation d’un package à partir d’une source locale qui n’existe pas lève une fausse [#1674](https://github.com/NuGet/Home/issues/1674) de messages</span><span class="sxs-lookup"><span data-stu-id="3a219-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="3a219-227">Le filtre « mise à niveau disponible » affiche des mises à niveau qui violent la contrainte de version- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="3a219-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="3a219-228">Impossible de mettre à jour les packages natifs- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="3a219-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="3a219-229">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3a219-229">Features</span></span>

* <span data-ttu-id="3a219-230">Prise en charge du paramètre CopyLocal sur false sur les références ajoutées par NuGet- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="3a219-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="3a219-231">Prise en charge nuget.exe pour MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="3a219-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="3a219-232">Prise en charge de Pack pour.`csproj`</span><span class="sxs-lookup"><span data-stu-id="3a219-232">Pack support for .`csproj`</span></span><span data-ttu-id="3a219-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="3a219-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="3a219-234">Désactiver l’action de l’utilisateur lorsque des actions de l’utilisateur sont exécutées- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="3a219-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="3a219-235">NuGet doit ajouter la prise en charge de `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="3a219-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="3a219-236">Ajouter des compatibilités de Framework manquantes dans NuGet 2. x (qui sont déjà en 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="3a219-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="3a219-237">Prise en charge des dossiers de package de secours- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="3a219-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="3a219-238">Concevez et implémentez une notion de type de package pour prendre en charge les packages d’outils- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="3a219-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="3a219-239">Ajoutez une API pour récupérer le chemin d’accès au dossier de packages globaux- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="3a219-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="3a219-240">Activer SemVer 2.0.0 dans Pack- [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="3a219-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="3a219-241">DCR</span><span class="sxs-lookup"><span data-stu-id="3a219-241">DCRs</span></span>

* <span data-ttu-id="3a219-242">Le paramètre nuget.exe Push-Timeout ne fonctionne pas- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="3a219-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="3a219-243">Le texte de description du package doit être sélectionnable- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="3a219-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="3a219-244">Activez nuget.exe pour produire `.props` `.targets` des fichiers et pour les `.nuproj` projets [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="3a219-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="3a219-245">Ajouter une API d’extensibilité pour comparer des frameworks à des importations- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="3a219-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="3a219-246">Masquer les options de dépendance lors de l’utilisation de `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="3a219-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="3a219-247">Imprimer l’en-tête de version nuget.exe dans la sortie détaillée- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="3a219-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="3a219-248">NuGet doit permettre aux utilisateurs de savoir que la mise à niveau/installation dans un PCL basé sur dotnet TFM peut provoquer des problèmes [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="3a219-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="3a219-249">Signaler une installation/mise à niveau incorrecte pour le projet w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="3a219-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="3a219-250">Résoudre les problèmes de performances avec remodeler et NuGet pour Update- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="3a219-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="3a219-251">Ajouter la prise en charge de netcoreapp11 et netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="3a219-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="3a219-252">Tirer parti de l’attribut AssemblyMetadata pour les `.nuspec` remplacements de jetons- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="3a219-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
