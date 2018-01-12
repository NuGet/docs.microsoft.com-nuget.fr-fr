---
title: Push et supprimer, NuGet API | Documents Microsoft
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Le service de publication autorise les clients à publier les nouveaux packages et de retrait de la liste ou de supprimer des packages existants."
keywords: "Package NuGet API push supprimer le package NuGet API, API NuGet package, le package de téléchargement NuGet API retirer de la liste, créer des package NuGet API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="7079b-104">Push et supprimer</span><span class="sxs-lookup"><span data-stu-id="7079b-104">Push and Delete</span></span>

<span data-ttu-id="7079b-105">Il est possible de transmettre, supprimer (ou retirer de la liste, en fonction de l’implémentation du serveur) et la remise des packages à l’aide de l’API de V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="7079b-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="7079b-106">Ces opérations sont en fonction de la `PackagePublish` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7079b-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7079b-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="7079b-107">Versioning</span></span>

<span data-ttu-id="7079b-108">Les éléments suivants `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="7079b-108">The following `@type` value is used:</span></span>

<span data-ttu-id="7079b-109">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="7079b-109">@type value</span></span>          | <span data-ttu-id="7079b-110">Notes</span><span class="sxs-lookup"><span data-stu-id="7079b-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="7079b-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="7079b-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="7079b-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="7079b-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7079b-113">URL de base</span><span class="sxs-lookup"><span data-stu-id="7079b-113">Base URL</span></span>

<span data-ttu-id="7079b-114">L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans la source de package [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7079b-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="7079b-115">Pour obtenir la documentation ci-dessous, nuget.org URL est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7079b-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="7079b-116">Envisagez de `https://www.nuget.org/api/v2/package` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="7079b-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="7079b-117">Notez que cette URL pointe vers le même emplacement que le point de terminaison de push V2 hérité, car le protocole est le même.</span><span class="sxs-lookup"><span data-stu-id="7079b-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7079b-118">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="7079b-118">HTTP methods</span></span>

<span data-ttu-id="7079b-119">Le `PUT`, `POST` et `DELETE` méthodes HTTP sont pris en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="7079b-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="7079b-120">Pour les méthodes qui sont pris en charge sur chaque point de terminaison, voir ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7079b-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="7079b-121">Un package de push</span><span class="sxs-lookup"><span data-stu-id="7079b-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="7079b-122">NuGet.org a [exigences supplémentaires](NuGet-Protocols.md) pour interagir avec le point de terminaison par émission de données.</span><span class="sxs-lookup"><span data-stu-id="7079b-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="7079b-123">NuGet.org prend en charge l’exécution d’un push des nouveaux packages à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="7079b-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="7079b-124">Si le package avec l’ID et la version fourni existe déjà, nuget.org rejette le push.</span><span class="sxs-lookup"><span data-stu-id="7079b-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="7079b-125">Autres sources de package peuvent prendre en charge le remplacement d’un package existant.</span><span class="sxs-lookup"><span data-stu-id="7079b-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="7079b-126">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7079b-126">Request parameters</span></span>

<span data-ttu-id="7079b-127">Name</span><span class="sxs-lookup"><span data-stu-id="7079b-127">Name</span></span>           | <span data-ttu-id="7079b-128">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="7079b-128">In</span></span>     | <span data-ttu-id="7079b-129">Type</span><span class="sxs-lookup"><span data-stu-id="7079b-129">Type</span></span>   | <span data-ttu-id="7079b-130">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7079b-130">Required</span></span> | <span data-ttu-id="7079b-131">Notes</span><span class="sxs-lookup"><span data-stu-id="7079b-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7079b-132">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7079b-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7079b-133">Header</span><span class="sxs-lookup"><span data-stu-id="7079b-133">Header</span></span> | <span data-ttu-id="7079b-134">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-134">string</span></span> | <span data-ttu-id="7079b-135">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-135">yes</span></span>      | <span data-ttu-id="7079b-136">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7079b-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="7079b-137">La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client.</span><span class="sxs-lookup"><span data-stu-id="7079b-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="7079b-138">Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé d’API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="7079b-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="7079b-139">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="7079b-139">Request body</span></span>

<span data-ttu-id="7079b-140">Le corps de la demande doit être placée sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="7079b-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="7079b-141">Données de formulaire en plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="7079b-141">Multipart form data</span></span>

<span data-ttu-id="7079b-142">L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande est les octets bruts de le .nupkg lancé.</span><span class="sxs-lookup"><span data-stu-id="7079b-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="7079b-143">Les éléments suivants dans le corps en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="7079b-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="7079b-144">Le nom de fichier ou de tous les autres en-têtes des éléments en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="7079b-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="7079b-145">Réponse</span><span class="sxs-lookup"><span data-stu-id="7079b-145">Response</span></span>

<span data-ttu-id="7079b-146">Code d’état</span><span class="sxs-lookup"><span data-stu-id="7079b-146">Status Code</span></span> | <span data-ttu-id="7079b-147">Signification</span><span class="sxs-lookup"><span data-stu-id="7079b-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="7079b-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="7079b-148">201, 202</span></span>    | <span data-ttu-id="7079b-149">Le package a été envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="7079b-149">The package was successfully pushed</span></span>
<span data-ttu-id="7079b-150">400</span><span class="sxs-lookup"><span data-stu-id="7079b-150">400</span></span>         | <span data-ttu-id="7079b-151">Le package fourni n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="7079b-151">The provided package is invalid</span></span>
<span data-ttu-id="7079b-152">409</span><span class="sxs-lookup"><span data-stu-id="7079b-152">409</span></span>         | <span data-ttu-id="7079b-153">Un package avec l’ID et la version fourni existe déjà</span><span class="sxs-lookup"><span data-stu-id="7079b-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="7079b-154">Les implémentations de serveur varient selon le code d’état de réussite retournés lorsqu’un package est envoyé avec succès.</span><span class="sxs-lookup"><span data-stu-id="7079b-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="7079b-155">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="7079b-155">Delete a package</span></span>

<span data-ttu-id="7079b-156">NuGet.org interprète la demande de suppression de package comme un « retirer de la liste ».</span><span class="sxs-lookup"><span data-stu-id="7079b-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="7079b-157">Cela signifie que le package est toujours disponible pour les utilisateurs existants du package, mais le package ne s’affiche plus dans les résultats de la recherche ou dans l’interface web.</span><span class="sxs-lookup"><span data-stu-id="7079b-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="7079b-158">Pour plus d’informations sur cette pratique, consultez la [supprimé les Packages](../policies/deleting-packages.md) stratégie.</span><span class="sxs-lookup"><span data-stu-id="7079b-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="7079b-159">Autres implémentations de serveur sont libres d’interpréter ce signal comme une suppression définitive, la suppression réversible ou retirer de la liste.</span><span class="sxs-lookup"><span data-stu-id="7079b-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="7079b-160">Par exemple, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur de prise en charge uniquement l’ancienne API V2) prend en charge gère cette requête comme un unlist ou une suppression définitive basé sur une option de configuration.</span><span class="sxs-lookup"><span data-stu-id="7079b-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="7079b-161">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7079b-161">Request parameters</span></span>

<span data-ttu-id="7079b-162">Name</span><span class="sxs-lookup"><span data-stu-id="7079b-162">Name</span></span>           | <span data-ttu-id="7079b-163">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="7079b-163">In</span></span>     | <span data-ttu-id="7079b-164">Type</span><span class="sxs-lookup"><span data-stu-id="7079b-164">Type</span></span>   | <span data-ttu-id="7079b-165">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7079b-165">Required</span></span> | <span data-ttu-id="7079b-166">Notes</span><span class="sxs-lookup"><span data-stu-id="7079b-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7079b-167">Id</span><span class="sxs-lookup"><span data-stu-id="7079b-167">ID</span></span>             | <span data-ttu-id="7079b-168">URL</span><span class="sxs-lookup"><span data-stu-id="7079b-168">URL</span></span>    | <span data-ttu-id="7079b-169">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-169">string</span></span> | <span data-ttu-id="7079b-170">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-170">yes</span></span>      | <span data-ttu-id="7079b-171">L’ID du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="7079b-171">The ID of the package to delete</span></span>
<span data-ttu-id="7079b-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="7079b-172">VERSION</span></span>        | <span data-ttu-id="7079b-173">URL</span><span class="sxs-lookup"><span data-stu-id="7079b-173">URL</span></span>    | <span data-ttu-id="7079b-174">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-174">string</span></span> | <span data-ttu-id="7079b-175">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-175">yes</span></span>      | <span data-ttu-id="7079b-176">La version du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="7079b-176">The version of the package to delete</span></span>
<span data-ttu-id="7079b-177">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7079b-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7079b-178">Header</span><span class="sxs-lookup"><span data-stu-id="7079b-178">Header</span></span> | <span data-ttu-id="7079b-179">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-179">string</span></span> | <span data-ttu-id="7079b-180">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-180">yes</span></span>      | <span data-ttu-id="7079b-181">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7079b-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="7079b-182">Réponse</span><span class="sxs-lookup"><span data-stu-id="7079b-182">Response</span></span>

<span data-ttu-id="7079b-183">Code d’état</span><span class="sxs-lookup"><span data-stu-id="7079b-183">Status Code</span></span> | <span data-ttu-id="7079b-184">Signification</span><span class="sxs-lookup"><span data-stu-id="7079b-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="7079b-185">204</span><span class="sxs-lookup"><span data-stu-id="7079b-185">204</span></span>         | <span data-ttu-id="7079b-186">Le package a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="7079b-186">The package was deleted</span></span>
<span data-ttu-id="7079b-187">404</span><span class="sxs-lookup"><span data-stu-id="7079b-187">404</span></span>         | <span data-ttu-id="7079b-188">Aucun package avec le paramètre `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="7079b-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="7079b-189">Remettre un package</span><span class="sxs-lookup"><span data-stu-id="7079b-189">Relist a package</span></span>

<span data-ttu-id="7079b-190">Si un package n’est pas spécifié, il est possible de rendre ce package à nouveau visible dans les résultats de recherche à l’aide du point de terminaison « remise ».</span><span class="sxs-lookup"><span data-stu-id="7079b-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="7079b-191">Ce point de terminaison a la même forme que le [supprimer (retirer de la liste) point de terminaison](#delete-a-package) , mais utilise le `POST` méthode HTTP au lieu du `DELETE` (méthode).</span><span class="sxs-lookup"><span data-stu-id="7079b-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="7079b-192">Si le package est déjà répertorié, la demande réussit toujours.</span><span class="sxs-lookup"><span data-stu-id="7079b-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="7079b-193">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="7079b-193">Request parameters</span></span>

<span data-ttu-id="7079b-194">Name</span><span class="sxs-lookup"><span data-stu-id="7079b-194">Name</span></span>           | <span data-ttu-id="7079b-195">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="7079b-195">In</span></span>     | <span data-ttu-id="7079b-196">Type</span><span class="sxs-lookup"><span data-stu-id="7079b-196">Type</span></span>   | <span data-ttu-id="7079b-197">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="7079b-197">Required</span></span> | <span data-ttu-id="7079b-198">Notes</span><span class="sxs-lookup"><span data-stu-id="7079b-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7079b-199">Id</span><span class="sxs-lookup"><span data-stu-id="7079b-199">ID</span></span>             | <span data-ttu-id="7079b-200">URL</span><span class="sxs-lookup"><span data-stu-id="7079b-200">URL</span></span>    | <span data-ttu-id="7079b-201">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-201">string</span></span> | <span data-ttu-id="7079b-202">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-202">yes</span></span>      | <span data-ttu-id="7079b-203">L’ID du package de remise</span><span class="sxs-lookup"><span data-stu-id="7079b-203">The ID of the package to relist</span></span>
<span data-ttu-id="7079b-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="7079b-204">VERSION</span></span>        | <span data-ttu-id="7079b-205">URL</span><span class="sxs-lookup"><span data-stu-id="7079b-205">URL</span></span>    | <span data-ttu-id="7079b-206">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-206">string</span></span> | <span data-ttu-id="7079b-207">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-207">yes</span></span>      | <span data-ttu-id="7079b-208">La version du package à remettre en vente</span><span class="sxs-lookup"><span data-stu-id="7079b-208">The version of the package to relist</span></span>
<span data-ttu-id="7079b-209">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7079b-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7079b-210">Header</span><span class="sxs-lookup"><span data-stu-id="7079b-210">Header</span></span> | <span data-ttu-id="7079b-211">chaîne</span><span class="sxs-lookup"><span data-stu-id="7079b-211">string</span></span> | <span data-ttu-id="7079b-212">oui</span><span class="sxs-lookup"><span data-stu-id="7079b-212">yes</span></span>      | <span data-ttu-id="7079b-213">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7079b-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="7079b-214">Réponse</span><span class="sxs-lookup"><span data-stu-id="7079b-214">Response</span></span>

<span data-ttu-id="7079b-215">Code d’état</span><span class="sxs-lookup"><span data-stu-id="7079b-215">Status Code</span></span> | <span data-ttu-id="7079b-216">Signification</span><span class="sxs-lookup"><span data-stu-id="7079b-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="7079b-217">200</span><span class="sxs-lookup"><span data-stu-id="7079b-217">200</span></span>         | <span data-ttu-id="7079b-218">Le package est maintenant répertorié.</span><span class="sxs-lookup"><span data-stu-id="7079b-218">The package is now listed</span></span>
<span data-ttu-id="7079b-219">404</span><span class="sxs-lookup"><span data-stu-id="7079b-219">404</span></span>         | <span data-ttu-id="7079b-220">Aucun package avec le paramètre `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="7079b-220">No package with the provided `ID` and `VERSION` exists</span></span>
