---
title: les protocoles NuGet.org | Documents Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Les protocoles nuget.org en constante évolution pour interagir avec les clients NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="b821b-103">Protocoles NuGet.org</span><span class="sxs-lookup"><span data-stu-id="b821b-103">nuget.org Protocols</span></span>

<span data-ttu-id="b821b-104">Pour interagir avec nuget.org, les clients doivent suivre certains protocoles.</span><span class="sxs-lookup"><span data-stu-id="b821b-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="b821b-105">Étant donné que ces protocoles conservent en constante évolution, les clients doivent identifier la version du protocole qu’ils utilisent lors de l’appel d’API de nuget.org spécifique.</span><span class="sxs-lookup"><span data-stu-id="b821b-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="b821b-106">Cela permet de nuget.org apporter des modifications d’une manière sans rupture pour les anciens clients.</span><span class="sxs-lookup"><span data-stu-id="b821b-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="b821b-107">Les API décrites dans cette page sont spécifiques à nuget.org et n’est pas garantie pour d’autres implémentations de serveur NuGet présenter ces API.</span><span class="sxs-lookup"><span data-stu-id="b821b-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="b821b-108">Pour plus d’informations sur l’API NuGet implémentés largement dans l’écosystème de NuGet, consultez le [présentation de l’API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="b821b-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="b821b-109">Cette rubrique répertorie les différents protocoles en tant qu’et lorsque leur présence.</span><span class="sxs-lookup"><span data-stu-id="b821b-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="b821b-110">Version du protocole NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="b821b-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="b821b-111">Le 4.1.0 protocole spécifie l’utilisation de clés de portée vérifier pour interagir avec les services autres que nuget.org, pour valider un package avec un compte de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b821b-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="b821b-112">Notez que le `4.1.0` version nombre est une chaîne opaque mais se produit pour coïncider avec la première version du client NuGet officiel pris en charge ce protocole.</span><span class="sxs-lookup"><span data-stu-id="b821b-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="b821b-113">Validation garantit que les clés API créés par l’utilisateur sont utilisées uniquement avec nuget.org, et que cette vérification ou la validation à partir d’un service tiers est gérée via un usage des clés de vérifier l’étendue.</span><span class="sxs-lookup"><span data-stu-id="b821b-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="b821b-114">Ces clés de vérifier l’étendue peuvent être utilisées pour valider que le package appartient à un utilisateur spécifique (compte) sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b821b-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="b821b-115">Spécification du client</span><span class="sxs-lookup"><span data-stu-id="b821b-115">Client requirement</span></span>

<span data-ttu-id="b821b-116">Les clients doivent passer de l’en-tête suivant lorsqu’ils effectuent des appels d’API à **push** packages nuget.org :</span><span class="sxs-lookup"><span data-stu-id="b821b-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="b821b-117">Notez que le préexistant `X-NuGet-Client-Version` en-tête a le même objectif, mais est désormais déconseillé et ne doit plus être utilisé.</span><span class="sxs-lookup"><span data-stu-id="b821b-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="b821b-118">Le **push** protocole lui-même est décrit dans la documentation relative à la [ `PackagePublish` ressources](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b821b-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="b821b-119">Si un client interagit avec les services externes et des besoins pour vérifier si un package appartient à un utilisateur spécifique (compte), il doit utiliser le protocole suivant et utiliser les clés de l’étendue de la vérification et pas les clés de l’API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b821b-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="b821b-120">API pour demander une clé de vérification étendue</span><span class="sxs-lookup"><span data-stu-id="b821b-120">API to request a verify-scope key</span></span>

<span data-ttu-id="b821b-121">Cette API est utilisée pour obtenir une clé de l’étendue de la vérification d’un auteur nuget.org valider un package détenu par ce dernier.</span><span class="sxs-lookup"><span data-stu-id="b821b-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="b821b-122">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="b821b-122">Request parameters</span></span>

<span data-ttu-id="b821b-123">Nom</span><span class="sxs-lookup"><span data-stu-id="b821b-123">Name</span></span>           | <span data-ttu-id="b821b-124">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="b821b-124">In</span></span>     | <span data-ttu-id="b821b-125">Type</span><span class="sxs-lookup"><span data-stu-id="b821b-125">Type</span></span>   | <span data-ttu-id="b821b-126">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="b821b-126">Required</span></span> | <span data-ttu-id="b821b-127">Remarques</span><span class="sxs-lookup"><span data-stu-id="b821b-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b821b-128">Id</span><span class="sxs-lookup"><span data-stu-id="b821b-128">ID</span></span>             | <span data-ttu-id="b821b-129">URL</span><span class="sxs-lookup"><span data-stu-id="b821b-129">URL</span></span>    | <span data-ttu-id="b821b-130">chaîne</span><span class="sxs-lookup"><span data-stu-id="b821b-130">string</span></span> | <span data-ttu-id="b821b-131">oui</span><span class="sxs-lookup"><span data-stu-id="b821b-131">yes</span></span>      | <span data-ttu-id="b821b-132">L’identidier de package pour lequel la clé de portée Vérifiez est demandée</span><span class="sxs-lookup"><span data-stu-id="b821b-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="b821b-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="b821b-133">VERSION</span></span>        | <span data-ttu-id="b821b-134">URL</span><span class="sxs-lookup"><span data-stu-id="b821b-134">URL</span></span>    | <span data-ttu-id="b821b-135">chaîne</span><span class="sxs-lookup"><span data-stu-id="b821b-135">string</span></span> | <span data-ttu-id="b821b-136">Non</span><span class="sxs-lookup"><span data-stu-id="b821b-136">no</span></span>       | <span data-ttu-id="b821b-137">La version du package</span><span class="sxs-lookup"><span data-stu-id="b821b-137">The package version</span></span>
<span data-ttu-id="b821b-138">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b821b-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b821b-139">Header</span><span class="sxs-lookup"><span data-stu-id="b821b-139">Header</span></span> | <span data-ttu-id="b821b-140">chaîne</span><span class="sxs-lookup"><span data-stu-id="b821b-140">string</span></span> | <span data-ttu-id="b821b-141">oui</span><span class="sxs-lookup"><span data-stu-id="b821b-141">yes</span></span>      | <span data-ttu-id="b821b-142">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="b821b-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="b821b-143">Réponse</span><span class="sxs-lookup"><span data-stu-id="b821b-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="b821b-144">API pour vérifier la clé de portée Vérifiez</span><span class="sxs-lookup"><span data-stu-id="b821b-144">API to verify the verify scope key</span></span>

<span data-ttu-id="b821b-145">Cette API est utilisée pour valider une clé de vérifier la portée pour le package détenu par l’auteur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b821b-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="b821b-146">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="b821b-146">Request parameters</span></span>

<span data-ttu-id="b821b-147">Nom</span><span class="sxs-lookup"><span data-stu-id="b821b-147">Name</span></span>           | <span data-ttu-id="b821b-148">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="b821b-148">In</span></span>     | <span data-ttu-id="b821b-149">Type</span><span class="sxs-lookup"><span data-stu-id="b821b-149">Type</span></span>   | <span data-ttu-id="b821b-150">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="b821b-150">Required</span></span> | <span data-ttu-id="b821b-151">Remarques</span><span class="sxs-lookup"><span data-stu-id="b821b-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="b821b-152">Id</span><span class="sxs-lookup"><span data-stu-id="b821b-152">ID</span></span>             | <span data-ttu-id="b821b-153">URL</span><span class="sxs-lookup"><span data-stu-id="b821b-153">URL</span></span>    | <span data-ttu-id="b821b-154">chaîne</span><span class="sxs-lookup"><span data-stu-id="b821b-154">string</span></span> | <span data-ttu-id="b821b-155">oui</span><span class="sxs-lookup"><span data-stu-id="b821b-155">yes</span></span>      | <span data-ttu-id="b821b-156">L’identificateur de package pour lequel la clé de portée Vérifiez est demandée</span><span class="sxs-lookup"><span data-stu-id="b821b-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="b821b-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="b821b-157">VERSION</span></span>        | <span data-ttu-id="b821b-158">URL</span><span class="sxs-lookup"><span data-stu-id="b821b-158">URL</span></span>    | <span data-ttu-id="b821b-159">chaîne</span><span class="sxs-lookup"><span data-stu-id="b821b-159">string</span></span> | <span data-ttu-id="b821b-160">Non</span><span class="sxs-lookup"><span data-stu-id="b821b-160">no</span></span>       | <span data-ttu-id="b821b-161">La version du package</span><span class="sxs-lookup"><span data-stu-id="b821b-161">The package version</span></span>
<span data-ttu-id="b821b-162">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b821b-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b821b-163">Header</span><span class="sxs-lookup"><span data-stu-id="b821b-163">Header</span></span> | <span data-ttu-id="b821b-164">chaîne</span><span class="sxs-lookup"><span data-stu-id="b821b-164">string</span></span> | <span data-ttu-id="b821b-165">oui</span><span class="sxs-lookup"><span data-stu-id="b821b-165">yes</span></span>      | <span data-ttu-id="b821b-166">Par exemple, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="b821b-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="b821b-167">Cette clé de portée API Vérifiez expire dans une journée ou à la première utilisation, selon ce qui se produit en premier.</span><span class="sxs-lookup"><span data-stu-id="b821b-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="b821b-168">Réponse</span><span class="sxs-lookup"><span data-stu-id="b821b-168">Response</span></span>

<span data-ttu-id="b821b-169">Code d’état</span><span class="sxs-lookup"><span data-stu-id="b821b-169">Status Code</span></span> | <span data-ttu-id="b821b-170">Signification</span><span class="sxs-lookup"><span data-stu-id="b821b-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="b821b-171">200</span><span class="sxs-lookup"><span data-stu-id="b821b-171">200</span></span>         | <span data-ttu-id="b821b-172">La clé API est valide</span><span class="sxs-lookup"><span data-stu-id="b821b-172">The API key is valid</span></span>
<span data-ttu-id="b821b-173">403</span><span class="sxs-lookup"><span data-stu-id="b821b-173">403</span></span>         | <span data-ttu-id="b821b-174">La clé API est non valide ou non autorisé à distribuer sur le package</span><span class="sxs-lookup"><span data-stu-id="b821b-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="b821b-175">404</span><span class="sxs-lookup"><span data-stu-id="b821b-175">404</span></span>         | <span data-ttu-id="b821b-176">Le package référencé par `ID` et `VERSION` (facultatif) n’existe pas</span><span class="sxs-lookup"><span data-stu-id="b821b-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
