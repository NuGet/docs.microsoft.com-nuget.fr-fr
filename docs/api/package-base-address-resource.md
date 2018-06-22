---
title: Contenu du package NuGet API
description: L’adresse de base du package est une interface simple pour extraire le package lui-même.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819175"
---
# <a name="package-content"></a><span data-ttu-id="d339c-103">Contenu du package</span><span class="sxs-lookup"><span data-stu-id="d339c-103">Package Content</span></span>

<span data-ttu-id="d339c-104">Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (le fichier .nupkg) à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="d339c-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="d339c-105">La ressource utilisée pour extraire le contenu du package est le `PackageBaseAddress` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d339c-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="d339c-106">Cette ressource permet également la découverte de toutes les versions d’un package répertorié ou non listées.</span><span class="sxs-lookup"><span data-stu-id="d339c-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="d339c-107">Cette ressource est communément soit « package adresse de base » ou « conteneur plat ».</span><span class="sxs-lookup"><span data-stu-id="d339c-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="d339c-108">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="d339c-108">Versioning</span></span>

<span data-ttu-id="d339c-109">Les éléments suivants `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="d339c-109">The following `@type` value is used:</span></span>

<span data-ttu-id="d339c-110">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="d339c-110">@type value</span></span>              | <span data-ttu-id="d339c-111">Notes</span><span class="sxs-lookup"><span data-stu-id="d339c-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="d339c-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="d339c-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="d339c-113">La version initiale</span><span class="sxs-lookup"><span data-stu-id="d339c-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d339c-114">URL de base</span><span class="sxs-lookup"><span data-stu-id="d339c-114">Base URL</span></span>

<span data-ttu-id="d339c-115">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur.</span><span class="sxs-lookup"><span data-stu-id="d339c-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="d339c-116">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="d339c-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d339c-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="d339c-117">HTTP methods</span></span>

<span data-ttu-id="d339c-118">Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d339c-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="d339c-119">Énumérer des versions de package</span><span class="sxs-lookup"><span data-stu-id="d339c-119">Enumerate package versions</span></span>

<span data-ttu-id="d339c-120">Si le client connaît un ID de package et souhaite découvrir qui package versions du package source disponible, le client peut construire une URL prévisible pour énumérer toutes les versions de package.</span><span class="sxs-lookup"><span data-stu-id="d339c-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="d339c-121">Cette liste doit être une « liste de répertoires » pour l’API de contenu de package indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d339c-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="d339c-122">Cette liste contient les deux versions de package répertoriés et non répertoriés.</span><span class="sxs-lookup"><span data-stu-id="d339c-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="d339c-123">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="d339c-123">Request parameters</span></span>

<span data-ttu-id="d339c-124">Name</span><span class="sxs-lookup"><span data-stu-id="d339c-124">Name</span></span>     | <span data-ttu-id="d339c-125">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="d339c-125">In</span></span>     | <span data-ttu-id="d339c-126">Type</span><span class="sxs-lookup"><span data-stu-id="d339c-126">Type</span></span>    | <span data-ttu-id="d339c-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="d339c-127">Required</span></span> | <span data-ttu-id="d339c-128">Notes</span><span class="sxs-lookup"><span data-stu-id="d339c-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="d339c-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d339c-129">LOWER_ID</span></span> | <span data-ttu-id="d339c-130">URL</span><span class="sxs-lookup"><span data-stu-id="d339c-130">URL</span></span>    | <span data-ttu-id="d339c-131">chaîne</span><span class="sxs-lookup"><span data-stu-id="d339c-131">string</span></span>  | <span data-ttu-id="d339c-132">oui</span><span class="sxs-lookup"><span data-stu-id="d339c-132">yes</span></span>      | <span data-ttu-id="d339c-133">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="d339c-133">The package ID, lowercase</span></span>

<span data-ttu-id="d339c-134">Le `LOWER_ID` valeur est l’ID de package souhaité minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="d339c-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="d339c-135">Réponse</span><span class="sxs-lookup"><span data-stu-id="d339c-135">Response</span></span>

<span data-ttu-id="d339c-136">Si la source du package n’a aucune version de l’ID de package fourni, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="d339c-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="d339c-137">Si la source du package a une ou plusieurs versions, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="d339c-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="d339c-138">Le corps de réponse est un objet JSON avec la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="d339c-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="d339c-139">Name</span><span class="sxs-lookup"><span data-stu-id="d339c-139">Name</span></span>     | <span data-ttu-id="d339c-140">Type</span><span class="sxs-lookup"><span data-stu-id="d339c-140">Type</span></span>             | <span data-ttu-id="d339c-141">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="d339c-141">Required</span></span> | <span data-ttu-id="d339c-142">Notes</span><span class="sxs-lookup"><span data-stu-id="d339c-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="d339c-143">versions</span><span class="sxs-lookup"><span data-stu-id="d339c-143">versions</span></span> | <span data-ttu-id="d339c-144">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="d339c-144">array of strings</span></span> | <span data-ttu-id="d339c-145">oui</span><span class="sxs-lookup"><span data-stu-id="d339c-145">yes</span></span>      | <span data-ttu-id="d339c-146">Le package ID disponibles</span><span class="sxs-lookup"><span data-stu-id="d339c-146">The package IDs available</span></span>

<span data-ttu-id="d339c-147">Les chaînes dans le `versions` tableau toutes les minuscules, [normalisée des chaînes de version de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d339c-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d339c-148">Les chaînes de version ne contiennent pas toutes les métadonnées de la build SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d339c-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="d339c-149">L’objectif est que les chaînes de version trouvées dans ce tableau peuvent être utilisés textuellement pour le `LOWER_VERSION` jetons situés dans les points de terminaison suivants.</span><span class="sxs-lookup"><span data-stu-id="d339c-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d339c-150">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d339c-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="d339c-151">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d339c-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="d339c-152">Télécharger le contenu du package (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="d339c-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="d339c-153">Si le client connaît un ID de package et la version et souhaite télécharger le contenu du package, ils doivent uniquement construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="d339c-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="d339c-154">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="d339c-154">Request parameters</span></span>

<span data-ttu-id="d339c-155">Name</span><span class="sxs-lookup"><span data-stu-id="d339c-155">Name</span></span>          | <span data-ttu-id="d339c-156">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="d339c-156">In</span></span>     | <span data-ttu-id="d339c-157">Type</span><span class="sxs-lookup"><span data-stu-id="d339c-157">Type</span></span>   | <span data-ttu-id="d339c-158">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="d339c-158">Required</span></span> | <span data-ttu-id="d339c-159">Notes</span><span class="sxs-lookup"><span data-stu-id="d339c-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d339c-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d339c-160">LOWER_ID</span></span>      | <span data-ttu-id="d339c-161">URL</span><span class="sxs-lookup"><span data-stu-id="d339c-161">URL</span></span>    | <span data-ttu-id="d339c-162">chaîne</span><span class="sxs-lookup"><span data-stu-id="d339c-162">string</span></span> | <span data-ttu-id="d339c-163">oui</span><span class="sxs-lookup"><span data-stu-id="d339c-163">yes</span></span>      | <span data-ttu-id="d339c-164">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="d339c-164">The package ID, lowercase</span></span>
<span data-ttu-id="d339c-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d339c-165">LOWER_VERSION</span></span> | <span data-ttu-id="d339c-166">URL</span><span class="sxs-lookup"><span data-stu-id="d339c-166">URL</span></span>    | <span data-ttu-id="d339c-167">chaîne</span><span class="sxs-lookup"><span data-stu-id="d339c-167">string</span></span> | <span data-ttu-id="d339c-168">oui</span><span class="sxs-lookup"><span data-stu-id="d339c-168">yes</span></span>      | <span data-ttu-id="d339c-169">La version du package, normalisé et minuscule</span><span class="sxs-lookup"><span data-stu-id="d339c-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d339c-170">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="d339c-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="d339c-171">Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d339c-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d339c-172">Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="d339c-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d339c-173">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="d339c-173">Response body</span></span>

<span data-ttu-id="d339c-174">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="d339c-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d339c-175">Le corps de réponse sera le contenu du package lui-même.</span><span class="sxs-lookup"><span data-stu-id="d339c-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="d339c-176">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="d339c-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d339c-177">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d339c-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="d339c-178">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d339c-178">Sample response</span></span>

<span data-ttu-id="d339c-179">Le flux binaire qui est la .nupkg pour Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="d339c-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="d339c-180">Télécharger le manifeste du package (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="d339c-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="d339c-181">Si le client connaît un ID de package et la version et souhaite télécharger le manifeste du package, ils doivent uniquement construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="d339c-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="d339c-182">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="d339c-182">Request parameters</span></span>

<span data-ttu-id="d339c-183">Name</span><span class="sxs-lookup"><span data-stu-id="d339c-183">Name</span></span>          | <span data-ttu-id="d339c-184">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="d339c-184">In</span></span>     | <span data-ttu-id="d339c-185">Type</span><span class="sxs-lookup"><span data-stu-id="d339c-185">Type</span></span>    | <span data-ttu-id="d339c-186">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="d339c-186">Required</span></span> | <span data-ttu-id="d339c-187">Notes</span><span class="sxs-lookup"><span data-stu-id="d339c-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="d339c-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="d339c-188">LOWER_ID</span></span>      | <span data-ttu-id="d339c-189">URL</span><span class="sxs-lookup"><span data-stu-id="d339c-189">URL</span></span>    | <span data-ttu-id="d339c-190">chaîne</span><span class="sxs-lookup"><span data-stu-id="d339c-190">string</span></span>  | <span data-ttu-id="d339c-191">oui</span><span class="sxs-lookup"><span data-stu-id="d339c-191">yes</span></span>      | <span data-ttu-id="d339c-192">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="d339c-192">The package ID, lowercase</span></span>
<span data-ttu-id="d339c-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="d339c-193">LOWER_VERSION</span></span> | <span data-ttu-id="d339c-194">URL</span><span class="sxs-lookup"><span data-stu-id="d339c-194">URL</span></span>    | <span data-ttu-id="d339c-195">entiers</span><span class="sxs-lookup"><span data-stu-id="d339c-195">integer</span></span> | <span data-ttu-id="d339c-196">oui</span><span class="sxs-lookup"><span data-stu-id="d339c-196">yes</span></span>      | <span data-ttu-id="d339c-197">La version du package, normalisé et minuscule</span><span class="sxs-lookup"><span data-stu-id="d339c-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="d339c-198">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="d339c-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="d339c-199">Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="d339c-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="d339c-200">Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="d339c-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="d339c-201">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="d339c-201">Response body</span></span>

<span data-ttu-id="d339c-202">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="d339c-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="d339c-203">Le corps de réponse sera le manifeste du package, qui est le .nuspec contenus dans le .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="d339c-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="d339c-204">Le .nuspec est un document XML.</span><span class="sxs-lookup"><span data-stu-id="d339c-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="d339c-205">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="d339c-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d339c-206">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d339c-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="d339c-207">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d339c-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
