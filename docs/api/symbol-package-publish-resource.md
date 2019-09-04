---
title: Packages Push Symbol, API NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Le service de publication permet aux clients de publier de nouveaux packages de symboles.
keywords: Package de symboles push de l’API NuGet
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235108"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="72c78-104">Envoyer des packages de symboles</span><span class="sxs-lookup"><span data-stu-id="72c78-104">Push Symbol Packages</span></span>

<span data-ttu-id="72c78-105">Il est possible d’envoyer des packages de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="72c78-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="72c78-106">Ces opérations sont basées sur la `SymbolPackagePublish` ressource trouvée dans l’index de [service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="72c78-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="72c78-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="72c78-107">Versioning</span></span>

<span data-ttu-id="72c78-108">La valeur `@type` suivante est utilisée :</span><span class="sxs-lookup"><span data-stu-id="72c78-108">The following `@type` value is used:</span></span>

<span data-ttu-id="72c78-109">Valeur@type</span><span class="sxs-lookup"><span data-stu-id="72c78-109">@type value</span></span>                 | <span data-ttu-id="72c78-110">Notes</span><span class="sxs-lookup"><span data-stu-id="72c78-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="72c78-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="72c78-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="72c78-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="72c78-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="72c78-113">URL de base</span><span class="sxs-lookup"><span data-stu-id="72c78-113">Base URL</span></span>

<span data-ttu-id="72c78-114">L’URL de base pour les API suivantes est la valeur de `@id` la propriété de `SymbolPackagePublish/4.9.0` la ressource dans l’index de [service](service-index.md)de la source du package.</span><span class="sxs-lookup"><span data-stu-id="72c78-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="72c78-115">Pour la documentation ci-dessous, l’URL de NuGet. org est utilisée.</span><span class="sxs-lookup"><span data-stu-id="72c78-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="72c78-116">Considérez `https://www.nuget.org/api/v2/symbolpackage` comme un espace réservé `@id` pour la valeur trouvée dans l’index de service.</span><span class="sxs-lookup"><span data-stu-id="72c78-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="72c78-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="72c78-117">HTTP methods</span></span>

<span data-ttu-id="72c78-118">La `PUT` méthode http est prise en charge par cette ressource.</span><span class="sxs-lookup"><span data-stu-id="72c78-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="72c78-119">Envoyer un package de symboles</span><span class="sxs-lookup"><span data-stu-id="72c78-119">Push a symbol package</span></span>

<span data-ttu-id="72c78-120">nuget.org prend en charge l’envoi d’un nouveau format de packages de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="72c78-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="72c78-121">Les packages de symboles avec le même ID et la même version peuvent être envoyés plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="72c78-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="72c78-122">Un package de symboles sera rejeté dans les cas suivants.</span><span class="sxs-lookup"><span data-stu-id="72c78-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="72c78-123">Un package ayant le même ID et la même version n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="72c78-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="72c78-124">Un package de symboles avec le même ID et la même version a fait l’objet d’un push, mais n’est pas encore publié.</span><span class="sxs-lookup"><span data-stu-id="72c78-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="72c78-125">Le package de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) n’est pas valide (consultez [contraintes de package de symboles](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="72c78-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="72c78-126">Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="72c78-126">Request parameters</span></span>

<span data-ttu-id="72c78-127">Name</span><span class="sxs-lookup"><span data-stu-id="72c78-127">Name</span></span>           | <span data-ttu-id="72c78-128">Dans</span><span class="sxs-lookup"><span data-stu-id="72c78-128">In</span></span>     | <span data-ttu-id="72c78-129">Type</span><span class="sxs-lookup"><span data-stu-id="72c78-129">Type</span></span>   | <span data-ttu-id="72c78-130">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="72c78-130">Required</span></span> | <span data-ttu-id="72c78-131">Notes</span><span class="sxs-lookup"><span data-stu-id="72c78-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="72c78-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="72c78-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="72c78-133">Header</span><span class="sxs-lookup"><span data-stu-id="72c78-133">Header</span></span> | <span data-ttu-id="72c78-134">string</span><span class="sxs-lookup"><span data-stu-id="72c78-134">string</span></span> | <span data-ttu-id="72c78-135">oui</span><span class="sxs-lookup"><span data-stu-id="72c78-135">yes</span></span>      | <span data-ttu-id="72c78-136">Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="72c78-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="72c78-137">La clé API est une chaîne opaque obtenue à partir de la source du package par l’utilisateur et configurée dans le client.</span><span class="sxs-lookup"><span data-stu-id="72c78-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="72c78-138">Aucun format de chaîne particulier n’est mandaté, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="72c78-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="72c78-139">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="72c78-139">Request body</span></span>

<span data-ttu-id="72c78-140">Le corps de la demande pour la notification push de symbole est le même que le corps de la demande d’une demande push de package (voir [push et suppression de packages](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="72c78-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="72c78-141">response</span><span class="sxs-lookup"><span data-stu-id="72c78-141">Response</span></span>

<span data-ttu-id="72c78-142">Code d’état</span><span class="sxs-lookup"><span data-stu-id="72c78-142">Status Code</span></span> | <span data-ttu-id="72c78-143">Signification</span><span class="sxs-lookup"><span data-stu-id="72c78-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="72c78-144">201</span><span class="sxs-lookup"><span data-stu-id="72c78-144">201</span></span>         | <span data-ttu-id="72c78-145">Le package de symboles a été correctement poussé.</span><span class="sxs-lookup"><span data-stu-id="72c78-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="72c78-146">400</span><span class="sxs-lookup"><span data-stu-id="72c78-146">400</span></span>         | <span data-ttu-id="72c78-147">Le package de symboles fourni n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="72c78-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="72c78-148">401</span><span class="sxs-lookup"><span data-stu-id="72c78-148">401</span></span>         | <span data-ttu-id="72c78-149">L’utilisateur n’est pas autorisé à effectuer cette action.</span><span class="sxs-lookup"><span data-stu-id="72c78-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="72c78-150">404</span><span class="sxs-lookup"><span data-stu-id="72c78-150">404</span></span>         | <span data-ttu-id="72c78-151">Un package correspondant avec l’ID et la version fournis n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="72c78-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="72c78-152">409</span><span class="sxs-lookup"><span data-stu-id="72c78-152">409</span></span>         | <span data-ttu-id="72c78-153">Un package de symboles avec l’ID et la version fournis a été envoyé, mais il n’est pas encore disponible.</span><span class="sxs-lookup"><span data-stu-id="72c78-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="72c78-154">413</span><span class="sxs-lookup"><span data-stu-id="72c78-154">413</span></span>         | <span data-ttu-id="72c78-155">Le package est trop volumineux.</span><span class="sxs-lookup"><span data-stu-id="72c78-155">The package is too large.</span></span>

