---
title: Saisie semi-automatique, NuGet API
description: Le service de la saisie semi-automatique search prend en charge les versions et découverte interactive de l’ID de package.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822134"
---
# <a name="autocomplete"></a><span data-ttu-id="360ca-103">Saisie semi-automatique</span><span class="sxs-lookup"><span data-stu-id="360ca-103">Autocomplete</span></span>

<span data-ttu-id="360ca-104">Il est possible de générer un package ID et la version la saisie semi-automatique expérience à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="360ca-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="360ca-105">La ressource utilisée pour effectuer des requêtes de la saisie semi-automatique est la `SearchAutocompleteService` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="360ca-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="360ca-106">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="360ca-106">Versioning</span></span>

<span data-ttu-id="360ca-107">Les éléments suivants `@type` les valeurs sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="360ca-107">The following `@type` values are used:</span></span>

<span data-ttu-id="360ca-108">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="360ca-108">@type value</span></span>                          | <span data-ttu-id="360ca-109">Notes</span><span class="sxs-lookup"><span data-stu-id="360ca-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="360ca-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="360ca-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="360ca-111">La version initiale</span><span class="sxs-lookup"><span data-stu-id="360ca-111">The initial release</span></span>
<span data-ttu-id="360ca-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="360ca-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="360ca-113">Alias de `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="360ca-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="360ca-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="360ca-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="360ca-115">Alias de `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="360ca-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="360ca-116">URL de base</span><span class="sxs-lookup"><span data-stu-id="360ca-116">Base URL</span></span>

<span data-ttu-id="360ca-117">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.</span><span class="sxs-lookup"><span data-stu-id="360ca-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="360ca-118">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="360ca-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="360ca-119">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="360ca-119">HTTP Methods</span></span>

<span data-ttu-id="360ca-120">Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="360ca-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="360ca-121">Recherchez les ID de package</span><span class="sxs-lookup"><span data-stu-id="360ca-121">Search for package IDs</span></span>

<span data-ttu-id="360ca-122">La saisie semi-automatique la première API prend en charge la recherche d’une partie d’une chaîne d’ID de package.</span><span class="sxs-lookup"><span data-stu-id="360ca-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="360ca-123">Il s’agit très lorsque vous souhaitez fournir une fonctionnalité de tampon clavier de package dans une interface utilisateur intégrée à une source de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="360ca-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="360ca-124">Un package avec uniquement les versions non listées n’apparaîtra pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="360ca-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="360ca-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="360ca-125">Request parameters</span></span>

<span data-ttu-id="360ca-126">Name</span><span class="sxs-lookup"><span data-stu-id="360ca-126">Name</span></span>        | <span data-ttu-id="360ca-127">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="360ca-127">In</span></span>     | <span data-ttu-id="360ca-128">Type</span><span class="sxs-lookup"><span data-stu-id="360ca-128">Type</span></span>    | <span data-ttu-id="360ca-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="360ca-129">Required</span></span> | <span data-ttu-id="360ca-130">Notes</span><span class="sxs-lookup"><span data-stu-id="360ca-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="360ca-131">q</span><span class="sxs-lookup"><span data-stu-id="360ca-131">q</span></span>           | <span data-ttu-id="360ca-132">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-132">URL</span></span>    | <span data-ttu-id="360ca-133">chaîne</span><span class="sxs-lookup"><span data-stu-id="360ca-133">string</span></span>  | <span data-ttu-id="360ca-134">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-134">no</span></span>       | <span data-ttu-id="360ca-135">La chaîne à comparer à l’ID de package</span><span class="sxs-lookup"><span data-stu-id="360ca-135">The string to compare against package IDs</span></span>
<span data-ttu-id="360ca-136">skip</span><span class="sxs-lookup"><span data-stu-id="360ca-136">skip</span></span>        | <span data-ttu-id="360ca-137">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-137">URL</span></span>    | <span data-ttu-id="360ca-138">entiers</span><span class="sxs-lookup"><span data-stu-id="360ca-138">integer</span></span> | <span data-ttu-id="360ca-139">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-139">no</span></span>       | <span data-ttu-id="360ca-140">Le nombre de résultats à ignorer, pour la pagination</span><span class="sxs-lookup"><span data-stu-id="360ca-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="360ca-141">prendre</span><span class="sxs-lookup"><span data-stu-id="360ca-141">take</span></span>        | <span data-ttu-id="360ca-142">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-142">URL</span></span>    | <span data-ttu-id="360ca-143">entiers</span><span class="sxs-lookup"><span data-stu-id="360ca-143">integer</span></span> | <span data-ttu-id="360ca-144">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-144">no</span></span>       | <span data-ttu-id="360ca-145">Le nombre de résultats à retourner pour la pagination</span><span class="sxs-lookup"><span data-stu-id="360ca-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="360ca-146">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="360ca-146">prerelease</span></span>  | <span data-ttu-id="360ca-147">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-147">URL</span></span>    | <span data-ttu-id="360ca-148">boolean</span><span class="sxs-lookup"><span data-stu-id="360ca-148">boolean</span></span> | <span data-ttu-id="360ca-149">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-149">no</span></span>       | <span data-ttu-id="360ca-150">`true` ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="360ca-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="360ca-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="360ca-151">semVerLevel</span></span> | <span data-ttu-id="360ca-152">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-152">URL</span></span>    | <span data-ttu-id="360ca-153">chaîne</span><span class="sxs-lookup"><span data-stu-id="360ca-153">string</span></span>  | <span data-ttu-id="360ca-154">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-154">no</span></span>       | <span data-ttu-id="360ca-155">Une chaîne de version SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="360ca-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="360ca-156">La requête de la saisie semi-automatique `q` est analysé de manière définie par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="360ca-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="360ca-157">NuGet.org prend en charge l’interrogation d’origine pour le préfixe de jetons d’ID de package, qui sont des éléments de l’ID de produit par spliting par des caractères de cas et le symbole mixte.</span><span class="sxs-lookup"><span data-stu-id="360ca-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="360ca-158">Le `skip` paramètre valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="360ca-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="360ca-159">Le `take` paramètre doit être un entier supérieur à zéro.</span><span class="sxs-lookup"><span data-stu-id="360ca-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="360ca-160">L’implémentation du serveur peut imposer une valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="360ca-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="360ca-161">Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.</span><span class="sxs-lookup"><span data-stu-id="360ca-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="360ca-162">Le `semVerLevel` paramètre de requête permet de choisir de [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="360ca-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="360ca-163">Si ce paramètre de requête est exclu, ID de package uniquement avec les versions compatibles de SemVer 1.0.0 seront retourné (avec la [version standard de NuGet](../reference/package-versioning.md) avertissements, telles que des chaînes de version avec 4 parties entier).</span><span class="sxs-lookup"><span data-stu-id="360ca-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="360ca-164">Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et les packages compatibles SemVer 2.0.0 seront retournés.</span><span class="sxs-lookup"><span data-stu-id="360ca-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="360ca-165">Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="360ca-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="360ca-166">Réponse</span><span class="sxs-lookup"><span data-stu-id="360ca-166">Response</span></span>

<span data-ttu-id="360ca-167">La réponse est document JSON contenant jusqu'à `take` les résultats de la saisie semi-automatique.</span><span class="sxs-lookup"><span data-stu-id="360ca-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="360ca-168">L’objet JSON racine a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="360ca-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="360ca-169">Name</span><span class="sxs-lookup"><span data-stu-id="360ca-169">Name</span></span>      | <span data-ttu-id="360ca-170">Type</span><span class="sxs-lookup"><span data-stu-id="360ca-170">Type</span></span>             | <span data-ttu-id="360ca-171">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="360ca-171">Required</span></span> | <span data-ttu-id="360ca-172">Notes</span><span class="sxs-lookup"><span data-stu-id="360ca-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="360ca-173">total des accès</span><span class="sxs-lookup"><span data-stu-id="360ca-173">totalHits</span></span> | <span data-ttu-id="360ca-174">entiers</span><span class="sxs-lookup"><span data-stu-id="360ca-174">integer</span></span>          | <span data-ttu-id="360ca-175">oui</span><span class="sxs-lookup"><span data-stu-id="360ca-175">yes</span></span>      | <span data-ttu-id="360ca-176">Le nombre total de correspondances, ignorant `skip` et `take`</span><span class="sxs-lookup"><span data-stu-id="360ca-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="360ca-177">Données</span><span class="sxs-lookup"><span data-stu-id="360ca-177">data</span></span>      | <span data-ttu-id="360ca-178">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="360ca-178">array of strings</span></span> | <span data-ttu-id="360ca-179">oui</span><span class="sxs-lookup"><span data-stu-id="360ca-179">yes</span></span>      | <span data-ttu-id="360ca-180">Les ID correspondant à la demande de package</span><span class="sxs-lookup"><span data-stu-id="360ca-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="360ca-181">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="360ca-181">Sample request</span></span>

<span data-ttu-id="360ca-182">TÉLÉCHARGER https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="360ca-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="360ca-183">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="360ca-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="360ca-184">Énumérer des versions de package</span><span class="sxs-lookup"><span data-stu-id="360ca-184">Enumerate package versions</span></span>

<span data-ttu-id="360ca-185">Une fois qu’un ID de package a été détecté à l’aide de l’API précédente, un client peut utiliser l’API de la saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.</span><span class="sxs-lookup"><span data-stu-id="360ca-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="360ca-186">Une version de package qui n’est pas spécifiée n’apparaîtra pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="360ca-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="360ca-187">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="360ca-187">Request parameters</span></span>

<span data-ttu-id="360ca-188">Name</span><span class="sxs-lookup"><span data-stu-id="360ca-188">Name</span></span>        | <span data-ttu-id="360ca-189">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="360ca-189">In</span></span>     | <span data-ttu-id="360ca-190">Type</span><span class="sxs-lookup"><span data-stu-id="360ca-190">Type</span></span>    | <span data-ttu-id="360ca-191">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="360ca-191">Required</span></span> | <span data-ttu-id="360ca-192">Notes</span><span class="sxs-lookup"><span data-stu-id="360ca-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="360ca-193">ID</span><span class="sxs-lookup"><span data-stu-id="360ca-193">id</span></span>          | <span data-ttu-id="360ca-194">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-194">URL</span></span>    | <span data-ttu-id="360ca-195">chaîne</span><span class="sxs-lookup"><span data-stu-id="360ca-195">string</span></span>  | <span data-ttu-id="360ca-196">oui</span><span class="sxs-lookup"><span data-stu-id="360ca-196">yes</span></span>      | <span data-ttu-id="360ca-197">Pour récupérer des versions pour l’ID de package</span><span class="sxs-lookup"><span data-stu-id="360ca-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="360ca-198">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="360ca-198">prerelease</span></span>  | <span data-ttu-id="360ca-199">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-199">URL</span></span>    | <span data-ttu-id="360ca-200">boolean</span><span class="sxs-lookup"><span data-stu-id="360ca-200">boolean</span></span> | <span data-ttu-id="360ca-201">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-201">no</span></span>       | <span data-ttu-id="360ca-202">`true` ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="360ca-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="360ca-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="360ca-203">semVerLevel</span></span> | <span data-ttu-id="360ca-204">URL</span><span class="sxs-lookup"><span data-stu-id="360ca-204">URL</span></span>    | <span data-ttu-id="360ca-205">chaîne</span><span class="sxs-lookup"><span data-stu-id="360ca-205">string</span></span>  | <span data-ttu-id="360ca-206">Non</span><span class="sxs-lookup"><span data-stu-id="360ca-206">no</span></span>       | <span data-ttu-id="360ca-207">Une chaîne de version SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="360ca-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="360ca-208">Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.</span><span class="sxs-lookup"><span data-stu-id="360ca-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="360ca-209">Le `semVerLevel` paramètre de requête permet de participer à des packages de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="360ca-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="360ca-210">Si ce paramètre de requête est exclu, seules les versions SemVer 1.0.0 seront retournées.</span><span class="sxs-lookup"><span data-stu-id="360ca-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="360ca-211">Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et SemVer 2.0.0 versions seront retournées.</span><span class="sxs-lookup"><span data-stu-id="360ca-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="360ca-212">Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="360ca-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="360ca-213">Réponse</span><span class="sxs-lookup"><span data-stu-id="360ca-213">Response</span></span>

<span data-ttu-id="360ca-214">La réponse est un document JSON qui contient toutes les versions de package de l’ID de package fourni, le filtrage par les paramètres de requête donnée.</span><span class="sxs-lookup"><span data-stu-id="360ca-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="360ca-215">L’objet JSON racine a la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="360ca-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="360ca-216">Name</span><span class="sxs-lookup"><span data-stu-id="360ca-216">Name</span></span>      | <span data-ttu-id="360ca-217">Type</span><span class="sxs-lookup"><span data-stu-id="360ca-217">Type</span></span>             | <span data-ttu-id="360ca-218">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="360ca-218">Required</span></span> | <span data-ttu-id="360ca-219">Notes</span><span class="sxs-lookup"><span data-stu-id="360ca-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="360ca-220">Données</span><span class="sxs-lookup"><span data-stu-id="360ca-220">data</span></span>      | <span data-ttu-id="360ca-221">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="360ca-221">array of strings</span></span> | <span data-ttu-id="360ca-222">oui</span><span class="sxs-lookup"><span data-stu-id="360ca-222">yes</span></span>      | <span data-ttu-id="360ca-223">Les versions de package correspondance à la demande</span><span class="sxs-lookup"><span data-stu-id="360ca-223">The package versions matched by the request</span></span>

<span data-ttu-id="360ca-224">Les versions de package dans le `data` tableau peut contenir des métadonnées de génération SemVer 2.0.0 (par exemple, `1.0.0+metadata`) si le `semVerLevel=2.0.0` a été fourni dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="360ca-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="360ca-225">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="360ca-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="360ca-226">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="360ca-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
