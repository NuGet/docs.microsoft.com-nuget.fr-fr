---
title: Limites du taux de transfert, API NuGet
description: Les API NuGet auront des limites de débit imposées pour empêcher tout abus.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813193"
---
# <a name="rate-limits"></a><span data-ttu-id="51ce3-103">Limites du débit</span><span class="sxs-lookup"><span data-stu-id="51ce3-103">Rate Limits</span></span>

<span data-ttu-id="51ce3-104">L’API NuGet.org applique la limitation du débit pour empêcher tout abus.</span><span class="sxs-lookup"><span data-stu-id="51ce3-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="51ce3-105">Les demandes qui dépassent la limite de débit retournent l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="51ce3-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="51ce3-106">En plus de la limitation des demandes à l’aide de limites de débit, certaines API appliquent également le quota.</span><span class="sxs-lookup"><span data-stu-id="51ce3-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="51ce3-107">Les demandes qui dépassent le quota renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="51ce3-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="51ce3-108">Les tableaux suivants répertorient les limites de taux de transfert pour l’API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="51ce3-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="51ce3-109">Recherche de packages</span><span class="sxs-lookup"><span data-stu-id="51ce3-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="51ce3-110">Nous vous recommandons d’utiliser les [API de recherche v3](search-query-service-resource.md) de NuGet. org, car elles ne sont pas limitées au tarif actuellement.</span><span class="sxs-lookup"><span data-stu-id="51ce3-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="51ce3-111">Pour les API de recherche v1 et v2, les limites suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="51ce3-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="51ce3-112">API</span><span class="sxs-lookup"><span data-stu-id="51ce3-112">API</span></span> | <span data-ttu-id="51ce3-113">Type de limite</span><span class="sxs-lookup"><span data-stu-id="51ce3-113">Limit Type</span></span> | <span data-ttu-id="51ce3-114">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="51ce3-114">Limit Value</span></span> | <span data-ttu-id="51ce3-115">UseCase d’API</span><span class="sxs-lookup"><span data-stu-id="51ce3-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="51ce3-116">**Recevoir** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="51ce3-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="51ce3-117">IP</span><span class="sxs-lookup"><span data-stu-id="51ce3-117">IP</span></span> | <span data-ttu-id="51ce3-118">1000/minute</span><span class="sxs-lookup"><span data-stu-id="51ce3-118">1000 / minute</span></span> | <span data-ttu-id="51ce3-119">Interroger les métadonnées du package NuGet via v1 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="51ce3-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="51ce3-120">**Recevoir** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="51ce3-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="51ce3-121">IP</span><span class="sxs-lookup"><span data-stu-id="51ce3-121">IP</span></span> | <span data-ttu-id="51ce3-122">3000/minute</span><span class="sxs-lookup"><span data-stu-id="51ce3-122">3000 / minute</span></span> | <span data-ttu-id="51ce3-123">Rechercher des packages NuGet via le point de terminaison de recherche v1</span><span class="sxs-lookup"><span data-stu-id="51ce3-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="51ce3-124">**Recevoir** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="51ce3-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="51ce3-125">IP</span><span class="sxs-lookup"><span data-stu-id="51ce3-125">IP</span></span> | <span data-ttu-id="51ce3-126">20000/minute</span><span class="sxs-lookup"><span data-stu-id="51ce3-126">20000 / minute</span></span> | <span data-ttu-id="51ce3-127">Interroger les métadonnées du package NuGet via v2 OData `Packages` collection</span><span class="sxs-lookup"><span data-stu-id="51ce3-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="51ce3-128">**Recevoir** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="51ce3-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="51ce3-129">IP</span><span class="sxs-lookup"><span data-stu-id="51ce3-129">IP</span></span> | <span data-ttu-id="51ce3-130">100/minute</span><span class="sxs-lookup"><span data-stu-id="51ce3-130">100 / minute</span></span> | <span data-ttu-id="51ce3-131">Interroger le nombre de packages NuGet via la collecte de `Packages` OData v2</span><span class="sxs-lookup"><span data-stu-id="51ce3-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="51ce3-132">Push et Unlist des packages</span><span class="sxs-lookup"><span data-stu-id="51ce3-132">Package Push and Unlist</span></span>

| <span data-ttu-id="51ce3-133">API</span><span class="sxs-lookup"><span data-stu-id="51ce3-133">API</span></span> | <span data-ttu-id="51ce3-134">Type de limite</span><span class="sxs-lookup"><span data-stu-id="51ce3-134">Limit Type</span></span> | <span data-ttu-id="51ce3-135">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="51ce3-135">Limit Value</span></span> | <span data-ttu-id="51ce3-136">UseCase d’API</span><span class="sxs-lookup"><span data-stu-id="51ce3-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="51ce3-137">**Placer** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="51ce3-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="51ce3-138">Clé API</span><span class="sxs-lookup"><span data-stu-id="51ce3-138">API Key</span></span> | <span data-ttu-id="51ce3-139">350/heure</span><span class="sxs-lookup"><span data-stu-id="51ce3-139">350 / hour</span></span> | <span data-ttu-id="51ce3-140">Télécharger un nouveau package NuGet (version) via un point de terminaison Push v2</span><span class="sxs-lookup"><span data-stu-id="51ce3-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="51ce3-141">**Supprimer** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="51ce3-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="51ce3-142">Clé API</span><span class="sxs-lookup"><span data-stu-id="51ce3-142">API Key</span></span> | <span data-ttu-id="51ce3-143">250/heure</span><span class="sxs-lookup"><span data-stu-id="51ce3-143">250 / hour</span></span> | <span data-ttu-id="51ce3-144">Délister un package NuGet (version) via un point de terminaison v2</span><span class="sxs-lookup"><span data-stu-id="51ce3-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
