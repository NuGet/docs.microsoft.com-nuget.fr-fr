---
title: Les Signatures de référentiel, l’API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La ressource de signatures de référentiel permet aux clients de sources de package annoncer leur référentiel fonctionnalités de signature.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547979"
---
# <a name="repository-signatures"></a><span data-ttu-id="ce0b7-103">Signatures de référentiel</span><span class="sxs-lookup"><span data-stu-id="ce0b7-103">Repository signatures</span></span>

<span data-ttu-id="ce0b7-104">Si une source de package prend en charge l’ajout des signatures de référentiel pour les packages publiés, il est possible pour un client déterminer la signature des certificats qui sont utilisés par la source du package.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="ce0b7-105">Cette ressource permet aux clients de détecter si un référentiel signé le package a été falsifié ou dispose d’un certificat de signature inattendu.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="ce0b7-106">La ressource utilisée pour récupérer ces informations de signature du référentiel est la `RepositorySignatures` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ce0b7-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="ce0b7-107">NuGet.org démarrera annonce la `RepositorySignatures` ressource dans un avenir proche.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="ce0b7-108">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="ce0b7-108">Versioning</span></span>

<span data-ttu-id="ce0b7-109">Ce qui suit `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="ce0b7-109">The following `@type` value is used:</span></span>

<span data-ttu-id="ce0b7-110">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="ce0b7-110">@type value</span></span>                | <span data-ttu-id="ce0b7-111">Notes</span><span class="sxs-lookup"><span data-stu-id="ce0b7-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="ce0b7-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="ce0b7-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="ce0b7-113">La version initiale</span><span class="sxs-lookup"><span data-stu-id="ce0b7-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="ce0b7-114">URL de base</span><span class="sxs-lookup"><span data-stu-id="ce0b7-114">Base URL</span></span>

<span data-ttu-id="ce0b7-115">L’URL de point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="ce0b7-116">Cette rubrique utilise l’URL de l’espace réservé `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="ce0b7-117">Notez que contrairement à d’autres ressources, le `{@id}` URL est nécessaire pour être pris en charge via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ce0b7-118">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="ce0b7-118">HTTP methods</span></span>

<span data-ttu-id="ce0b7-119">Toutes les URL figurant dans les méthodes de prise en charge uniquement le protocole HTTP de référentiel signatures ressource `GET` et `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="ce0b7-120">Index de signatures du référentiel</span><span class="sxs-lookup"><span data-stu-id="ce0b7-120">Repository signatures index</span></span>

<span data-ttu-id="ce0b7-121">L’index de signatures de référentiel contient deux informations :</span><span class="sxs-lookup"><span data-stu-id="ce0b7-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="ce0b7-122">S’il faut ou non tous les packages se trouvent sur la source sont référentiel signée par cette source de package.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="ce0b7-123">La liste des certificats utilisés par la source du package pour signer les packages.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="ce0b7-124">La plupart des cas, la liste des certificats uniquement jamais est ajoutée à.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="ce0b7-125">Nouveaux certificats étaient être ajoutés à la liste lorsque le certificat de signature précédent a expiré et la source du package a besoin commencer à utiliser un certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="ce0b7-126">Si un certificat est supprimé de la liste, ce qui signifie que toutes les signatures de package créés avec le certificat de signature supprimé doivent plus être considérés comme valides par le client.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="ce0b7-127">Dans ce cas, la signature du package (mais pas nécessairement le package) n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="ce0b7-128">Une stratégie du client peut-être autoriser l’installation du package comme étant non signés.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="ce0b7-129">Dans le cas de la révocation de certificats (par exemple, clé compromise), la source du package est prévue pour signer à nouveau tous les packages signés par le certificat en question.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="ce0b7-130">En outre, la source du package doit supprimer le certificat en question à partir de la liste de certificats de signature.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="ce0b7-131">La requête suivante extrait l’index de signatures de référentiel.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="ce0b7-132">L’index de signature de référentiel est un document JSON qui contient un objet avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce0b7-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="ce0b7-133">Name</span><span class="sxs-lookup"><span data-stu-id="ce0b7-133">Name</span></span>                | <span data-ttu-id="ce0b7-134">Type</span><span class="sxs-lookup"><span data-stu-id="ce0b7-134">Type</span></span>             | <span data-ttu-id="ce0b7-135">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="ce0b7-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="ce0b7-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="ce0b7-136">allRepositorySigned</span></span> | <span data-ttu-id="ce0b7-137">boolean</span><span class="sxs-lookup"><span data-stu-id="ce0b7-137">boolean</span></span>          | <span data-ttu-id="ce0b7-138">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-138">yes</span></span>
<span data-ttu-id="ce0b7-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="ce0b7-139">signingCertificates</span></span> | <span data-ttu-id="ce0b7-140">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="ce0b7-140">array of objects</span></span> | <span data-ttu-id="ce0b7-141">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-141">yes</span></span>

<span data-ttu-id="ce0b7-142">Le `allRepositorySigned` valeur booléenne est définie sur false si la source du package a certains packages ayant aucune signature de référentiel.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="ce0b7-143">Si la valeur booléenne est définie sur true, tous les packages disponibles sur la source doit avoir une signature de référentiel produite par un des certificats de signature mentionnés dans `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="ce0b7-144">Il doit y avoir un ou plusieurs certificats de signature dans le `signingCertificates` tableau si le `allRepositorySigned` valeur booléenne est définie sur true.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="ce0b7-145">Si le tableau est vide et `allRepositorySigned` est définie sur true, tous les packages à partir de la source doivent être considéré comme non valides, même si une stratégie de client peut autorise toujours la consommation de packages.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="ce0b7-146">Chaque élément de ce tableau est un objet JSON avec les propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="ce0b7-147">Name</span><span class="sxs-lookup"><span data-stu-id="ce0b7-147">Name</span></span>         | <span data-ttu-id="ce0b7-148">Type</span><span class="sxs-lookup"><span data-stu-id="ce0b7-148">Type</span></span>   | <span data-ttu-id="ce0b7-149">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="ce0b7-149">Required</span></span> | <span data-ttu-id="ce0b7-150">Notes</span><span class="sxs-lookup"><span data-stu-id="ce0b7-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="ce0b7-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="ce0b7-151">contentUrl</span></span>   | <span data-ttu-id="ce0b7-152">chaîne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-152">string</span></span> | <span data-ttu-id="ce0b7-153">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-153">yes</span></span>      | <span data-ttu-id="ce0b7-154">URL absolue pour le certificat public encodé DER</span><span class="sxs-lookup"><span data-stu-id="ce0b7-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="ce0b7-155">empreintes digitales</span><span class="sxs-lookup"><span data-stu-id="ce0b7-155">fingerprints</span></span> | <span data-ttu-id="ce0b7-156">object</span><span class="sxs-lookup"><span data-stu-id="ce0b7-156">object</span></span> | <span data-ttu-id="ce0b7-157">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-157">yes</span></span>      |
<span data-ttu-id="ce0b7-158">Objet</span><span class="sxs-lookup"><span data-stu-id="ce0b7-158">subject</span></span>      | <span data-ttu-id="ce0b7-159">chaîne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-159">string</span></span> | <span data-ttu-id="ce0b7-160">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-160">yes</span></span>      | <span data-ttu-id="ce0b7-161">Le nom unique du sujet du certificat</span><span class="sxs-lookup"><span data-stu-id="ce0b7-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="ce0b7-162">issuer</span><span class="sxs-lookup"><span data-stu-id="ce0b7-162">issuer</span></span>       | <span data-ttu-id="ce0b7-163">chaîne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-163">string</span></span> | <span data-ttu-id="ce0b7-164">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-164">yes</span></span>      | <span data-ttu-id="ce0b7-165">Le nom unique de l’émetteur du certificat</span><span class="sxs-lookup"><span data-stu-id="ce0b7-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="ce0b7-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="ce0b7-166">notBefore</span></span>    | <span data-ttu-id="ce0b7-167">chaîne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-167">string</span></span> | <span data-ttu-id="ce0b7-168">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-168">yes</span></span>      | <span data-ttu-id="ce0b7-169">L’horodatage de début de période de validité du certificat</span><span class="sxs-lookup"><span data-stu-id="ce0b7-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="ce0b7-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="ce0b7-170">notAfter</span></span>     | <span data-ttu-id="ce0b7-171">chaîne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-171">string</span></span> | <span data-ttu-id="ce0b7-172">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-172">yes</span></span>      | <span data-ttu-id="ce0b7-173">L’horodatage de fin de période de validité du certificat</span><span class="sxs-lookup"><span data-stu-id="ce0b7-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="ce0b7-174">Notez que le `contentUrl` est nécessaire pour être pris en charge via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="ce0b7-175">Cette URL n’a aucun modèle d’URL spécifique et doit être découverts dynamiquement à l’aide de ce document d’index de signatures référentiel.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="ce0b7-176">Toutes les propriétés de cet objet (outre `contentUrl`) doit être dérivé du certificat, consultez `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="ce0b7-177">Ces propriétés dérivables sont fournies pour des raisons pratiques afin de réduire les allers-retours.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="ce0b7-178">Le `fingerprints` objet a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce0b7-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="ce0b7-179">Name</span><span class="sxs-lookup"><span data-stu-id="ce0b7-179">Name</span></span>                   | <span data-ttu-id="ce0b7-180">Type</span><span class="sxs-lookup"><span data-stu-id="ce0b7-180">Type</span></span>   | <span data-ttu-id="ce0b7-181">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="ce0b7-181">Required</span></span> | <span data-ttu-id="ce0b7-182">Notes</span><span class="sxs-lookup"><span data-stu-id="ce0b7-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="ce0b7-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="ce0b7-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="ce0b7-184">chaîne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-184">string</span></span> | <span data-ttu-id="ce0b7-185">oui</span><span class="sxs-lookup"><span data-stu-id="ce0b7-185">yes</span></span>      | <span data-ttu-id="ce0b7-186">L’empreinte SHA-256</span><span class="sxs-lookup"><span data-stu-id="ce0b7-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="ce0b7-187">Le nom de clé `2.16.840.1.101.3.4.2.1` est l’OID de l’algorithme de hachage SHA-256.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="ce0b7-188">Toutes les valeurs de hachage doivent être représentations sous forme de chaîne en minuscules, codé en hexadécimal du résumé de hachage.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ce0b7-189">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="ce0b7-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="ce0b7-190">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="ce0b7-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
