---
title: Notes de publication de NuGet 5,6
description: Notes de publication de NuGet 5,6, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727820"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="77b7b-103">Notes de publication de NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="77b7b-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="77b7b-104">Véhicules de distribution NuGet :</span><span class="sxs-lookup"><span data-stu-id="77b7b-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="77b7b-105">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="77b7b-105">NuGet version</span></span> | <span data-ttu-id="77b7b-106">Disponible dans la version Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77b7b-106">Available in Visual Studio version</span></span>| <span data-ttu-id="77b7b-107">Disponible dans les SDK .NET</span><span class="sxs-lookup"><span data-stu-id="77b7b-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="77b7b-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="77b7b-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="77b7b-109">Visual Studio 2019 version 16,6</span><span class="sxs-lookup"><span data-stu-id="77b7b-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="77b7b-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="77b7b-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="77b7b-111"><sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core</span><span class="sxs-lookup"><span data-stu-id="77b7b-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="77b7b-112">Résumé : nouveautés de 5,6</span><span class="sxs-lookup"><span data-stu-id="77b7b-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="77b7b-113">Prendre en charge les packages de version préliminaire avec des versions flottantes.</span><span class="sxs-lookup"><span data-stu-id="77b7b-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="77b7b-114">`Version="*-*"`, `Version="1.*-*"` et sont similaires aux versions les plus récentes, y compris les versions préliminaires, au sein de la plage spécifiée- [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="77b7b-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="77b7b-115">Problèmes résolus dans cette version</span><span class="sxs-lookup"><span data-stu-id="77b7b-115">Issues fixed in this release</span></span>

<span data-ttu-id="77b7b-116">**Corrigé**</span><span class="sxs-lookup"><span data-stu-id="77b7b-116">**Bugs:**</span></span>

* <span data-ttu-id="77b7b-117">`nuget push *.nupkg`échoue quand snupkg n’existe pas- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="77b7b-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="77b7b-118">Pack, et plusieurs autres chemins de code, ne dépendent pas des paramètres régionaux.</span><span class="sxs-lookup"><span data-stu-id="77b7b-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="77b7b-119">Utilisez RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="77b7b-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="77b7b-120">Perf : la spécification DG pour les scénarios de projet non chargés ne doit pas être écrite dans les restaurations de l’aperçu- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="77b7b-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="77b7b-121">Restauration : améliorer les performances en mettant en cache la spécification du graphique de dépendances de solution- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="77b7b-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="77b7b-122">L’interface utilisateur PM ne fonctionne pas pour les projets de style SDK après l’installation d’un package avec la console PM- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="77b7b-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="77b7b-123">L’icône incorporée ne peut pas être affichée dans l’interface utilisateur PM avec un flux de package local-en fonction de/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="77b7b-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="77b7b-124">NuGetVersion. TryParseStrict () doit retourner false s’il ne parvient pas à analyser- [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="77b7b-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="77b7b-125">`nuget.exe push`aide pour `-source` , doit suggérer l’utilisation du nom de la source, et non l’URL source- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="77b7b-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="77b7b-126">`dotnet nuget add package SourceUri`crée un nom de source de package par défaut incorrect- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="77b7b-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="77b7b-127">Le lecteur d’écran n’annonce pas la « recherche... » message lors du changement d’onglets- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="77b7b-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="77b7b-128">Accessibilité : la couleur du rectangle n’est pas accessible dans les onglets de l’interface utilisateur PM dans le thème sombre- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="77b7b-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="77b7b-129">échec de la restauration de NuGet. exe 5,5 avec MSBuild 14 ou sous- [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="77b7b-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="77b7b-130">Ne pas journaliser les durées en millisecondes des messages de restauration- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="77b7b-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="77b7b-131">Rendre IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="77b7b-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="77b7b-132">Le choix de la version MSBuild fonctionne mal sur certaines cultures non anglaises- [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="77b7b-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="77b7b-133">La valeur par défaut du format est manquante sur `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="77b7b-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="77b7b-134">Perf : RestoreOperationLogger a une affinité de thread inutile- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="77b7b-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="77b7b-135">Création automatisée de documents pour les `dotnet nuget` commandes- [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="77b7b-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="77b7b-136">Le niveau de détail par défaut ne doit pas signaler la restauration NOOP de chaque projet- [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="77b7b-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="77b7b-137">Paramètre de prise en charge `-DependencyVersion` pour `NuGet.exe update` , similaire à la commande d’installation [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="77b7b-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="77b7b-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="77b7b-138">**DCRs:**</span></span>

* <span data-ttu-id="77b7b-139">Ajouter la prise en charge initiale de .net 5.0 Target Framework- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="77b7b-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="77b7b-140">Triez les packages par ID sous l’onglet mises à jour de l’interface utilisateur PM- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="77b7b-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="77b7b-141">**[Liste de tous les problèmes résolus dans cette version-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="77b7b-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
