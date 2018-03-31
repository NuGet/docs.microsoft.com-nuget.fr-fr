---
title: Limites du taux de | Documents Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Les APIs NuGet sera ont appliqué les limites de taux pour prévenir les abus.
keywords: Limitation du débit NuGet API,
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="75b82-104">Limites du débit</span><span class="sxs-lookup"><span data-stu-id="75b82-104">Rate Limits</span></span>

<span data-ttu-id="75b82-105">L’API NuGet.org applique la limitation du débit pour prévenir les abus.</span><span class="sxs-lookup"><span data-stu-id="75b82-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="75b82-106">Requêtes qui dépassent la limite du taux renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="75b82-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="75b82-107">Les tableaux suivants répertorient les limites de taux pour l’API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="75b82-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="75b82-108">Recherche de package</span><span class="sxs-lookup"><span data-stu-id="75b82-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="75b82-109">Nous vous recommandons d’utiliser des NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) pour la recherche est performant et n’avez aucune limite actuellement.</span><span class="sxs-lookup"><span data-stu-id="75b82-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="75b82-110">Pour V1 et V2 les API de recherche, les limites followins s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="75b82-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="75b82-111">API</span><span class="sxs-lookup"><span data-stu-id="75b82-111">API</span></span> | <span data-ttu-id="75b82-112">Type de limite</span><span class="sxs-lookup"><span data-stu-id="75b82-112">Limit Type</span></span> | <span data-ttu-id="75b82-113">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="75b82-113">Limit Value</span></span> | <span data-ttu-id="75b82-114">API usecase</span><span class="sxs-lookup"><span data-stu-id="75b82-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="75b82-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="75b82-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="75b82-116">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-116">IP</span></span> | <span data-ttu-id="75b82-117">1000 / minute</span><span class="sxs-lookup"><span data-stu-id="75b82-117">1000 / minute</span></span> | <span data-ttu-id="75b82-118">Interroger les métadonnées de package NuGet via v1 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="75b82-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="75b82-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="75b82-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="75b82-120">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-120">IP</span></span> | <span data-ttu-id="75b82-121">3000 / minute</span><span class="sxs-lookup"><span data-stu-id="75b82-121">3000 / minute</span></span> | <span data-ttu-id="75b82-122">Rechercher les packages NuGet via le point de terminaison recherche v1</span><span class="sxs-lookup"><span data-stu-id="75b82-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="75b82-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="75b82-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="75b82-124">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-124">IP</span></span> | <span data-ttu-id="75b82-125">20000 / minute</span><span class="sxs-lookup"><span data-stu-id="75b82-125">20000 / minute</span></span> | <span data-ttu-id="75b82-126">Interroger les métadonnées de package NuGet via v2 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="75b82-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="75b82-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="75b82-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="75b82-128">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-128">IP</span></span> | <span data-ttu-id="75b82-129">100 / minute</span><span class="sxs-lookup"><span data-stu-id="75b82-129">100 / minute</span></span> | <span data-ttu-id="75b82-130">Nombre de package NuGet via v2 OData de requête `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="75b82-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="75b82-131">Package Push et de retrait de la liste</span><span class="sxs-lookup"><span data-stu-id="75b82-131">Package Push and Unlist</span></span>

| <span data-ttu-id="75b82-132">API</span><span class="sxs-lookup"><span data-stu-id="75b82-132">API</span></span> | <span data-ttu-id="75b82-133">Type de limite</span><span class="sxs-lookup"><span data-stu-id="75b82-133">Limit Type</span></span> | <span data-ttu-id="75b82-134">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="75b82-134">Limit Value</span></span> | <span data-ttu-id="75b82-135">APU usecase</span><span class="sxs-lookup"><span data-stu-id="75b82-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="75b82-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="75b82-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="75b82-137">Clé API</span><span class="sxs-lookup"><span data-stu-id="75b82-137">API Key</span></span> | <span data-ttu-id="75b82-138">100 / minute</span><span class="sxs-lookup"><span data-stu-id="75b82-138">100 / minute</span></span> | <span data-ttu-id="75b82-139">Téléchargez un nouveau package NuGet (version) via le point de terminaison par émission de données v2</span><span class="sxs-lookup"><span data-stu-id="75b82-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="75b82-140">**SUPPRIMER** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="75b82-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="75b82-141">Clé API</span><span class="sxs-lookup"><span data-stu-id="75b82-141">API Key</span></span> | <span data-ttu-id="75b82-142">100 / minute</span><span class="sxs-lookup"><span data-stu-id="75b82-142">100 / minute</span></span> | <span data-ttu-id="75b82-143">Retrait de la liste un package NuGet (version) via le point de terminaison v2</span><span class="sxs-lookup"><span data-stu-id="75b82-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
