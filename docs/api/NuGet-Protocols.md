---
title: Protocoles NuGet.org
description: Les protocoles nuget.org en constante évolution pour interagir avec les clients NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822576"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="20d33-103">protocoles NuGet.org</span><span class="sxs-lookup"><span data-stu-id="20d33-103">nuget.org protocols</span></span>

<span data-ttu-id="20d33-104">Pour interagir avec nuget.org, les clients doivent suivre certains protocoles.</span><span class="sxs-lookup"><span data-stu-id="20d33-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="20d33-105">Étant donné que ces protocoles conservent en constante évolution, les clients doivent identifier la version du protocole qu’ils utilisent lors de l’appel d’API de nuget.org spécifique.</span><span class="sxs-lookup"><span data-stu-id="20d33-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="20d33-106">Cela permet de nuget.org apporter des modifications d’une manière sans rupture pour les anciens clients.</span><span class="sxs-lookup"><span data-stu-id="20d33-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="20d33-107">Les API décrites dans cette page sont spécifiques à nuget.org et n’est pas garantie pour d’autres implémentations de serveur NuGet présenter ces API.</span><span class="sxs-lookup"><span data-stu-id="20d33-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="20d33-108">Pour plus d’informations sur l’API NuGet implémentés largement dans l’écosystème de NuGet, consultez le [présentation de l’API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="20d33-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="20d33-109">Cette rubrique répertorie les différents protocoles en tant qu’et lorsque leur présence.</span><span class="sxs-lookup"><span data-stu-id="20d33-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="20d33-110">Version du protocole NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="20d33-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="20d33-111">Le 4.1.0 protocole spécifie l’utilisation de clés de portée vérifier pour interagir avec les services autres que nuget.org, pour valider un package avec un compte de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20d33-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="20d33-112">Notez que le `4.1.0` version nombre est une chaîne opaque mais se produit pour coïncider avec la première version du client NuGet officiel pris en charge ce protocole.</span><span class="sxs-lookup"><span data-stu-id="20d33-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="20d33-113">Validation garantit que les clés API créés par l’utilisateur sont utilisées uniquement avec nuget.org, et que cette vérification ou la validation à partir d’un service tiers est gérée via un usage des clés de vérifier l’étendue.</span><span class="sxs-lookup"><span data-stu-id="20d33-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="20d33-114">Ces clés de vérifier l’étendue peuvent être utilisées pour valider que le package appartient à un utilisateur spécifique (compte) sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20d33-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="20d33-115">Spécification du client</span><span class="sxs-lookup"><span data-stu-id="20d33-115">Client requirement</span></span>

<span data-ttu-id="20d33-116">Les clients doivent passer de l’en-tête suivant lorsqu’ils effectuent des appels d’API à **push** packages nuget.org :</span><span class="sxs-lookup"><span data-stu-id="20d33-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="20d33-117">Notez que le `X-NuGet-Client-Version` en-tête a une sémantique similaire, mais elle est réservé à utiliser par le client NuGet officiels.</span><span class="sxs-lookup"><span data-stu-id="20d33-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="20d33-118">Les clients tiers doivent utiliser le `X-NuGet-Protocol-Version` en-tête et valeur.</span><span class="sxs-lookup"><span data-stu-id="20d33-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="20d33-119">Le **push** protocole lui-même est décrit dans la documentation relative à la [ `PackagePublish` ressources](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="20d33-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="20d33-120">Si un client interagit avec les services externes et des besoins pour vérifier si un package appartient à un utilisateur spécifique (compte), il doit utiliser le protocole suivant et utiliser les clés de l’étendue de la vérification et pas les clés de l’API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20d33-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="20d33-121">API pour demander une clé de vérification étendue</span><span class="sxs-lookup"><span data-stu-id="20d33-121">API to request a verify-scope key</span></span>

<span data-ttu-id="20d33-122">Cette API est utilisée pour obtenir une clé de l’étendue de la vérification d’un auteur nuget.org valider un package détenu par ce dernier.</span><span class="sxs-lookup"><span data-stu-id="20d33-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="20d33-123">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="20d33-123">Request parameters</span></span>

<span data-ttu-id="20d33-124">Name</span><span class="sxs-lookup"><span data-stu-id="20d33-124">Name</span></span>           | <span data-ttu-id="20d33-125">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="20d33-125">In</span></span>     | <span data-ttu-id="20d33-126">Type</span><span class="sxs-lookup"><span data-stu-id="20d33-126">Type</span></span>   | <span data-ttu-id="20d33-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="20d33-127">Required</span></span> | <span data-ttu-id="20d33-128">Notes</span><span class="sxs-lookup"><span data-stu-id="20d33-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="20d33-129">Id</span><span class="sxs-lookup"><span data-stu-id="20d33-129">ID</span></span>             | <span data-ttu-id="20d33-130">URL</span><span class="sxs-lookup"><span data-stu-id="20d33-130">URL</span></span>    | <span data-ttu-id="20d33-131">chaîne</span><span class="sxs-lookup"><span data-stu-id="20d33-131">string</span></span> | <span data-ttu-id="20d33-132">oui</span><span class="sxs-lookup"><span data-stu-id="20d33-132">yes</span></span>      | <span data-ttu-id="20d33-133">L’identidier de package pour lequel la clé de portée Vérifiez est demandée</span><span class="sxs-lookup"><span data-stu-id="20d33-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="20d33-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="20d33-134">VERSION</span></span>        | <span data-ttu-id="20d33-135">URL</span><span class="sxs-lookup"><span data-stu-id="20d33-135">URL</span></span>    | <span data-ttu-id="20d33-136">chaîne</span><span class="sxs-lookup"><span data-stu-id="20d33-136">string</span></span> | <span data-ttu-id="20d33-137">Non</span><span class="sxs-lookup"><span data-stu-id="20d33-137">no</span></span>       | <span data-ttu-id="20d33-138">La version du package</span><span class="sxs-lookup"><span data-stu-id="20d33-138">The package version</span></span>
<span data-ttu-id="20d33-139">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="20d33-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="20d33-140">Header</span><span class="sxs-lookup"><span data-stu-id="20d33-140">Header</span></span> | <span data-ttu-id="20d33-141">chaîne</span><span class="sxs-lookup"><span data-stu-id="20d33-141">string</span></span> | <span data-ttu-id="20d33-142">oui</span><span class="sxs-lookup"><span data-stu-id="20d33-142">yes</span></span>      | <span data-ttu-id="20d33-143">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="20d33-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="20d33-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="20d33-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="20d33-145">API pour vérifier la clé de portée Vérifiez</span><span class="sxs-lookup"><span data-stu-id="20d33-145">API to verify the verify scope key</span></span>

<span data-ttu-id="20d33-146">Cette API est utilisée pour valider une clé de vérifier la portée pour le package détenu par l’auteur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20d33-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="20d33-147">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="20d33-147">Request parameters</span></span>

<span data-ttu-id="20d33-148">Name</span><span class="sxs-lookup"><span data-stu-id="20d33-148">Name</span></span>           | <span data-ttu-id="20d33-149">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="20d33-149">In</span></span>     | <span data-ttu-id="20d33-150">Type</span><span class="sxs-lookup"><span data-stu-id="20d33-150">Type</span></span>   | <span data-ttu-id="20d33-151">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="20d33-151">Required</span></span> | <span data-ttu-id="20d33-152">Notes</span><span class="sxs-lookup"><span data-stu-id="20d33-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="20d33-153">Id</span><span class="sxs-lookup"><span data-stu-id="20d33-153">ID</span></span>             | <span data-ttu-id="20d33-154">URL</span><span class="sxs-lookup"><span data-stu-id="20d33-154">URL</span></span>    | <span data-ttu-id="20d33-155">chaîne</span><span class="sxs-lookup"><span data-stu-id="20d33-155">string</span></span> | <span data-ttu-id="20d33-156">oui</span><span class="sxs-lookup"><span data-stu-id="20d33-156">yes</span></span>      | <span data-ttu-id="20d33-157">L’identificateur de package pour lequel la clé de portée Vérifiez est demandée</span><span class="sxs-lookup"><span data-stu-id="20d33-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="20d33-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="20d33-158">VERSION</span></span>        | <span data-ttu-id="20d33-159">URL</span><span class="sxs-lookup"><span data-stu-id="20d33-159">URL</span></span>    | <span data-ttu-id="20d33-160">chaîne</span><span class="sxs-lookup"><span data-stu-id="20d33-160">string</span></span> | <span data-ttu-id="20d33-161">Non</span><span class="sxs-lookup"><span data-stu-id="20d33-161">no</span></span>       | <span data-ttu-id="20d33-162">La version du package</span><span class="sxs-lookup"><span data-stu-id="20d33-162">The package version</span></span>
<span data-ttu-id="20d33-163">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="20d33-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="20d33-164">Header</span><span class="sxs-lookup"><span data-stu-id="20d33-164">Header</span></span> | <span data-ttu-id="20d33-165">chaîne</span><span class="sxs-lookup"><span data-stu-id="20d33-165">string</span></span> | <span data-ttu-id="20d33-166">oui</span><span class="sxs-lookup"><span data-stu-id="20d33-166">yes</span></span>      | <span data-ttu-id="20d33-167">Par exemple, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="20d33-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="20d33-168">Cette clé de portée API Vérifiez expire dans une journée ou à la première utilisation, selon ce qui se produit en premier.</span><span class="sxs-lookup"><span data-stu-id="20d33-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="20d33-169">Réponse</span><span class="sxs-lookup"><span data-stu-id="20d33-169">Response</span></span>

<span data-ttu-id="20d33-170">Code d’état</span><span class="sxs-lookup"><span data-stu-id="20d33-170">Status Code</span></span> | <span data-ttu-id="20d33-171">Signification</span><span class="sxs-lookup"><span data-stu-id="20d33-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="20d33-172">200</span><span class="sxs-lookup"><span data-stu-id="20d33-172">200</span></span>         | <span data-ttu-id="20d33-173">La clé API est valide</span><span class="sxs-lookup"><span data-stu-id="20d33-173">The API key is valid</span></span>
<span data-ttu-id="20d33-174">403</span><span class="sxs-lookup"><span data-stu-id="20d33-174">403</span></span>         | <span data-ttu-id="20d33-175">La clé API est non valide ou non autorisé à distribuer sur le package</span><span class="sxs-lookup"><span data-stu-id="20d33-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="20d33-176">404</span><span class="sxs-lookup"><span data-stu-id="20d33-176">404</span></span>         | <span data-ttu-id="20d33-177">Le package référencé par `ID` et `VERSION` (facultatif) n’existe pas</span><span class="sxs-lookup"><span data-stu-id="20d33-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
