---
title: Notes de publication NuGet 2.8.1 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "Notes de publication pour NuGet 2.8.1, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.8.1 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="0309a-104">Notes de mise à jour de NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="0309a-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="0309a-105">[Notes de publication NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet point 2.8.2 Notes de publication](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="0309a-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="0309a-106">NuGet 2.8.1 a été publiée le 2 avril 2014.</span><span class="sxs-lookup"><span data-stu-id="0309a-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="0309a-107">Fonctionnalités notables dans la version</span><span class="sxs-lookup"><span data-stu-id="0309a-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="0309a-108">Prise en charge pour les projets Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="0309a-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="0309a-109">Cette version prend désormais en charge des monikers framework cible suivant nouvelle qui peuvent être utilisé pour les projets ciblent Windows Phone 8.1 :</span><span class="sxs-lookup"><span data-stu-id="0309a-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="0309a-110">WindowsPhone81 / WP81 (pour les projets de Windows Phone basés sur Silverlight)</span><span class="sxs-lookup"><span data-stu-id="0309a-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="0309a-111">WindowsPhoneApp81 / WPA81 (pour les projets d’application Windows Phone WinRT)</span><span class="sxs-lookup"><span data-stu-id="0309a-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="0309a-112">Mise à jour de l’Extension de WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="0309a-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="0309a-113">Cette version met à jour le client NuGet trouvé dans WebMatrix pour [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 et met avec elle fonctionnalités telles que les transformations XDT.</span><span class="sxs-lookup"><span data-stu-id="0309a-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="0309a-114">Plus important encore, le 2.6.1 mise à jour principale permet au client de WebMatrix installer les packages NuGet qui contiennent des versions plus récentes de la `.nuspec` schéma, qui inclut les packages NuGet ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0309a-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="0309a-115">Pour plus d’informations sur la mise à jour de l’Extension de WebMatrix, consultez spécifiques [notes de publication](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="0309a-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="0309a-116">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="0309a-116">Bug Fixes</span></span>
<span data-ttu-id="0309a-117">Outre ces fonctionnalités, cette version de NuGet inclut autres correctifs de bogues.</span><span class="sxs-lookup"><span data-stu-id="0309a-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="0309a-118">Il existait des problèmes de total 16 traités dans la mise en production.</span><span class="sxs-lookup"><span data-stu-id="0309a-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="0309a-119">Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet 2.8.1, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="0309a-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="0309a-120">Reshipping avec Visual Studio « 14 » CTP</span><span class="sxs-lookup"><span data-stu-id="0309a-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="0309a-121">Dans Visual Studio « 14 » CTP de juin 3e 2014 a publié, NuGet 2.8.1 est fourni dans la zone.</span><span class="sxs-lookup"><span data-stu-id="0309a-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="0309a-122">Il prend en charge les fonctionnalités de restent dans par avec d’autres 2.8.1 VSIXes tel que celui de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0309a-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
