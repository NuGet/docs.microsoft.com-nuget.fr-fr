---
title: 3.5 Notes de version bêta 2 de
description: Notes de publication pour NuGet 3.5 bêta 2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="ba4cc-103">Notes de mise à jour de NuGet 3.5 bêta 2</span><span class="sxs-lookup"><span data-stu-id="ba4cc-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="ba4cc-104">[Notes de version bêta de 3.5 NuGet](../release-notes/nuget-3.5-Beta.md) | [Notes 3.5 RC de NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="ba4cc-105">NuGet 3.5 bêta 2 RTM publiée le 27 juin 2016 pour Visual Studio 2013 et nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ba4cc-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="ba4cc-106">Journal complet</span><span class="sxs-lookup"><span data-stu-id="ba4cc-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="ba4cc-107">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="ba4cc-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="ba4cc-108">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="ba4cc-108">Bug Fixes</span></span>

* <span data-ttu-id="ba4cc-109">Message d’erreur de mise à jour à un manque de prise en charge de decrpytion de mot de passe dans le .NET Core pour les flux authentifiés - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="ba4cc-110">Get-Package la Console Gestionnaire de package échoue si les projets .NET Core sont open - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="ba4cc-111">Corriger une gestion incorrecte des 403 dans une commande NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="ba4cc-112">Résoudre les problèmes lors de la désinstallation des packages dans une solution liée au contrôle de code source TFS lorsque disableSourceControlIntegration a la valeur true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="ba4cc-113">Corriger la mise à jour de package pour tenir les packages non cibles compte - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="ba4cc-114">Utiliser le niveau de détail de MSBuild pour définir des actions d’interface utilisateur - niveau de journal pour le Gestionnaire de package Nuget [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="ba4cc-115">Corrigez la configuration NuGet est une erreur non valide dans les projets de site Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="ba4cc-116">Résoudre les problèmes de pack de `.csproj` lorsque les fichiers de contenu sont inclus - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="ba4cc-117">DefaultPushSource dans `NuGetDefaults.Config` (`ProgramData\NuGet`) ne fonctionne pas - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="ba4cc-118">Corrigez le problème dans la version Nuget 3.4.3 - la valeur ne peut pas être null lors de la création de package - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="ba4cc-119">L’instruction RESTORE utilise les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="ba4cc-120">Performances - correctif les allocations excessives dans le code de comparaison de version - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="ba4cc-121">Résoudre les problèmes lorsque plusieurs instances de nuget.exe tente d’installer le même package en parallèle - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="ba4cc-122">Performances - informations de dépendance de Cache pour les opérations de plusieurs projets - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="ba4cc-123">Corrigez le problème où vous ne pouvez pas les sources de package ajoutées à partir de paramètres lors de la liste source est vide - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="ba4cc-124">Corrigez trompeurs erreur lorsque vous tentez d’installer le package dépend au moment du design façades - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="ba4cc-125">Installation d’un package à partir de la console PackageManager avec le paramètre « All » tente uniquement de première source - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="ba4cc-126">Résoudre les problèmes avec les packages qui ont des fichiers avec des temps d’écriture dans le futur (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="ba4cc-127">Afficher l’exception lors d’un échec des projets de recherche dans la commande update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="ba4cc-128">Contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un v3.3 nuget + flux avec l’argument - NoCache lorsque le package contient `.nupkg` fichiers - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="ba4cc-129">Problème de correctif avec package Installer (toutes les Sources) lorsque le package est manquant à partir de la source de 1 - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="ba4cc-130">Installer des blocs si une seule source échoue autorisation - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="ba4cc-131">`.nuspec` version plage doit substituer IncludeReferencedProjects - version - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="ba4cc-132">Échec de la mise à jour de NuGet 3.3.0 avec ' une contrainte supplémentaire... défini dans packages.config empêche cette opération. »</span><span class="sxs-lookup"><span data-stu-id="ba4cc-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="ba4cc-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="ba4cc-134">mise à jour de NuGet.exe supprime le nom fort d’assembly et l’attribut privé.</span><span class="sxs-lookup"><span data-stu-id="ba4cc-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="ba4cc-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="ba4cc-136">Résoudre les problèmes avec le chemin d’accès relatif pour « DefaultPushSource » - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="ba4cc-137">Améliorer les messages de défaillance de programme de résolution de mise à jour - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="ba4cc-138">Fonctionnalités et modifications de comportement</span><span class="sxs-lookup"><span data-stu-id="ba4cc-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="ba4cc-139">push de NuGet.exe - paramètre de délai d’attente ne fonctionne pas - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="ba4cc-140">restauration de NuGet.exe ne produit pas `.props` et `.targets` pour les fichiers `.nuproj` projets (régression dans v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="ba4cc-141">Besoin d’extensibilité API pour comparer des infrastructures des importations - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="ba4cc-142">Masquer les options de dépendance lors de l’utilisation `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="ba4cc-143">Impression nuget.exe en-tête de version dans une sortie détaillée - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="ba4cc-144">NuGet doit prendre en charge pour /runtimes/ {rid} /nativeassets/ {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="ba4cc-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>