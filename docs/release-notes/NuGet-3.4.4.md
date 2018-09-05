---
title: Notes de publication de NuGet 3.4.4
description: Notes de publication pour NuGet 3.4.4, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547471"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="2a4ec-103">Notes de publication de NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="2a4ec-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="2a4ec-104">[Notes de publication de NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [Notes de publication NuGet 3.5 bêta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="2a4ec-105">Le principal objectif de cette version a été améliorations apportées à la qualité de 3.4.3 version de nuget.exe avec quelques correctifs à l’extension de Visual Studio et.</span><span class="sxs-lookup"><span data-stu-id="2a4ec-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="2a4ec-106">Vous pouvez télécharger l’extension VSIX et nuget.exe [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="2a4ec-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="2a4ec-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="2a4ec-108">Journal des modifications complet</span><span class="sxs-lookup"><span data-stu-id="2a4ec-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="2a4ec-109">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="2a4ec-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="2a4ec-110">Modifications</span><span class="sxs-lookup"><span data-stu-id="2a4ec-110">Changes</span></span>

- <span data-ttu-id="2a4ec-111">Améliorations du Pack : Améliorations pour la compression des symboles, de livraison avec `project.json` et plus [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="2a4ec-112">Afficher l’exception lors de l’échec de recherche de projets dans la commande de mise à jour [\#605](https://github.com/NuGet/NuGet.Client/pull/605)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="2a4ec-113">Lire le type de package à partir de l’entrée `.nuspec` et `project.json` lors de la compression [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="2a4ec-114">Rendre NuGet.Shared pas un projet.</span><span class="sxs-lookup"><span data-stu-id="2a4ec-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="2a4ec-115">\#602</span><span class="sxs-lookup"><span data-stu-id="2a4ec-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="2a4ec-116">Utiliser le délai d’attente de transmission en tant que le délai d’expiration de la réponse HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="2a4ec-117">Fichiers de package avec des dates futures n’aura pas leurs utilisations [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="2a4ec-118">La mise à jour `NuGet.Core.dll` version à 2.12.0 pour résoudre le problème de XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="2a4ec-119">Prise en charge de v -./NuGet.CommandLine.XPlat \<commentaires\> \<mode\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="2a4ec-120">Restauration d’erreur complet sans `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="2a4ec-121">Résolution des versions de dépendances lorsque diffèrent des versions requises [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="2a4ec-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>