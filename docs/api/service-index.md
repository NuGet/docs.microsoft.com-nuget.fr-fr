---
title: Index de service, API NuGet
description: L’index de service est le point d’entrée de l’API HTTP NuGet et énumère les fonctionnalités du serveur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775357"
---
# <a name="service-index"></a><span data-ttu-id="9159e-103">Index de service</span><span class="sxs-lookup"><span data-stu-id="9159e-103">Service index</span></span>

<span data-ttu-id="9159e-104">L’index de service est un document JSON qui est le point d’entrée d’une source de package NuGet et permet à une implémentation cliente de découvrir les fonctionnalités de la source du package.</span><span class="sxs-lookup"><span data-stu-id="9159e-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="9159e-105">L’index de service est un objet JSON avec deux propriétés obligatoires : `version` (la version de schéma de l’index de service) et `resources`  (les points de terminaison ou les fonctionnalités de la source du package).</span><span class="sxs-lookup"><span data-stu-id="9159e-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="9159e-106">l’index de service de NuGet. org se trouve à l’emplacement `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="9159e-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="9159e-107">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="9159e-107">Versioning</span></span>

<span data-ttu-id="9159e-108">La `version` valeur est une chaîne de version analysable SemVer 2.0.0 qui indique la version de schéma de l’index de service.</span><span class="sxs-lookup"><span data-stu-id="9159e-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="9159e-109">L’API impose que la chaîne de version ait un numéro de version principale de `3` .</span><span class="sxs-lookup"><span data-stu-id="9159e-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="9159e-110">À mesure que des modifications sans rupture sont apportées au schéma d’index de service, la version mineure de la chaîne de version est augmentée.</span><span class="sxs-lookup"><span data-stu-id="9159e-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="9159e-111">Chaque ressource de l’index de service est gérée indépendamment de la version du schéma d’index de service.</span><span class="sxs-lookup"><span data-stu-id="9159e-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="9159e-112">La version du schéma actuel est `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="9159e-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="9159e-113">La `3.0.0` version est fonctionnellement équivalente à l’ancienne `3.0.0-beta.1` version, mais elle doit être préférée, car elle communique plus clairement le schéma stable et défini.</span><span class="sxs-lookup"><span data-stu-id="9159e-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9159e-114">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="9159e-114">HTTP methods</span></span>

<span data-ttu-id="9159e-115">L’index de service est accessible à l’aide des méthodes HTTP `GET` et `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="9159e-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="9159e-116">Ressources</span><span class="sxs-lookup"><span data-stu-id="9159e-116">Resources</span></span>

<span data-ttu-id="9159e-117">La `resources` propriété contient un tableau de ressources prises en charge par cette source de package.</span><span class="sxs-lookup"><span data-stu-id="9159e-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="9159e-118">Ressource</span><span class="sxs-lookup"><span data-stu-id="9159e-118">Resource</span></span>

<span data-ttu-id="9159e-119">Une ressource est un objet dans le `resources` tableau.</span><span class="sxs-lookup"><span data-stu-id="9159e-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="9159e-120">Il représente une fonctionnalité avec version d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="9159e-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="9159e-121">Une ressource a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="9159e-121">A resource has the following properties:</span></span>

<span data-ttu-id="9159e-122">Nom</span><span class="sxs-lookup"><span data-stu-id="9159e-122">Name</span></span>          | <span data-ttu-id="9159e-123">Type</span><span class="sxs-lookup"><span data-stu-id="9159e-123">Type</span></span>   | <span data-ttu-id="9159e-124">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9159e-124">Required</span></span> | <span data-ttu-id="9159e-125">Notes</span><span class="sxs-lookup"><span data-stu-id="9159e-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="9159e-126">string</span><span class="sxs-lookup"><span data-stu-id="9159e-126">string</span></span> | <span data-ttu-id="9159e-127">Oui</span><span class="sxs-lookup"><span data-stu-id="9159e-127">yes</span></span>      | <span data-ttu-id="9159e-128">URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="9159e-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="9159e-129">string</span><span class="sxs-lookup"><span data-stu-id="9159e-129">string</span></span> | <span data-ttu-id="9159e-130">Oui</span><span class="sxs-lookup"><span data-stu-id="9159e-130">yes</span></span>      | <span data-ttu-id="9159e-131">Constante de chaîne représentant le type de ressource</span><span class="sxs-lookup"><span data-stu-id="9159e-131">A string constant representing the resource type</span></span>
<span data-ttu-id="9159e-132">comment</span><span class="sxs-lookup"><span data-stu-id="9159e-132">comment</span></span>       | <span data-ttu-id="9159e-133">string</span><span class="sxs-lookup"><span data-stu-id="9159e-133">string</span></span> | <span data-ttu-id="9159e-134">non</span><span class="sxs-lookup"><span data-stu-id="9159e-134">no</span></span>       | <span data-ttu-id="9159e-135">Description lisible par l’utilisateur de la ressource</span><span class="sxs-lookup"><span data-stu-id="9159e-135">A human readable description of the resource</span></span>

<span data-ttu-id="9159e-136">`@id`Est une URL qui doit être absolue et doit avoir le schéma http ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9159e-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="9159e-137">`@type`Est utilisé pour identifier le protocole spécifique à utiliser lors de l’interaction avec la ressource.</span><span class="sxs-lookup"><span data-stu-id="9159e-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="9159e-138">Le type de la ressource est une chaîne opaque mais a généralement le format :</span><span class="sxs-lookup"><span data-stu-id="9159e-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="9159e-139">Les clients sont censés coder en dur les `@type` valeurs qu’ils comprennent et les Rechercher dans l’index de service d’une source de package.</span><span class="sxs-lookup"><span data-stu-id="9159e-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="9159e-140">Les valeurs exactes `@type` utilisées aujourd’hui sont énumérées sur les documents de référence de ressource individuels répertoriés dans la [vue d’ensemble](overview.md#resources-and-schema)de l’API.</span><span class="sxs-lookup"><span data-stu-id="9159e-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="9159e-141">Dans le cadre de cette documentation, la documentation sur les différentes ressources sera essentiellement regroupée par le `{RESOURCE_NAME}` trouvé dans l’index de service, ce qui est analogue au regroupement par scénario.</span><span class="sxs-lookup"><span data-stu-id="9159e-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="9159e-142">Il n’est pas obligatoire que chaque ressource dispose d’un ou d’un unique `@id` `@type` .</span><span class="sxs-lookup"><span data-stu-id="9159e-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="9159e-143">C’est à l’implémentation cliente de déterminer la ressource à préférer à une autre.</span><span class="sxs-lookup"><span data-stu-id="9159e-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="9159e-144">Une implémentation possible est que les ressources de même ou compatibles `@type` peuvent être utilisées en mode tourniquet (Round Robin) en cas d’échec de connexion ou d’erreur de serveur.</span><span class="sxs-lookup"><span data-stu-id="9159e-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9159e-145">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="9159e-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="9159e-146">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="9159e-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
