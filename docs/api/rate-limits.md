---
title: Limites, NuGet API du taux
description: Les APIs NuGet sera ont appliqué les limites de débit pour empêcher les abus.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548675"
---
# <a name="rate-limits"></a><span data-ttu-id="7b78f-103">Limites du débit</span><span class="sxs-lookup"><span data-stu-id="7b78f-103">Rate Limits</span></span>

<span data-ttu-id="7b78f-104">L’API de NuGet.org applique la limitation du débit pour empêcher les abus.</span><span class="sxs-lookup"><span data-stu-id="7b78f-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="7b78f-105">Requêtes qui dépassent la limite de débit renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="7b78f-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="7b78f-106">En plus de la demande à l’aide des limites de taux de limitation, certaines API également appliquent des quotas.</span><span class="sxs-lookup"><span data-stu-id="7b78f-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="7b78f-107">Requêtes qui dépassent le quota renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="7b78f-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="7b78f-108">Les tableaux suivants répertorient les limites de taux pour l’API de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7b78f-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="7b78f-109">Recherche de package</span><span class="sxs-lookup"><span data-stu-id="7b78f-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="7b78f-110">Nous recommandons l’utilisation de NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) pour recherche performante et n’avez aucune limite actuellement.</span><span class="sxs-lookup"><span data-stu-id="7b78f-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="7b78f-111">API de recherche pour V1 et V2, les limites followins s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="7b78f-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="7b78f-112">API</span><span class="sxs-lookup"><span data-stu-id="7b78f-112">API</span></span> | <span data-ttu-id="7b78f-113">Type de limite</span><span class="sxs-lookup"><span data-stu-id="7b78f-113">Limit Type</span></span> | <span data-ttu-id="7b78f-114">Valeur de la limite</span><span class="sxs-lookup"><span data-stu-id="7b78f-114">Limit Value</span></span> | <span data-ttu-id="7b78f-115">API CasUtilisation</span><span class="sxs-lookup"><span data-stu-id="7b78f-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="7b78f-116">**TÉLÉCHARGER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="7b78f-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="7b78f-117">IP</span><span class="sxs-lookup"><span data-stu-id="7b78f-117">IP</span></span> | <span data-ttu-id="7b78f-118">1000 / minute</span><span class="sxs-lookup"><span data-stu-id="7b78f-118">1000 / minute</span></span> | <span data-ttu-id="7b78f-119">Interroger les métadonnées de package NuGet via OData de v1 `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="7b78f-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="7b78f-120">**TÉLÉCHARGER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="7b78f-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="7b78f-121">IP</span><span class="sxs-lookup"><span data-stu-id="7b78f-121">IP</span></span> | <span data-ttu-id="7b78f-122">3000 / minute</span><span class="sxs-lookup"><span data-stu-id="7b78f-122">3000 / minute</span></span> | <span data-ttu-id="7b78f-123">Rechercher des packages NuGet via le point de terminaison v1 recherche</span><span class="sxs-lookup"><span data-stu-id="7b78f-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="7b78f-124">**TÉLÉCHARGER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="7b78f-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="7b78f-125">IP</span><span class="sxs-lookup"><span data-stu-id="7b78f-125">IP</span></span> | <span data-ttu-id="7b78f-126">20000 / minute</span><span class="sxs-lookup"><span data-stu-id="7b78f-126">20000 / minute</span></span> | <span data-ttu-id="7b78f-127">Interroger les métadonnées de package NuGet via OData de v2 `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="7b78f-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="7b78f-128">**TÉLÉCHARGER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="7b78f-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="7b78f-129">IP</span><span class="sxs-lookup"><span data-stu-id="7b78f-129">IP</span></span> | <span data-ttu-id="7b78f-130">100 / minute</span><span class="sxs-lookup"><span data-stu-id="7b78f-130">100 / minute</span></span> | <span data-ttu-id="7b78f-131">Interroger le nombre de packages NuGet via OData de v2 `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="7b78f-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="7b78f-132">Package Push et de retirer de la liste</span><span class="sxs-lookup"><span data-stu-id="7b78f-132">Package Push and Unlist</span></span>

| <span data-ttu-id="7b78f-133">API</span><span class="sxs-lookup"><span data-stu-id="7b78f-133">API</span></span> | <span data-ttu-id="7b78f-134">Type de limite</span><span class="sxs-lookup"><span data-stu-id="7b78f-134">Limit Type</span></span> | <span data-ttu-id="7b78f-135">Valeur de la limite</span><span class="sxs-lookup"><span data-stu-id="7b78f-135">Limit Value</span></span> | <span data-ttu-id="7b78f-136">API CasUtilisation</span><span class="sxs-lookup"><span data-stu-id="7b78f-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="7b78f-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="7b78f-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="7b78f-138">Clé API</span><span class="sxs-lookup"><span data-stu-id="7b78f-138">API Key</span></span> | <span data-ttu-id="7b78f-139">250 / heure</span><span class="sxs-lookup"><span data-stu-id="7b78f-139">250 / hour</span></span> | <span data-ttu-id="7b78f-140">Charger un nouveau package NuGet (version) via le point de terminaison v2 push</span><span class="sxs-lookup"><span data-stu-id="7b78f-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="7b78f-141">**SUPPRIMER** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="7b78f-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="7b78f-142">Clé API</span><span class="sxs-lookup"><span data-stu-id="7b78f-142">API Key</span></span> | <span data-ttu-id="7b78f-143">250 / heure</span><span class="sxs-lookup"><span data-stu-id="7b78f-143">250 / hour</span></span> | <span data-ttu-id="7b78f-144">Retirer de la liste un package NuGet (version) via le point de terminaison v2</span><span class="sxs-lookup"><span data-stu-id="7b78f-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
