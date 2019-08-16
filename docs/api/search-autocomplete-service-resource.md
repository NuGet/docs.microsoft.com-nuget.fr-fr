---
title: Saisie semi-automatique, API NuGet
description: Le service de saisie semi-automatique de la recherche prend en charge la découverte interactive des ID de package et des versions.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488307"
---
# <a name="autocomplete"></a><span data-ttu-id="7d42a-103">Saisie semi-automatique</span><span class="sxs-lookup"><span data-stu-id="7d42a-103">Autocomplete</span></span>

<span data-ttu-id="7d42a-104">Il est possible de générer un ID de package et une expérience de saisie semi-automatique de version à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="7d42a-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="7d42a-105">La ressource utilisée pour effectuer des requêtes de saisie semi `SearchAutocompleteService` -automatique est la ressource trouvée dans l' [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7d42a-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7d42a-106">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="7d42a-106">Versioning</span></span>

<span data-ttu-id="7d42a-107">Les valeurs `@type` suivantes sont utilisées:</span><span class="sxs-lookup"><span data-stu-id="7d42a-107">The following `@type` values are used:</span></span>

<span data-ttu-id="7d42a-108">Valeur@type</span><span class="sxs-lookup"><span data-stu-id="7d42a-108">@type value</span></span>                          | <span data-ttu-id="7d42a-109">Notes</span><span class="sxs-lookup"><span data-stu-id="7d42a-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="7d42a-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="7d42a-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="7d42a-111">La version initiale</span><span class="sxs-lookup"><span data-stu-id="7d42a-111">The initial release</span></span>
<span data-ttu-id="7d42a-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="7d42a-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="7d42a-113">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="7d42a-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="7d42a-114">SearchAutocompleteService/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="7d42a-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="7d42a-115">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="7d42a-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="7d42a-116">URL de base</span><span class="sxs-lookup"><span data-stu-id="7d42a-116">Base URL</span></span>

<span data-ttu-id="7d42a-117">L’URL de base pour les API suivantes est la valeur de `@id` la propriété associée à l’une des valeurs `@type` de ressource mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7d42a-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="7d42a-118">Dans le document suivant, l’URL `{@id}` de base de l’espace réservé sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="7d42a-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7d42a-119">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="7d42a-119">HTTP Methods</span></span>

<span data-ttu-id="7d42a-120">Toutes les URL trouvées dans la ressource d’inscription prennent en `GET` charge `HEAD`les méthodes http et.</span><span class="sxs-lookup"><span data-stu-id="7d42a-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="7d42a-121">Rechercher des ID de package</span><span class="sxs-lookup"><span data-stu-id="7d42a-121">Search for package IDs</span></span>

<span data-ttu-id="7d42a-122">La première API de saisie semi-automatique prend en charge la recherche d’une partie d’une chaîne d’ID de package.</span><span class="sxs-lookup"><span data-stu-id="7d42a-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="7d42a-123">C’est très utile lorsque vous souhaitez fournir une fonctionnalité TypeAhead de package dans une interface utilisateur intégrée à une source de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d42a-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="7d42a-124">Un package avec uniquement des versions non répertoriées n’apparaît pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="7d42a-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7d42a-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7d42a-125">Request parameters</span></span>

<span data-ttu-id="7d42a-126">Nom</span><span class="sxs-lookup"><span data-stu-id="7d42a-126">Name</span></span>        | <span data-ttu-id="7d42a-127">Dans</span><span class="sxs-lookup"><span data-stu-id="7d42a-127">In</span></span>     | <span data-ttu-id="7d42a-128">Type</span><span class="sxs-lookup"><span data-stu-id="7d42a-128">Type</span></span>    | <span data-ttu-id="7d42a-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7d42a-129">Required</span></span> | <span data-ttu-id="7d42a-130">Notes</span><span class="sxs-lookup"><span data-stu-id="7d42a-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7d42a-131">q</span><span class="sxs-lookup"><span data-stu-id="7d42a-131">q</span></span>           | <span data-ttu-id="7d42a-132">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-132">URL</span></span>    | <span data-ttu-id="7d42a-133">string</span><span class="sxs-lookup"><span data-stu-id="7d42a-133">string</span></span>  | <span data-ttu-id="7d42a-134">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-134">no</span></span>       | <span data-ttu-id="7d42a-135">Chaîne à comparer aux ID de package</span><span class="sxs-lookup"><span data-stu-id="7d42a-135">The string to compare against package IDs</span></span>
<span data-ttu-id="7d42a-136">skip</span><span class="sxs-lookup"><span data-stu-id="7d42a-136">skip</span></span>        | <span data-ttu-id="7d42a-137">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-137">URL</span></span>    | <span data-ttu-id="7d42a-138">integer</span><span class="sxs-lookup"><span data-stu-id="7d42a-138">integer</span></span> | <span data-ttu-id="7d42a-139">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-139">no</span></span>       | <span data-ttu-id="7d42a-140">Nombre de résultats à ignorer pour la pagination</span><span class="sxs-lookup"><span data-stu-id="7d42a-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="7d42a-141">prendre</span><span class="sxs-lookup"><span data-stu-id="7d42a-141">take</span></span>        | <span data-ttu-id="7d42a-142">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-142">URL</span></span>    | <span data-ttu-id="7d42a-143">integer</span><span class="sxs-lookup"><span data-stu-id="7d42a-143">integer</span></span> | <span data-ttu-id="7d42a-144">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-144">no</span></span>       | <span data-ttu-id="7d42a-145">Nombre de résultats à retourner, pour la pagination</span><span class="sxs-lookup"><span data-stu-id="7d42a-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="7d42a-146">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="7d42a-146">prerelease</span></span>  | <span data-ttu-id="7d42a-147">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-147">URL</span></span>    | <span data-ttu-id="7d42a-148">booléenne</span><span class="sxs-lookup"><span data-stu-id="7d42a-148">boolean</span></span> | <span data-ttu-id="7d42a-149">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-149">no</span></span>       | <span data-ttu-id="7d42a-150">`true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion</span><span class="sxs-lookup"><span data-stu-id="7d42a-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7d42a-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7d42a-151">semVerLevel</span></span> | <span data-ttu-id="7d42a-152">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-152">URL</span></span>    | <span data-ttu-id="7d42a-153">string</span><span class="sxs-lookup"><span data-stu-id="7d42a-153">string</span></span>  | <span data-ttu-id="7d42a-154">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-154">no</span></span>       | <span data-ttu-id="7d42a-155">Chaîne de version SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="7d42a-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="7d42a-156">La requête `q` de saisie semi-automatique est analysée d’une manière définie par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="7d42a-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="7d42a-157">nuget.org prend en charge l’interrogation du préfixe des jetons d’ID de package, qui sont des éléments de l’ID produit par le fractionnement de la casse et des caractères de symboles mixtes originaux.</span><span class="sxs-lookup"><span data-stu-id="7d42a-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="7d42a-158">La `skip` valeur par défaut du paramètre est 0.</span><span class="sxs-lookup"><span data-stu-id="7d42a-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="7d42a-159">Le `take` paramètre doit être un entier supérieur à zéro.</span><span class="sxs-lookup"><span data-stu-id="7d42a-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="7d42a-160">L’implémentation du serveur peut imposer une valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="7d42a-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="7d42a-161">Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.</span><span class="sxs-lookup"><span data-stu-id="7d42a-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7d42a-162">Le `semVerLevel` paramètre de requête permet de s’abonner à des [packages SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="7d42a-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="7d42a-163">Si ce paramètre de requête est exclu, seuls les ID de package avec des versions compatibles SemVer 1.0.0 sont retournés (avec les avertissements de [version NuGet standard](../concepts/package-versioning.md) , tels que les chaînes de version avec 4 éléments entiers).</span><span class="sxs-lookup"><span data-stu-id="7d42a-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="7d42a-164">Si `semVerLevel=2.0.0` est fourni, les packages compatibles SemVer 1.0.0 et SemVer 2.0.0 sont retournés.</span><span class="sxs-lookup"><span data-stu-id="7d42a-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="7d42a-165">Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="7d42a-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7d42a-166">response</span><span class="sxs-lookup"><span data-stu-id="7d42a-166">Response</span></span>

<span data-ttu-id="7d42a-167">La réponse est un document JSON contenant des `take` résultats de saisie semi-automatique.</span><span class="sxs-lookup"><span data-stu-id="7d42a-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="7d42a-168">L’objet JSON racine a les propriétés suivantes:</span><span class="sxs-lookup"><span data-stu-id="7d42a-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="7d42a-169">Nom</span><span class="sxs-lookup"><span data-stu-id="7d42a-169">Name</span></span>      | <span data-ttu-id="7d42a-170">Type</span><span class="sxs-lookup"><span data-stu-id="7d42a-170">Type</span></span>             | <span data-ttu-id="7d42a-171">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7d42a-171">Required</span></span> | <span data-ttu-id="7d42a-172">Notes</span><span class="sxs-lookup"><span data-stu-id="7d42a-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7d42a-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="7d42a-173">totalHits</span></span> | <span data-ttu-id="7d42a-174">integer</span><span class="sxs-lookup"><span data-stu-id="7d42a-174">integer</span></span>          | <span data-ttu-id="7d42a-175">oui</span><span class="sxs-lookup"><span data-stu-id="7d42a-175">yes</span></span>      | <span data-ttu-id="7d42a-176">Nombre total de correspondances, à l' `skip` égard de et`take`</span><span class="sxs-lookup"><span data-stu-id="7d42a-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="7d42a-177">data</span><span class="sxs-lookup"><span data-stu-id="7d42a-177">data</span></span>      | <span data-ttu-id="7d42a-178">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="7d42a-178">array of strings</span></span> | <span data-ttu-id="7d42a-179">oui</span><span class="sxs-lookup"><span data-stu-id="7d42a-179">yes</span></span>      | <span data-ttu-id="7d42a-180">ID de package correspondants à la requête</span><span class="sxs-lookup"><span data-stu-id="7d42a-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="7d42a-181">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="7d42a-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7d42a-182">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="7d42a-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="7d42a-183">Énumérer les versions du package</span><span class="sxs-lookup"><span data-stu-id="7d42a-183">Enumerate package versions</span></span>

<span data-ttu-id="7d42a-184">Une fois qu’un ID de package est découvert à l’aide de l’API précédente, un client peut utiliser l’API de saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.</span><span class="sxs-lookup"><span data-stu-id="7d42a-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="7d42a-185">Une version de package non listée n’apparaît pas dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="7d42a-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7d42a-186">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7d42a-186">Request parameters</span></span>

<span data-ttu-id="7d42a-187">Name</span><span class="sxs-lookup"><span data-stu-id="7d42a-187">Name</span></span>        | <span data-ttu-id="7d42a-188">Dans</span><span class="sxs-lookup"><span data-stu-id="7d42a-188">In</span></span>     | <span data-ttu-id="7d42a-189">Type</span><span class="sxs-lookup"><span data-stu-id="7d42a-189">Type</span></span>    | <span data-ttu-id="7d42a-190">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7d42a-190">Required</span></span> | <span data-ttu-id="7d42a-191">Notes</span><span class="sxs-lookup"><span data-stu-id="7d42a-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7d42a-192">id</span><span class="sxs-lookup"><span data-stu-id="7d42a-192">id</span></span>          | <span data-ttu-id="7d42a-193">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-193">URL</span></span>    | <span data-ttu-id="7d42a-194">string</span><span class="sxs-lookup"><span data-stu-id="7d42a-194">string</span></span>  | <span data-ttu-id="7d42a-195">oui</span><span class="sxs-lookup"><span data-stu-id="7d42a-195">yes</span></span>      | <span data-ttu-id="7d42a-196">ID de package pour lequel extraire les versions</span><span class="sxs-lookup"><span data-stu-id="7d42a-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="7d42a-197">version préliminaire</span><span class="sxs-lookup"><span data-stu-id="7d42a-197">prerelease</span></span>  | <span data-ttu-id="7d42a-198">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-198">URL</span></span>    | <span data-ttu-id="7d42a-199">booléenne</span><span class="sxs-lookup"><span data-stu-id="7d42a-199">boolean</span></span> | <span data-ttu-id="7d42a-200">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-200">no</span></span>       | <span data-ttu-id="7d42a-201">`true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion</span><span class="sxs-lookup"><span data-stu-id="7d42a-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7d42a-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7d42a-202">semVerLevel</span></span> | <span data-ttu-id="7d42a-203">URL</span><span class="sxs-lookup"><span data-stu-id="7d42a-203">URL</span></span>    | <span data-ttu-id="7d42a-204">string</span><span class="sxs-lookup"><span data-stu-id="7d42a-204">string</span></span>  | <span data-ttu-id="7d42a-205">Non</span><span class="sxs-lookup"><span data-stu-id="7d42a-205">no</span></span>       | <span data-ttu-id="7d42a-206">Une chaîne de version SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="7d42a-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="7d42a-207">Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.</span><span class="sxs-lookup"><span data-stu-id="7d42a-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7d42a-208">Le `semVerLevel` paramètre de requête permet de s’abonner à des packages SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7d42a-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="7d42a-209">Si ce paramètre de requête est exclu, seules les versions de SemVer 1.0.0 sont retournées.</span><span class="sxs-lookup"><span data-stu-id="7d42a-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="7d42a-210">Si `semVerLevel=2.0.0` est fourni, les versions SemVer 1.0.0 et SemVer 2.0.0 sont retournées.</span><span class="sxs-lookup"><span data-stu-id="7d42a-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="7d42a-211">Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="7d42a-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7d42a-212">response</span><span class="sxs-lookup"><span data-stu-id="7d42a-212">Response</span></span>

<span data-ttu-id="7d42a-213">La réponse est un document JSON contenant toutes les versions de package de l’ID de package fourni, en filtrant par les paramètres de requête donnés.</span><span class="sxs-lookup"><span data-stu-id="7d42a-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="7d42a-214">L’objet JSON racine a la propriété suivante:</span><span class="sxs-lookup"><span data-stu-id="7d42a-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="7d42a-215">Nom</span><span class="sxs-lookup"><span data-stu-id="7d42a-215">Name</span></span>      | <span data-ttu-id="7d42a-216">Type</span><span class="sxs-lookup"><span data-stu-id="7d42a-216">Type</span></span>             | <span data-ttu-id="7d42a-217">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7d42a-217">Required</span></span> | <span data-ttu-id="7d42a-218">Notes</span><span class="sxs-lookup"><span data-stu-id="7d42a-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7d42a-219">data</span><span class="sxs-lookup"><span data-stu-id="7d42a-219">data</span></span>      | <span data-ttu-id="7d42a-220">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="7d42a-220">array of strings</span></span> | <span data-ttu-id="7d42a-221">oui</span><span class="sxs-lookup"><span data-stu-id="7d42a-221">yes</span></span>      | <span data-ttu-id="7d42a-222">Versions du package correspondant à la requête</span><span class="sxs-lookup"><span data-stu-id="7d42a-222">The package versions matched by the request</span></span>

<span data-ttu-id="7d42a-223">Les versions de package dans `data` le tableau peuvent contenir des métadonnées de build SemVer `1.0.0+metadata`2.0.0 (par `semVerLevel=2.0.0` exemple,) si le est fourni dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="7d42a-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7d42a-224">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="7d42a-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7d42a-225">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="7d42a-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
