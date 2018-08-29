---
title: Les Signatures de référentiel, l’API NuGet | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: La ressource de signatures de référentiel permet aux clients de sources de package annoncer leur référentiel fonctionnalités de signature.
keywords: Signatures de référentiel d’API NuGet, nuget.org signature des certificats, la signature du package nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793288"
---
# <a name="repository-signatures"></a><span data-ttu-id="1d176-104">Signatures de référentiel</span><span class="sxs-lookup"><span data-stu-id="1d176-104">Repository signatures</span></span>

<span data-ttu-id="1d176-105">Si une source de package prend en charge l’ajout des signatures de référentiel pour les packages publiés, il est possible pour un client déterminer la signature des certificats qui sont utilisés par la source du package.</span><span class="sxs-lookup"><span data-stu-id="1d176-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="1d176-106">Cette ressource permet aux clients de détecter si un référentiel signé le package a été falsifié ou dispose d’un certificat de signature inattendu.</span><span class="sxs-lookup"><span data-stu-id="1d176-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="1d176-107">La ressource utilisée pour récupérer ces informations de signature du référentiel est la `RepositorySignatures` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1d176-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="1d176-108">NuGet.org démarrera annonce la `RepositorySignatures` ressource dans un avenir proche.</span><span class="sxs-lookup"><span data-stu-id="1d176-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="1d176-109">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="1d176-109">Versioning</span></span>

<span data-ttu-id="1d176-110">Ce qui suit `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="1d176-110">The following `@type` value is used:</span></span>

<span data-ttu-id="1d176-111">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="1d176-111">@type value</span></span>                | <span data-ttu-id="1d176-112">Notes</span><span class="sxs-lookup"><span data-stu-id="1d176-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="1d176-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="1d176-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="1d176-114">La version initiale</span><span class="sxs-lookup"><span data-stu-id="1d176-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="1d176-115">URL de base</span><span class="sxs-lookup"><span data-stu-id="1d176-115">Base URL</span></span>

<span data-ttu-id="1d176-116">L’URL de point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur.</span><span class="sxs-lookup"><span data-stu-id="1d176-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="1d176-117">Cette rubrique utilise l’URL de l’espace réservé `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="1d176-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="1d176-118">Notez que contrairement à d’autres ressources, le `{@id}` URL est nécessaire pour être pris en charge via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d176-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1d176-119">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="1d176-119">HTTP methods</span></span>

<span data-ttu-id="1d176-120">Toutes les URL figurant dans les méthodes de prise en charge uniquement le protocole HTTP de référentiel signatures ressource `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="1d176-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="1d176-121">Index de signatures du référentiel</span><span class="sxs-lookup"><span data-stu-id="1d176-121">Repository signatures index</span></span>

<span data-ttu-id="1d176-122">L’index de signatures de référentiel contient deux informations :</span><span class="sxs-lookup"><span data-stu-id="1d176-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="1d176-123">S’il faut ou non tous les packages se trouvent sur la source sont référentiel signée par cette source de package.</span><span class="sxs-lookup"><span data-stu-id="1d176-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="1d176-124">La liste des certificats utilisés par la source du package pour signer les packages.</span><span class="sxs-lookup"><span data-stu-id="1d176-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="1d176-125">La plupart des cas, la liste des certificats uniquement jamais est ajoutée à.</span><span class="sxs-lookup"><span data-stu-id="1d176-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="1d176-126">Nouveaux certificats étaient être ajoutés à la liste lorsque le certificat de signature précédent a expiré et la source du package a besoin commencer à utiliser un certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="1d176-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="1d176-127">Si un certificat est supprimé de la liste, ce qui signifie que toutes les signatures de package créés avec le certificat de signature supprimé doivent plus être considérés comme valides par le client.</span><span class="sxs-lookup"><span data-stu-id="1d176-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="1d176-128">Dans ce cas, la signature du package (mais pas nécessairement le package) n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="1d176-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="1d176-129">Une stratégie du client peut-être autoriser l’installation du package comme étant non signés.</span><span class="sxs-lookup"><span data-stu-id="1d176-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="1d176-130">Dans le cas de la révocation de certificats (par exemple, clé compromise), la source du package est prévue pour signer à nouveau tous les packages signés par le certificat en question.</span><span class="sxs-lookup"><span data-stu-id="1d176-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="1d176-131">En outre, la source du package doit supprimer le certificat en question à partir de la liste de certificats de signature.</span><span class="sxs-lookup"><span data-stu-id="1d176-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="1d176-132">La requête suivante extrait l’index de signatures de référentiel.</span><span class="sxs-lookup"><span data-stu-id="1d176-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="1d176-133">L’index de signature de référentiel est un document JSON qui contient un objet avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d176-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="1d176-134">Name</span><span class="sxs-lookup"><span data-stu-id="1d176-134">Name</span></span>                | <span data-ttu-id="1d176-135">Type</span><span class="sxs-lookup"><span data-stu-id="1d176-135">Type</span></span>             | <span data-ttu-id="1d176-136">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="1d176-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="1d176-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="1d176-137">allRepositorySigned</span></span> | <span data-ttu-id="1d176-138">boolean</span><span class="sxs-lookup"><span data-stu-id="1d176-138">boolean</span></span>          | <span data-ttu-id="1d176-139">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-139">yes</span></span>
<span data-ttu-id="1d176-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="1d176-140">signingCertificates</span></span> | <span data-ttu-id="1d176-141">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="1d176-141">array of objects</span></span> | <span data-ttu-id="1d176-142">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-142">yes</span></span>

<span data-ttu-id="1d176-143">Le `allRepositorySigned` valeur booléenne est définie sur false si la source du package a certains packages ayant aucune signature de référentiel.</span><span class="sxs-lookup"><span data-stu-id="1d176-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="1d176-144">Si la valeur booléenne est définie sur true, tous les packages disponibles sur la source doit avoir une signature de référentiel produite par un des certificats de signature mentionnés dans `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="1d176-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="1d176-145">Il doit y avoir un ou plusieurs certificats de signature dans le `signingCertificates` tableau si le `allRepositorySigned` valeur booléenne est définie sur true.</span><span class="sxs-lookup"><span data-stu-id="1d176-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="1d176-146">Si le tableau est vide et `allRepositorySigned` est définie sur true, tous les packages à partir de la source doivent être considéré comme non valides, même si une stratégie de client peut autorise toujours la consommation de packages.</span><span class="sxs-lookup"><span data-stu-id="1d176-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="1d176-147">Chaque élément de ce tableau est un objet JSON avec les propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="1d176-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="1d176-148">Name</span><span class="sxs-lookup"><span data-stu-id="1d176-148">Name</span></span>         | <span data-ttu-id="1d176-149">Type</span><span class="sxs-lookup"><span data-stu-id="1d176-149">Type</span></span>   | <span data-ttu-id="1d176-150">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="1d176-150">Required</span></span> | <span data-ttu-id="1d176-151">Notes</span><span class="sxs-lookup"><span data-stu-id="1d176-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="1d176-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="1d176-152">contentUrl</span></span>   | <span data-ttu-id="1d176-153">chaîne</span><span class="sxs-lookup"><span data-stu-id="1d176-153">string</span></span> | <span data-ttu-id="1d176-154">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-154">yes</span></span>      | <span data-ttu-id="1d176-155">URL absolue pour le certificat public encodé DER</span><span class="sxs-lookup"><span data-stu-id="1d176-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="1d176-156">empreintes digitales</span><span class="sxs-lookup"><span data-stu-id="1d176-156">fingerprints</span></span> | <span data-ttu-id="1d176-157">object</span><span class="sxs-lookup"><span data-stu-id="1d176-157">object</span></span> | <span data-ttu-id="1d176-158">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-158">yes</span></span>      |
<span data-ttu-id="1d176-159">Objet</span><span class="sxs-lookup"><span data-stu-id="1d176-159">subject</span></span>      | <span data-ttu-id="1d176-160">chaîne</span><span class="sxs-lookup"><span data-stu-id="1d176-160">string</span></span> | <span data-ttu-id="1d176-161">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-161">yes</span></span>      | <span data-ttu-id="1d176-162">Le nom unique du sujet du certificat</span><span class="sxs-lookup"><span data-stu-id="1d176-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="1d176-163">issuer</span><span class="sxs-lookup"><span data-stu-id="1d176-163">issuer</span></span>       | <span data-ttu-id="1d176-164">chaîne</span><span class="sxs-lookup"><span data-stu-id="1d176-164">string</span></span> | <span data-ttu-id="1d176-165">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-165">yes</span></span>      | <span data-ttu-id="1d176-166">Le nom unique de l’émetteur du certificat</span><span class="sxs-lookup"><span data-stu-id="1d176-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="1d176-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="1d176-167">notBefore</span></span>    | <span data-ttu-id="1d176-168">chaîne</span><span class="sxs-lookup"><span data-stu-id="1d176-168">string</span></span> | <span data-ttu-id="1d176-169">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-169">yes</span></span>      | <span data-ttu-id="1d176-170">L’horodatage de début de période de validité du certificat</span><span class="sxs-lookup"><span data-stu-id="1d176-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="1d176-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="1d176-171">notAfter</span></span>     | <span data-ttu-id="1d176-172">chaîne</span><span class="sxs-lookup"><span data-stu-id="1d176-172">string</span></span> | <span data-ttu-id="1d176-173">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-173">yes</span></span>      | <span data-ttu-id="1d176-174">L’horodatage de fin de période de validité du certificat</span><span class="sxs-lookup"><span data-stu-id="1d176-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="1d176-175">Notez que le `contentUrl` est nécessaire pour être pris en charge via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d176-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="1d176-176">Cette URL n’a aucun modèle d’URL spécifique et doit être découverts dynamiquement à l’aide de ce document d’index de signatures référentiel.</span><span class="sxs-lookup"><span data-stu-id="1d176-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="1d176-177">Toutes les propriétés de cet objet (outre `contentUrl`) doit être dérivé du certificat, consultez `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="1d176-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="1d176-178">Ces propriétés dérivables sont fournies pour des raisons pratiques afin de réduire les allers-retours.</span><span class="sxs-lookup"><span data-stu-id="1d176-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="1d176-179">Le `fingerprints` objet a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d176-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="1d176-180">Name</span><span class="sxs-lookup"><span data-stu-id="1d176-180">Name</span></span>                   | <span data-ttu-id="1d176-181">Type</span><span class="sxs-lookup"><span data-stu-id="1d176-181">Type</span></span>   | <span data-ttu-id="1d176-182">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="1d176-182">Required</span></span> | <span data-ttu-id="1d176-183">Notes</span><span class="sxs-lookup"><span data-stu-id="1d176-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="1d176-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="1d176-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="1d176-185">chaîne</span><span class="sxs-lookup"><span data-stu-id="1d176-185">string</span></span> | <span data-ttu-id="1d176-186">oui</span><span class="sxs-lookup"><span data-stu-id="1d176-186">yes</span></span>      | <span data-ttu-id="1d176-187">L’empreinte SHA-256</span><span class="sxs-lookup"><span data-stu-id="1d176-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="1d176-188">Le nom de clé `2.16.840.1.101.3.4.2.1` est l’OID de l’algorithme de hachage SHA-256.</span><span class="sxs-lookup"><span data-stu-id="1d176-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="1d176-189">Toutes les valeurs de hachage doivent être représentations sous forme de chaîne en minuscules, codé en hexadécimal du résumé de hachage.</span><span class="sxs-lookup"><span data-stu-id="1d176-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="1d176-190">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="1d176-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="1d176-191">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="1d176-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]