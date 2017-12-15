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
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "L’adresse de base du package est une interface simple pour extraire le package lui-même."
keywords: "NuGet plats conteneur, adresse de base de package NuGet, NuGet nupkg API, les versions de package NuGet API, les API NuGet packages non listées, NuGet API téléchargement nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 756001ff7376a8dd8d66bd2136408e90e6a85d19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="package-content"></a><span data-ttu-id="c85f5-104">Contenu du package</span><span class="sxs-lookup"><span data-stu-id="c85f5-104">Package Content</span></span>

<span data-ttu-id="c85f5-105">Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (le fichier .nupkg) à l’aide de l’API V3.</span><span class="sxs-lookup"><span data-stu-id="c85f5-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="c85f5-106">La ressource utilisée pour extraire le contenu du package est le `PackageBaseAddress` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c85f5-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="c85f5-107">Cette ressource permet également la découverte de toutes les versions d’un package répertorié ou non listées.</span><span class="sxs-lookup"><span data-stu-id="c85f5-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="c85f5-108">Cette ressource est communément soit « package adresse de base » ou « conteneur plat ».</span><span class="sxs-lookup"><span data-stu-id="c85f5-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="c85f5-109">Versioning</span><span class="sxs-lookup"><span data-stu-id="c85f5-109">Versioning</span></span>

<span data-ttu-id="c85f5-110">Les éléments suivants `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="c85f5-110">The following `@type` value is used:</span></span>

<span data-ttu-id="c85f5-111">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="c85f5-111">@type value</span></span>              | <span data-ttu-id="c85f5-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="c85f5-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="c85f5-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="c85f5-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="c85f5-114">La version initiale</span><span class="sxs-lookup"><span data-stu-id="c85f5-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c85f5-115">URL de base</span><span class="sxs-lookup"><span data-stu-id="c85f5-115">Base URL</span></span>

<span data-ttu-id="c85f5-116">L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur.</span><span class="sxs-lookup"><span data-stu-id="c85f5-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="c85f5-117">Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="c85f5-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c85f5-118">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="c85f5-118">HTTP methods</span></span>

<span data-ttu-id="c85f5-119">Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="c85f5-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="c85f5-120">Énumérer des versions de package</span><span class="sxs-lookup"><span data-stu-id="c85f5-120">Enumerate package versions</span></span>

<span data-ttu-id="c85f5-121">Si le client connaît un ID de package et souhaite découvrir qui package versions du package source disponible, le client peut construire une URL prévisible pour énumérer toutes les versions de package.</span><span class="sxs-lookup"><span data-stu-id="c85f5-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="c85f5-122">Cette liste doit être une « liste de répertoires » pour l’API de contenu de package indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c85f5-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="c85f5-123">Cette liste contient les deux versions de package répertoriés et non répertoriés.</span><span class="sxs-lookup"><span data-stu-id="c85f5-123">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="c85f5-124">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="c85f5-124">Request parameters</span></span>

<span data-ttu-id="c85f5-125">Nom</span><span class="sxs-lookup"><span data-stu-id="c85f5-125">Name</span></span>     | <span data-ttu-id="c85f5-126">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="c85f5-126">In</span></span>     | <span data-ttu-id="c85f5-127">Type</span><span class="sxs-lookup"><span data-stu-id="c85f5-127">Type</span></span>    | <span data-ttu-id="c85f5-128">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="c85f5-128">Required</span></span> | <span data-ttu-id="c85f5-129">Remarques</span><span class="sxs-lookup"><span data-stu-id="c85f5-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="c85f5-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="c85f5-130">LOWER_ID</span></span> | <span data-ttu-id="c85f5-131">URL</span><span class="sxs-lookup"><span data-stu-id="c85f5-131">URL</span></span>    | <span data-ttu-id="c85f5-132">chaîne</span><span class="sxs-lookup"><span data-stu-id="c85f5-132">string</span></span>  | <span data-ttu-id="c85f5-133">oui</span><span class="sxs-lookup"><span data-stu-id="c85f5-133">yes</span></span>      | <span data-ttu-id="c85f5-134">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="c85f5-134">The package ID, lowercase</span></span>

<span data-ttu-id="c85f5-135">Le `LOWER_ID` valeur est l’ID de package souhaité minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="c85f5-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) method.</span></span>

### <a name="response"></a><span data-ttu-id="c85f5-136">Réponse</span><span class="sxs-lookup"><span data-stu-id="c85f5-136">Response</span></span>

<span data-ttu-id="c85f5-137">Si la source du package n’a aucune version de l’ID de package fourni, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="c85f5-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="c85f5-138">Si la source du package a une ou plusieurs versions, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="c85f5-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="c85f5-139">Le corps de réponse est un objet JSON avec la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="c85f5-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="c85f5-140">Nom</span><span class="sxs-lookup"><span data-stu-id="c85f5-140">Name</span></span>     | <span data-ttu-id="c85f5-141">Type</span><span class="sxs-lookup"><span data-stu-id="c85f5-141">Type</span></span>             | <span data-ttu-id="c85f5-142">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="c85f5-142">Required</span></span> | <span data-ttu-id="c85f5-143">Remarques</span><span class="sxs-lookup"><span data-stu-id="c85f5-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="c85f5-144">versions</span><span class="sxs-lookup"><span data-stu-id="c85f5-144">versions</span></span> | <span data-ttu-id="c85f5-145">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="c85f5-145">array of strings</span></span> | <span data-ttu-id="c85f5-146">oui</span><span class="sxs-lookup"><span data-stu-id="c85f5-146">yes</span></span>      | <span data-ttu-id="c85f5-147">Le package ID disponibles</span><span class="sxs-lookup"><span data-stu-id="c85f5-147">The package IDs available</span></span>

<span data-ttu-id="c85f5-148">Les chaînes dans le `versions` tableau toutes les minuscules, [normalisée des chaînes de version de NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c85f5-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="c85f5-149">Les chaînes de version ne contiennent pas toutes les métadonnées de la build SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="c85f5-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="c85f5-150">L’objectif est que les chaînes de version trouvées dans ce tableau peuvent être utilisés textuellement pour le `LOWER_VERSION` jetons situés dans les points de terminaison suivants.</span><span class="sxs-lookup"><span data-stu-id="c85f5-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c85f5-151">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="c85f5-151">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="c85f5-152">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="c85f5-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="c85f5-153">Télécharger le contenu du package (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="c85f5-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="c85f5-154">Si le client connaît un ID de package et la version et souhaite télécharger le contenu du package, ils doivent uniquement construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="c85f5-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="c85f5-155">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="c85f5-155">Request parameters</span></span>

<span data-ttu-id="c85f5-156">Nom</span><span class="sxs-lookup"><span data-stu-id="c85f5-156">Name</span></span>          | <span data-ttu-id="c85f5-157">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="c85f5-157">In</span></span>     | <span data-ttu-id="c85f5-158">Type</span><span class="sxs-lookup"><span data-stu-id="c85f5-158">Type</span></span>   | <span data-ttu-id="c85f5-159">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="c85f5-159">Required</span></span> | <span data-ttu-id="c85f5-160">Remarques</span><span class="sxs-lookup"><span data-stu-id="c85f5-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c85f5-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="c85f5-161">LOWER_ID</span></span>      | <span data-ttu-id="c85f5-162">URL</span><span class="sxs-lookup"><span data-stu-id="c85f5-162">URL</span></span>    | <span data-ttu-id="c85f5-163">chaîne</span><span class="sxs-lookup"><span data-stu-id="c85f5-163">string</span></span> | <span data-ttu-id="c85f5-164">oui</span><span class="sxs-lookup"><span data-stu-id="c85f5-164">yes</span></span>      | <span data-ttu-id="c85f5-165">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="c85f5-165">The package ID, lowercase</span></span>
<span data-ttu-id="c85f5-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="c85f5-166">LOWER_VERSION</span></span> | <span data-ttu-id="c85f5-167">URL</span><span class="sxs-lookup"><span data-stu-id="c85f5-167">URL</span></span>    | <span data-ttu-id="c85f5-168">chaîne</span><span class="sxs-lookup"><span data-stu-id="c85f5-168">string</span></span> | <span data-ttu-id="c85f5-169">oui</span><span class="sxs-lookup"><span data-stu-id="c85f5-169">yes</span></span>      | <span data-ttu-id="c85f5-170">La version du package, normalisé et minuscule</span><span class="sxs-lookup"><span data-stu-id="c85f5-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="c85f5-171">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="c85f5-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) method.</span></span>

<span data-ttu-id="c85f5-172">Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c85f5-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="c85f5-173">Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="c85f5-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="c85f5-174">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="c85f5-174">Response body</span></span>

<span data-ttu-id="c85f5-175">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="c85f5-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="c85f5-176">Le corps de réponse sera le contenu du package lui-même.</span><span class="sxs-lookup"><span data-stu-id="c85f5-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="c85f5-177">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="c85f5-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c85f5-178">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="c85f5-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="c85f5-179">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="c85f5-179">Sample response</span></span>

<span data-ttu-id="c85f5-180">Le flux binaire qui est la .nupkg pour Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="c85f5-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="c85f5-181">Télécharger le manifeste du package (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="c85f5-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="c85f5-182">Si le client connaît un ID de package et la version et souhaite télécharger le manifeste du package, ils doivent uniquement construire l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="c85f5-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="c85f5-183">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="c85f5-183">Request parameters</span></span>

<span data-ttu-id="c85f5-184">Nom</span><span class="sxs-lookup"><span data-stu-id="c85f5-184">Name</span></span>          | <span data-ttu-id="c85f5-185">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="c85f5-185">In</span></span>     | <span data-ttu-id="c85f5-186">Type</span><span class="sxs-lookup"><span data-stu-id="c85f5-186">Type</span></span>    | <span data-ttu-id="c85f5-187">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="c85f5-187">Required</span></span> | <span data-ttu-id="c85f5-188">Remarques</span><span class="sxs-lookup"><span data-stu-id="c85f5-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="c85f5-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="c85f5-189">LOWER_ID</span></span>      | <span data-ttu-id="c85f5-190">URL</span><span class="sxs-lookup"><span data-stu-id="c85f5-190">URL</span></span>    | <span data-ttu-id="c85f5-191">chaîne</span><span class="sxs-lookup"><span data-stu-id="c85f5-191">string</span></span>  | <span data-ttu-id="c85f5-192">oui</span><span class="sxs-lookup"><span data-stu-id="c85f5-192">yes</span></span>      | <span data-ttu-id="c85f5-193">L’ID de package, en minuscules</span><span class="sxs-lookup"><span data-stu-id="c85f5-193">The package ID, lowercase</span></span>
<span data-ttu-id="c85f5-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="c85f5-194">LOWER_VERSION</span></span> | <span data-ttu-id="c85f5-195">URL</span><span class="sxs-lookup"><span data-stu-id="c85f5-195">URL</span></span>    | <span data-ttu-id="c85f5-196">entiers</span><span class="sxs-lookup"><span data-stu-id="c85f5-196">integer</span></span> | <span data-ttu-id="c85f5-197">oui</span><span class="sxs-lookup"><span data-stu-id="c85f5-197">yes</span></span>      | <span data-ttu-id="c85f5-198">La version du package, normalisé et minuscule</span><span class="sxs-lookup"><span data-stu-id="c85f5-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="c85f5-199">Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="c85f5-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) method.</span></span>

<span data-ttu-id="c85f5-200">Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c85f5-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="c85f5-201">Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="c85f5-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="c85f5-202">Corps de réponse</span><span class="sxs-lookup"><span data-stu-id="c85f5-202">Response body</span></span>

<span data-ttu-id="c85f5-203">Si le package existe sur la source du package, un code de 200 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="c85f5-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="c85f5-204">Le corps de réponse sera le manifeste du package, qui est le .nuspec contenus dans le .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="c85f5-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="c85f5-205">Le .nuspec est un document XML.</span><span class="sxs-lookup"><span data-stu-id="c85f5-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="c85f5-206">Si le package n’existe pas sur la source du package, un code de 404 état est retourné.</span><span class="sxs-lookup"><span data-stu-id="c85f5-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c85f5-207">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="c85f5-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="c85f5-208">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="c85f5-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
