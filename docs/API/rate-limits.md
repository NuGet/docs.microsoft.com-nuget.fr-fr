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
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a><span data-ttu-id="d2849-103">Limites du débit</span><span class="sxs-lookup"><span data-stu-id="d2849-103">Rate Limits</span></span>

<span data-ttu-id="d2849-104">L’API NuGet.org applique la limitation du débit pour prévenir les abus.</span><span class="sxs-lookup"><span data-stu-id="d2849-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="d2849-105">Requêtes qui dépassent la limite du taux renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="d2849-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="d2849-106">Les tableaux suivants répertorient les limites de taux pour l’API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d2849-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="d2849-107">Recherche de package</span><span class="sxs-lookup"><span data-stu-id="d2849-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="d2849-108">Nous vous recommandons d’utiliser des NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) pour la recherche est performant et n’avez aucune limite actuellement.</span><span class="sxs-lookup"><span data-stu-id="d2849-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="d2849-109">Pour V1 et V2 les API de recherche, les limites followins s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="d2849-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="d2849-110">API</span><span class="sxs-lookup"><span data-stu-id="d2849-110">API</span></span> | <span data-ttu-id="d2849-111">Type de limite</span><span class="sxs-lookup"><span data-stu-id="d2849-111">Limit Type</span></span> | <span data-ttu-id="d2849-112">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="d2849-112">Limit Value</span></span> | <span data-ttu-id="d2849-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="d2849-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="d2849-114">**TÉLÉCHARGER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="d2849-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="d2849-115">IP</span><span class="sxs-lookup"><span data-stu-id="d2849-115">IP</span></span> | <span data-ttu-id="d2849-116">1000 / minute</span><span class="sxs-lookup"><span data-stu-id="d2849-116">1000 / minute</span></span> | <span data-ttu-id="d2849-117">Interroger les métadonnées de package NuGet via v1 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="d2849-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="d2849-118">**TÉLÉCHARGER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="d2849-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="d2849-119">IP</span><span class="sxs-lookup"><span data-stu-id="d2849-119">IP</span></span> | <span data-ttu-id="d2849-120">3000 / minute</span><span class="sxs-lookup"><span data-stu-id="d2849-120">3000 / minute</span></span> | <span data-ttu-id="d2849-121">Rechercher les packages NuGet via le point de terminaison recherche v1</span><span class="sxs-lookup"><span data-stu-id="d2849-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="d2849-122">**TÉLÉCHARGER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="d2849-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="d2849-123">IP</span><span class="sxs-lookup"><span data-stu-id="d2849-123">IP</span></span> | <span data-ttu-id="d2849-124">20000 / minute</span><span class="sxs-lookup"><span data-stu-id="d2849-124">20000 / minute</span></span> | <span data-ttu-id="d2849-125">Interroger les métadonnées de package NuGet via v2 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="d2849-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="d2849-126">**TÉLÉCHARGER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="d2849-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="d2849-127">IP</span><span class="sxs-lookup"><span data-stu-id="d2849-127">IP</span></span> | <span data-ttu-id="d2849-128">100 / minute</span><span class="sxs-lookup"><span data-stu-id="d2849-128">100 / minute</span></span> | <span data-ttu-id="d2849-129">Nombre de package NuGet via v2 OData de requête `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="d2849-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="d2849-130">Package Push et de retrait de la liste</span><span class="sxs-lookup"><span data-stu-id="d2849-130">Package Push and Unlist</span></span>

| <span data-ttu-id="d2849-131">API</span><span class="sxs-lookup"><span data-stu-id="d2849-131">API</span></span> | <span data-ttu-id="d2849-132">Type de limite</span><span class="sxs-lookup"><span data-stu-id="d2849-132">Limit Type</span></span> | <span data-ttu-id="d2849-133">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="d2849-133">Limit Value</span></span> | <span data-ttu-id="d2849-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="d2849-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="d2849-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="d2849-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="d2849-136">Clé API</span><span class="sxs-lookup"><span data-stu-id="d2849-136">API Key</span></span> | <span data-ttu-id="d2849-137">100 / minute</span><span class="sxs-lookup"><span data-stu-id="d2849-137">100 / minute</span></span> | <span data-ttu-id="d2849-138">Téléchargez un nouveau package NuGet (version) via le point de terminaison par émission de données v2</span><span class="sxs-lookup"><span data-stu-id="d2849-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="d2849-139">**SUPPRIMER** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="d2849-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="d2849-140">Clé API</span><span class="sxs-lookup"><span data-stu-id="d2849-140">API Key</span></span> | <span data-ttu-id="d2849-141">100 / minute</span><span class="sxs-lookup"><span data-stu-id="d2849-141">100 / minute</span></span> | <span data-ttu-id="d2849-142">Retrait de la liste un package NuGet (version) via le point de terminaison v2</span><span class="sxs-lookup"><span data-stu-id="d2849-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
