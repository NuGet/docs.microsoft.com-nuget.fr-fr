---
title: Notes de mise à jour de NuGet 3.4.4
description: Notes de publication pour NuGet 3.4.4, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="e5ed2-103">Notes de mise à jour de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="e5ed2-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="e5ed2-104">[Notes de publication NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [Notes de version bêta de 3.5 NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="e5ed2-105">Le principal objectif de cette version : les améliorations de la qualité du 3.4.3 version de nuget.exe avec quelques correctifs ainsi l’extension de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e5ed2-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="e5ed2-106">Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="e5ed2-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="e5ed2-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="e5ed2-108">Journal complet</span><span class="sxs-lookup"><span data-stu-id="e5ed2-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="e5ed2-109">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="e5ed2-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="e5ed2-110">Modifications</span><span class="sxs-lookup"><span data-stu-id="e5ed2-110">Changes</span></span>

- <span data-ttu-id="e5ed2-111">Améliorations du Pack : Les améliorations à la compression des symboles, de livraison avec `project.json` plus [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="e5ed2-112">Afficher l’exception lors de l’échec de recherche de projets dans la commande de mise à jour [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="e5ed2-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="e5ed2-113">Lire le type de package à partir de l’entrée `.nuspec` et `project.json` lors de la livraison [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="e5ed2-114">Vérifiez NuGet.Shared pas un projet.</span><span class="sxs-lookup"><span data-stu-id="e5ed2-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="e5ed2-115">\#602</span><span class="sxs-lookup"><span data-stu-id="e5ed2-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="e5ed2-116">Utilisez le délai d’attente de transmission en tant que le délai d’attente de la réponse HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="e5ed2-117">Fichiers de package avec la prochaine fois n’auront pas leurs utilisations [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="e5ed2-118">Mise à jour `NuGet.Core.dll` version 2.12.0 pour résoudre le problème de XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="e5ed2-119">Prend en charge./NuGet.CommandLine.XPlat - v \<détail\> \<mode\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="e5ed2-120">Affichage erreur restauration sans `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="e5ed2-121">Résolution des versions de la dépendance lorsque les versions requises diffèrent [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="e5ed2-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>