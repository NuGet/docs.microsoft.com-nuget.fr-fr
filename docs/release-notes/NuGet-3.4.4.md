---
title: Notes de publication de NuGet 3.4.4
description: Notes de publication pour NuGet 3.4.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780220"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="363e4-103">Notes de publication de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="363e4-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="363e4-104">Notes de publication de [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Notes de publication de NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="363e4-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="363e4-105">L’objectif principal de cette version était d’améliorer la qualité de la version 3.4.3 de nuget.exe avec quelques correctifs de l’extension Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="363e4-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="363e4-106">Vous pouvez télécharger les versions VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="363e4-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="363e4-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="363e4-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="363e4-108">Journal des modifications complet</span><span class="sxs-lookup"><span data-stu-id="363e4-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="363e4-109">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="363e4-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="363e4-110">Modifications</span><span class="sxs-lookup"><span data-stu-id="363e4-110">Changes</span></span>

- <span data-ttu-id="363e4-111">Améliorations des packs : améliorations de la compression des symboles, compression avec `project.json` et plus de [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="363e4-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="363e4-112">Afficher une exception en cas d’échec lors de la recherche de projets dans la commande Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="363e4-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="363e4-113">Lire le type de package à partir de l’entrée `.nuspec` et lors de la `project.json` compression [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="363e4-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="363e4-114">Mettez NuGet. Shared non un projet.</span><span class="sxs-lookup"><span data-stu-id="363e4-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="363e4-115">\#602</span><span class="sxs-lookup"><span data-stu-id="363e4-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="363e4-116">Utilisez le délai d’expiration de Push comme délai de réponse HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="363e4-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="363e4-117">Les fichiers de package avec des heures futures n’auront pas les heures utilisées [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="363e4-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="363e4-118">Mise à jour `NuGet.Core.dll` de la version vers 2.12.0 pour résoudre le problème XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="363e4-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="363e4-119">Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="363e4-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="363e4-120">Afficher les erreurs de restauration sans `project.json` ou `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="363e4-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="363e4-121">Correction des versions de dépendance lorsque les versions requises diffèrent de [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="363e4-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>