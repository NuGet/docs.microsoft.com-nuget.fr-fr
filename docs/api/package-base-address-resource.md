---
title: Contenu du package, API NuGet
description: L’adresse de base du package est une interface simple permettant d’extraire le package lui-même.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488221"
---
# <a name="package-content"></a><span data-ttu-id="6da9b-103">Contenu du package</span><span class="sxs-lookup"><span data-stu-id="6da9b-103">Package Content</span></span>

<span data-ttu-id="6da9b-104">Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (fichier. nupkg) à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="6da9b-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="6da9b-105">La ressource utilisée pour récupérer le contenu du package est `PackageBaseAddress` la ressource trouvée dans l' [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6da9b-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="6da9b-106">Cette ressource permet également la détection de toutes les versions d’un package, répertoriées ou désactivées.</span><span class="sxs-lookup"><span data-stu-id="6da9b-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="6da9b-107">Cette ressource est communément appelée «adresse de base du package» ou «conteneur plat».</span><span class="sxs-lookup"><span data-stu-id="6da9b-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="6da9b-108">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="6da9b-108">Versioning</span></span>

<span data-ttu-id="6da9b-109">La valeur `@type` suivante est utilisée:</span><span class="sxs-lookup"><span data-stu-id="6da9b-109">The following `@type` value is used:</span></span>

<span data-ttu-id="6da9b-110">Valeur@type</span><span class="sxs-lookup"><span data-stu-id="6da9b-110">@type value</span></span>              | <span data-ttu-id="6da9b-111">Notes</span><span class="sxs-lookup"><span data-stu-id="6da9b-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="6da9b-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="6da9b-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="6da9b-113">La version initiale</span><span class="sxs-lookup"><span data-stu-id="6da9b-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6da9b-114">URL de base</span><span class="sxs-lookup"><span data-stu-id="6da9b-114">Base URL</span></span>

<span data-ttu-id="6da9b-115">L’URL de base pour les API suivantes est la valeur de `@id` la propriété associée à la valeur `@type` de ressource mentionnée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6da9b-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="6da9b-116">Dans le document suivant, l’URL `{@id}` de base de l’espace réservé sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="6da9b-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6da9b-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="6da9b-117">HTTP methods</span></span>

<span data-ttu-id="6da9b-118">Toutes les URL trouvées dans la ressource d’inscription prennent en `GET` charge `HEAD`les méthodes http et.</span><span class="sxs-lookup"><span data-stu-id="6da9b-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="6da9b-119">Énumérer les versions du package</span><span class="sxs-lookup"><span data-stu-id="6da9b-119">Enumerate package versions</span></span>

<span data-ttu-id="6da9b-120">Si le client connaît un ID de package et souhaite découvrir quelles versions de package la source du package a disponibles, le client peut construire une URL prévisible pour énumérer toutes les versions du package.</span><span class="sxs-lookup"><span data-stu-id="6da9b-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="6da9b-121">Cette liste est censée être une «liste de répertoires» pour l’API de contenu de package mentionnée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6da9b-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="6da9b-122">Cette liste contient à la fois les versions de packages listées et désinscrites.</span><span class="sxs-lookup"><span data-stu-id="6da9b-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="6da9b-123">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="6da9b-123">Request parameters</span></span>

<span data-ttu-id="6da9b-124">Name</span><span class="sxs-lookup"><span data-stu-id="6da9b-124">Name</span></span>     | <span data-ttu-id="6da9b-125">Dans</span><span class="sxs-lookup"><span data-stu-id="6da9b-125">In</span></span>     | <span data-ttu-id="6da9b-126">Type</span><span class="sxs-lookup"><span data-stu-id="6da9b-126">Type</span></span>    | <span data-ttu-id="6da9b-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="6da9b-127">Required</span></span> | <span data-ttu-id="6da9b-128">Notes</span><span class="sxs-lookup"><span data-stu-id="6da9b-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="6da9b-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6da9b-129">LOWER_ID</span></span> | <span data-ttu-id="6da9b-130">URL</span><span class="sxs-lookup"><span data-stu-id="6da9b-130">URL</span></span>    | <span data-ttu-id="6da9b-131">string</span><span class="sxs-lookup"><span data-stu-id="6da9b-131">string</span></span>  | <span data-ttu-id="6da9b-132">oui</span><span class="sxs-lookup"><span data-stu-id="6da9b-132">yes</span></span>      | <span data-ttu-id="6da9b-133">ID de package, minuscules</span><span class="sxs-lookup"><span data-stu-id="6da9b-133">The package ID, lowercase</span></span>

<span data-ttu-id="6da9b-134">La `LOWER_ID` valeur est l’ID de package souhaité en minuscules à l’aide des règles implémentées par. Méthode du [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) réseau.</span><span class="sxs-lookup"><span data-stu-id="6da9b-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="6da9b-135">response</span><span class="sxs-lookup"><span data-stu-id="6da9b-135">Response</span></span>

<span data-ttu-id="6da9b-136">Si la source du package n’a pas de version de l’ID de package fourni, un code d’État 404 est retourné.</span><span class="sxs-lookup"><span data-stu-id="6da9b-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="6da9b-137">Si la source du package a une ou plusieurs versions, un code d’état 200 est retourné.</span><span class="sxs-lookup"><span data-stu-id="6da9b-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="6da9b-138">Le corps de la réponse est un objet JSON avec la propriété suivante:</span><span class="sxs-lookup"><span data-stu-id="6da9b-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="6da9b-139">Name</span><span class="sxs-lookup"><span data-stu-id="6da9b-139">Name</span></span>     | <span data-ttu-id="6da9b-140">Type</span><span class="sxs-lookup"><span data-stu-id="6da9b-140">Type</span></span>             | <span data-ttu-id="6da9b-141">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="6da9b-141">Required</span></span> | <span data-ttu-id="6da9b-142">Notes</span><span class="sxs-lookup"><span data-stu-id="6da9b-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="6da9b-143">versions</span><span class="sxs-lookup"><span data-stu-id="6da9b-143">versions</span></span> | <span data-ttu-id="6da9b-144">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="6da9b-144">array of strings</span></span> | <span data-ttu-id="6da9b-145">oui</span><span class="sxs-lookup"><span data-stu-id="6da9b-145">yes</span></span>      | <span data-ttu-id="6da9b-146">ID de package disponibles</span><span class="sxs-lookup"><span data-stu-id="6da9b-146">The package IDs available</span></span>

<span data-ttu-id="6da9b-147">Les chaînes du `versions` tableau sont toutes des [chaînes de version NuGet](../concepts/package-versioning.md#normalized-version-numbers), normalisées et en minuscules.</span><span class="sxs-lookup"><span data-stu-id="6da9b-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6da9b-148">Les chaînes de version ne contiennent pas de métadonnées de build SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6da9b-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="6da9b-149">L’objectif est que les chaînes de version trouvées dans ce tableau peuvent être utilisées textuellement `LOWER_VERSION` pour les jetons trouvés dans les points de terminaison suivants.</span><span class="sxs-lookup"><span data-stu-id="6da9b-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6da9b-150">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="6da9b-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="6da9b-151">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="6da9b-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="6da9b-152">Télécharger le contenu du package (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="6da9b-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="6da9b-153">Si le client connaît un ID de package et une version et qu’il souhaite télécharger le contenu du package, il n’a besoin que de créer l’URL suivante:</span><span class="sxs-lookup"><span data-stu-id="6da9b-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="6da9b-154">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="6da9b-154">Request parameters</span></span>

<span data-ttu-id="6da9b-155">Name</span><span class="sxs-lookup"><span data-stu-id="6da9b-155">Name</span></span>          | <span data-ttu-id="6da9b-156">Dans</span><span class="sxs-lookup"><span data-stu-id="6da9b-156">In</span></span>     | <span data-ttu-id="6da9b-157">Type</span><span class="sxs-lookup"><span data-stu-id="6da9b-157">Type</span></span>   | <span data-ttu-id="6da9b-158">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="6da9b-158">Required</span></span> | <span data-ttu-id="6da9b-159">Notes</span><span class="sxs-lookup"><span data-stu-id="6da9b-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6da9b-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6da9b-160">LOWER_ID</span></span>      | <span data-ttu-id="6da9b-161">URL</span><span class="sxs-lookup"><span data-stu-id="6da9b-161">URL</span></span>    | <span data-ttu-id="6da9b-162">string</span><span class="sxs-lookup"><span data-stu-id="6da9b-162">string</span></span> | <span data-ttu-id="6da9b-163">oui</span><span class="sxs-lookup"><span data-stu-id="6da9b-163">yes</span></span>      | <span data-ttu-id="6da9b-164">ID de package, minuscules</span><span class="sxs-lookup"><span data-stu-id="6da9b-164">The package ID, lowercase</span></span>
<span data-ttu-id="6da9b-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="6da9b-165">LOWER_VERSION</span></span> | <span data-ttu-id="6da9b-166">URL</span><span class="sxs-lookup"><span data-stu-id="6da9b-166">URL</span></span>    | <span data-ttu-id="6da9b-167">string</span><span class="sxs-lookup"><span data-stu-id="6da9b-167">string</span></span> | <span data-ttu-id="6da9b-168">oui</span><span class="sxs-lookup"><span data-stu-id="6da9b-168">yes</span></span>      | <span data-ttu-id="6da9b-169">Version du package, normalisée et en minuscules</span><span class="sxs-lookup"><span data-stu-id="6da9b-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="6da9b-170">`LOWER_ID` Et`LOWER_VERSION` sont en minuscules à l’aide des règles implémentées par. Du réseau[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="6da9b-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="6da9b-171">.</span><span class="sxs-lookup"><span data-stu-id="6da9b-171">method.</span></span>

<span data-ttu-id="6da9b-172">Est `LOWER_VERSION` la version de package souhaitée normalisée à l’aide des [règles de normalisation](../concepts/package-versioning.md#normalized-version-numbers)de la version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="6da9b-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6da9b-173">Cela signifie que les métadonnées de build autorisées par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="6da9b-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="6da9b-174">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="6da9b-174">Response body</span></span>

<span data-ttu-id="6da9b-175">Si le package existe sur la source du package, un code d’état 200 est retourné.</span><span class="sxs-lookup"><span data-stu-id="6da9b-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="6da9b-176">Le corps de la réponse sera le contenu du package lui-même.</span><span class="sxs-lookup"><span data-stu-id="6da9b-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="6da9b-177">Si le package n’existe pas sur la source du package, un code d’État 404 est retourné.</span><span class="sxs-lookup"><span data-stu-id="6da9b-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6da9b-178">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="6da9b-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="6da9b-179">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="6da9b-179">Sample response</span></span>

<span data-ttu-id="6da9b-180">Flux binaire qui est le fichier. nupkg pour Newtonsoft. JSON version9.0.1.</span><span class="sxs-lookup"><span data-stu-id="6da9b-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="6da9b-181">Télécharger le manifeste du package (. NuSpec)</span><span class="sxs-lookup"><span data-stu-id="6da9b-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="6da9b-182">Si le client connaît un ID de package et une version et qu’il souhaite télécharger le manifeste du package, il n’a besoin que de créer l’URL suivante:</span><span class="sxs-lookup"><span data-stu-id="6da9b-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="6da9b-183">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="6da9b-183">Request parameters</span></span>

<span data-ttu-id="6da9b-184">Name</span><span class="sxs-lookup"><span data-stu-id="6da9b-184">Name</span></span>          | <span data-ttu-id="6da9b-185">Dans</span><span class="sxs-lookup"><span data-stu-id="6da9b-185">In</span></span>     | <span data-ttu-id="6da9b-186">Type</span><span class="sxs-lookup"><span data-stu-id="6da9b-186">Type</span></span>   | <span data-ttu-id="6da9b-187">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="6da9b-187">Required</span></span> | <span data-ttu-id="6da9b-188">Notes</span><span class="sxs-lookup"><span data-stu-id="6da9b-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6da9b-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6da9b-189">LOWER_ID</span></span>      | <span data-ttu-id="6da9b-190">URL</span><span class="sxs-lookup"><span data-stu-id="6da9b-190">URL</span></span>    | <span data-ttu-id="6da9b-191">string</span><span class="sxs-lookup"><span data-stu-id="6da9b-191">string</span></span> | <span data-ttu-id="6da9b-192">oui</span><span class="sxs-lookup"><span data-stu-id="6da9b-192">yes</span></span>      | <span data-ttu-id="6da9b-193">ID de package, minuscules</span><span class="sxs-lookup"><span data-stu-id="6da9b-193">The package ID, lowercase</span></span>
<span data-ttu-id="6da9b-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="6da9b-194">LOWER_VERSION</span></span> | <span data-ttu-id="6da9b-195">URL</span><span class="sxs-lookup"><span data-stu-id="6da9b-195">URL</span></span>    | <span data-ttu-id="6da9b-196">string</span><span class="sxs-lookup"><span data-stu-id="6da9b-196">string</span></span> | <span data-ttu-id="6da9b-197">oui</span><span class="sxs-lookup"><span data-stu-id="6da9b-197">yes</span></span>      | <span data-ttu-id="6da9b-198">Version du package, normalisée et en minuscules</span><span class="sxs-lookup"><span data-stu-id="6da9b-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="6da9b-199">`LOWER_ID` Et`LOWER_VERSION` sont en minuscules à l’aide des règles implémentées par. Méthode du [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) réseau.</span><span class="sxs-lookup"><span data-stu-id="6da9b-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="6da9b-200">Est `LOWER_VERSION` la version de package souhaitée normalisée à l’aide des [règles de normalisation](../concepts/package-versioning.md#normalized-version-numbers)de la version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="6da9b-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6da9b-201">Cela signifie que les métadonnées de build autorisées par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="6da9b-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="6da9b-202">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="6da9b-202">Response body</span></span>

<span data-ttu-id="6da9b-203">Si le package existe sur la source du package, un code d’état 200 est retourné.</span><span class="sxs-lookup"><span data-stu-id="6da9b-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="6da9b-204">Le corps de la réponse sera le manifeste du package, qui est le. NuSpec contenu dans le fichier. nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="6da9b-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="6da9b-205">Le fichier. NuSpec est un document XML.</span><span class="sxs-lookup"><span data-stu-id="6da9b-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="6da9b-206">Si le package n’existe pas sur la source du package, un code d’État 404 est retourné.</span><span class="sxs-lookup"><span data-stu-id="6da9b-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6da9b-207">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="6da9b-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="6da9b-208">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="6da9b-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
