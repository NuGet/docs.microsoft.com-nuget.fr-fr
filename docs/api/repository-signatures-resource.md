---
title: Signatures de référentiel, API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La ressource de signatures de référentiels permet aux sources de package de clients d’annoncer leurs fonctionnalités de signature de référentiel.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775331"
---
# <a name="repository-signatures"></a><span data-ttu-id="667da-103">Signatures de dépôt</span><span class="sxs-lookup"><span data-stu-id="667da-103">Repository signatures</span></span>

<span data-ttu-id="667da-104">Si une source de package prend en charge l’ajout de signatures de référentiel aux packages publiés, un client peut déterminer les certificats de signature utilisés par la source du package.</span><span class="sxs-lookup"><span data-stu-id="667da-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="667da-105">Cette ressource permet aux clients de détecter si un package signé de référentiel a été falsifié ou s’il dispose d’un certificat de signature inattendu.</span><span class="sxs-lookup"><span data-stu-id="667da-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="667da-106">La ressource utilisée pour récupérer ces informations de signature de référentiel est la `RepositorySignatures` ressource trouvée dans l' [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="667da-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="667da-107">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="667da-107">Versioning</span></span>

<span data-ttu-id="667da-108">La `@type` valeur suivante est utilisée :</span><span class="sxs-lookup"><span data-stu-id="667da-108">The following `@type` value is used:</span></span>

<span data-ttu-id="667da-109">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="667da-109">@type value</span></span>                | <span data-ttu-id="667da-110">Notes</span><span class="sxs-lookup"><span data-stu-id="667da-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="667da-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="667da-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="667da-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="667da-112">The initial release</span></span>
<span data-ttu-id="667da-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="667da-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="667da-114">Pris en charge par les clients NuGet v 4.9 +</span><span class="sxs-lookup"><span data-stu-id="667da-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="667da-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="667da-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="667da-116">Autorise l’activation de `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="667da-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="667da-117">Pris en charge par les clients NuGet v 5.0 +</span><span class="sxs-lookup"><span data-stu-id="667da-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="667da-118">URL de base</span><span class="sxs-lookup"><span data-stu-id="667da-118">Base URL</span></span>

<span data-ttu-id="667da-119">L’URL du point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la valeur de ressource mentionnée ci-dessus `@type` .</span><span class="sxs-lookup"><span data-stu-id="667da-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="667da-120">Cette rubrique utilise l’URL de l’espace réservé `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="667da-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="667da-121">Notez que, contrairement à d’autres ressources, l' `{@id}` URL doit être fournie via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="667da-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="667da-122">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="667da-122">HTTP methods</span></span>

<span data-ttu-id="667da-123">Toutes les URL trouvées dans la ressource de signatures de référentiel prennent uniquement en charge les méthodes HTTP `GET` et `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="667da-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="667da-124">Index des signatures de référentiel</span><span class="sxs-lookup"><span data-stu-id="667da-124">Repository signatures index</span></span>

<span data-ttu-id="667da-125">L’index des signatures de référentiel contient deux informations :</span><span class="sxs-lookup"><span data-stu-id="667da-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="667da-126">Indique si tous les packages trouvés sur la source sont des référentiels signés par cette source de package.</span><span class="sxs-lookup"><span data-stu-id="667da-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="667da-127">Liste des certificats utilisés par la source du package pour signer des packages.</span><span class="sxs-lookup"><span data-stu-id="667da-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="667da-128">Dans la plupart des cas, la liste des certificats n’est jamais ajoutée à.</span><span class="sxs-lookup"><span data-stu-id="667da-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="667da-129">De nouveaux certificats sont ajoutés à la liste lorsque le certificat de signature précédent a expiré et que la source du package doit commencer à utiliser un nouveau certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="667da-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="667da-130">Si un certificat est supprimé de la liste, cela signifie que toutes les signatures de package créées avec le certificat de signature supprimé ne doivent plus être considérées comme valides par le client.</span><span class="sxs-lookup"><span data-stu-id="667da-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="667da-131">Dans ce cas, la signature du package (mais pas nécessairement le package) n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="667da-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="667da-132">Une stratégie client peut autoriser l’installation du package en tant que non signé.</span><span class="sxs-lookup"><span data-stu-id="667da-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="667da-133">Dans le cas de la révocation de certificat (par exemple, la compromission d’une clé), la source du package est censée signer à nouveau tous les packages signés par le certificat affecté.</span><span class="sxs-lookup"><span data-stu-id="667da-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="667da-134">En outre, la source du package doit supprimer le certificat affecté de la liste des certificats de signature.</span><span class="sxs-lookup"><span data-stu-id="667da-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="667da-135">La requête suivante extrait l’index des signatures de référentiel.</span><span class="sxs-lookup"><span data-stu-id="667da-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="667da-136">L’index de signature du référentiel est un document JSON qui contient un objet avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="667da-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="667da-137">Nom</span><span class="sxs-lookup"><span data-stu-id="667da-137">Name</span></span>                | <span data-ttu-id="667da-138">Type</span><span class="sxs-lookup"><span data-stu-id="667da-138">Type</span></span>             | <span data-ttu-id="667da-139">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="667da-139">Required</span></span> | <span data-ttu-id="667da-140">Notes</span><span class="sxs-lookup"><span data-stu-id="667da-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="667da-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="667da-141">allRepositorySigned</span></span> | <span data-ttu-id="667da-142">boolean</span><span class="sxs-lookup"><span data-stu-id="667da-142">boolean</span></span>          | <span data-ttu-id="667da-143">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-143">yes</span></span>      | <span data-ttu-id="667da-144">Doit se trouver `false` sur les ressources 4.7.0 et 4.9.0</span><span class="sxs-lookup"><span data-stu-id="667da-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="667da-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="667da-145">signingCertificates</span></span> | <span data-ttu-id="667da-146">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="667da-146">array of objects</span></span> | <span data-ttu-id="667da-147">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-147">yes</span></span>      | 

<span data-ttu-id="667da-148">La valeur `allRepositorySigned` booléenne est définie sur false si la source du package contient des packages qui n’ont pas de signature de référentiel.</span><span class="sxs-lookup"><span data-stu-id="667da-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="667da-149">Si la valeur booléenne est définie sur true, tous les packages disponibles sur la source doivent avoir une signature de référentiel produite par l’un des certificats de signature mentionnés dans `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="667da-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="667da-150">La valeur `allRepositorySigned` booléenne doit être false sur les ressources 4.7.0 et 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="667da-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="667da-151">Les clients NuGet v 4.7, v 4.8 et v 4.9 ne peuvent pas installer de packages à partir de sources dont la propriété a la valeur `allRepositorySigned` true.</span><span class="sxs-lookup"><span data-stu-id="667da-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="667da-152">Il doit y avoir un ou plusieurs certificats de signature dans le `signingCertificates` tableau si le `allRepositorySigned` booléen a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="667da-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="667da-153">Si le tableau est vide et `allRepositorySigned` a la valeur true, tous les packages de la source doivent être considérés comme non valides, bien qu’une stratégie client puisse toujours autoriser la consommation de packages.</span><span class="sxs-lookup"><span data-stu-id="667da-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="667da-154">Chaque élément de ce tableau est un objet JSON avec les propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="667da-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="667da-155">Nom</span><span class="sxs-lookup"><span data-stu-id="667da-155">Name</span></span>         | <span data-ttu-id="667da-156">Type</span><span class="sxs-lookup"><span data-stu-id="667da-156">Type</span></span>   | <span data-ttu-id="667da-157">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="667da-157">Required</span></span> | <span data-ttu-id="667da-158">Notes</span><span class="sxs-lookup"><span data-stu-id="667da-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="667da-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="667da-159">contentUrl</span></span>   | <span data-ttu-id="667da-160">string</span><span class="sxs-lookup"><span data-stu-id="667da-160">string</span></span> | <span data-ttu-id="667da-161">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-161">yes</span></span>      | <span data-ttu-id="667da-162">URL absolue du certificat public encodé DER</span><span class="sxs-lookup"><span data-stu-id="667da-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="667da-163">empreintes digitales</span><span class="sxs-lookup"><span data-stu-id="667da-163">fingerprints</span></span> | <span data-ttu-id="667da-164">objet</span><span class="sxs-lookup"><span data-stu-id="667da-164">object</span></span> | <span data-ttu-id="667da-165">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-165">yes</span></span>      |
<span data-ttu-id="667da-166">subject</span><span class="sxs-lookup"><span data-stu-id="667da-166">subject</span></span>      | <span data-ttu-id="667da-167">string</span><span class="sxs-lookup"><span data-stu-id="667da-167">string</span></span> | <span data-ttu-id="667da-168">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-168">yes</span></span>      | <span data-ttu-id="667da-169">Nom unique du sujet du certificat</span><span class="sxs-lookup"><span data-stu-id="667da-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="667da-170">émetteur</span><span class="sxs-lookup"><span data-stu-id="667da-170">issuer</span></span>       | <span data-ttu-id="667da-171">string</span><span class="sxs-lookup"><span data-stu-id="667da-171">string</span></span> | <span data-ttu-id="667da-172">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-172">yes</span></span>      | <span data-ttu-id="667da-173">Nom unique de l’émetteur du certificat</span><span class="sxs-lookup"><span data-stu-id="667da-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="667da-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="667da-174">notBefore</span></span>    | <span data-ttu-id="667da-175">string</span><span class="sxs-lookup"><span data-stu-id="667da-175">string</span></span> | <span data-ttu-id="667da-176">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-176">yes</span></span>      | <span data-ttu-id="667da-177">Horodateur de début de la période de validité du certificat</span><span class="sxs-lookup"><span data-stu-id="667da-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="667da-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="667da-178">notAfter</span></span>     | <span data-ttu-id="667da-179">string</span><span class="sxs-lookup"><span data-stu-id="667da-179">string</span></span> | <span data-ttu-id="667da-180">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-180">yes</span></span>      | <span data-ttu-id="667da-181">Horodateur de fin de la période de validité du certificat</span><span class="sxs-lookup"><span data-stu-id="667da-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="667da-182">Notez que doit `contentUrl` être servi via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="667da-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="667da-183">Cette URL n’a pas de modèle d’URL spécifique et doit être détectée de manière dynamique à l’aide de ce document d’index de signatures de référentiel.</span><span class="sxs-lookup"><span data-stu-id="667da-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="667da-184">Toutes les propriétés de cet objet (à part de `contentUrl` ) doivent être extraites du certificat trouvé à l’adresse `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="667da-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="667da-185">Ces propriétés de l’agent sont fournies à titre de commodité pour réduire les allers-retours.</span><span class="sxs-lookup"><span data-stu-id="667da-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="667da-186">L’objet `fingerprints` dispose des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="667da-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="667da-187">Nom</span><span class="sxs-lookup"><span data-stu-id="667da-187">Name</span></span>                   | <span data-ttu-id="667da-188">Type</span><span class="sxs-lookup"><span data-stu-id="667da-188">Type</span></span>   | <span data-ttu-id="667da-189">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="667da-189">Required</span></span> | <span data-ttu-id="667da-190">Notes</span><span class="sxs-lookup"><span data-stu-id="667da-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="667da-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="667da-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="667da-192">string</span><span class="sxs-lookup"><span data-stu-id="667da-192">string</span></span> | <span data-ttu-id="667da-193">Oui</span><span class="sxs-lookup"><span data-stu-id="667da-193">yes</span></span>      | <span data-ttu-id="667da-194">L’empreinte SHA-256</span><span class="sxs-lookup"><span data-stu-id="667da-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="667da-195">Le nom `2.16.840.1.101.3.4.2.1` de clé est l’OID de l’algorithme de hachage SHA-256.</span><span class="sxs-lookup"><span data-stu-id="667da-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="667da-196">Toutes les valeurs de hachage doivent être des représentations sous forme de chaîne en minuscules et encodées en hex du condensé de hachage.</span><span class="sxs-lookup"><span data-stu-id="667da-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="667da-197">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="667da-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="667da-198">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="667da-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
