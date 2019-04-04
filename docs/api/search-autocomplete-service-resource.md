---
title: Saisie semi-automatique, API NuGet
description: Le service de la saisie semi-automatique de recherche prend en charge les versions et découverte interactive de l’ID de package.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911047"
---
# <a name="autocomplete"></a><span data-ttu-id="a071d-103">Saisie semi-automatique</span><span class="sxs-lookup"><span data-stu-id="a071d-103">Autocomplete</span></span>

<span data-ttu-id="a071d-104">Il est possible de créer un package ID et la version la saisie semi-automatique expérience à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="a071d-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="a071d-105">La ressource utilisée pour effectuer des requêtes de la saisie semi-automatique est la `SearchAutocompleteService` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="a071d-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="a071d-106">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="a071d-106">Versioning</span></span>

<span data-ttu-id="a071d-107">Les éléments suivants `@type` les valeurs sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="a071d-107">The following `@type` values are used:</span></span>

<span data-ttu-id="a071d-108">Valeur@type </span><span class="sxs-lookup"><span data-stu-id="a071d-108">@type value</span></span>                          | <span data-ttu-id="a071d-109">Notes</span><span class="sxs-lookup"><span data-stu-id="a071d-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="a071d-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="a071d-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="a071d-111">La version initiale</span><span class="sxs-lookup"><span data-stu-id="a071d-111">The initial release</span></span>
<span data-ttu-id="a071d-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="a071d-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="a071d-113">Alias de</span><span class="sxs-lookup"><span data-stu-id="a071d-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="a071d-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="a071d-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="a071d-115">Alias de</span><span class="sxs-lookup"><span data-stu-id="a071d-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="a071d-116">URL de base</span><span class="sxs-lookup"><span data-stu-id="a071d-116">Base URL</span></span>

<span data-ttu-id="a071d-117">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.</span><span class="sxs-lookup"><span data-stu-id="a071d-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="a071d-118">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="a071d-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a071d-119">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="a071d-119">HTTP Methods</span></span>

<span data-ttu-id="a071d-120">Toutes les URL trouvés dans la prise en charge de la ressource d’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="a071d-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="a071d-121">Recherchez les ID de package</span><span class="sxs-lookup"><span data-stu-id="a071d-121">Search for package IDs</span></span>

<span data-ttu-id="a071d-122">La saisie semi-automatique première API prend en charge la recherche pour une partie d’une chaîne d’ID de package.</span><span class="sxs-lookup"><span data-stu-id="a071d-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="a071d-123">C’est formidable lorsque vous souhaitez fournir une fonctionnalité de prédictives de package dans une interface utilisateur intégrée à une source de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="a071d-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="a071d-124">Un package avec uniquement les versions non listées n’apparaîtra pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="a071d-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="a071d-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="a071d-125">Request parameters</span></span>

<span data-ttu-id="a071d-126">Nom</span><span class="sxs-lookup"><span data-stu-id="a071d-126">Name</span></span>        | <span data-ttu-id="a071d-127">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="a071d-127">In</span></span>     | <span data-ttu-id="a071d-128">Type</span><span class="sxs-lookup"><span data-stu-id="a071d-128">Type</span></span>    | <span data-ttu-id="a071d-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="a071d-129">Required</span></span> | <span data-ttu-id="a071d-130">Notes</span><span class="sxs-lookup"><span data-stu-id="a071d-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="a071d-131">q</span><span class="sxs-lookup"><span data-stu-id="a071d-131">q</span></span>           | <span data-ttu-id="a071d-132">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-132">URL</span></span>    | <span data-ttu-id="a071d-133">string</span><span class="sxs-lookup"><span data-stu-id="a071d-133">string</span></span>  | <span data-ttu-id="a071d-134">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-134">no</span></span>       | <span data-ttu-id="a071d-135">La chaîne à comparer à l’ID de package</span><span class="sxs-lookup"><span data-stu-id="a071d-135">The string to compare against package IDs</span></span>
<span data-ttu-id="a071d-136">skip</span><span class="sxs-lookup"><span data-stu-id="a071d-136">skip</span></span>        | <span data-ttu-id="a071d-137">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-137">URL</span></span>    | <span data-ttu-id="a071d-138">entiers</span><span class="sxs-lookup"><span data-stu-id="a071d-138">integer</span></span> | <span data-ttu-id="a071d-139">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-139">no</span></span>       | <span data-ttu-id="a071d-140">Le nombre de résultats à ignorer, pour la pagination</span><span class="sxs-lookup"><span data-stu-id="a071d-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="a071d-141">Take</span><span class="sxs-lookup"><span data-stu-id="a071d-141">take</span></span>        | <span data-ttu-id="a071d-142">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-142">URL</span></span>    | <span data-ttu-id="a071d-143">entiers</span><span class="sxs-lookup"><span data-stu-id="a071d-143">integer</span></span> | <span data-ttu-id="a071d-144">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-144">no</span></span>       | <span data-ttu-id="a071d-145">Le nombre de résultats à retourner pour la pagination</span><span class="sxs-lookup"><span data-stu-id="a071d-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="a071d-146">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="a071d-146">prerelease</span></span>  | <span data-ttu-id="a071d-147">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-147">URL</span></span>    | <span data-ttu-id="a071d-148">boolean</span><span class="sxs-lookup"><span data-stu-id="a071d-148">boolean</span></span> | <span data-ttu-id="a071d-149">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-149">no</span></span>       | `true` <span data-ttu-id="a071d-150">ou `false` déterminer s’il faut inclure [packages de préversion](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a071d-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="a071d-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="a071d-151">semVerLevel</span></span> | <span data-ttu-id="a071d-152">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-152">URL</span></span>    | <span data-ttu-id="a071d-153">string</span><span class="sxs-lookup"><span data-stu-id="a071d-153">string</span></span>  | <span data-ttu-id="a071d-154">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-154">no</span></span>       | <span data-ttu-id="a071d-155">Une chaîne de version SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="a071d-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="a071d-156">La requête de la saisie semi-automatique `q` est analysé d’une manière qui est définie par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="a071d-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="a071d-157">NuGet.org prend en charge l’interrogation d’origine pour le préfixe de jetons d’ID de package, qui sont des éléments de l’ID de produit par fractionnement par des caractères de cas et le symbole mixte.</span><span class="sxs-lookup"><span data-stu-id="a071d-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="a071d-158">Le `skip` paramètre valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="a071d-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="a071d-159">Le `take` paramètre doit être un entier supérieur à zéro.</span><span class="sxs-lookup"><span data-stu-id="a071d-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="a071d-160">L’implémentation du serveur peut imposer une valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="a071d-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="a071d-161">Si `prerelease` n’est pas fourni, packages de préversion sont exclus.</span><span class="sxs-lookup"><span data-stu-id="a071d-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="a071d-162">Le `semVerLevel` paramètre de requête permet de participer à la [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="a071d-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="a071d-163">Si ce paramètre de requête est exclu, ID de package uniquement avec les versions compatibles de SemVer 1.0.0 seront retourné (avec le [le contrôle de version NuGet standard](../reference/package-versioning.md) mises en garde, tels que les chaînes de version avec 4 éléments entier).</span><span class="sxs-lookup"><span data-stu-id="a071d-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="a071d-164">Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et packages compatibles SemVer 2.0.0 seront retournés.</span><span class="sxs-lookup"><span data-stu-id="a071d-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="a071d-165">Consultez le [prise en charge de SemVer 2.0.0 pour nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a071d-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="a071d-166">Réponse</span><span class="sxs-lookup"><span data-stu-id="a071d-166">Response</span></span>

<span data-ttu-id="a071d-167">La réponse est document JSON contenant jusqu'à `take` les résultats de la saisie semi-automatique.</span><span class="sxs-lookup"><span data-stu-id="a071d-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="a071d-168">L’objet JSON racine a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a071d-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="a071d-169">Nom</span><span class="sxs-lookup"><span data-stu-id="a071d-169">Name</span></span>      | <span data-ttu-id="a071d-170">Type</span><span class="sxs-lookup"><span data-stu-id="a071d-170">Type</span></span>             | <span data-ttu-id="a071d-171">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="a071d-171">Required</span></span> | <span data-ttu-id="a071d-172">Notes</span><span class="sxs-lookup"><span data-stu-id="a071d-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="a071d-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="a071d-173">totalHits</span></span> | <span data-ttu-id="a071d-174">entiers</span><span class="sxs-lookup"><span data-stu-id="a071d-174">integer</span></span>          | <span data-ttu-id="a071d-175">oui</span><span class="sxs-lookup"><span data-stu-id="a071d-175">yes</span></span>      | <span data-ttu-id="a071d-176">Le nombre total de correspondances, en ignorant `skip` et</span><span class="sxs-lookup"><span data-stu-id="a071d-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="a071d-177">Données</span><span class="sxs-lookup"><span data-stu-id="a071d-177">data</span></span>      | <span data-ttu-id="a071d-178">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="a071d-178">array of strings</span></span> | <span data-ttu-id="a071d-179">oui</span><span class="sxs-lookup"><span data-stu-id="a071d-179">yes</span></span>      | <span data-ttu-id="a071d-180">Les ID mis en correspondance par la demande de package</span><span class="sxs-lookup"><span data-stu-id="a071d-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="a071d-181">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a071d-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="a071d-182">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a071d-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="a071d-183">Énumérer les versions de package</span><span class="sxs-lookup"><span data-stu-id="a071d-183">Enumerate package versions</span></span>

<span data-ttu-id="a071d-184">Une fois qu’un ID de package est découvert à l’aide de l’API précédente, un client peut utiliser l’API de saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.</span><span class="sxs-lookup"><span data-stu-id="a071d-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="a071d-185">Une version de package n’est pas répertoriée n’apparaîtra pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="a071d-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="a071d-186">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="a071d-186">Request parameters</span></span>

<span data-ttu-id="a071d-187">Nom</span><span class="sxs-lookup"><span data-stu-id="a071d-187">Name</span></span>        | <span data-ttu-id="a071d-188">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="a071d-188">In</span></span>     | <span data-ttu-id="a071d-189">Type</span><span class="sxs-lookup"><span data-stu-id="a071d-189">Type</span></span>    | <span data-ttu-id="a071d-190">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="a071d-190">Required</span></span> | <span data-ttu-id="a071d-191">Notes</span><span class="sxs-lookup"><span data-stu-id="a071d-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="a071d-192">ID</span><span class="sxs-lookup"><span data-stu-id="a071d-192">id</span></span>          | <span data-ttu-id="a071d-193">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-193">URL</span></span>    | <span data-ttu-id="a071d-194">string</span><span class="sxs-lookup"><span data-stu-id="a071d-194">string</span></span>  | <span data-ttu-id="a071d-195">oui</span><span class="sxs-lookup"><span data-stu-id="a071d-195">yes</span></span>      | <span data-ttu-id="a071d-196">L’ID de package pour extraire les versions pour</span><span class="sxs-lookup"><span data-stu-id="a071d-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="a071d-197">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="a071d-197">prerelease</span></span>  | <span data-ttu-id="a071d-198">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-198">URL</span></span>    | <span data-ttu-id="a071d-199">boolean</span><span class="sxs-lookup"><span data-stu-id="a071d-199">boolean</span></span> | <span data-ttu-id="a071d-200">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-200">no</span></span>       | `true` <span data-ttu-id="a071d-201">ou `false` déterminer s’il faut inclure [packages de préversion](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a071d-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="a071d-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="a071d-202">semVerLevel</span></span> | <span data-ttu-id="a071d-203">URL</span><span class="sxs-lookup"><span data-stu-id="a071d-203">URL</span></span>    | <span data-ttu-id="a071d-204">string</span><span class="sxs-lookup"><span data-stu-id="a071d-204">string</span></span>  | <span data-ttu-id="a071d-205">Non</span><span class="sxs-lookup"><span data-stu-id="a071d-205">no</span></span>       | <span data-ttu-id="a071d-206">Une chaîne de version SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a071d-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="a071d-207">Si `prerelease` n’est pas fourni, packages de préversion sont exclus.</span><span class="sxs-lookup"><span data-stu-id="a071d-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="a071d-208">Le `semVerLevel` paramètre de requête permet de participer aux packages de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a071d-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="a071d-209">Si ce paramètre de requête est exclu, seules les versions de SemVer 1.0.0 seront affichera.</span><span class="sxs-lookup"><span data-stu-id="a071d-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="a071d-210">Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et les versions de SemVer 2.0.0 seront retournées.</span><span class="sxs-lookup"><span data-stu-id="a071d-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="a071d-211">Consultez le [prise en charge de SemVer 2.0.0 pour nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a071d-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="a071d-212">Réponse</span><span class="sxs-lookup"><span data-stu-id="a071d-212">Response</span></span>

<span data-ttu-id="a071d-213">La réponse est un document JSON contenant toutes les versions de package de l’ID de package fourni, le filtrage par les paramètres de requête donnée.</span><span class="sxs-lookup"><span data-stu-id="a071d-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="a071d-214">L’objet JSON racine a la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="a071d-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="a071d-215">Nom</span><span class="sxs-lookup"><span data-stu-id="a071d-215">Name</span></span>      | <span data-ttu-id="a071d-216">Type</span><span class="sxs-lookup"><span data-stu-id="a071d-216">Type</span></span>             | <span data-ttu-id="a071d-217">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="a071d-217">Required</span></span> | <span data-ttu-id="a071d-218">Notes</span><span class="sxs-lookup"><span data-stu-id="a071d-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="a071d-219">Données</span><span class="sxs-lookup"><span data-stu-id="a071d-219">data</span></span>      | <span data-ttu-id="a071d-220">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="a071d-220">array of strings</span></span> | <span data-ttu-id="a071d-221">oui</span><span class="sxs-lookup"><span data-stu-id="a071d-221">yes</span></span>      | <span data-ttu-id="a071d-222">Les versions de package correspondance à la demande</span><span class="sxs-lookup"><span data-stu-id="a071d-222">The package versions matched by the request</span></span>

<span data-ttu-id="a071d-223">Les versions de package dans le `data` tableau peut-être contenir des métadonnées de build de SemVer 2.0.0 (par exemple, `1.0.0+metadata`) si le `semVerLevel=2.0.0` est fourni dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="a071d-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a071d-224">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a071d-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="a071d-225">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a071d-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
