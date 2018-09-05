---
title: Notes de publication de NuGet 2.8.5
description: Notes de publication pour NuGet 2.8.5, notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548623"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="8e0a3-103">Notes de publication de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="8e0a3-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="8e0a3-104">[Notes de publication de NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [Notes de publication de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="8e0a3-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="8e0a3-105">NuGet 2.8.5 a été publiée le 30 mars 2015.</span><span class="sxs-lookup"><span data-stu-id="8e0a3-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="8e0a3-106">Il est une mise à jour mineure sur notre 2.8.3 VSIX avec certains ciblé des correctifs.</span><span class="sxs-lookup"><span data-stu-id="8e0a3-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="8e0a3-107">Dans cette version, la prise en charge pour la boîte de dialogue Gestionnaire de Package NuGet a été ajoutée pour [Monikers du Framework cible DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="8e0a3-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="8e0a3-108">Ces nouvelles monikers du framework qui sont pris en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e0a3-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="8e0a3-109">**core50** : un moniker du framework (TFM) qui est compatible avec le CLR de base 'base' cible.</span><span class="sxs-lookup"><span data-stu-id="8e0a3-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="8e0a3-110">**dnx452** : un moniker du Framework cible des applications spécifiques basée sur DNX à l’aide de la 4.5.2 complète version du framework</span><span class="sxs-lookup"><span data-stu-id="8e0a3-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="8e0a3-111">**dnx46** : un moniker du Framework cible des applications spécifiques basée sur DNX à l’aide de la version 4.6 complète du framework</span><span class="sxs-lookup"><span data-stu-id="8e0a3-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="8e0a3-112">**: dnxcore50** : un moniker du Framework cible des applications spécifiques basée sur DNX à l’aide de la version 5.0 de Core du framework</span><span class="sxs-lookup"><span data-stu-id="8e0a3-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="8e0a3-113">Un bogue a été résolu que les packages a empêché de s’installer correctement dans les projets FSharp :</span><span class="sxs-lookup"><span data-stu-id="8e0a3-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400