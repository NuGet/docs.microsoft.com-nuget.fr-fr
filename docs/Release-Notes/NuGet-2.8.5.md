---
title: Notes de publication NuGet 2.8.5 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Notes de publication pour NuGet 2.8.5, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 2.8.5 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="967b4-104">Notes de mise à jour de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="967b4-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="967b4-105">[Notes de publication NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Notes de publication](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="967b4-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="967b4-106">NuGet 2.8.5 a été publiée le 30 mars 2015.</span><span class="sxs-lookup"><span data-stu-id="967b4-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="967b4-107">Il est une mise à jour mineure sur notre 2.8.3 VSIX avec certains ciblé des correctifs.</span><span class="sxs-lookup"><span data-stu-id="967b4-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="967b4-108">Dans cette version, la prise en charge pour la boîte de dialogue Gestionnaire de Package NuGet a été ajouté pour [Monikers du Framework cible DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="967b4-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="967b4-109">Ces nouveaux monikers d’infrastructure qui sont prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="967b4-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="967b4-110">**core50** - un moniker du framework (TFM) qui est compatible avec la version CLR de base 'base' cible.</span><span class="sxs-lookup"><span data-stu-id="967b4-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="967b4-111">**dnx452** : à l’aide de la 4.5.2 complète des applications spécifiques à DNX TFM d’une version du framework</span><span class="sxs-lookup"><span data-stu-id="967b4-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="967b4-112">**dnx46** - A TFM des applications spécifiques en fonction de DNX à l’aide de la version 4.6 complète de l’infrastructure</span><span class="sxs-lookup"><span data-stu-id="967b4-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="967b4-113">**dnxcore50** - A TFM des applications spécifiques en fonction de DNX à l’aide de la version 5.0 de cœur du framework</span><span class="sxs-lookup"><span data-stu-id="967b4-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="967b4-114">Un bogue a été résolu que les packages a empêché de s’installer correctement dans les projets FSharp :</span><span class="sxs-lookup"><span data-stu-id="967b4-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="967b4-115">https://NuGet.codeplex.com/WorkItem/4400</span><span class="sxs-lookup"><span data-stu-id="967b4-115">https://nuget.codeplex.com/workitem/4400</span></span>