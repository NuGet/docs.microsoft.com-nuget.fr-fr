---
title: Notes de publication de NuGet 2,9-RC
description: Notes de publication de NuGet 2,9 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780311"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="891ac-103">Notes de publication de NuGet 2,9-RC</span><span class="sxs-lookup"><span data-stu-id="891ac-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="891ac-104">Notes de publication de [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Notes de publication de NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="891ac-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="891ac-105">NuGet 2,9 a été publié le 10 septembre 2015 en tant que mise à jour de 2.8.7 VSIX pour Visual Studio 2012 et 2013.</span><span class="sxs-lookup"><span data-stu-id="891ac-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="891ac-106">Mises à jour dans cette version</span><span class="sxs-lookup"><span data-stu-id="891ac-106">Updates in this release</span></span>

* <span data-ttu-id="891ac-107">À présent, les packages de traitement sont ignorés si leur `.nuspec` document contenu est incorrect- [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="891ac-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="891ac-108">Correction du traitement multipartwebrequest de \r\n pour les scénarios UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="891ac-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="891ac-109">Correction de l’intégration avec les événements de build dans Visual Studio 2013 Édition Community- [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="891ac-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="891ac-110">La liste complète des correctifs dans cette version est disponible sur GitHub dans le [jalon 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="891ac-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
