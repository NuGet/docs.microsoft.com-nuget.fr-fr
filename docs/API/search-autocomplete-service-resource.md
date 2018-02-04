---
title: La saisie semi-automatique, NuGet API | Documents Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Le service de la saisie semi-automatique search prend en charge les versions et découverte interactive de l’ID de package."
keywords: "API de la saisie semi-automatique de NuGet, ID de package NuGet recherche, ID de package de sous-chaîne"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a><span data-ttu-id="dd0c4-104">Saisie semi-automatique</span><span class="sxs-lookup"><span data-stu-id="dd0c4-104">Autocomplete</span></span>

<span data-ttu-id="dd0c4-105">Il est possible de générer un package ID et la version la saisie semi-automatique expérience à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="dd0c4-106">La ressource utilisée pour effectuer des requêtes de la saisie semi-automatique est la `SearchAutocompleteService` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="dd0c4-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="dd0c4-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="dd0c4-107">Versioning</span></span>

<span data-ttu-id="dd0c4-108">Les éléments suivants `@type` les valeurs sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="dd0c4-108">The following `@type` values are used:</span></span>

<span data-ttu-id="dd0c4-109">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="dd0c4-109">@type value</span></span>                          | <span data-ttu-id="dd0c4-110">Notes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="dd0c4-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="dd0c4-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="dd0c4-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="dd0c4-112">The initial release</span></span>
<span data-ttu-id="dd0c4-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="dd0c4-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="dd0c4-114">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="dd0c4-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="dd0c4-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="dd0c4-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="dd0c4-116">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="dd0c4-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="dd0c4-117">URL de base</span><span class="sxs-lookup"><span data-stu-id="dd0c4-117">Base URL</span></span>

<span data-ttu-id="dd0c4-118">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="dd0c4-119">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="dd0c4-120">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="dd0c4-120">HTTP Methods</span></span>

<span data-ttu-id="dd0c4-121">Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="dd0c4-122">Recherchez les ID de package</span><span class="sxs-lookup"><span data-stu-id="dd0c4-122">Search for package IDs</span></span>

<span data-ttu-id="dd0c4-123">La saisie semi-automatique la première API prend en charge la recherche d’une partie d’une chaîne d’ID de package.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="dd0c4-124">Il s’agit très lorsque vous souhaitez fournir une fonctionnalité de tampon clavier de package dans une interface utilisateur intégrée à une source de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="dd0c4-125">Un package avec uniquement les versions non listées n’apparaîtra pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="dd0c4-126">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="dd0c4-126">Request parameters</span></span>

<span data-ttu-id="dd0c4-127">Name</span><span class="sxs-lookup"><span data-stu-id="dd0c4-127">Name</span></span>        | <span data-ttu-id="dd0c4-128">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="dd0c4-128">In</span></span>     | <span data-ttu-id="dd0c4-129">Type</span><span class="sxs-lookup"><span data-stu-id="dd0c4-129">Type</span></span>    | <span data-ttu-id="dd0c4-130">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="dd0c4-130">Required</span></span> | <span data-ttu-id="dd0c4-131">Notes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="dd0c4-132">q</span><span class="sxs-lookup"><span data-stu-id="dd0c4-132">q</span></span>           | <span data-ttu-id="dd0c4-133">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-133">URL</span></span>    | <span data-ttu-id="dd0c4-134">chaîne</span><span class="sxs-lookup"><span data-stu-id="dd0c4-134">string</span></span>  | <span data-ttu-id="dd0c4-135">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-135">no</span></span>       | <span data-ttu-id="dd0c4-136">La chaîne à comparer à l’ID de package</span><span class="sxs-lookup"><span data-stu-id="dd0c4-136">The string to compare against package IDs</span></span>
<span data-ttu-id="dd0c4-137">skip</span><span class="sxs-lookup"><span data-stu-id="dd0c4-137">skip</span></span>        | <span data-ttu-id="dd0c4-138">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-138">URL</span></span>    | <span data-ttu-id="dd0c4-139">entiers</span><span class="sxs-lookup"><span data-stu-id="dd0c4-139">integer</span></span> | <span data-ttu-id="dd0c4-140">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-140">no</span></span>       | <span data-ttu-id="dd0c4-141">Le nombre de résultats à ignorer, pour la pagination</span><span class="sxs-lookup"><span data-stu-id="dd0c4-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="dd0c4-142">prendre</span><span class="sxs-lookup"><span data-stu-id="dd0c4-142">take</span></span>        | <span data-ttu-id="dd0c4-143">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-143">URL</span></span>    | <span data-ttu-id="dd0c4-144">entiers</span><span class="sxs-lookup"><span data-stu-id="dd0c4-144">integer</span></span> | <span data-ttu-id="dd0c4-145">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-145">no</span></span>       | <span data-ttu-id="dd0c4-146">Le nombre de résultats à retourner pour la pagination</span><span class="sxs-lookup"><span data-stu-id="dd0c4-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="dd0c4-147">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="dd0c4-147">prerelease</span></span>  | <span data-ttu-id="dd0c4-148">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-148">URL</span></span>    | <span data-ttu-id="dd0c4-149">boolean</span><span class="sxs-lookup"><span data-stu-id="dd0c4-149">boolean</span></span> | <span data-ttu-id="dd0c4-150">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-150">no</span></span>       | <span data-ttu-id="dd0c4-151">`true`ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="dd0c4-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="dd0c4-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="dd0c4-152">semVerLevel</span></span> | <span data-ttu-id="dd0c4-153">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-153">URL</span></span>    | <span data-ttu-id="dd0c4-154">chaîne</span><span class="sxs-lookup"><span data-stu-id="dd0c4-154">string</span></span>  | <span data-ttu-id="dd0c4-155">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-155">no</span></span>       | <span data-ttu-id="dd0c4-156">Une chaîne de version SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="dd0c4-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="dd0c4-157">La requête de la saisie semi-automatique `q` est analysé de manière définie par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="dd0c4-158">NuGet.org prend en charge l’interrogation d’origine pour le préfixe de jetons d’ID de package, qui sont des éléments de l’ID de produit par spliting par des caractères de cas et le symbole mixte.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="dd0c4-159">Le `skip` paramètre valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="dd0c4-160">Le `take` paramètre doit être un entier supérieur à zéro.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="dd0c4-161">L’implémentation du serveur peut imposer une valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="dd0c4-162">Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="dd0c4-163">Le `semVerLevel` paramètre de requête permet de choisir de [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="dd0c4-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="dd0c4-164">Si ce paramètre de requête est exclu, ID de package uniquement avec les versions compatibles de SemVer 1.0.0 seront retourné (avec la [version standard de NuGet](../reference/package-versioning.md) avertissements, telles que des chaînes de version avec 4 parties entier).</span><span class="sxs-lookup"><span data-stu-id="dd0c4-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="dd0c4-165">Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et les packages compatibles SemVer 2.0.0 seront retournés.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="dd0c4-166">Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="dd0c4-167">Réponse</span><span class="sxs-lookup"><span data-stu-id="dd0c4-167">Response</span></span>

<span data-ttu-id="dd0c4-168">La réponse est document JSON contenant jusqu'à `take` les résultats de la saisie semi-automatique.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="dd0c4-169">L’objet JSON racine a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd0c4-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="dd0c4-170">Name</span><span class="sxs-lookup"><span data-stu-id="dd0c4-170">Name</span></span>      | <span data-ttu-id="dd0c4-171">Type</span><span class="sxs-lookup"><span data-stu-id="dd0c4-171">Type</span></span>             | <span data-ttu-id="dd0c4-172">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="dd0c4-172">Required</span></span> | <span data-ttu-id="dd0c4-173">Notes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="dd0c4-174">total des accès</span><span class="sxs-lookup"><span data-stu-id="dd0c4-174">totalHits</span></span> | <span data-ttu-id="dd0c4-175">entiers</span><span class="sxs-lookup"><span data-stu-id="dd0c4-175">integer</span></span>          | <span data-ttu-id="dd0c4-176">oui</span><span class="sxs-lookup"><span data-stu-id="dd0c4-176">yes</span></span>      | <span data-ttu-id="dd0c4-177">Le nombre total de correspondances, ignorant `skip` et`take`</span><span class="sxs-lookup"><span data-stu-id="dd0c4-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="dd0c4-178">Données</span><span class="sxs-lookup"><span data-stu-id="dd0c4-178">data</span></span>      | <span data-ttu-id="dd0c4-179">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-179">array of strings</span></span> | <span data-ttu-id="dd0c4-180">oui</span><span class="sxs-lookup"><span data-stu-id="dd0c4-180">yes</span></span>      | <span data-ttu-id="dd0c4-181">Les ID correspondant à la demande de package</span><span class="sxs-lookup"><span data-stu-id="dd0c4-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="dd0c4-182">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="dd0c4-182">Sample request</span></span>

<span data-ttu-id="dd0c4-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="dd0c4-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="dd0c4-184">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="dd0c4-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="dd0c4-185">Énumérer des versions de package</span><span class="sxs-lookup"><span data-stu-id="dd0c4-185">Enumerate package versions</span></span>

<span data-ttu-id="dd0c4-186">Une fois qu’un ID de package a été détecté à l’aide de l’API précédente, un client peut utiliser l’API de la saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="dd0c4-187">Une version de package qui n’est pas spécifiée n’apparaîtra pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="dd0c4-188">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="dd0c4-188">Request parameters</span></span>

<span data-ttu-id="dd0c4-189">Name</span><span class="sxs-lookup"><span data-stu-id="dd0c4-189">Name</span></span>        | <span data-ttu-id="dd0c4-190">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="dd0c4-190">In</span></span>     | <span data-ttu-id="dd0c4-191">Type</span><span class="sxs-lookup"><span data-stu-id="dd0c4-191">Type</span></span>    | <span data-ttu-id="dd0c4-192">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="dd0c4-192">Required</span></span> | <span data-ttu-id="dd0c4-193">Notes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="dd0c4-194">ID</span><span class="sxs-lookup"><span data-stu-id="dd0c4-194">id</span></span>          | <span data-ttu-id="dd0c4-195">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-195">URL</span></span>    | <span data-ttu-id="dd0c4-196">chaîne</span><span class="sxs-lookup"><span data-stu-id="dd0c4-196">string</span></span>  | <span data-ttu-id="dd0c4-197">oui</span><span class="sxs-lookup"><span data-stu-id="dd0c4-197">yes</span></span>      | <span data-ttu-id="dd0c4-198">Pour récupérer des versions pour l’ID de package</span><span class="sxs-lookup"><span data-stu-id="dd0c4-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="dd0c4-199">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="dd0c4-199">prerelease</span></span>  | <span data-ttu-id="dd0c4-200">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-200">URL</span></span>    | <span data-ttu-id="dd0c4-201">boolean</span><span class="sxs-lookup"><span data-stu-id="dd0c4-201">boolean</span></span> | <span data-ttu-id="dd0c4-202">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-202">no</span></span>       | <span data-ttu-id="dd0c4-203">`true`ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="dd0c4-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="dd0c4-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="dd0c4-204">semVerLevel</span></span> | <span data-ttu-id="dd0c4-205">URL</span><span class="sxs-lookup"><span data-stu-id="dd0c4-205">URL</span></span>    | <span data-ttu-id="dd0c4-206">chaîne</span><span class="sxs-lookup"><span data-stu-id="dd0c4-206">string</span></span>  | <span data-ttu-id="dd0c4-207">Non</span><span class="sxs-lookup"><span data-stu-id="dd0c4-207">no</span></span>       | <span data-ttu-id="dd0c4-208">Une chaîne de version SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="dd0c4-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="dd0c4-209">Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="dd0c4-210">Le `semVerLevel` paramètre de requête permet de participer à des packages de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="dd0c4-211">Si ce paramètre de requête est exclu, seules les versions SemVer 1.0.0 seront retournées.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="dd0c4-212">Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et SemVer 2.0.0 versions seront retournées.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="dd0c4-213">Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="dd0c4-214">Réponse</span><span class="sxs-lookup"><span data-stu-id="dd0c4-214">Response</span></span>

<span data-ttu-id="dd0c4-215">La réponse est un document JSON qui contient toutes les versions de package de l’ID de package fourni, le filtrage par les paramètres de requête donnée.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="dd0c4-216">L’objet JSON racine a la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="dd0c4-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="dd0c4-217">Name</span><span class="sxs-lookup"><span data-stu-id="dd0c4-217">Name</span></span>      | <span data-ttu-id="dd0c4-218">Type</span><span class="sxs-lookup"><span data-stu-id="dd0c4-218">Type</span></span>             | <span data-ttu-id="dd0c4-219">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="dd0c4-219">Required</span></span> | <span data-ttu-id="dd0c4-220">Notes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="dd0c4-221">Données</span><span class="sxs-lookup"><span data-stu-id="dd0c4-221">data</span></span>      | <span data-ttu-id="dd0c4-222">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="dd0c4-222">array of strings</span></span> | <span data-ttu-id="dd0c4-223">oui</span><span class="sxs-lookup"><span data-stu-id="dd0c4-223">yes</span></span>      | <span data-ttu-id="dd0c4-224">Les versions de package correspondance à la demande</span><span class="sxs-lookup"><span data-stu-id="dd0c4-224">The package versions matched by the request</span></span>

<span data-ttu-id="dd0c4-225">Les versions de package dans le `data` tableau peut contenir des métadonnées de génération SemVer 2.0.0 (par exemple, `1.0.0+metadata`) si le `semVerLevel=2.0.0` a été fourni dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="dd0c4-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="dd0c4-226">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="dd0c4-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="dd0c4-227">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="dd0c4-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
