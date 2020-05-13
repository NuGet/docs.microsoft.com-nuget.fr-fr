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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367932"
---
# <a name="rate-limits"></a><span data-ttu-id="c8483-103">Limites du débit</span><span class="sxs-lookup"><span data-stu-id="c8483-103">Rate Limits</span></span>

<span data-ttu-id="c8483-104">L’API NuGet.org applique la limitation du débit pour empêcher tout abus.</span><span class="sxs-lookup"><span data-stu-id="c8483-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c8483-105">Les demandes qui dépassent la limite de débit retournent l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="c8483-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c8483-106">En plus de la limitation des demandes à l’aide de limites de débit, certaines API appliquent également le quota.</span><span class="sxs-lookup"><span data-stu-id="c8483-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="c8483-107">Les demandes qui dépassent le quota renvoient l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="c8483-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="c8483-108">Les tableaux suivants répertorient les limites de taux de transfert pour l’API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c8483-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c8483-109">Recherche de packages</span><span class="sxs-lookup"><span data-stu-id="c8483-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="c8483-110">Nous vous recommandons d’utiliser les [API de recherche v3](search-query-service-resource.md) de NuGet. org, car elles ne sont pas limitées au tarif actuellement.</span><span class="sxs-lookup"><span data-stu-id="c8483-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="c8483-111">Pour les API de recherche v1 et v2, les limites suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="c8483-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="c8483-112">API</span><span class="sxs-lookup"><span data-stu-id="c8483-112">API</span></span> | <span data-ttu-id="c8483-113">Type de limite</span><span class="sxs-lookup"><span data-stu-id="c8483-113">Limit Type</span></span> | <span data-ttu-id="c8483-114">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="c8483-114">Limit Value</span></span> | <span data-ttu-id="c8483-115">Cas d’usage d’API</span><span class="sxs-lookup"><span data-stu-id="c8483-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c8483-116">En **savoir** plus`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c8483-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c8483-117">IP</span><span class="sxs-lookup"><span data-stu-id="c8483-117">IP</span></span> | <span data-ttu-id="c8483-118">1000/minute</span><span class="sxs-lookup"><span data-stu-id="c8483-118">1000 / minute</span></span> | <span data-ttu-id="c8483-119">Interroger les métadonnées du package NuGet via la collection OData v1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="c8483-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c8483-120">En **savoir** plus`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c8483-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c8483-121">IP</span><span class="sxs-lookup"><span data-stu-id="c8483-121">IP</span></span> | <span data-ttu-id="c8483-122">3000/minute</span><span class="sxs-lookup"><span data-stu-id="c8483-122">3000 / minute</span></span> | <span data-ttu-id="c8483-123">Rechercher des packages NuGet via le point de terminaison de recherche v1</span><span class="sxs-lookup"><span data-stu-id="c8483-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c8483-124">En **savoir** plus`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c8483-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c8483-125">IP</span><span class="sxs-lookup"><span data-stu-id="c8483-125">IP</span></span> | <span data-ttu-id="c8483-126">20000/minute</span><span class="sxs-lookup"><span data-stu-id="c8483-126">20000 / minute</span></span> | <span data-ttu-id="c8483-127">Interroger les métadonnées du package NuGet via la collection OData v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="c8483-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c8483-128">En **savoir** plus`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c8483-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c8483-129">IP</span><span class="sxs-lookup"><span data-stu-id="c8483-129">IP</span></span> | <span data-ttu-id="c8483-130">100/minute</span><span class="sxs-lookup"><span data-stu-id="c8483-130">100 / minute</span></span> | <span data-ttu-id="c8483-131">Interroger le nombre de packages NuGet via la collection OData v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="c8483-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c8483-132">Push et Unlist des packages</span><span class="sxs-lookup"><span data-stu-id="c8483-132">Package Push and Unlist</span></span>

| <span data-ttu-id="c8483-133">API</span><span class="sxs-lookup"><span data-stu-id="c8483-133">API</span></span> | <span data-ttu-id="c8483-134">Type de limite</span><span class="sxs-lookup"><span data-stu-id="c8483-134">Limit Type</span></span> | <span data-ttu-id="c8483-135">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="c8483-135">Limit Value</span></span> | <span data-ttu-id="c8483-136">Cas d’usage d’API</span><span class="sxs-lookup"><span data-stu-id="c8483-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c8483-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c8483-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c8483-138">Clé de l’API</span><span class="sxs-lookup"><span data-stu-id="c8483-138">API Key</span></span> | <span data-ttu-id="c8483-139">350/heure</span><span class="sxs-lookup"><span data-stu-id="c8483-139">350 / hour</span></span> | <span data-ttu-id="c8483-140">Télécharger un nouveau package NuGet (version) via un point de terminaison Push v2</span><span class="sxs-lookup"><span data-stu-id="c8483-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c8483-141">**Supprimer**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c8483-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c8483-142">Clé de l’API</span><span class="sxs-lookup"><span data-stu-id="c8483-142">API Key</span></span> | <span data-ttu-id="c8483-143">250/heure</span><span class="sxs-lookup"><span data-stu-id="c8483-143">250 / hour</span></span> | <span data-ttu-id="c8483-144">Délister un package NuGet (version) via un point de terminaison v2</span><span class="sxs-lookup"><span data-stu-id="c8483-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="c8483-145">affichages de pages de site Web nuget.org</span><span class="sxs-lookup"><span data-stu-id="c8483-145">nuget.org website page views</span></span>

<span data-ttu-id="c8483-146">Si vous accédez aux pages Web nuget.org par programme, envisagez d’examiner nos [API V3](overview.md)documentées.</span><span class="sxs-lookup"><span data-stu-id="c8483-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="c8483-147">Ces points de terminaison permettent un accès plus simple aux métadonnées et au contenu des packages.</span><span class="sxs-lookup"><span data-stu-id="c8483-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="c8483-148">L’API V3 offre une meilleure disponibilité et offre des performances supérieures à celles des pages Web de la galerie NuGet, qui sont conçues pour l’interaction du navigateur Web.</span><span class="sxs-lookup"><span data-stu-id="c8483-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="c8483-149">API</span><span class="sxs-lookup"><span data-stu-id="c8483-149">API</span></span> | <span data-ttu-id="c8483-150">Type de limite</span><span class="sxs-lookup"><span data-stu-id="c8483-150">Limit Type</span></span> | <span data-ttu-id="c8483-151">Valeur limite</span><span class="sxs-lookup"><span data-stu-id="c8483-151">Limit Value</span></span> | <span data-ttu-id="c8483-152">Cas d’usage d’API</span><span class="sxs-lookup"><span data-stu-id="c8483-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c8483-153">En **savoir** plus`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c8483-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="c8483-154">IP</span><span class="sxs-lookup"><span data-stu-id="c8483-154">IP</span></span> | <span data-ttu-id="c8483-155">50/minute</span><span class="sxs-lookup"><span data-stu-id="c8483-155">50 / minute</span></span> | <span data-ttu-id="c8483-156">Affichez la page des détails du package (version).</span><span class="sxs-lookup"><span data-stu-id="c8483-156">Display package (version) details page.</span></span> 
