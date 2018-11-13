---
title: Envoyez des Packages de symboles, API NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Le service de publication permet aux clients de publier de nouveaux packages de symboles.
keywords: Package de symboles NuGet API push
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580412"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="8f881-104">Packages de symboles de push</span><span class="sxs-lookup"><span data-stu-id="8f881-104">Push Symbol Packages</span></span>

<span data-ttu-id="8f881-105">Il est possible de packages de symboles push ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API V3 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f881-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="8f881-106">Ces opérations sont basées issu de la `SymbolPackagePublish` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8f881-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8f881-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="8f881-107">Versioning</span></span>

<span data-ttu-id="8f881-108">Ce qui suit `@type` valeur est utilisée :</span><span class="sxs-lookup"><span data-stu-id="8f881-108">The following `@type` value is used:</span></span>

<span data-ttu-id="8f881-109">Valeur@type </span><span class="sxs-lookup"><span data-stu-id="8f881-109">@type value</span></span>                 | <span data-ttu-id="8f881-110">Notes</span><span class="sxs-lookup"><span data-stu-id="8f881-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="8f881-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="8f881-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="8f881-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="8f881-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="8f881-113">URL de base</span><span class="sxs-lookup"><span data-stu-id="8f881-113">Base URL</span></span>

<span data-ttu-id="8f881-114">L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `SymbolPackagePublish/4.9.0` ressource dans la source de package [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8f881-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="8f881-115">Pour obtenir la documentation ci-dessous, les URL de nuget.org est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8f881-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="8f881-116">Envisagez `https://www.nuget.org/api/v2/symbolpackage` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="8f881-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8f881-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="8f881-117">HTTP methods</span></span>

<span data-ttu-id="8f881-118">Le `PUT` méthode HTTP est pris en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="8f881-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="8f881-119">Envoyer un package de symboles</span><span class="sxs-lookup"><span data-stu-id="8f881-119">Push a symbol package</span></span>

<span data-ttu-id="8f881-120">NuGet.org prend en charge l’exécution de type push nouveau format de packages de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="8f881-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="8f881-121">Les packages de symboles avec le même ID et la version peuvent être soumis plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="8f881-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="8f881-122">Un package de symboles est rejeté dans les cas suivants.</span><span class="sxs-lookup"><span data-stu-id="8f881-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="8f881-123">Un package avec le même ID et la version n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8f881-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="8f881-124">Un package de symboles avec le même ID et la version a été envoyé, mais n’est pas encore publié.</span><span class="sxs-lookup"><span data-stu-id="8f881-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="8f881-125">Le package de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) n’est pas valide (consultez [contraintes de package de symboles](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="8f881-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="8f881-126">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="8f881-126">Request parameters</span></span>

<span data-ttu-id="8f881-127">Name</span><span class="sxs-lookup"><span data-stu-id="8f881-127">Name</span></span>           | <span data-ttu-id="8f881-128">Vers l'avant</span><span class="sxs-lookup"><span data-stu-id="8f881-128">In</span></span>     | <span data-ttu-id="8f881-129">Type</span><span class="sxs-lookup"><span data-stu-id="8f881-129">Type</span></span>   | <span data-ttu-id="8f881-130">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="8f881-130">Required</span></span> | <span data-ttu-id="8f881-131">Notes</span><span class="sxs-lookup"><span data-stu-id="8f881-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="8f881-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="8f881-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="8f881-133">Header</span><span class="sxs-lookup"><span data-stu-id="8f881-133">Header</span></span> | <span data-ttu-id="8f881-134">chaîne</span><span class="sxs-lookup"><span data-stu-id="8f881-134">string</span></span> | <span data-ttu-id="8f881-135">oui</span><span class="sxs-lookup"><span data-stu-id="8f881-135">yes</span></span>      | <span data-ttu-id="8f881-136">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="8f881-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="8f881-137">La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client.</span><span class="sxs-lookup"><span data-stu-id="8f881-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="8f881-138">Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="8f881-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="8f881-139">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="8f881-139">Request body</span></span>

<span data-ttu-id="8f881-140">Le corps de demande pour le push de symbole est identique à celle dont le corps d’une demande de push de package (consultez [push de package et de supprimer](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="8f881-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="8f881-141">Réponse</span><span class="sxs-lookup"><span data-stu-id="8f881-141">Response</span></span>

<span data-ttu-id="8f881-142">Code d’état</span><span class="sxs-lookup"><span data-stu-id="8f881-142">Status Code</span></span> | <span data-ttu-id="8f881-143">Signification</span><span class="sxs-lookup"><span data-stu-id="8f881-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="8f881-144">201</span><span class="sxs-lookup"><span data-stu-id="8f881-144">201</span></span>         | <span data-ttu-id="8f881-145">Le package de symboles a été correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="8f881-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="8f881-146">400</span><span class="sxs-lookup"><span data-stu-id="8f881-146">400</span></span>         | <span data-ttu-id="8f881-147">Le package de symboles fourni n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="8f881-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="8f881-148">401</span><span class="sxs-lookup"><span data-stu-id="8f881-148">401</span></span>         | <span data-ttu-id="8f881-149">L’utilisateur n’est pas autorisé à effectuer cette action.</span><span class="sxs-lookup"><span data-stu-id="8f881-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="8f881-150">404</span><span class="sxs-lookup"><span data-stu-id="8f881-150">404</span></span>         | <span data-ttu-id="8f881-151">Un package avec l’ID et la version fournie correspondant n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8f881-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="8f881-152">409</span><span class="sxs-lookup"><span data-stu-id="8f881-152">409</span></span>         | <span data-ttu-id="8f881-153">Un package de symboles avec l’ID et la version fournie a été envoyé, mais il n'est pas encore disponible.</span><span class="sxs-lookup"><span data-stu-id="8f881-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="8f881-154">413</span><span class="sxs-lookup"><span data-stu-id="8f881-154">413</span></span>         | <span data-ttu-id="8f881-155">Le package est trop volumineux.</span><span class="sxs-lookup"><span data-stu-id="8f881-155">The package is too large.</span></span>

