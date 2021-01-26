---
title: Push et Delete, API NuGet
description: Le service de publication permet aux clients de publier de nouveaux packages et de retirer ou de supprimer des packages existants.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773923"
---
# <a name="push-and-delete"></a><span data-ttu-id="71159-103">Push et Delete</span><span class="sxs-lookup"><span data-stu-id="71159-103">Push and Delete</span></span>

<span data-ttu-id="71159-104">Il est possible d’effectuer un push, une suppression (ou une annulation de liste, selon l’implémentation du serveur) et de relister les packages à l’aide de l’API NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="71159-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="71159-105">Ces opérations sont basées sur la `PackagePublish` ressource trouvée dans l' [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="71159-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="71159-106">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="71159-106">Versioning</span></span>

<span data-ttu-id="71159-107">La `@type` valeur suivante est utilisée :</span><span class="sxs-lookup"><span data-stu-id="71159-107">The following `@type` value is used:</span></span>

<span data-ttu-id="71159-108">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="71159-108">@type value</span></span>          | <span data-ttu-id="71159-109">Notes</span><span class="sxs-lookup"><span data-stu-id="71159-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="71159-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="71159-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="71159-111">La version initiale</span><span class="sxs-lookup"><span data-stu-id="71159-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="71159-112">URL de base</span><span class="sxs-lookup"><span data-stu-id="71159-112">Base URL</span></span>

<span data-ttu-id="71159-113">L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans l’index de [service](service-index.md)de la source du package.</span><span class="sxs-lookup"><span data-stu-id="71159-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="71159-114">Pour la documentation ci-dessous, l’URL de NuGet. org est utilisée.</span><span class="sxs-lookup"><span data-stu-id="71159-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="71159-115">Considérez `https://www.nuget.org/api/v2/package` comme un espace réservé pour la `@id` valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="71159-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="71159-116">Notez que cette URL pointe vers le même emplacement que le point de terminaison v2 Push hérité puisque le protocole est le même.</span><span class="sxs-lookup"><span data-stu-id="71159-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="71159-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="71159-117">HTTP methods</span></span>

<span data-ttu-id="71159-118">Les `PUT` `POST` `DELETE` méthodes http et sont prises en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="71159-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="71159-119">Pour connaître les méthodes prises en charge sur chaque point de terminaison, voir ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="71159-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="71159-120">Envoyer (push) un package</span><span class="sxs-lookup"><span data-stu-id="71159-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="71159-121">nuget.org a des [exigences supplémentaires](NuGet-Protocols.md) pour interagir avec le point de terminaison push.</span><span class="sxs-lookup"><span data-stu-id="71159-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="71159-122">nuget.org prend en charge le push de nouveaux packages à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="71159-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="71159-123">Si le package avec l’ID et la version fournis existe déjà, nuget.org rejette l’opération push.</span><span class="sxs-lookup"><span data-stu-id="71159-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="71159-124">D’autres sources de package peuvent prendre en charge le remplacement d’un package existant.</span><span class="sxs-lookup"><span data-stu-id="71159-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="71159-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="71159-125">Request parameters</span></span>

<span data-ttu-id="71159-126">Nom</span><span class="sxs-lookup"><span data-stu-id="71159-126">Name</span></span>           | <span data-ttu-id="71159-127">Dans</span><span class="sxs-lookup"><span data-stu-id="71159-127">In</span></span>     | <span data-ttu-id="71159-128">Type</span><span class="sxs-lookup"><span data-stu-id="71159-128">Type</span></span>   | <span data-ttu-id="71159-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="71159-129">Required</span></span> | <span data-ttu-id="71159-130">Notes</span><span class="sxs-lookup"><span data-stu-id="71159-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="71159-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="71159-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="71159-132">En-tête</span><span class="sxs-lookup"><span data-stu-id="71159-132">Header</span></span> | <span data-ttu-id="71159-133">string</span><span class="sxs-lookup"><span data-stu-id="71159-133">string</span></span> | <span data-ttu-id="71159-134">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-134">yes</span></span>      | <span data-ttu-id="71159-135">Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="71159-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="71159-136">La clé API est une chaîne opaque obtenue à partir de la source du package par l’utilisateur et configurée dans le client.</span><span class="sxs-lookup"><span data-stu-id="71159-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="71159-137">Aucun format de chaîne particulier n’est mandaté, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="71159-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="71159-138">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="71159-138">Request body</span></span>

<span data-ttu-id="71159-139">Le corps de la demande doit se présenter sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="71159-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="71159-140">Données de formulaire en plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="71159-140">Multipart form data</span></span>

<span data-ttu-id="71159-141">L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande correspond aux octets bruts du. nupkg faisant l’objet d’un push.</span><span class="sxs-lookup"><span data-stu-id="71159-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="71159-142">Les éléments suivants dans le corps en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="71159-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="71159-143">Le nom de fichier ou tout autre en-tête des éléments en plusieurs parties est ignoré.</span><span class="sxs-lookup"><span data-stu-id="71159-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="71159-144">response</span><span class="sxs-lookup"><span data-stu-id="71159-144">Response</span></span>

<span data-ttu-id="71159-145">Code d’état</span><span class="sxs-lookup"><span data-stu-id="71159-145">Status Code</span></span> | <span data-ttu-id="71159-146">Signification</span><span class="sxs-lookup"><span data-stu-id="71159-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="71159-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="71159-147">201, 202</span></span>    | <span data-ttu-id="71159-148">Le package a bien fait l’objet d’un push</span><span class="sxs-lookup"><span data-stu-id="71159-148">The package was successfully pushed</span></span>
<span data-ttu-id="71159-149">400</span><span class="sxs-lookup"><span data-stu-id="71159-149">400</span></span>         | <span data-ttu-id="71159-150">Le package fourni n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="71159-150">The provided package is invalid</span></span>
<span data-ttu-id="71159-151">409</span><span class="sxs-lookup"><span data-stu-id="71159-151">409</span></span>         | <span data-ttu-id="71159-152">Un package avec l’ID et la version fournis existe déjà</span><span class="sxs-lookup"><span data-stu-id="71159-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="71159-153">Les implémentations de serveur varient en fonction du code d’état de réussite renvoyé lorsqu’un package est correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="71159-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="71159-154">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="71159-154">Delete a package</span></span>

<span data-ttu-id="71159-155">nuget.org interprète la demande de suppression du package comme une « annulation de la liste ».</span><span class="sxs-lookup"><span data-stu-id="71159-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="71159-156">Cela signifie que le package est toujours disponible pour les consommateurs existants du package, mais le package n’apparaît plus dans les résultats de la recherche ou dans l’interface Web.</span><span class="sxs-lookup"><span data-stu-id="71159-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="71159-157">Pour plus d’informations sur cette pratique, consultez la stratégie [packages supprimés](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="71159-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="71159-158">D’autres implémentations de serveur sont gratuites pour interpréter ce signal comme une suppression définitive, une suppression réversible ou une suppression de liste.</span><span class="sxs-lookup"><span data-stu-id="71159-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="71159-159">Par exemple, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur qui prend uniquement en charge l’ancienne API v2) prend en charge la gestion de cette demande sous la forme d’une suppression de liste ou d’une suppression forcée basée sur une option de configuration.</span><span class="sxs-lookup"><span data-stu-id="71159-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="71159-160">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="71159-160">Request parameters</span></span>

<span data-ttu-id="71159-161">Nom</span><span class="sxs-lookup"><span data-stu-id="71159-161">Name</span></span>           | <span data-ttu-id="71159-162">Dans</span><span class="sxs-lookup"><span data-stu-id="71159-162">In</span></span>     | <span data-ttu-id="71159-163">Type</span><span class="sxs-lookup"><span data-stu-id="71159-163">Type</span></span>   | <span data-ttu-id="71159-164">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="71159-164">Required</span></span> | <span data-ttu-id="71159-165">Notes</span><span class="sxs-lookup"><span data-stu-id="71159-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="71159-166">id</span><span class="sxs-lookup"><span data-stu-id="71159-166">ID</span></span>             | <span data-ttu-id="71159-167">URL</span><span class="sxs-lookup"><span data-stu-id="71159-167">URL</span></span>    | <span data-ttu-id="71159-168">string</span><span class="sxs-lookup"><span data-stu-id="71159-168">string</span></span> | <span data-ttu-id="71159-169">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-169">yes</span></span>      | <span data-ttu-id="71159-170">ID du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="71159-170">The ID of the package to delete</span></span>
<span data-ttu-id="71159-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="71159-171">VERSION</span></span>        | <span data-ttu-id="71159-172">URL</span><span class="sxs-lookup"><span data-stu-id="71159-172">URL</span></span>    | <span data-ttu-id="71159-173">string</span><span class="sxs-lookup"><span data-stu-id="71159-173">string</span></span> | <span data-ttu-id="71159-174">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-174">yes</span></span>      | <span data-ttu-id="71159-175">Version du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="71159-175">The version of the package to delete</span></span>
<span data-ttu-id="71159-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="71159-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="71159-177">En-tête</span><span class="sxs-lookup"><span data-stu-id="71159-177">Header</span></span> | <span data-ttu-id="71159-178">string</span><span class="sxs-lookup"><span data-stu-id="71159-178">string</span></span> | <span data-ttu-id="71159-179">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-179">yes</span></span>      | <span data-ttu-id="71159-180">Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="71159-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="71159-181">response</span><span class="sxs-lookup"><span data-stu-id="71159-181">Response</span></span>

<span data-ttu-id="71159-182">Code d’état</span><span class="sxs-lookup"><span data-stu-id="71159-182">Status Code</span></span> | <span data-ttu-id="71159-183">Signification</span><span class="sxs-lookup"><span data-stu-id="71159-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="71159-184">204</span><span class="sxs-lookup"><span data-stu-id="71159-184">204</span></span>         | <span data-ttu-id="71159-185">Le package a été supprimé</span><span class="sxs-lookup"><span data-stu-id="71159-185">The package was deleted</span></span>
<span data-ttu-id="71159-186">404</span><span class="sxs-lookup"><span data-stu-id="71159-186">404</span></span>         | <span data-ttu-id="71159-187">Aucun package avec le fourni `ID` et n' `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="71159-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="71159-188">Remettre en vente un package</span><span class="sxs-lookup"><span data-stu-id="71159-188">Relist a package</span></span>

<span data-ttu-id="71159-189">Si un package n’est pas répertorié, il est possible de le rendre à nouveau visible dans les résultats de la recherche à l’aide du point de terminaison « Relist ».</span><span class="sxs-lookup"><span data-stu-id="71159-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="71159-190">Ce point de terminaison a la même forme que le [point de terminaison de suppression (Unlist)](#delete-a-package) , mais utilise la `POST` méthode http à la place de la `DELETE` méthode.</span><span class="sxs-lookup"><span data-stu-id="71159-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="71159-191">Si le package est déjà listé, la demande est toujours réussie.</span><span class="sxs-lookup"><span data-stu-id="71159-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="71159-192">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="71159-192">Request parameters</span></span>

<span data-ttu-id="71159-193">Nom</span><span class="sxs-lookup"><span data-stu-id="71159-193">Name</span></span>           | <span data-ttu-id="71159-194">Dans</span><span class="sxs-lookup"><span data-stu-id="71159-194">In</span></span>     | <span data-ttu-id="71159-195">Type</span><span class="sxs-lookup"><span data-stu-id="71159-195">Type</span></span>   | <span data-ttu-id="71159-196">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="71159-196">Required</span></span> | <span data-ttu-id="71159-197">Notes</span><span class="sxs-lookup"><span data-stu-id="71159-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="71159-198">id</span><span class="sxs-lookup"><span data-stu-id="71159-198">ID</span></span>             | <span data-ttu-id="71159-199">URL</span><span class="sxs-lookup"><span data-stu-id="71159-199">URL</span></span>    | <span data-ttu-id="71159-200">string</span><span class="sxs-lookup"><span data-stu-id="71159-200">string</span></span> | <span data-ttu-id="71159-201">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-201">yes</span></span>      | <span data-ttu-id="71159-202">ID du package à remettre en liste</span><span class="sxs-lookup"><span data-stu-id="71159-202">The ID of the package to relist</span></span>
<span data-ttu-id="71159-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="71159-203">VERSION</span></span>        | <span data-ttu-id="71159-204">URL</span><span class="sxs-lookup"><span data-stu-id="71159-204">URL</span></span>    | <span data-ttu-id="71159-205">string</span><span class="sxs-lookup"><span data-stu-id="71159-205">string</span></span> | <span data-ttu-id="71159-206">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-206">yes</span></span>      | <span data-ttu-id="71159-207">Version du package à remettre en vente</span><span class="sxs-lookup"><span data-stu-id="71159-207">The version of the package to relist</span></span>
<span data-ttu-id="71159-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="71159-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="71159-209">En-tête</span><span class="sxs-lookup"><span data-stu-id="71159-209">Header</span></span> | <span data-ttu-id="71159-210">string</span><span class="sxs-lookup"><span data-stu-id="71159-210">string</span></span> | <span data-ttu-id="71159-211">Oui</span><span class="sxs-lookup"><span data-stu-id="71159-211">yes</span></span>      | <span data-ttu-id="71159-212">Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="71159-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="71159-213">response</span><span class="sxs-lookup"><span data-stu-id="71159-213">Response</span></span>

<span data-ttu-id="71159-214">Code d’état</span><span class="sxs-lookup"><span data-stu-id="71159-214">Status Code</span></span> | <span data-ttu-id="71159-215">Signification</span><span class="sxs-lookup"><span data-stu-id="71159-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="71159-216">200</span><span class="sxs-lookup"><span data-stu-id="71159-216">200</span></span>         | <span data-ttu-id="71159-217">Le package est maintenant listé</span><span class="sxs-lookup"><span data-stu-id="71159-217">The package is now listed</span></span>
<span data-ttu-id="71159-218">404</span><span class="sxs-lookup"><span data-stu-id="71159-218">404</span></span>         | <span data-ttu-id="71159-219">Aucun package avec le fourni `ID` et n' `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="71159-219">No package with the provided `ID` and `VERSION` exists</span></span>
