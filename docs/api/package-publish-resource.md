---
title: Push et supprimer des API NuGet
description: Le service de publication permet aux clients publier les nouveaux packages et de retirer de la liste ou de supprimer des packages existants.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426720"
---
# <a name="push-and-delete"></a><span data-ttu-id="7433c-103">Push et supprimer</span><span class="sxs-lookup"><span data-stu-id="7433c-103">Push and Delete</span></span>

<span data-ttu-id="7433c-104">Il est possible d’envoyer, supprimer (ou retirer de la liste, selon l’implémentation de serveur) et les remettre dans la liste des packages à l’aide de l’API V3 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7433c-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="7433c-105">Ces opérations sont basées issu de la `PackagePublish` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7433c-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7433c-106">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="7433c-106">Versioning</span></span>

<span data-ttu-id="7433c-107">Ce qui suit `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="7433c-107">The following `@type` value is used:</span></span>

<span data-ttu-id="7433c-108">Valeur@type</span><span class="sxs-lookup"><span data-stu-id="7433c-108">@type value</span></span>          | <span data-ttu-id="7433c-109">Notes</span><span class="sxs-lookup"><span data-stu-id="7433c-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="7433c-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="7433c-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="7433c-111">La version initiale</span><span class="sxs-lookup"><span data-stu-id="7433c-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7433c-112">URL de base</span><span class="sxs-lookup"><span data-stu-id="7433c-112">Base URL</span></span>

<span data-ttu-id="7433c-113">L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans la source de package [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7433c-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="7433c-114">Pour obtenir la documentation ci-dessous, les URL de nuget.org est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7433c-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="7433c-115">Envisagez `https://www.nuget.org/api/v2/package` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="7433c-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="7433c-116">Notez que cette URL pointe vers le même emplacement que le point de terminaison push V2 héritée, étant donné que le protocole est le même.</span><span class="sxs-lookup"><span data-stu-id="7433c-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7433c-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="7433c-117">HTTP methods</span></span>

<span data-ttu-id="7433c-118">Le `PUT`, `POST` et `DELETE` méthodes HTTP sont pris en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="7433c-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="7433c-119">Pour les méthodes sont prises en charge sur chaque point de terminaison, voir ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7433c-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="7433c-120">Push d’un package</span><span class="sxs-lookup"><span data-stu-id="7433c-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="7433c-121">NuGet.org a [des exigences supplémentaires](NuGet-Protocols.md) permettant d’interagir avec le point de terminaison push.</span><span class="sxs-lookup"><span data-stu-id="7433c-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="7433c-122">NuGet.org prend en charge l’exécution de type push des nouveaux packages à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="7433c-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="7433c-123">Si le package avec l’ID et la version fournie existe déjà, nuget.org rejette la notification push.</span><span class="sxs-lookup"><span data-stu-id="7433c-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="7433c-124">Autres sources de package peuvent prendre en charge le remplacement d’un package existant.</span><span class="sxs-lookup"><span data-stu-id="7433c-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="7433c-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7433c-125">Request parameters</span></span>

<span data-ttu-id="7433c-126">Nom</span><span class="sxs-lookup"><span data-stu-id="7433c-126">Name</span></span>           | <span data-ttu-id="7433c-127">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="7433c-127">In</span></span>     | <span data-ttu-id="7433c-128">Type</span><span class="sxs-lookup"><span data-stu-id="7433c-128">Type</span></span>   | <span data-ttu-id="7433c-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7433c-129">Required</span></span> | <span data-ttu-id="7433c-130">Notes</span><span class="sxs-lookup"><span data-stu-id="7433c-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7433c-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7433c-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7433c-132">Header</span><span class="sxs-lookup"><span data-stu-id="7433c-132">Header</span></span> | <span data-ttu-id="7433c-133">string</span><span class="sxs-lookup"><span data-stu-id="7433c-133">string</span></span> | <span data-ttu-id="7433c-134">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-134">yes</span></span>      | <span data-ttu-id="7433c-135">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7433c-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="7433c-136">La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client.</span><span class="sxs-lookup"><span data-stu-id="7433c-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="7433c-137">Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="7433c-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="7433c-138">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="7433c-138">Request body</span></span>

<span data-ttu-id="7433c-139">Le corps de la demande doit être placée sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="7433c-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="7433c-140">Données de formulaire en plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="7433c-140">Multipart form data</span></span>

<span data-ttu-id="7433c-141">L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande est les octets bruts du fichier .nupkg poussé.</span><span class="sxs-lookup"><span data-stu-id="7433c-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="7433c-142">Les éléments suivants dans le corps en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="7433c-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="7433c-143">Le nom de fichier ou de tous les autres en-têtes des éléments en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="7433c-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="7433c-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="7433c-144">Response</span></span>

<span data-ttu-id="7433c-145">Code d’état</span><span class="sxs-lookup"><span data-stu-id="7433c-145">Status Code</span></span> | <span data-ttu-id="7433c-146">Signification</span><span class="sxs-lookup"><span data-stu-id="7433c-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="7433c-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="7433c-147">201, 202</span></span>    | <span data-ttu-id="7433c-148">Le package a été correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="7433c-148">The package was successfully pushed</span></span>
<span data-ttu-id="7433c-149">400</span><span class="sxs-lookup"><span data-stu-id="7433c-149">400</span></span>         | <span data-ttu-id="7433c-150">Le package fourni n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="7433c-150">The provided package is invalid</span></span>
<span data-ttu-id="7433c-151">409</span><span class="sxs-lookup"><span data-stu-id="7433c-151">409</span></span>         | <span data-ttu-id="7433c-152">Un package avec l’ID et la version fournie existe déjà</span><span class="sxs-lookup"><span data-stu-id="7433c-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="7433c-153">Les implémentations serveur varient sur le code d’état de réussite retourné lorsqu’un package est envoyé avec succès.</span><span class="sxs-lookup"><span data-stu-id="7433c-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="7433c-154">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="7433c-154">Delete a package</span></span>

<span data-ttu-id="7433c-155">NuGet.org interprète la demande de suppression de package comme un « retirer de la liste ».</span><span class="sxs-lookup"><span data-stu-id="7433c-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="7433c-156">Cela signifie que le package est toujours disponible pour les consommateurs existants du package, mais le package n’apparaît plus dans les résultats de recherche ou dans l’interface web.</span><span class="sxs-lookup"><span data-stu-id="7433c-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="7433c-157">Pour plus d’informations sur cette pratique, consultez le [Packages supprimés](../nuget-org/policies/deleting-packages.md) stratégie.</span><span class="sxs-lookup"><span data-stu-id="7433c-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="7433c-158">Autres implémentations de serveur sont libres d’interpréter ce signal comme une suppression de disque dur, de suppression réversible ou de retirer de la liste.</span><span class="sxs-lookup"><span data-stu-id="7433c-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="7433c-159">Par exemple, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur uniquement prise en charge de l’ancienne API V2) prend en charge la gestion de cette demande comme une suppression de la liste ou une suppression dure basée sur une option de configuration.</span><span class="sxs-lookup"><span data-stu-id="7433c-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="7433c-160">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7433c-160">Request parameters</span></span>

<span data-ttu-id="7433c-161">Nom</span><span class="sxs-lookup"><span data-stu-id="7433c-161">Name</span></span>           | <span data-ttu-id="7433c-162">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="7433c-162">In</span></span>     | <span data-ttu-id="7433c-163">Type</span><span class="sxs-lookup"><span data-stu-id="7433c-163">Type</span></span>   | <span data-ttu-id="7433c-164">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7433c-164">Required</span></span> | <span data-ttu-id="7433c-165">Notes</span><span class="sxs-lookup"><span data-stu-id="7433c-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7433c-166">Id</span><span class="sxs-lookup"><span data-stu-id="7433c-166">ID</span></span>             | <span data-ttu-id="7433c-167">URL</span><span class="sxs-lookup"><span data-stu-id="7433c-167">URL</span></span>    | <span data-ttu-id="7433c-168">string</span><span class="sxs-lookup"><span data-stu-id="7433c-168">string</span></span> | <span data-ttu-id="7433c-169">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-169">yes</span></span>      | <span data-ttu-id="7433c-170">L’ID du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="7433c-170">The ID of the package to delete</span></span>
<span data-ttu-id="7433c-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="7433c-171">VERSION</span></span>        | <span data-ttu-id="7433c-172">URL</span><span class="sxs-lookup"><span data-stu-id="7433c-172">URL</span></span>    | <span data-ttu-id="7433c-173">string</span><span class="sxs-lookup"><span data-stu-id="7433c-173">string</span></span> | <span data-ttu-id="7433c-174">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-174">yes</span></span>      | <span data-ttu-id="7433c-175">La version du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="7433c-175">The version of the package to delete</span></span>
<span data-ttu-id="7433c-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7433c-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7433c-177">Header</span><span class="sxs-lookup"><span data-stu-id="7433c-177">Header</span></span> | <span data-ttu-id="7433c-178">string</span><span class="sxs-lookup"><span data-stu-id="7433c-178">string</span></span> | <span data-ttu-id="7433c-179">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-179">yes</span></span>      | <span data-ttu-id="7433c-180">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7433c-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="7433c-181">Réponse</span><span class="sxs-lookup"><span data-stu-id="7433c-181">Response</span></span>

<span data-ttu-id="7433c-182">Code d’état</span><span class="sxs-lookup"><span data-stu-id="7433c-182">Status Code</span></span> | <span data-ttu-id="7433c-183">Signification</span><span class="sxs-lookup"><span data-stu-id="7433c-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="7433c-184">204</span><span class="sxs-lookup"><span data-stu-id="7433c-184">204</span></span>         | <span data-ttu-id="7433c-185">Le package a été supprimé</span><span class="sxs-lookup"><span data-stu-id="7433c-185">The package was deleted</span></span>
<span data-ttu-id="7433c-186">404</span><span class="sxs-lookup"><span data-stu-id="7433c-186">404</span></span>         | <span data-ttu-id="7433c-187">Aucun package avec l’argument `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="7433c-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="7433c-188">Remettre dans la liste d’un package</span><span class="sxs-lookup"><span data-stu-id="7433c-188">Relist a package</span></span>

<span data-ttu-id="7433c-189">Si un package n’est pas répertorié, il est possible de rendre ce package une fois encore visible dans les résultats de recherche à l’aide du point de terminaison « remise ».</span><span class="sxs-lookup"><span data-stu-id="7433c-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="7433c-190">Ce point de terminaison a la même forme que la [supprimer (retirer de la liste) point de terminaison](#delete-a-package) , mais utilise le `POST` méthode HTTP au lieu du `DELETE` (méthode).</span><span class="sxs-lookup"><span data-stu-id="7433c-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="7433c-191">Si le package est déjà répertorié, la demande réussit toujours.</span><span class="sxs-lookup"><span data-stu-id="7433c-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="7433c-192">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7433c-192">Request parameters</span></span>

<span data-ttu-id="7433c-193">Nom</span><span class="sxs-lookup"><span data-stu-id="7433c-193">Name</span></span>           | <span data-ttu-id="7433c-194">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="7433c-194">In</span></span>     | <span data-ttu-id="7433c-195">Type</span><span class="sxs-lookup"><span data-stu-id="7433c-195">Type</span></span>   | <span data-ttu-id="7433c-196">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7433c-196">Required</span></span> | <span data-ttu-id="7433c-197">Notes</span><span class="sxs-lookup"><span data-stu-id="7433c-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7433c-198">Id</span><span class="sxs-lookup"><span data-stu-id="7433c-198">ID</span></span>             | <span data-ttu-id="7433c-199">URL</span><span class="sxs-lookup"><span data-stu-id="7433c-199">URL</span></span>    | <span data-ttu-id="7433c-200">string</span><span class="sxs-lookup"><span data-stu-id="7433c-200">string</span></span> | <span data-ttu-id="7433c-201">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-201">yes</span></span>      | <span data-ttu-id="7433c-202">L’ID du package à remettre dans la liste</span><span class="sxs-lookup"><span data-stu-id="7433c-202">The ID of the package to relist</span></span>
<span data-ttu-id="7433c-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="7433c-203">VERSION</span></span>        | <span data-ttu-id="7433c-204">URL</span><span class="sxs-lookup"><span data-stu-id="7433c-204">URL</span></span>    | <span data-ttu-id="7433c-205">string</span><span class="sxs-lookup"><span data-stu-id="7433c-205">string</span></span> | <span data-ttu-id="7433c-206">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-206">yes</span></span>      | <span data-ttu-id="7433c-207">La version du package à remettre dans la liste</span><span class="sxs-lookup"><span data-stu-id="7433c-207">The version of the package to relist</span></span>
<span data-ttu-id="7433c-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7433c-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7433c-209">Header</span><span class="sxs-lookup"><span data-stu-id="7433c-209">Header</span></span> | <span data-ttu-id="7433c-210">string</span><span class="sxs-lookup"><span data-stu-id="7433c-210">string</span></span> | <span data-ttu-id="7433c-211">oui</span><span class="sxs-lookup"><span data-stu-id="7433c-211">yes</span></span>      | <span data-ttu-id="7433c-212">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7433c-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="7433c-213">Réponse</span><span class="sxs-lookup"><span data-stu-id="7433c-213">Response</span></span>

<span data-ttu-id="7433c-214">Code d’état</span><span class="sxs-lookup"><span data-stu-id="7433c-214">Status Code</span></span> | <span data-ttu-id="7433c-215">Signification</span><span class="sxs-lookup"><span data-stu-id="7433c-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="7433c-216">200</span><span class="sxs-lookup"><span data-stu-id="7433c-216">200</span></span>         | <span data-ttu-id="7433c-217">Le package est maintenant répertorié.</span><span class="sxs-lookup"><span data-stu-id="7433c-217">The package is now listed</span></span>
<span data-ttu-id="7433c-218">404</span><span class="sxs-lookup"><span data-stu-id="7433c-218">404</span></span>         | <span data-ttu-id="7433c-219">Aucun package avec l’argument `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="7433c-219">No package with the provided `ID` and `VERSION` exists</span></span>
