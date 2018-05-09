---
title: Notes de publication NuGet 2.9-RC
description: Notes de publication pour RC 2.9 de NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="5b0bd-103">Notes de publication NuGet 2.9-RC</span><span class="sxs-lookup"><span data-stu-id="5b0bd-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="5b0bd-104">[Notes de publication NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [Notes de version préliminaire de NuGet 3.0](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="5b0bd-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="5b0bd-105">NuGet 2.9 a été publiée le 10 septembre 2015, comme une mise à jour le 2.8.7 VSIX pour Visual Studio 2012 et 2013.</span><span class="sxs-lookup"><span data-stu-id="5b0bd-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="5b0bd-106">Dans cette version, les mises à jour</span><span class="sxs-lookup"><span data-stu-id="5b0bd-106">Updates in this release</span></span>

* <span data-ttu-id="5b0bd-107">Maintenant ignorer le traitement des packages si leur relation contenant-contenu `.nuspec` document est incorrect - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="5b0bd-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="5b0bd-108">Correction de la gestion des multipartwebrequest de \r\n pour les scénarios d’Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="5b0bd-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="5b0bd-109">Correction de l’intégration avec les événements de build dans les éditions Visual Studio Community 2013 - [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="5b0bd-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="5b0bd-110">Vous trouverez la liste complète des correctifs dans cette version sur GitHub dans le [2.8.8 étape majeure](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="5b0bd-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
