---
title: Notes de publication de NuGet 2.8.1
description: Notes de publication pour NuGet 2.8.1 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545237"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="3260d-103">Notes de publication de NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="3260d-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="3260d-104">[Notes de publication NuGet 2.8](../release-notes/nuget-2.8.md) | [Notes de publication de NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="3260d-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="3260d-105">NuGet 2.8.1 a été publiée le 2 avril 2014.</span><span class="sxs-lookup"><span data-stu-id="3260d-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="3260d-106">Fonctionnalités notables dans la version</span><span class="sxs-lookup"><span data-stu-id="3260d-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="3260d-107">Prise en charge pour les projets Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="3260d-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="3260d-108">Cette version prend désormais en charge les suivant monikers du framework cible nouvelle qui peuvent être utilisé pour les projets ciblent Windows Phone 8.1 :</span><span class="sxs-lookup"><span data-stu-id="3260d-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="3260d-109">WindowsPhone81 / WP81 (pour les projets de Windows Phone basé sur Silverlight)</span><span class="sxs-lookup"><span data-stu-id="3260d-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="3260d-110">WindowsPhoneApp81 / WPA81 (pour les projets d’application Windows Phone WinRT)</span><span class="sxs-lookup"><span data-stu-id="3260d-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="3260d-111">Mise à jour de l’Extension de WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="3260d-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="3260d-112">Cette version met à jour le client NuGet trouvé dans WebMatrix pour [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 et apporte avec elle fonctionnalités telles que les transformations XDT.</span><span class="sxs-lookup"><span data-stu-id="3260d-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="3260d-113">Plus important encore, le 2.6.1 mises à jour core permet au client de WebMatrix installer les packages NuGet qui contiennent des versions plus récentes de la `.nuspec` schéma, qui inclut les packages NuGet ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3260d-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="3260d-114">Pour plus d’informations sur la mise à jour de l’Extension de WebMatrix, consultez ces spécifiques [notes de version](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="3260d-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="3260d-115">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="3260d-115">Bug Fixes</span></span>
<span data-ttu-id="3260d-116">Outre ces fonctionnalités, cette version de NuGet inclut des correctifs de bogues.</span><span class="sxs-lookup"><span data-stu-id="3260d-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="3260d-117">Vous rencontrez des problèmes de total 16 résolus dans la version.</span><span class="sxs-lookup"><span data-stu-id="3260d-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="3260d-118">Pour obtenir la liste complète des travaux éléments résolus dans NuGet 2.8.1, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="3260d-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="3260d-119">Reshipping avec Visual Studio « 14 » CTP</span><span class="sxs-lookup"><span data-stu-id="3260d-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="3260d-120">Dans les CTP Visual Studio « 14 » publié en juin 3e 2014, NuGet 2.8.1 est fourni dans la zone.</span><span class="sxs-lookup"><span data-stu-id="3260d-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="3260d-121">Les fonctionnalités il prend en charge restent dans pair avec les autres 2.8.1 VSIXes tel que celui pour Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="3260d-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
