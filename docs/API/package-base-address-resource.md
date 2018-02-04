---
title: Package NuGet API, le contenu | Documents Microsoft
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
description: "L’adresse de base du package est une interface simple pour extraire le package lui-même."
keywords: "NuGet plats conteneur, adresse de base de package NuGet, NuGet nupkg API, les versions de package NuGet API, les API NuGet packages non listées, NuGet API téléchargement nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="891d2-104">Contenu du package</span><span class="sxs-lookup"><span data-stu-id="891d2-104">Package Content</span></span>

<span data-ttu-id="891d2-105">Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (le fichier .nupkg) à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="891d2-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="891d2-106">La ressource utilisée pour extraire le contenu du package est le `PackageBaseAddress` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="891d2-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="891d2-107">Cette ressource permet également la découverte de toutes les versions d’un package répertorié ou non listées.</span><span class="sxs-lookup"><span data-stu-id="891d2-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="891d2-108">Cette ressource est communément soit « package adresse de base » ou « conteneur plat ».</span><span class="sxs-lookup"><span data-stu-id="891d2-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="891d2-109">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="891d2-109">Versioning</span></span>

<span data-ttu-id="891d2-110">Les éléments suivants `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="891d2-110">The following `@type` value is used:</span></span>

<span data-ttu-id="891d2-111">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="891d2-111">@type value</span></span>              | <span data-ttu-id="891d2-112">Notes</span><span class="sxs-lookup"><span data-stu-id="891d2-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="891d2-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="891d2-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="891d2-114">La version initiale</span><span class="sxs-lookup"><span data-stu-id="891d2-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="891d2-115">URL de base</span><span class="sxs-lookup"><span data-stu-id="891d2-115">Base URL</span></span>

<span data-ttu-id="891d2-116">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur.</span><span class="sxs-lookup"><span data-stu-id="891d2-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="891d2-117">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="891d2-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="891d2-118">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="891d2-118">HTTP methods</span></span>

<span data-ttu-id="891d2-119">Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="891d2-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="891d2-120">Énumérer des versions de package</span><span class="sxs-lookup"><span data-stu-id="891d2-120">Enumerate package versions</span></span>

<span data-ttu-id="891d2-121">Si le client connaît un ID de package et souhaite découvrir qui package versions du package source disponible, le client peut construire une URL prévisible pour énumérer toutes les versions de package.</span><span class="sxs-lookup"><span data-stu-id="891d2-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="891d2-122">Cette liste doit être une « liste de répertoires » pour l’API de contenu de package indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="891d2-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="891d2-123">Cette liste contient les deux versions de package répertoriés et non répertoriés.</span><span class="sxs-lookup"><span data-stu-id="891d2-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="891d2-124">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="891d2-124">Request parameters</span></span>

<span data-ttu-id="891d2-125">Name</span><span class="sxs-lookup"><span data-stu-id="891d2-125">Name</span></span>     | <span data-ttu-id="891d2-126">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="891d2-126">In</span></span>     | <span data-ttu-id="891d2-127">Type</span><span class="sxs-lookup"><span data-stu-id="891d2-127">Type</span></span>    | <span data-ttu-id="891d2-128">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="891d2-128">Required</span></span> | <span data-ttu-id="891d2-129">Notes</span><span class="sxs-lookup"><span data-stu-id="891d2-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="891d2-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="891d2-130">LOWER_ID</span></span> | <span data-ttu-id="891d2-131">URL</span><span class="sxs-lookup"><span data-stu-id="891d2-131">URL</span></span>    | <span data-ttu-id="891d2-132">chaîne</span><span class="sxs-lookup"><span data-stu-id="891d2-132">string</span></span>  | <span data-ttu-id="891d2-133">oui</span><span class="sxs-lookup"><span data-stu-id="891d2-133">yes</span></span>      | <span data-ttu-id="891d2-134">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="891d2-134">The package ID, lowercase</span></span>

<span data-ttu-id="891d2-135">Le `LOWER_ID` valeur est l’ID de package souhaité minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="891d2-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="891d2-136">Réponse</span><span class="sxs-lookup"><span data-stu-id="891d2-136">Response</span></span>

<span data-ttu-id="891d2-137">Si la source du package n’a aucune version de l’ID de package fourni, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="891d2-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="891d2-138">Si la source du package a une ou plusieurs versions, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="891d2-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="891d2-139">Le corps de réponse est un objet JSON avec la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="891d2-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="891d2-140">Name</span><span class="sxs-lookup"><span data-stu-id="891d2-140">Name</span></span>     | <span data-ttu-id="891d2-141">Type</span><span class="sxs-lookup"><span data-stu-id="891d2-141">Type</span></span>             | <span data-ttu-id="891d2-142">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="891d2-142">Required</span></span> | <span data-ttu-id="891d2-143">Notes</span><span class="sxs-lookup"><span data-stu-id="891d2-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="891d2-144">versions</span><span class="sxs-lookup"><span data-stu-id="891d2-144">versions</span></span> | <span data-ttu-id="891d2-145">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="891d2-145">array of strings</span></span> | <span data-ttu-id="891d2-146">oui</span><span class="sxs-lookup"><span data-stu-id="891d2-146">yes</span></span>      | <span data-ttu-id="891d2-147">Le package ID disponibles</span><span class="sxs-lookup"><span data-stu-id="891d2-147">The package IDs available</span></span>

<span data-ttu-id="891d2-148">Les chaînes dans le `versions` tableau toutes les minuscules, [normalisée des chaînes de version de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="891d2-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="891d2-149">Les chaînes de version ne contiennent pas toutes les métadonnées de la build SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="891d2-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="891d2-150">L’objectif est que les chaînes de version trouvées dans ce tableau peuvent être utilisés textuellement pour le `LOWER_VERSION` jetons situés dans les points de terminaison suivants.</span><span class="sxs-lookup"><span data-stu-id="891d2-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="891d2-151">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="891d2-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="891d2-152">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="891d2-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="891d2-153">Télécharger le contenu du package (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="891d2-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="891d2-154">Si le client connaît un ID de package et la version et souhaite télécharger le contenu du package, ils doivent uniquement construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="891d2-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="891d2-155">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="891d2-155">Request parameters</span></span>

<span data-ttu-id="891d2-156">Name</span><span class="sxs-lookup"><span data-stu-id="891d2-156">Name</span></span>          | <span data-ttu-id="891d2-157">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="891d2-157">In</span></span>     | <span data-ttu-id="891d2-158">Type</span><span class="sxs-lookup"><span data-stu-id="891d2-158">Type</span></span>   | <span data-ttu-id="891d2-159">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="891d2-159">Required</span></span> | <span data-ttu-id="891d2-160">Notes</span><span class="sxs-lookup"><span data-stu-id="891d2-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="891d2-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="891d2-161">LOWER_ID</span></span>      | <span data-ttu-id="891d2-162">URL</span><span class="sxs-lookup"><span data-stu-id="891d2-162">URL</span></span>    | <span data-ttu-id="891d2-163">chaîne</span><span class="sxs-lookup"><span data-stu-id="891d2-163">string</span></span> | <span data-ttu-id="891d2-164">oui</span><span class="sxs-lookup"><span data-stu-id="891d2-164">yes</span></span>      | <span data-ttu-id="891d2-165">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="891d2-165">The package ID, lowercase</span></span>
<span data-ttu-id="891d2-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="891d2-166">LOWER_VERSION</span></span> | <span data-ttu-id="891d2-167">URL</span><span class="sxs-lookup"><span data-stu-id="891d2-167">URL</span></span>    | <span data-ttu-id="891d2-168">chaîne</span><span class="sxs-lookup"><span data-stu-id="891d2-168">string</span></span> | <span data-ttu-id="891d2-169">oui</span><span class="sxs-lookup"><span data-stu-id="891d2-169">yes</span></span>      | <span data-ttu-id="891d2-170">La version du package, normalisé et minuscule</span><span class="sxs-lookup"><span data-stu-id="891d2-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="891d2-171">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="891d2-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="891d2-172">Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="891d2-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="891d2-173">Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="891d2-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="891d2-174">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="891d2-174">Response body</span></span>

<span data-ttu-id="891d2-175">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="891d2-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="891d2-176">Le corps de réponse sera le contenu du package lui-même.</span><span class="sxs-lookup"><span data-stu-id="891d2-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="891d2-177">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="891d2-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="891d2-178">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="891d2-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="891d2-179">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="891d2-179">Sample response</span></span>

<span data-ttu-id="891d2-180">Le flux binaire qui est la .nupkg pour Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="891d2-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="891d2-181">Télécharger le manifeste du package (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="891d2-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="891d2-182">Si le client connaît un ID de package et la version et souhaite télécharger le manifeste du package, ils doivent uniquement construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="891d2-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="891d2-183">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="891d2-183">Request parameters</span></span>

<span data-ttu-id="891d2-184">Name</span><span class="sxs-lookup"><span data-stu-id="891d2-184">Name</span></span>          | <span data-ttu-id="891d2-185">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="891d2-185">In</span></span>     | <span data-ttu-id="891d2-186">Type</span><span class="sxs-lookup"><span data-stu-id="891d2-186">Type</span></span>    | <span data-ttu-id="891d2-187">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="891d2-187">Required</span></span> | <span data-ttu-id="891d2-188">Notes</span><span class="sxs-lookup"><span data-stu-id="891d2-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="891d2-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="891d2-189">LOWER_ID</span></span>      | <span data-ttu-id="891d2-190">URL</span><span class="sxs-lookup"><span data-stu-id="891d2-190">URL</span></span>    | <span data-ttu-id="891d2-191">chaîne</span><span class="sxs-lookup"><span data-stu-id="891d2-191">string</span></span>  | <span data-ttu-id="891d2-192">oui</span><span class="sxs-lookup"><span data-stu-id="891d2-192">yes</span></span>      | <span data-ttu-id="891d2-193">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="891d2-193">The package ID, lowercase</span></span>
<span data-ttu-id="891d2-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="891d2-194">LOWER_VERSION</span></span> | <span data-ttu-id="891d2-195">URL</span><span class="sxs-lookup"><span data-stu-id="891d2-195">URL</span></span>    | <span data-ttu-id="891d2-196">entiers</span><span class="sxs-lookup"><span data-stu-id="891d2-196">integer</span></span> | <span data-ttu-id="891d2-197">oui</span><span class="sxs-lookup"><span data-stu-id="891d2-197">yes</span></span>      | <span data-ttu-id="891d2-198">La version du package, normalisé et minuscule</span><span class="sxs-lookup"><span data-stu-id="891d2-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="891d2-199">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).</span><span class="sxs-lookup"><span data-stu-id="891d2-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="891d2-200">Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="891d2-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="891d2-201">Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="891d2-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="891d2-202">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="891d2-202">Response body</span></span>

<span data-ttu-id="891d2-203">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="891d2-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="891d2-204">Le corps de réponse sera le manifeste du package, qui est le .nuspec contenus dans le .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="891d2-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="891d2-205">Le .nuspec est un document XML.</span><span class="sxs-lookup"><span data-stu-id="891d2-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="891d2-206">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="891d2-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="891d2-207">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="891d2-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="891d2-208">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="891d2-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
