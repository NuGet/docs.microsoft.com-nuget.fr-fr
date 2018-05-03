---
title: Push et supprimer, NuGet API
description: Le service de publication autorise les clients à publier les nouveaux packages et de retrait de la liste ou de supprimer des packages existants.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="72266-103">Push et supprimer</span><span class="sxs-lookup"><span data-stu-id="72266-103">Push and Delete</span></span>

<span data-ttu-id="72266-104">Il est possible de transmettre, supprimer (ou retirer de la liste, en fonction de l’implémentation du serveur) et la remise des packages à l’aide de l’API de V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="72266-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="72266-105">Ces opérations sont en fonction de la `PackagePublish` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="72266-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="72266-106">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="72266-106">Versioning</span></span>

<span data-ttu-id="72266-107">Les éléments suivants `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="72266-107">The following `@type` value is used:</span></span>

<span data-ttu-id="72266-108">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="72266-108">@type value</span></span>          | <span data-ttu-id="72266-109">Notes</span><span class="sxs-lookup"><span data-stu-id="72266-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="72266-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="72266-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="72266-111">La version initiale</span><span class="sxs-lookup"><span data-stu-id="72266-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="72266-112">URL de base</span><span class="sxs-lookup"><span data-stu-id="72266-112">Base URL</span></span>

<span data-ttu-id="72266-113">L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans la source de package [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="72266-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="72266-114">Pour obtenir la documentation ci-dessous, nuget.org URL est utilisé.</span><span class="sxs-lookup"><span data-stu-id="72266-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="72266-115">Envisagez de `https://www.nuget.org/api/v2/package` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="72266-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="72266-116">Notez que cette URL pointe vers le même emplacement que le point de terminaison de push V2 hérité, car le protocole est le même.</span><span class="sxs-lookup"><span data-stu-id="72266-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="72266-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="72266-117">HTTP methods</span></span>

<span data-ttu-id="72266-118">Le `PUT`, `POST` et `DELETE` méthodes HTTP sont pris en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="72266-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="72266-119">Pour les méthodes qui sont pris en charge sur chaque point de terminaison, voir ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="72266-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="72266-120">Un package de push</span><span class="sxs-lookup"><span data-stu-id="72266-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="72266-121">NuGet.org a [exigences supplémentaires](NuGet-Protocols.md) pour interagir avec le point de terminaison par émission de données.</span><span class="sxs-lookup"><span data-stu-id="72266-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="72266-122">NuGet.org prend en charge l’exécution d’un push des nouveaux packages à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="72266-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="72266-123">Si le package avec l’ID et la version fourni existe déjà, nuget.org rejette le push.</span><span class="sxs-lookup"><span data-stu-id="72266-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="72266-124">Autres sources de package peuvent prendre en charge le remplacement d’un package existant.</span><span class="sxs-lookup"><span data-stu-id="72266-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="72266-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="72266-125">Request parameters</span></span>

<span data-ttu-id="72266-126">Name</span><span class="sxs-lookup"><span data-stu-id="72266-126">Name</span></span>           | <span data-ttu-id="72266-127">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="72266-127">In</span></span>     | <span data-ttu-id="72266-128">Type</span><span class="sxs-lookup"><span data-stu-id="72266-128">Type</span></span>   | <span data-ttu-id="72266-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="72266-129">Required</span></span> | <span data-ttu-id="72266-130">Notes</span><span class="sxs-lookup"><span data-stu-id="72266-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="72266-131">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="72266-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="72266-132">Header</span><span class="sxs-lookup"><span data-stu-id="72266-132">Header</span></span> | <span data-ttu-id="72266-133">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-133">string</span></span> | <span data-ttu-id="72266-134">oui</span><span class="sxs-lookup"><span data-stu-id="72266-134">yes</span></span>      | <span data-ttu-id="72266-135">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="72266-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="72266-136">La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client.</span><span class="sxs-lookup"><span data-stu-id="72266-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="72266-137">Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé d’API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="72266-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="72266-138">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="72266-138">Request body</span></span>

<span data-ttu-id="72266-139">Le corps de la demande doit être placée sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="72266-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="72266-140">Données de formulaire en plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="72266-140">Multipart form data</span></span>

<span data-ttu-id="72266-141">L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande est les octets bruts de le .nupkg lancé.</span><span class="sxs-lookup"><span data-stu-id="72266-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="72266-142">Les éléments suivants dans le corps en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="72266-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="72266-143">Le nom de fichier ou de tous les autres en-têtes des éléments en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="72266-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="72266-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="72266-144">Response</span></span>

<span data-ttu-id="72266-145">Code d’état</span><span class="sxs-lookup"><span data-stu-id="72266-145">Status Code</span></span> | <span data-ttu-id="72266-146">Signification</span><span class="sxs-lookup"><span data-stu-id="72266-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="72266-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="72266-147">201, 202</span></span>    | <span data-ttu-id="72266-148">Le package a été envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="72266-148">The package was successfully pushed</span></span>
<span data-ttu-id="72266-149">400</span><span class="sxs-lookup"><span data-stu-id="72266-149">400</span></span>         | <span data-ttu-id="72266-150">Le package fourni n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="72266-150">The provided package is invalid</span></span>
<span data-ttu-id="72266-151">409</span><span class="sxs-lookup"><span data-stu-id="72266-151">409</span></span>         | <span data-ttu-id="72266-152">Un package avec l’ID et la version fourni existe déjà</span><span class="sxs-lookup"><span data-stu-id="72266-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="72266-153">Les implémentations de serveur varient selon le code d’état de réussite retournés lorsqu’un package est envoyé avec succès.</span><span class="sxs-lookup"><span data-stu-id="72266-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="72266-154">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="72266-154">Delete a package</span></span>

<span data-ttu-id="72266-155">NuGet.org interprète la demande de suppression de package comme un « retirer de la liste ».</span><span class="sxs-lookup"><span data-stu-id="72266-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="72266-156">Cela signifie que le package est toujours disponible pour les utilisateurs existants du package, mais le package ne s’affiche plus dans les résultats de la recherche ou dans l’interface web.</span><span class="sxs-lookup"><span data-stu-id="72266-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="72266-157">Pour plus d’informations sur cette pratique, consultez la [supprimé les Packages](../policies/deleting-packages.md) stratégie.</span><span class="sxs-lookup"><span data-stu-id="72266-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="72266-158">Autres implémentations de serveur sont libres d’interpréter ce signal comme une suppression définitive, la suppression réversible ou retirer de la liste.</span><span class="sxs-lookup"><span data-stu-id="72266-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="72266-159">Par exemple, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur de prise en charge uniquement l’ancienne API V2) prend en charge gère cette requête comme un unlist ou une suppression définitive basé sur une option de configuration.</span><span class="sxs-lookup"><span data-stu-id="72266-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="72266-160">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="72266-160">Request parameters</span></span>

<span data-ttu-id="72266-161">Name</span><span class="sxs-lookup"><span data-stu-id="72266-161">Name</span></span>           | <span data-ttu-id="72266-162">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="72266-162">In</span></span>     | <span data-ttu-id="72266-163">Type</span><span class="sxs-lookup"><span data-stu-id="72266-163">Type</span></span>   | <span data-ttu-id="72266-164">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="72266-164">Required</span></span> | <span data-ttu-id="72266-165">Notes</span><span class="sxs-lookup"><span data-stu-id="72266-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="72266-166">Id</span><span class="sxs-lookup"><span data-stu-id="72266-166">ID</span></span>             | <span data-ttu-id="72266-167">URL</span><span class="sxs-lookup"><span data-stu-id="72266-167">URL</span></span>    | <span data-ttu-id="72266-168">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-168">string</span></span> | <span data-ttu-id="72266-169">oui</span><span class="sxs-lookup"><span data-stu-id="72266-169">yes</span></span>      | <span data-ttu-id="72266-170">L’ID du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="72266-170">The ID of the package to delete</span></span>
<span data-ttu-id="72266-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="72266-171">VERSION</span></span>        | <span data-ttu-id="72266-172">URL</span><span class="sxs-lookup"><span data-stu-id="72266-172">URL</span></span>    | <span data-ttu-id="72266-173">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-173">string</span></span> | <span data-ttu-id="72266-174">oui</span><span class="sxs-lookup"><span data-stu-id="72266-174">yes</span></span>      | <span data-ttu-id="72266-175">La version du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="72266-175">The version of the package to delete</span></span>
<span data-ttu-id="72266-176">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="72266-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="72266-177">Header</span><span class="sxs-lookup"><span data-stu-id="72266-177">Header</span></span> | <span data-ttu-id="72266-178">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-178">string</span></span> | <span data-ttu-id="72266-179">oui</span><span class="sxs-lookup"><span data-stu-id="72266-179">yes</span></span>      | <span data-ttu-id="72266-180">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="72266-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="72266-181">Réponse</span><span class="sxs-lookup"><span data-stu-id="72266-181">Response</span></span>

<span data-ttu-id="72266-182">Code d’état</span><span class="sxs-lookup"><span data-stu-id="72266-182">Status Code</span></span> | <span data-ttu-id="72266-183">Signification</span><span class="sxs-lookup"><span data-stu-id="72266-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="72266-184">204</span><span class="sxs-lookup"><span data-stu-id="72266-184">204</span></span>         | <span data-ttu-id="72266-185">Le package a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="72266-185">The package was deleted</span></span>
<span data-ttu-id="72266-186">404</span><span class="sxs-lookup"><span data-stu-id="72266-186">404</span></span>         | <span data-ttu-id="72266-187">Aucun package avec le paramètre `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="72266-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="72266-188">Remettre un package</span><span class="sxs-lookup"><span data-stu-id="72266-188">Relist a package</span></span>

<span data-ttu-id="72266-189">Si un package n’est pas spécifié, il est possible de rendre ce package à nouveau visible dans les résultats de recherche à l’aide du point de terminaison « remise ».</span><span class="sxs-lookup"><span data-stu-id="72266-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="72266-190">Ce point de terminaison a la même forme que le [supprimer (retirer de la liste) point de terminaison](#delete-a-package) , mais utilise le `POST` méthode HTTP au lieu du `DELETE` (méthode).</span><span class="sxs-lookup"><span data-stu-id="72266-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="72266-191">Si le package est déjà répertorié, la demande réussit toujours.</span><span class="sxs-lookup"><span data-stu-id="72266-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="72266-192">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="72266-192">Request parameters</span></span>

<span data-ttu-id="72266-193">Name</span><span class="sxs-lookup"><span data-stu-id="72266-193">Name</span></span>           | <span data-ttu-id="72266-194">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="72266-194">In</span></span>     | <span data-ttu-id="72266-195">Type</span><span class="sxs-lookup"><span data-stu-id="72266-195">Type</span></span>   | <span data-ttu-id="72266-196">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="72266-196">Required</span></span> | <span data-ttu-id="72266-197">Notes</span><span class="sxs-lookup"><span data-stu-id="72266-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="72266-198">Id</span><span class="sxs-lookup"><span data-stu-id="72266-198">ID</span></span>             | <span data-ttu-id="72266-199">URL</span><span class="sxs-lookup"><span data-stu-id="72266-199">URL</span></span>    | <span data-ttu-id="72266-200">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-200">string</span></span> | <span data-ttu-id="72266-201">oui</span><span class="sxs-lookup"><span data-stu-id="72266-201">yes</span></span>      | <span data-ttu-id="72266-202">L’ID du package de remise</span><span class="sxs-lookup"><span data-stu-id="72266-202">The ID of the package to relist</span></span>
<span data-ttu-id="72266-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="72266-203">VERSION</span></span>        | <span data-ttu-id="72266-204">URL</span><span class="sxs-lookup"><span data-stu-id="72266-204">URL</span></span>    | <span data-ttu-id="72266-205">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-205">string</span></span> | <span data-ttu-id="72266-206">oui</span><span class="sxs-lookup"><span data-stu-id="72266-206">yes</span></span>      | <span data-ttu-id="72266-207">La version du package à remettre en vente</span><span class="sxs-lookup"><span data-stu-id="72266-207">The version of the package to relist</span></span>
<span data-ttu-id="72266-208">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="72266-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="72266-209">Header</span><span class="sxs-lookup"><span data-stu-id="72266-209">Header</span></span> | <span data-ttu-id="72266-210">chaîne</span><span class="sxs-lookup"><span data-stu-id="72266-210">string</span></span> | <span data-ttu-id="72266-211">oui</span><span class="sxs-lookup"><span data-stu-id="72266-211">yes</span></span>      | <span data-ttu-id="72266-212">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="72266-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="72266-213">Réponse</span><span class="sxs-lookup"><span data-stu-id="72266-213">Response</span></span>

<span data-ttu-id="72266-214">Code d’état</span><span class="sxs-lookup"><span data-stu-id="72266-214">Status Code</span></span> | <span data-ttu-id="72266-215">Signification</span><span class="sxs-lookup"><span data-stu-id="72266-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="72266-216">200</span><span class="sxs-lookup"><span data-stu-id="72266-216">200</span></span>         | <span data-ttu-id="72266-217">Le package est maintenant répertorié.</span><span class="sxs-lookup"><span data-stu-id="72266-217">The package is now listed</span></span>
<span data-ttu-id="72266-218">404</span><span class="sxs-lookup"><span data-stu-id="72266-218">404</span></span>         | <span data-ttu-id="72266-219">Aucun package avec le paramètre `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="72266-219">No package with the provided `ID` and `VERSION` exists</span></span>
