---
title: Index de service, API NuGet
description: L’index de service est le point d’entrée de l’API HTTP de NuGet et énumère les fonctionnalités du serveur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 478b74f98caafdc7c6b69423b9f9d72890c8d7cb
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545255"
---
# <a name="service-index"></a><span data-ttu-id="27ac0-103">Index de service</span><span class="sxs-lookup"><span data-stu-id="27ac0-103">Service index</span></span>

<span data-ttu-id="27ac0-104">L’index de service est un document JSON qui est le point d’entrée pour une source de package NuGet et permet une implémentation de client découvrir les fonctionnalités de la source du package.</span><span class="sxs-lookup"><span data-stu-id="27ac0-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="27ac0-105">L’index de service est un objet JSON avec deux propriétés requises : `version` (la version de schéma de l’index de service) et `resources` (les points de terminaison ou les capacités de la source du package).</span><span class="sxs-lookup"><span data-stu-id="27ac0-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="27ac0-106">index de service de NuGet.org se trouve dans `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="27ac0-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="27ac0-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="27ac0-107">Versioning</span></span>

<span data-ttu-id="27ac0-108">Le `version` valeur est une chaîne de version analysable SemVer 2.0.0 qui indique la version du schéma de l’index de service.</span><span class="sxs-lookup"><span data-stu-id="27ac0-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="27ac0-109">L’API impose que la chaîne de version a un numéro de version principale de `3`.</span><span class="sxs-lookup"><span data-stu-id="27ac0-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="27ac0-110">Quand des modifications sans rupture sont apportées au schéma d’index de service, version mineure de la chaîne de version sera augmentée.</span><span class="sxs-lookup"><span data-stu-id="27ac0-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="27ac0-111">Chaque ressource dans l’index de service est gérée indépendamment de la version de schéma d’index service.</span><span class="sxs-lookup"><span data-stu-id="27ac0-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="27ac0-112">La version de schéma actuelle est `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="27ac0-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="27ac0-113">Le `3.0.0` version est fonctionnellement équivalente à l’ancien `3.0.0-beta.1` version mais il est préférable qu’il communique plus clairement le schéma stable, défini.</span><span class="sxs-lookup"><span data-stu-id="27ac0-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="27ac0-114">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="27ac0-114">HTTP methods</span></span>

<span data-ttu-id="27ac0-115">L’index de service est accessible à l’aide de méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="27ac0-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="27ac0-116">Ressources</span><span class="sxs-lookup"><span data-stu-id="27ac0-116">Resources</span></span>

<span data-ttu-id="27ac0-117">Le `resources` propriété contient un ensemble de ressources pris en charge par cette source de package.</span><span class="sxs-lookup"><span data-stu-id="27ac0-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="27ac0-118">Ressource</span><span class="sxs-lookup"><span data-stu-id="27ac0-118">Resource</span></span>

<span data-ttu-id="27ac0-119">Une ressource est un objet dans le `resources` tableau.</span><span class="sxs-lookup"><span data-stu-id="27ac0-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="27ac0-120">Il représente une fonctionnalité avec contrôle de version d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="27ac0-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="27ac0-121">Une ressource a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="27ac0-121">A resource has the following properties:</span></span>

<span data-ttu-id="27ac0-122">Name</span><span class="sxs-lookup"><span data-stu-id="27ac0-122">Name</span></span>          | <span data-ttu-id="27ac0-123">Type</span><span class="sxs-lookup"><span data-stu-id="27ac0-123">Type</span></span>   | <span data-ttu-id="27ac0-124">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="27ac0-124">Required</span></span> | <span data-ttu-id="27ac0-125">Notes</span><span class="sxs-lookup"><span data-stu-id="27ac0-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="27ac0-126">chaîne</span><span class="sxs-lookup"><span data-stu-id="27ac0-126">string</span></span> | <span data-ttu-id="27ac0-127">oui</span><span class="sxs-lookup"><span data-stu-id="27ac0-127">yes</span></span>      | <span data-ttu-id="27ac0-128">L’URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="27ac0-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="27ac0-129">chaîne</span><span class="sxs-lookup"><span data-stu-id="27ac0-129">string</span></span> | <span data-ttu-id="27ac0-130">oui</span><span class="sxs-lookup"><span data-stu-id="27ac0-130">yes</span></span>      | <span data-ttu-id="27ac0-131">Constante de chaîne représentant le type de ressource</span><span class="sxs-lookup"><span data-stu-id="27ac0-131">A string constant representing the resource type</span></span>
<span data-ttu-id="27ac0-132">commentaire</span><span class="sxs-lookup"><span data-stu-id="27ac0-132">comment</span></span>       | <span data-ttu-id="27ac0-133">chaîne</span><span class="sxs-lookup"><span data-stu-id="27ac0-133">string</span></span> | <span data-ttu-id="27ac0-134">Non</span><span class="sxs-lookup"><span data-stu-id="27ac0-134">no</span></span>       | <span data-ttu-id="27ac0-135">Description explicite de la ressource</span><span class="sxs-lookup"><span data-stu-id="27ac0-135">A human readable description of the resource</span></span>

<span data-ttu-id="27ac0-136">Le `@id` est une URL qui doit être absolu et doit avoir le schéma HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="27ac0-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="27ac0-137">Le `@type` est utilisé pour identifier le protocole spécifique à utiliser lors de l’interaction avec les ressources.</span><span class="sxs-lookup"><span data-stu-id="27ac0-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="27ac0-138">Le type de la ressource est une chaîne opaque, mais est généralement au format :</span><span class="sxs-lookup"><span data-stu-id="27ac0-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="27ac0-139">Les clients sont censés coder en dur le `@type` valeurs qu’ils comprennent et les consulter dans l’index de service d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="27ac0-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="27ac0-140">Exactement `@type` valeurs utilisés aujourd'hui sont énumérées sur les documents de référence de ressource individuelle répertoriées dans le [vue d’ensemble de l’API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="27ac0-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="27ac0-141">Pour des raisons de cette documentation, la documentation sur les différentes ressources est essentiellement regroupée par le `{RESOURCE_NAME}` trouvé dans l’index de service qui est analogue à un regroupement par scénario.</span><span class="sxs-lookup"><span data-stu-id="27ac0-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="27ac0-142">Il n’est pas nécessaire que chaque ressource a une valeur unique `@id` ou `@type`.</span><span class="sxs-lookup"><span data-stu-id="27ac0-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="27ac0-143">C’est à l’implémentation de client pour déterminer quelle ressource préférez plutôt qu’un autre.</span><span class="sxs-lookup"><span data-stu-id="27ac0-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="27ac0-144">Une implémentation possible est que les ressources d’identiques ou compatibles `@type` peut être utilisé de manière alternée en cas d’erreur de serveur ou d’échec de connexion.</span><span class="sxs-lookup"><span data-stu-id="27ac0-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="27ac0-145">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="27ac0-145">Sample request</span></span>

<span data-ttu-id="27ac0-146">TÉLÉCHARGER https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="27ac0-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="27ac0-147">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="27ac0-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
