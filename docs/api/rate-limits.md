---
title: Taux de limites, NuGet API
description: Les APIs NuGet sera ont appliqué les limites de taux pour prévenir les abus.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2018
---
# <a name="rate-limits"></a><span data-ttu-id="4dce9-103">Limites du débit</span><span class="sxs-lookup"><span data-stu-id="4dce9-103">Rate Limits</span></span>

<span data-ttu-id="4dce9-104">L’API NuGet.org applique la limitation du débit pour prévenir les abus.</span><span class="sxs-lookup"><span data-stu-id="4dce9-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="4dce9-105">Requêtes qui dépassent la limite du taux renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="4dce9-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="4dce9-106">Les tableaux suivants répertorient les limites de taux pour l’API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4dce9-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="4dce9-107">Recherche de package</span><span class="sxs-lookup"><span data-stu-id="4dce9-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="4dce9-108">Nous vous recommandons d’utiliser des NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) pour la recherche est performant et n’avez aucune limite actuellement.</span><span class="sxs-lookup"><span data-stu-id="4dce9-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="4dce9-109">Pour V1 et V2 les API de recherche, les limites followins s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="4dce9-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="4dce9-110">API</span><span class="sxs-lookup"><span data-stu-id="4dce9-110">API</span></span> | <span data-ttu-id="4dce9-111">Type de limite</span><span class="sxs-lookup"><span data-stu-id="4dce9-111">Limit Type</span></span> | <span data-ttu-id="4dce9-112">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="4dce9-112">Limit Value</span></span> | <span data-ttu-id="4dce9-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="4dce9-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="4dce9-114">**TÉLÉCHARGER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="4dce9-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="4dce9-115">IP</span><span class="sxs-lookup"><span data-stu-id="4dce9-115">IP</span></span> | <span data-ttu-id="4dce9-116">1000 / minute</span><span class="sxs-lookup"><span data-stu-id="4dce9-116">1000 / minute</span></span> | <span data-ttu-id="4dce9-117">Interroger les métadonnées de package NuGet via v1 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="4dce9-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="4dce9-118">**TÉLÉCHARGER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="4dce9-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="4dce9-119">IP</span><span class="sxs-lookup"><span data-stu-id="4dce9-119">IP</span></span> | <span data-ttu-id="4dce9-120">3000 / minute</span><span class="sxs-lookup"><span data-stu-id="4dce9-120">3000 / minute</span></span> | <span data-ttu-id="4dce9-121">Rechercher les packages NuGet via le point de terminaison recherche v1</span><span class="sxs-lookup"><span data-stu-id="4dce9-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="4dce9-122">**TÉLÉCHARGER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="4dce9-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="4dce9-123">IP</span><span class="sxs-lookup"><span data-stu-id="4dce9-123">IP</span></span> | <span data-ttu-id="4dce9-124">20000 / minute</span><span class="sxs-lookup"><span data-stu-id="4dce9-124">20000 / minute</span></span> | <span data-ttu-id="4dce9-125">Interroger les métadonnées de package NuGet via v2 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="4dce9-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="4dce9-126">**TÉLÉCHARGER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="4dce9-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="4dce9-127">IP</span><span class="sxs-lookup"><span data-stu-id="4dce9-127">IP</span></span> | <span data-ttu-id="4dce9-128">100 / minute</span><span class="sxs-lookup"><span data-stu-id="4dce9-128">100 / minute</span></span> | <span data-ttu-id="4dce9-129">Nombre de package NuGet via v2 OData de requête `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="4dce9-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="4dce9-130">Package Push et de retrait de la liste</span><span class="sxs-lookup"><span data-stu-id="4dce9-130">Package Push and Unlist</span></span>

| <span data-ttu-id="4dce9-131">API</span><span class="sxs-lookup"><span data-stu-id="4dce9-131">API</span></span> | <span data-ttu-id="4dce9-132">Type de limite</span><span class="sxs-lookup"><span data-stu-id="4dce9-132">Limit Type</span></span> | <span data-ttu-id="4dce9-133">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="4dce9-133">Limit Value</span></span> | <span data-ttu-id="4dce9-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="4dce9-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="4dce9-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="4dce9-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="4dce9-136">Clé API</span><span class="sxs-lookup"><span data-stu-id="4dce9-136">API Key</span></span> | <span data-ttu-id="4dce9-137">250 / heure</span><span class="sxs-lookup"><span data-stu-id="4dce9-137">250 / hour</span></span> | <span data-ttu-id="4dce9-138">Téléchargez un nouveau package NuGet (version) via le point de terminaison par émission de données v2</span><span class="sxs-lookup"><span data-stu-id="4dce9-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="4dce9-139">**SUPPRIMER** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="4dce9-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="4dce9-140">Clé API</span><span class="sxs-lookup"><span data-stu-id="4dce9-140">API Key</span></span> | <span data-ttu-id="4dce9-141">250 / heure</span><span class="sxs-lookup"><span data-stu-id="4dce9-141">250 / hour</span></span> | <span data-ttu-id="4dce9-142">Retrait de la liste un package NuGet (version) via le point de terminaison v2</span><span class="sxs-lookup"><span data-stu-id="4dce9-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
