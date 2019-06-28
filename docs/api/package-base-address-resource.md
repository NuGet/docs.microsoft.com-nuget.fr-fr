---
title: Contenu du package, NuGet API
description: L’adresse de base du package est une interface simple pour récupérer le package lui-même.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426766"
---
# <a name="package-content"></a><span data-ttu-id="9f9d0-103">Contenu du package</span><span class="sxs-lookup"><span data-stu-id="9f9d0-103">Package Content</span></span>

<span data-ttu-id="9f9d0-104">Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (le fichier .nupkg) à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="9f9d0-105">La ressource utilisée pour extraire le contenu du package est le `PackageBaseAddress` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9f9d0-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="9f9d0-106">Cette ressource permet également de détecter toutes les versions d’un package répertorié ou non répertoriée.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="9f9d0-107">Cette ressource est communément soit « package adresse de base » ou « conteneur plat ».</span><span class="sxs-lookup"><span data-stu-id="9f9d0-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="9f9d0-108">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="9f9d0-108">Versioning</span></span>

<span data-ttu-id="9f9d0-109">Ce qui suit `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="9f9d0-109">The following `@type` value is used:</span></span>

<span data-ttu-id="9f9d0-110">Valeur@type</span><span class="sxs-lookup"><span data-stu-id="9f9d0-110">@type value</span></span>              | <span data-ttu-id="9f9d0-111">Notes</span><span class="sxs-lookup"><span data-stu-id="9f9d0-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="9f9d0-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="9f9d0-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="9f9d0-113">La version initiale</span><span class="sxs-lookup"><span data-stu-id="9f9d0-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="9f9d0-114">URL de base</span><span class="sxs-lookup"><span data-stu-id="9f9d0-114">Base URL</span></span>

<span data-ttu-id="9f9d0-115">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="9f9d0-116">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9f9d0-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="9f9d0-117">HTTP methods</span></span>

<span data-ttu-id="9f9d0-118">Toutes les URL trouvés dans la prise en charge de la ressource d’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="9f9d0-119">Énumérer les versions de package</span><span class="sxs-lookup"><span data-stu-id="9f9d0-119">Enumerate package versions</span></span>

<span data-ttu-id="9f9d0-120">Si le client connaît un ID de package et qu’il souhaite découvrir que le package auquel les versions du package source disponible, le client peut construire une URL prévisible pour énumérer toutes les versions de package.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="9f9d0-121">Cette liste est destinée à être une « liste de répertoires » pour l’API de contenu de package indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="9f9d0-122">Cette liste contient les deux versions de package répertoriés et non répertoriés.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="9f9d0-123">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="9f9d0-123">Request parameters</span></span>

<span data-ttu-id="9f9d0-124">Nom</span><span class="sxs-lookup"><span data-stu-id="9f9d0-124">Name</span></span>     | <span data-ttu-id="9f9d0-125">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="9f9d0-125">In</span></span>     | <span data-ttu-id="9f9d0-126">Type</span><span class="sxs-lookup"><span data-stu-id="9f9d0-126">Type</span></span>    | <span data-ttu-id="9f9d0-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9f9d0-127">Required</span></span> | <span data-ttu-id="9f9d0-128">Notes</span><span class="sxs-lookup"><span data-stu-id="9f9d0-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="9f9d0-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="9f9d0-129">LOWER_ID</span></span> | <span data-ttu-id="9f9d0-130">URL</span><span class="sxs-lookup"><span data-stu-id="9f9d0-130">URL</span></span>    | <span data-ttu-id="9f9d0-131">string</span><span class="sxs-lookup"><span data-stu-id="9f9d0-131">string</span></span>  | <span data-ttu-id="9f9d0-132">oui</span><span class="sxs-lookup"><span data-stu-id="9f9d0-132">yes</span></span>      | <span data-ttu-id="9f9d0-133">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="9f9d0-133">The package ID, lowercase</span></span>

<span data-ttu-id="9f9d0-134">Le `LOWER_ID` valeur est l’ID de package souhaité minuscule en utilisant les règles implémentées par. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="9f9d0-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="9f9d0-135">Réponse</span><span class="sxs-lookup"><span data-stu-id="9f9d0-135">Response</span></span>

<span data-ttu-id="9f9d0-136">Si la source du package n’existe aucune version de l’ID de package fourni, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="9f9d0-137">Si la source du package a une ou plusieurs versions, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="9f9d0-138">Le corps de réponse est un objet JSON avec la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="9f9d0-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="9f9d0-139">Nom</span><span class="sxs-lookup"><span data-stu-id="9f9d0-139">Name</span></span>     | <span data-ttu-id="9f9d0-140">Type</span><span class="sxs-lookup"><span data-stu-id="9f9d0-140">Type</span></span>             | <span data-ttu-id="9f9d0-141">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9f9d0-141">Required</span></span> | <span data-ttu-id="9f9d0-142">Notes</span><span class="sxs-lookup"><span data-stu-id="9f9d0-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="9f9d0-143">versions</span><span class="sxs-lookup"><span data-stu-id="9f9d0-143">versions</span></span> | <span data-ttu-id="9f9d0-144">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="9f9d0-144">array of strings</span></span> | <span data-ttu-id="9f9d0-145">oui</span><span class="sxs-lookup"><span data-stu-id="9f9d0-145">yes</span></span>      | <span data-ttu-id="9f9d0-146">Le package d’ID disponibles</span><span class="sxs-lookup"><span data-stu-id="9f9d0-146">The package IDs available</span></span>

<span data-ttu-id="9f9d0-147">Les chaînes dans le `versions` tableau toutes les minuscules, [normalisée des chaînes de version de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="9f9d0-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="9f9d0-148">Les chaînes de version ne contiennent pas toutes les métadonnées de build de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="9f9d0-149">L’objectif est que les chaînes de version trouvés dans ce tableau peuvent être utilisés textuellement pour le `LOWER_VERSION` jetons trouvés dans les points de terminaison suivants.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9f9d0-150">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="9f9d0-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="9f9d0-151">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="9f9d0-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="9f9d0-152">Télécharger le contenu du package (fichier .nupkg)</span><span class="sxs-lookup"><span data-stu-id="9f9d0-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="9f9d0-153">Si le client connaît un ID de package et une version et souhaite télécharger le contenu du package, il suffit de construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="9f9d0-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="9f9d0-154">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="9f9d0-154">Request parameters</span></span>

<span data-ttu-id="9f9d0-155">Nom</span><span class="sxs-lookup"><span data-stu-id="9f9d0-155">Name</span></span>          | <span data-ttu-id="9f9d0-156">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="9f9d0-156">In</span></span>     | <span data-ttu-id="9f9d0-157">Type</span><span class="sxs-lookup"><span data-stu-id="9f9d0-157">Type</span></span>   | <span data-ttu-id="9f9d0-158">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9f9d0-158">Required</span></span> | <span data-ttu-id="9f9d0-159">Notes</span><span class="sxs-lookup"><span data-stu-id="9f9d0-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9f9d0-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="9f9d0-160">LOWER_ID</span></span>      | <span data-ttu-id="9f9d0-161">URL</span><span class="sxs-lookup"><span data-stu-id="9f9d0-161">URL</span></span>    | <span data-ttu-id="9f9d0-162">string</span><span class="sxs-lookup"><span data-stu-id="9f9d0-162">string</span></span> | <span data-ttu-id="9f9d0-163">oui</span><span class="sxs-lookup"><span data-stu-id="9f9d0-163">yes</span></span>      | <span data-ttu-id="9f9d0-164">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="9f9d0-164">The package ID, lowercase</span></span>
<span data-ttu-id="9f9d0-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="9f9d0-165">LOWER_VERSION</span></span> | <span data-ttu-id="9f9d0-166">URL</span><span class="sxs-lookup"><span data-stu-id="9f9d0-166">URL</span></span>    | <span data-ttu-id="9f9d0-167">string</span><span class="sxs-lookup"><span data-stu-id="9f9d0-167">string</span></span> | <span data-ttu-id="9f9d0-168">oui</span><span class="sxs-lookup"><span data-stu-id="9f9d0-168">yes</span></span>      | <span data-ttu-id="9f9d0-169">La version du package, normalisées et minuscule</span><span class="sxs-lookup"><span data-stu-id="9f9d0-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="9f9d0-170">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="9f9d0-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="9f9d0-171">.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-171">method.</span></span>

<span data-ttu-id="9f9d0-172">Le `LOWER_VERSION` est la version du package souhaité normalisée à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="9f9d0-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="9f9d0-173">Cela signifie que les métadonnées de build sont autorisée par la spécification de SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="9f9d0-174">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="9f9d0-174">Response body</span></span>

<span data-ttu-id="9f9d0-175">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="9f9d0-176">Le corps de réponse sera le contenu du package lui-même.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="9f9d0-177">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9f9d0-178">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="9f9d0-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="9f9d0-179">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="9f9d0-179">Sample response</span></span>

<span data-ttu-id="9f9d0-180">Le flux binaire qui est le fichier .nupkg pour Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="9f9d0-181">Télécharger le manifeste de package (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="9f9d0-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="9f9d0-182">Si le client connaît un ID de package et une version et souhaite télécharger le manifeste du package, il suffit de construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="9f9d0-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="9f9d0-183">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="9f9d0-183">Request parameters</span></span>

<span data-ttu-id="9f9d0-184">Nom</span><span class="sxs-lookup"><span data-stu-id="9f9d0-184">Name</span></span>          | <span data-ttu-id="9f9d0-185">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="9f9d0-185">In</span></span>     | <span data-ttu-id="9f9d0-186">Type</span><span class="sxs-lookup"><span data-stu-id="9f9d0-186">Type</span></span>   | <span data-ttu-id="9f9d0-187">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9f9d0-187">Required</span></span> | <span data-ttu-id="9f9d0-188">Notes</span><span class="sxs-lookup"><span data-stu-id="9f9d0-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9f9d0-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="9f9d0-189">LOWER_ID</span></span>      | <span data-ttu-id="9f9d0-190">URL</span><span class="sxs-lookup"><span data-stu-id="9f9d0-190">URL</span></span>    | <span data-ttu-id="9f9d0-191">string</span><span class="sxs-lookup"><span data-stu-id="9f9d0-191">string</span></span> | <span data-ttu-id="9f9d0-192">oui</span><span class="sxs-lookup"><span data-stu-id="9f9d0-192">yes</span></span>      | <span data-ttu-id="9f9d0-193">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="9f9d0-193">The package ID, lowercase</span></span>
<span data-ttu-id="9f9d0-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="9f9d0-194">LOWER_VERSION</span></span> | <span data-ttu-id="9f9d0-195">URL</span><span class="sxs-lookup"><span data-stu-id="9f9d0-195">URL</span></span>    | <span data-ttu-id="9f9d0-196">string</span><span class="sxs-lookup"><span data-stu-id="9f9d0-196">string</span></span> | <span data-ttu-id="9f9d0-197">oui</span><span class="sxs-lookup"><span data-stu-id="9f9d0-197">yes</span></span>      | <span data-ttu-id="9f9d0-198">La version du package, normalisées et minuscule</span><span class="sxs-lookup"><span data-stu-id="9f9d0-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="9f9d0-199">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="9f9d0-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="9f9d0-200">Le `LOWER_VERSION` est la version du package souhaité normalisée à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="9f9d0-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="9f9d0-201">Cela signifie que les métadonnées de build sont autorisée par la spécification de SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="9f9d0-202">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="9f9d0-202">Response body</span></span>

<span data-ttu-id="9f9d0-203">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="9f9d0-204">Le corps de réponse sera le manifeste du package, qui est le fichier .nuspec contenus dans le fichier .nupkg correspondante.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="9f9d0-205">Le fichier .nuspec est un document XML.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="9f9d0-206">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="9f9d0-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9f9d0-207">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="9f9d0-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="9f9d0-208">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="9f9d0-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
