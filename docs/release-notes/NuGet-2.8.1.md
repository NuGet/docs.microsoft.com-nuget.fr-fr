---
title: Notes de publication de NuGet 2.8.1
description: Notes de publication pour NuGet 2.8.1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776774"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="88035-103">Notes de publication de NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="88035-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="88035-104">Notes de publication de [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Notes de publication de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="88035-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="88035-105">NuGet 2.8.1 a été publié le 2 avril 2014.</span><span class="sxs-lookup"><span data-stu-id="88035-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="88035-106">Fonctionnalités notables dans la version</span><span class="sxs-lookup"><span data-stu-id="88035-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="88035-107">Prise en charge des projets Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="88035-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="88035-108">Cette version prend désormais en charge les nouveaux monikers de Framework cible suivants qui peuvent être utilisés pour cibler des projets Windows Phone 8,1 :</span><span class="sxs-lookup"><span data-stu-id="88035-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="88035-109">WindowsPhone81/WP81 (pour les projets de Windows Phone basés sur Silverlight)</span><span class="sxs-lookup"><span data-stu-id="88035-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="88035-110">WindowsPhoneApp81/WPA81 (pour les projets d’application Windows Phone basés sur WinRT)</span><span class="sxs-lookup"><span data-stu-id="88035-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="88035-111">Mise à jour de l’extension NuGet WebMatrix</span><span class="sxs-lookup"><span data-stu-id="88035-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="88035-112">Cette version met à jour le client NuGet trouvé dans WebMatrix à l’aide de [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 et intègre des fonctionnalités telles que les transformations xdt.</span><span class="sxs-lookup"><span data-stu-id="88035-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="88035-113">Plus important encore, la mise à jour de base de 2.6.1 permet au client WebMatrix d’installer des packages NuGet qui contiennent des versions plus récentes du `.nuspec` schéma, y compris les packages nuget ASP.net.</span><span class="sxs-lookup"><span data-stu-id="88035-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="88035-114">Pour plus d’informations sur la mise à jour de l’extension WebMatrix, consultez ces [notes de publication](../release-notes/nuget-2.6.1-for-WebMatrix.md)spécifiques.</span><span class="sxs-lookup"><span data-stu-id="88035-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="88035-115">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="88035-115">Bug Fixes</span></span>
<span data-ttu-id="88035-116">Outre ces fonctionnalités, cette version de NuGet comprend d’autres correctifs de bogues.</span><span class="sxs-lookup"><span data-stu-id="88035-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="88035-117">16 problèmes ont été résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="88035-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="88035-118">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2.8.1, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="88035-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="88035-119">Réexpédition avec Visual Studio « 14 » CTP</span><span class="sxs-lookup"><span data-stu-id="88035-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="88035-120">Dans Visual Studio « 14 » CTP publié le 3 juin 2014, NuGet 2.8.1 est fourni dans la zone.</span><span class="sxs-lookup"><span data-stu-id="88035-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="88035-121">Les fonctionnalités qu’il prend en charge restent les unes des autres avec d’autres VSIXes 2.8.1, comme celui de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="88035-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
