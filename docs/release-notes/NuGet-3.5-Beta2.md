---
title: Notes de publication de 3,5 beta2
description: Notes de publication de NuGet 3,5 Beta 2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776393"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="df520-103">Notes de publication de NuGet 3,5 beta2</span><span class="sxs-lookup"><span data-stu-id="df520-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="df520-104">Notes de publication [de NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)  |  [Notes de publication de NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="df520-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="df520-105">La version RTM de NuGet 3,5 bêta 2 a été publiée le 27 juin 2016 pour Visual Studio 2013 et nuget.exe</span><span class="sxs-lookup"><span data-stu-id="df520-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="df520-106">Journal des modifications complet</span><span class="sxs-lookup"><span data-stu-id="df520-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="df520-107">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="df520-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="df520-108">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="df520-108">Bug Fixes</span></span>

* <span data-ttu-id="df520-109">Mise à jour du message d’erreur en absence de prise en charge du mot de passe decrpytion dans .NET Core pour les flux authentifiés- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="df520-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="df520-110">La console du gestionnaire de package Get-Package échoue si le projet .NET Core est ouvert- [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="df520-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="df520-111">Correction de la gestion incorrecte de 403 dans la commande NuGet Push [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="df520-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="df520-112">Résoudre les problèmes de désinstallation des packages dans une solution liée au contrôle de code source TFS quand disableSourceControlIntegration a la valeur true- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="df520-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="df520-113">Corriger la mise à jour du package pour prendre en compte les packages non cibles- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="df520-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="df520-114">Utiliser le niveau de détail MSBuild pour définir le niveau de journalisation pour les actions d’interface utilisateur du gestionnaire de package NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="df520-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="df520-115">Corriger la configuration NuGet n’est pas une erreur dans les projets de site Web-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="df520-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="df520-116">Corriger les problèmes de package à partir du `.csproj` moment où les fichiers de contenu sont inclus- [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="df520-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="df520-117">DefaultPushSource dans `NuGetDefaults.Config` ( `ProgramData\NuGet` ) ne fonctionne pas- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="df520-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="df520-118">Résoudre le problème dans NuGet 3.4.3 Release-la valeur ne peut pas être null lors de la création du package- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="df520-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="df520-119">La restauration utilise les informations d’identification stockées à partir de Nuget.Config pour les flux VSTS, [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="df520-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="df520-120">Performances-corriger des allocations excessives dans le code de la version d’analyse de version- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="df520-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="df520-121">Résoudre les problèmes lorsque plusieurs instances de nuget.exe essaient d’installer le même package en parallèle [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="df520-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="df520-122">Performances-mettre en cache les informations de dépendance pour les opérations de projets multiples- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="df520-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="df520-123">Résoudre le problème où les sources de package ne sont pas ajoutées à partir des paramètres lorsque la liste source est vide- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="df520-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="df520-124">Corriger l’erreur trompeuse lors de la tentative d’installation du package qui dépend des façades au moment de la conception- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="df520-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="df520-125">L’installation d’un package à partir de la console PackageManager avec le paramètre « All » essaie uniquement la première source [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="df520-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="df520-126">Résoudre les problèmes liés aux packages dont les fichiers ont des temps d’écriture à l’avenir (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="df520-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="df520-127">Afficher une exception en cas d’échec lors de la recherche de projets dans la commande de mise à jour [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="df520-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="df520-128">Le contenu du package n’est pas restauré correctement lors de l’installation d’un package à partir d’un flux NuGet v 3.3 + avec l’argument-NoCache quand le package contient `.nupkg` des fichiers- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="df520-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="df520-129">Résoudre le problème d’installation du package (toutes les sources) quand le package est manquant dans 1 [#2322](https://github.com/NuGet/Home/issues/2322) source</span><span class="sxs-lookup"><span data-stu-id="df520-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="df520-130">Installer les blocs si une seule source ne parvient pas à obtenir l’autorisation- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="df520-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="df520-131">`.nuspec` la plage de versions doit remplacer-IncludeReferencedProjects version- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="df520-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="df520-132">La mise à jour NuGet 3.3.0 échoue avec «une contrainte supplémentaire... défini dans packages.config empêche cette opération.»</span><span class="sxs-lookup"><span data-stu-id="df520-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="df520-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="df520-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="df520-134">nuget.exe mise à jour supprime le nom fort et l’attribut privé de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="df520-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="df520-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="df520-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="df520-136">Résoudre les problèmes liés au chemin de fichier relatif pour « DefaultPushSource »- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="df520-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="df520-137">Améliorer les messages d’échec du programme de résolution des mises à jour- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="df520-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="df520-138">Fonctionnalités et changements de comportement</span><span class="sxs-lookup"><span data-stu-id="df520-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="df520-139">Le paramètre nuget.exe Push-Timeout ne fonctionne pas- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="df520-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="df520-140">nuget.exe restauration ne produit pas les `.props` `.targets` fichiers et pour les `.nuproj` projets (régression dans v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="df520-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="df520-141">Nécessite une API d’extensibilité pour comparer des frameworks à des importations- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="df520-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="df520-142">Masquer les options de dépendance lors de l’utilisation de `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="df520-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="df520-143">Imprimer l’en-tête de version nuget.exe dans la sortie détaillée- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="df520-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="df520-144">NuGet doit ajouter la prise en charge de/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="df520-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>