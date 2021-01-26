---
title: Notes de publication de NuGet 2.8.5
description: Notes de publication pour NuGet 2.8.5, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780358"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="039f3-103">Notes de publication de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="039f3-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="039f3-104">Notes de publication de [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Notes de publication de NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="039f3-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="039f3-105">NuGet 2.8.5 a été publié le 30 mars 2015.</span><span class="sxs-lookup"><span data-stu-id="039f3-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="039f3-106">Il s’agit d’une mise à jour mineure de notre VSIX 2.8.3 avec certains correctifs ciblés.</span><span class="sxs-lookup"><span data-stu-id="039f3-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="039f3-107">Dans cette version, la boîte de dialogue prise en charge du gestionnaire de package NuGet a été ajoutée pour les [monikers du Framework cible DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="039f3-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="039f3-108">Ces nouveaux monikers de Framework pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="039f3-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="039f3-109">**core50** -un moniker de Framework cible’base' (TFM) qui est compatible avec le CLR principal.</span><span class="sxs-lookup"><span data-stu-id="039f3-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="039f3-110">**dnx452** -A TFM spécifique aux applications basées sur DNX utilisant la version 4.5.2 complète de l’infrastructure</span><span class="sxs-lookup"><span data-stu-id="039f3-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="039f3-111">**dnx46** -A TFM spécifique aux applications basées sur DNX utilisant la version 4,6 complète de l’infrastructure</span><span class="sxs-lookup"><span data-stu-id="039f3-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="039f3-112">**dnxcore50** -A TFM spécifique aux applications basées sur DNX à l’aide de la version 5,0 principale de l’infrastructure</span><span class="sxs-lookup"><span data-stu-id="039f3-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="039f3-113">Un bogue qui empêchait l’installation correcte des packages dans les projets FSharp a été corrigé :</span><span class="sxs-lookup"><span data-stu-id="039f3-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400