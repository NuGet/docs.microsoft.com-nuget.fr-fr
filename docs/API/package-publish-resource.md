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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="e9927-104">Push et supprimer</span><span class="sxs-lookup"><span data-stu-id="e9927-104">Push and Delete</span></span>

<span data-ttu-id="e9927-105">Il est possible de transmettre et supprimer (ou retirer de la liste, en fonction de l’implémentation du serveur) à l’aide de l’API de V3 NuGet de packages.</span><span class="sxs-lookup"><span data-stu-id="e9927-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="e9927-106">Les deux opérations sont en fonction de la `PackagePublish` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e9927-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e9927-107">Versioning</span><span class="sxs-lookup"><span data-stu-id="e9927-107">Versioning</span></span>

<span data-ttu-id="e9927-108">Les éléments suivants `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="e9927-108">The following `@type` value is used:</span></span>

<span data-ttu-id="e9927-109">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="e9927-109">@type value</span></span>          | <span data-ttu-id="e9927-110">Remarques</span><span class="sxs-lookup"><span data-stu-id="e9927-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="e9927-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="e9927-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="e9927-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="e9927-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="e9927-113">URL de base</span><span class="sxs-lookup"><span data-stu-id="e9927-113">Base URL</span></span>

<span data-ttu-id="e9927-114">L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans la source de package [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e9927-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="e9927-115">Pour obtenir la documentation ci-dessous, nuget.org URL est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e9927-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="e9927-116">Envisagez de `https://www.nuget.org/api/v2/package` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="e9927-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="e9927-117">Notez que cette URL pointe vers le même emplacement que le point de terminaison de push V2 hérité, car le protocole est le même.</span><span class="sxs-lookup"><span data-stu-id="e9927-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e9927-118">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="e9927-118">HTTP methods</span></span>

<span data-ttu-id="e9927-119">Le `PUT` et `DELETE` méthodes HTTP sont pris en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="e9927-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="e9927-120">Pour les méthodes qui sont pris en charge sur chaque point de terminaison, voir ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e9927-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="e9927-121">Un package de push</span><span class="sxs-lookup"><span data-stu-id="e9927-121">Push a package</span></span>

<span data-ttu-id="e9927-122">NuGet.org prend en charge l’exécution d’un push des nouveaux packages à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="e9927-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="e9927-123">Si le package avec l’ID et la version fourni existe déjà, nuget.org rejette le push.</span><span class="sxs-lookup"><span data-stu-id="e9927-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="e9927-124">Autres sources de package peuvent prendre en charge le remplacement d’un package existant.</span><span class="sxs-lookup"><span data-stu-id="e9927-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="e9927-125">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="e9927-125">Request parameters</span></span>

<span data-ttu-id="e9927-126">Nom</span><span class="sxs-lookup"><span data-stu-id="e9927-126">Name</span></span>           | <span data-ttu-id="e9927-127">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="e9927-127">In</span></span>     | <span data-ttu-id="e9927-128">Type</span><span class="sxs-lookup"><span data-stu-id="e9927-128">Type</span></span>   | <span data-ttu-id="e9927-129">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="e9927-129">Required</span></span> | <span data-ttu-id="e9927-130">Remarques</span><span class="sxs-lookup"><span data-stu-id="e9927-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e9927-131">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e9927-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e9927-132">Header</span><span class="sxs-lookup"><span data-stu-id="e9927-132">Header</span></span> | <span data-ttu-id="e9927-133">chaîne</span><span class="sxs-lookup"><span data-stu-id="e9927-133">string</span></span> | <span data-ttu-id="e9927-134">oui</span><span class="sxs-lookup"><span data-stu-id="e9927-134">yes</span></span>      | <span data-ttu-id="e9927-135">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="e9927-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="e9927-136">La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client.</span><span class="sxs-lookup"><span data-stu-id="e9927-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="e9927-137">Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé d’API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="e9927-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="e9927-138">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="e9927-138">Request body</span></span>

<span data-ttu-id="e9927-139">Le corps de la demande doit être placée sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="e9927-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="e9927-140">Données de formulaire en plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="e9927-140">Multipart form data</span></span>

<span data-ttu-id="e9927-141">L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande est les octets bruts de le .nupkg lancé.</span><span class="sxs-lookup"><span data-stu-id="e9927-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="e9927-142">Les éléments suivants dans le corps en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="e9927-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="e9927-143">Le nom de fichier ou de tous les autres en-têtes des éléments en plusieurs parties sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="e9927-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="e9927-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="e9927-144">Response</span></span>

<span data-ttu-id="e9927-145">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e9927-145">Status Code</span></span> | <span data-ttu-id="e9927-146">Signification</span><span class="sxs-lookup"><span data-stu-id="e9927-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="e9927-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="e9927-147">201, 202</span></span>    | <span data-ttu-id="e9927-148">Le package a été envoyée avec succès</span><span class="sxs-lookup"><span data-stu-id="e9927-148">The package was successfully pushed</span></span>
<span data-ttu-id="e9927-149">400</span><span class="sxs-lookup"><span data-stu-id="e9927-149">400</span></span>         | <span data-ttu-id="e9927-150">Le package fourni n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="e9927-150">The provided package is invalid</span></span>
<span data-ttu-id="e9927-151">409</span><span class="sxs-lookup"><span data-stu-id="e9927-151">409</span></span>         | <span data-ttu-id="e9927-152">Un package avec l’ID et la version fourni existe déjà</span><span class="sxs-lookup"><span data-stu-id="e9927-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="e9927-153">Les implémentations de serveur varient selon le code d’état de réussite retournés lorsqu’un package est envoyé avec succès.</span><span class="sxs-lookup"><span data-stu-id="e9927-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="e9927-154">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="e9927-154">Delete a package</span></span>

<span data-ttu-id="e9927-155">NuGet.org interprète la demande de suppression de package comme un « retirer de la liste ».</span><span class="sxs-lookup"><span data-stu-id="e9927-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="e9927-156">Cela signifie que le package est toujours disponible pour les utilisateurs existants du package, mais le package ne s’affiche plus dans les résultats de la recherche ou dans l’interface web.</span><span class="sxs-lookup"><span data-stu-id="e9927-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="e9927-157">Pour plus d’informations sur cette pratique, consultez la [supprimé les Packages](../policies/deleting-packages.md) stratégie.</span><span class="sxs-lookup"><span data-stu-id="e9927-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="e9927-158">Autres implémentations de serveur sont libres d’interpréter ce signal comme une suppression définitive, la suppression réversible ou retirer de la liste.</span><span class="sxs-lookup"><span data-stu-id="e9927-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="e9927-159">Par exemple, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur de prise en charge uniquement l’ancienne API V2) prend en charge gère cette requête comme un unlist ou une suppression définitive basé sur une option de configuration.</span><span class="sxs-lookup"><span data-stu-id="e9927-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="e9927-160">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="e9927-160">Request parameters</span></span>

<span data-ttu-id="e9927-161">Nom</span><span class="sxs-lookup"><span data-stu-id="e9927-161">Name</span></span>           | <span data-ttu-id="e9927-162">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="e9927-162">In</span></span>     | <span data-ttu-id="e9927-163">Type</span><span class="sxs-lookup"><span data-stu-id="e9927-163">Type</span></span>   | <span data-ttu-id="e9927-164">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="e9927-164">Required</span></span> | <span data-ttu-id="e9927-165">Remarques</span><span class="sxs-lookup"><span data-stu-id="e9927-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e9927-166">Id</span><span class="sxs-lookup"><span data-stu-id="e9927-166">ID</span></span>             | <span data-ttu-id="e9927-167">URL</span><span class="sxs-lookup"><span data-stu-id="e9927-167">URL</span></span>    | <span data-ttu-id="e9927-168">chaîne</span><span class="sxs-lookup"><span data-stu-id="e9927-168">string</span></span> | <span data-ttu-id="e9927-169">oui</span><span class="sxs-lookup"><span data-stu-id="e9927-169">yes</span></span>      | <span data-ttu-id="e9927-170">L’ID du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="e9927-170">The ID of the package to delete</span></span>
<span data-ttu-id="e9927-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="e9927-171">VERSION</span></span>        | <span data-ttu-id="e9927-172">URL</span><span class="sxs-lookup"><span data-stu-id="e9927-172">URL</span></span>    | <span data-ttu-id="e9927-173">chaîne</span><span class="sxs-lookup"><span data-stu-id="e9927-173">string</span></span> | <span data-ttu-id="e9927-174">oui</span><span class="sxs-lookup"><span data-stu-id="e9927-174">yes</span></span>      | <span data-ttu-id="e9927-175">La version du package à supprimer</span><span class="sxs-lookup"><span data-stu-id="e9927-175">The version of the package to delete</span></span>
<span data-ttu-id="e9927-176">NuGet-X-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e9927-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e9927-177">Header</span><span class="sxs-lookup"><span data-stu-id="e9927-177">Header</span></span> | <span data-ttu-id="e9927-178">chaîne</span><span class="sxs-lookup"><span data-stu-id="e9927-178">string</span></span> | <span data-ttu-id="e9927-179">oui</span><span class="sxs-lookup"><span data-stu-id="e9927-179">yes</span></span>      | <span data-ttu-id="e9927-180">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="e9927-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="e9927-181">Réponse</span><span class="sxs-lookup"><span data-stu-id="e9927-181">Response</span></span>

<span data-ttu-id="e9927-182">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e9927-182">Status Code</span></span> | <span data-ttu-id="e9927-183">Signification</span><span class="sxs-lookup"><span data-stu-id="e9927-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="e9927-184">204</span><span class="sxs-lookup"><span data-stu-id="e9927-184">204</span></span>         | <span data-ttu-id="e9927-185">Le package a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="e9927-185">The package was deleted</span></span>
<span data-ttu-id="e9927-186">404</span><span class="sxs-lookup"><span data-stu-id="e9927-186">404</span></span>         | <span data-ttu-id="e9927-187">Aucun package avec le paramètre `ID` et `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="e9927-187">No package with the provided `ID` and `VERSION` exists</span></span>
