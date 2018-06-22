---
title: Notes de mise à jour de NuGet 2.8.5
description: Notes de publication pour NuGet 2.8.5, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820077"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="42593-103">Notes de mise à jour de NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="42593-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="42593-104">[Notes de publication NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Notes de publication](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="42593-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="42593-105">NuGet 2.8.5 a été publiée le 30 mars 2015.</span><span class="sxs-lookup"><span data-stu-id="42593-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="42593-106">Il est une mise à jour mineure sur notre 2.8.3 VSIX avec certains ciblé des correctifs.</span><span class="sxs-lookup"><span data-stu-id="42593-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="42593-107">Dans cette version, la prise en charge pour la boîte de dialogue Gestionnaire de Package NuGet a été ajouté pour [Monikers du Framework cible DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="42593-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="42593-108">Ces nouveaux monikers d’infrastructure qui sont prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="42593-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="42593-109">**core50** - un moniker du framework (TFM) qui est compatible avec la version CLR de base 'base' cible.</span><span class="sxs-lookup"><span data-stu-id="42593-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="42593-110">**dnx452** : à l’aide de la 4.5.2 complète des applications spécifiques à DNX TFM d’une version du framework</span><span class="sxs-lookup"><span data-stu-id="42593-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="42593-111">**dnx46** - A TFM des applications spécifiques en fonction de DNX à l’aide de la version 4.6 complète de l’infrastructure</span><span class="sxs-lookup"><span data-stu-id="42593-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="42593-112">**dnxcore50** - A TFM des applications spécifiques en fonction de DNX à l’aide de la version 5.0 de cœur du framework</span><span class="sxs-lookup"><span data-stu-id="42593-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="42593-113">Un bogue a été résolu que les packages a empêché de s’installer correctement dans les projets FSharp :</span><span class="sxs-lookup"><span data-stu-id="42593-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400