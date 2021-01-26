---
title: Protocoles nuget.org
description: Les protocoles nuget.org en constante évolution pour interagir avec les clients NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773974"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="9a369-103">Protocoles nuget.org</span><span class="sxs-lookup"><span data-stu-id="9a369-103">nuget.org protocols</span></span>

<span data-ttu-id="9a369-104">Pour interagir avec nuget.org, les clients doivent suivre certains protocoles.</span><span class="sxs-lookup"><span data-stu-id="9a369-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="9a369-105">Étant donné que ces protocoles continuent d’évoluer, les clients doivent identifier la version de protocole qu’ils utilisent lors de l’appel d’API nuget.org spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9a369-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="9a369-106">Cela permet à nuget.org d’introduire des modifications de manière non-critique pour les anciens clients.</span><span class="sxs-lookup"><span data-stu-id="9a369-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="9a369-107">Les API documentées dans cette page sont spécifiques à nuget.org et il n’est pas prévu que d’autres implémentations de serveur NuGet introduisent ces API.</span><span class="sxs-lookup"><span data-stu-id="9a369-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="9a369-108">Pour plus d’informations sur l’API NuGet implémentée globalement sur l’écosystème NuGet, consultez la [vue d’ensemble](overview.md)de l’API.</span><span class="sxs-lookup"><span data-stu-id="9a369-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="9a369-109">Cette rubrique répertorie les différents protocoles tels qu’ils existent et à quel moment.</span><span class="sxs-lookup"><span data-stu-id="9a369-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="9a369-110">Version du protocole NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="9a369-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="9a369-111">Le protocole 4.1.0 spécifie l’utilisation des clés de la portée de vérification pour interagir avec des services autres que nuget.org, pour valider un package par rapport à un compte nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9a369-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="9a369-112">Notez que le `4.1.0` numéro de version est une chaîne opaque, mais qu’il coïncide avec la première version du client officiel NuGet qui prenait en charge ce protocole.</span><span class="sxs-lookup"><span data-stu-id="9a369-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="9a369-113">La validation garantit que les clés d’API créées par l’utilisateur sont utilisées uniquement avec nuget.org, et que d’autres vérifications ou validations à partir d’un service tiers sont gérées par le biais de clés de la portée de vérification à usage unique.</span><span class="sxs-lookup"><span data-stu-id="9a369-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="9a369-114">Ces clés de l’étendue de vérification peuvent être utilisées pour valider le fait que le package appartient à un utilisateur particulier (compte) sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9a369-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="9a369-115">Configuration requise du client</span><span class="sxs-lookup"><span data-stu-id="9a369-115">Client requirement</span></span>

<span data-ttu-id="9a369-116">Les clients doivent passer l’en-tête suivant lorsqu’ils effectuent des appels d’API vers des packages **Push** vers NuGet.org :</span><span class="sxs-lookup"><span data-stu-id="9a369-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="9a369-117">Notez que l' `X-NuGet-Client-Version` en-tête a une sémantique similaire, mais qu’il est réservé pour être utilisé uniquement par le client NuGet officiel.</span><span class="sxs-lookup"><span data-stu-id="9a369-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="9a369-118">Les clients tiers doivent utiliser l' `X-NuGet-Protocol-Version` en-tête et la valeur.</span><span class="sxs-lookup"><span data-stu-id="9a369-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="9a369-119">Le protocole **Push** lui-même est décrit dans la documentation de la [ `PackagePublish` ressource](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="9a369-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="9a369-120">Si un client interagit avec des services externes et doit vérifier si un package appartient à un utilisateur particulier (compte), il doit utiliser le protocole suivant et utiliser les clés de la portée de vérification et non les clés API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9a369-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="9a369-121">API pour demander une clé de la portée de la vérification</span><span class="sxs-lookup"><span data-stu-id="9a369-121">API to request a verify-scope key</span></span>

<span data-ttu-id="9a369-122">Cette API est utilisée pour obtenir une clé de la portée de la vérification pour un auteur nuget.org afin de valider un package qui lui appartient.</span><span class="sxs-lookup"><span data-stu-id="9a369-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="9a369-123">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="9a369-123">Request parameters</span></span>

<span data-ttu-id="9a369-124">Nom</span><span class="sxs-lookup"><span data-stu-id="9a369-124">Name</span></span>           | <span data-ttu-id="9a369-125">Dans</span><span class="sxs-lookup"><span data-stu-id="9a369-125">In</span></span>     | <span data-ttu-id="9a369-126">Type</span><span class="sxs-lookup"><span data-stu-id="9a369-126">Type</span></span>   | <span data-ttu-id="9a369-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9a369-127">Required</span></span> | <span data-ttu-id="9a369-128">Notes</span><span class="sxs-lookup"><span data-stu-id="9a369-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9a369-129">id</span><span class="sxs-lookup"><span data-stu-id="9a369-129">ID</span></span>             | <span data-ttu-id="9a369-130">URL</span><span class="sxs-lookup"><span data-stu-id="9a369-130">URL</span></span>    | <span data-ttu-id="9a369-131">string</span><span class="sxs-lookup"><span data-stu-id="9a369-131">string</span></span> | <span data-ttu-id="9a369-132">Oui</span><span class="sxs-lookup"><span data-stu-id="9a369-132">yes</span></span>      | <span data-ttu-id="9a369-133">Identidier de package pour lequel la clé de vérification de la portée est demandée</span><span class="sxs-lookup"><span data-stu-id="9a369-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="9a369-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="9a369-134">VERSION</span></span>        | <span data-ttu-id="9a369-135">URL</span><span class="sxs-lookup"><span data-stu-id="9a369-135">URL</span></span>    | <span data-ttu-id="9a369-136">string</span><span class="sxs-lookup"><span data-stu-id="9a369-136">string</span></span> | <span data-ttu-id="9a369-137">non</span><span class="sxs-lookup"><span data-stu-id="9a369-137">no</span></span>       | <span data-ttu-id="9a369-138">Version du package</span><span class="sxs-lookup"><span data-stu-id="9a369-138">The package version</span></span>
<span data-ttu-id="9a369-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9a369-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9a369-140">En-tête</span><span class="sxs-lookup"><span data-stu-id="9a369-140">Header</span></span> | <span data-ttu-id="9a369-141">string</span><span class="sxs-lookup"><span data-stu-id="9a369-141">string</span></span> | <span data-ttu-id="9a369-142">Oui</span><span class="sxs-lookup"><span data-stu-id="9a369-142">yes</span></span>      | <span data-ttu-id="9a369-143">Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9a369-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="9a369-144">response</span><span class="sxs-lookup"><span data-stu-id="9a369-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="9a369-145">API pour vérifier la clé de l’étendue</span><span class="sxs-lookup"><span data-stu-id="9a369-145">API to verify the verify scope key</span></span>

<span data-ttu-id="9a369-146">Cette API est utilisée pour valider une clé de la portée de vérification pour le package détenu par l’auteur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9a369-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="9a369-147">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="9a369-147">Request parameters</span></span>

<span data-ttu-id="9a369-148">Nom</span><span class="sxs-lookup"><span data-stu-id="9a369-148">Name</span></span>           | <span data-ttu-id="9a369-149">Dans</span><span class="sxs-lookup"><span data-stu-id="9a369-149">In</span></span>     | <span data-ttu-id="9a369-150">Type</span><span class="sxs-lookup"><span data-stu-id="9a369-150">Type</span></span>   | <span data-ttu-id="9a369-151">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="9a369-151">Required</span></span> | <span data-ttu-id="9a369-152">Notes</span><span class="sxs-lookup"><span data-stu-id="9a369-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="9a369-153">id</span><span class="sxs-lookup"><span data-stu-id="9a369-153">ID</span></span>             | <span data-ttu-id="9a369-154">URL</span><span class="sxs-lookup"><span data-stu-id="9a369-154">URL</span></span>    | <span data-ttu-id="9a369-155">string</span><span class="sxs-lookup"><span data-stu-id="9a369-155">string</span></span> | <span data-ttu-id="9a369-156">Oui</span><span class="sxs-lookup"><span data-stu-id="9a369-156">yes</span></span>      | <span data-ttu-id="9a369-157">Identificateur du package pour lequel la clé de vérification de la portée est demandée.</span><span class="sxs-lookup"><span data-stu-id="9a369-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="9a369-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="9a369-158">VERSION</span></span>        | <span data-ttu-id="9a369-159">URL</span><span class="sxs-lookup"><span data-stu-id="9a369-159">URL</span></span>    | <span data-ttu-id="9a369-160">string</span><span class="sxs-lookup"><span data-stu-id="9a369-160">string</span></span> | <span data-ttu-id="9a369-161">non</span><span class="sxs-lookup"><span data-stu-id="9a369-161">no</span></span>       | <span data-ttu-id="9a369-162">Version du package</span><span class="sxs-lookup"><span data-stu-id="9a369-162">The package version</span></span>
<span data-ttu-id="9a369-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9a369-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9a369-164">En-tête</span><span class="sxs-lookup"><span data-stu-id="9a369-164">Header</span></span> | <span data-ttu-id="9a369-165">string</span><span class="sxs-lookup"><span data-stu-id="9a369-165">string</span></span> | <span data-ttu-id="9a369-166">Oui</span><span class="sxs-lookup"><span data-stu-id="9a369-166">yes</span></span>      | <span data-ttu-id="9a369-167">Par exemple : `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9a369-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="9a369-168">Cette clé de l’API de la portée de vérification expire dans l’heure d’un jour ou lors de la première utilisation, selon ce qui se produit en premier.</span><span class="sxs-lookup"><span data-stu-id="9a369-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="9a369-169">response</span><span class="sxs-lookup"><span data-stu-id="9a369-169">Response</span></span>

<span data-ttu-id="9a369-170">Code d’état</span><span class="sxs-lookup"><span data-stu-id="9a369-170">Status Code</span></span> | <span data-ttu-id="9a369-171">Signification</span><span class="sxs-lookup"><span data-stu-id="9a369-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="9a369-172">200</span><span class="sxs-lookup"><span data-stu-id="9a369-172">200</span></span>         | <span data-ttu-id="9a369-173">La clé API est valide</span><span class="sxs-lookup"><span data-stu-id="9a369-173">The API key is valid</span></span>
<span data-ttu-id="9a369-174">403</span><span class="sxs-lookup"><span data-stu-id="9a369-174">403</span></span>         | <span data-ttu-id="9a369-175">La clé API n’est pas valide ou n’est pas autorisée à effectuer une transmission de type push sur le package</span><span class="sxs-lookup"><span data-stu-id="9a369-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="9a369-176">404</span><span class="sxs-lookup"><span data-stu-id="9a369-176">404</span></span>         | <span data-ttu-id="9a369-177">Le package référencé par `ID` et `VERSION` (facultatif) n’existe pas</span><span class="sxs-lookup"><span data-stu-id="9a369-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
