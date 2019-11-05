---
title: Modèle d’URL Détails du package, API NuGet
description: Le modèle d’URL Détails du package permet aux clients d’afficher dans leur interface utilisateur un lien Web vers d’autres détails sur le package
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610960"
---
# <a name="package-details-url-template"></a><span data-ttu-id="869fe-103">Modèle d’URL Détails du package</span><span class="sxs-lookup"><span data-stu-id="869fe-103">Package details URL template</span></span>

<span data-ttu-id="869fe-104">Il est possible pour un client de créer une URL qui peut être utilisée par l’utilisateur pour afficher plus de détails sur le package dans son navigateur Web.</span><span class="sxs-lookup"><span data-stu-id="869fe-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="869fe-105">Cela s’avère utile quand une source de package souhaite afficher des informations supplémentaires sur un package qui ne tiennent pas dans l’étendue de ce que l’application cliente NuGet affiche.</span><span class="sxs-lookup"><span data-stu-id="869fe-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="869fe-106">La ressource utilisée pour générer cette URL est la ressource `PackageDetailsUriTemplate` trouvée dans l' [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="869fe-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="869fe-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="869fe-107">Versioning</span></span>

<span data-ttu-id="869fe-108">Les valeurs de `@type` suivantes sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="869fe-108">The following `@type` values are used:</span></span>

<span data-ttu-id="869fe-109">Valeur@type</span><span class="sxs-lookup"><span data-stu-id="869fe-109">@type value</span></span>                     | <span data-ttu-id="869fe-110">Notes</span><span class="sxs-lookup"><span data-stu-id="869fe-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="869fe-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="869fe-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="869fe-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="869fe-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="869fe-113">Modèle d’URL</span><span class="sxs-lookup"><span data-stu-id="869fe-113">URL template</span></span>

<span data-ttu-id="869fe-114">L’URL de l’API suivante est la valeur de la propriété `@id` associée à l’une des valeurs de `@type` de ressource mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="869fe-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="869fe-115">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="869fe-115">HTTP methods</span></span>

<span data-ttu-id="869fe-116">Bien que le client ne soit pas destiné à effectuer des requêtes sur l’URL des détails du package pour le compte de l’utilisateur, la page Web doit prendre en charge la méthode `GET` pour permettre l’ouverture facile d’une URL cliquée dans un navigateur Web.</span><span class="sxs-lookup"><span data-stu-id="869fe-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="869fe-117">Construire l’URL</span><span class="sxs-lookup"><span data-stu-id="869fe-117">Construct the URL</span></span>

<span data-ttu-id="869fe-118">Avec un ID de package connu et une version, l’implémentation cliente peut construire une URL utilisée pour accéder à une interface Web.</span><span class="sxs-lookup"><span data-stu-id="869fe-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="869fe-119">L’implémentation du client doit afficher cette URL construite (ou un lien de clic) pour permettre à l’utilisateur d’ouvrir un navigateur Web à l’URL et d’en savoir plus sur le package.</span><span class="sxs-lookup"><span data-stu-id="869fe-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="869fe-120">Le contenu de la page Détails du package est déterminé par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="869fe-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="869fe-121">L’URL doit être une URL absolue et le schéma (protocole) doit être HTTPs.</span><span class="sxs-lookup"><span data-stu-id="869fe-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="869fe-122">La valeur de la `@id` dans l’index de service est une chaîne d’URL contenant l’un des jetons d’espaces réservés suivants :</span><span class="sxs-lookup"><span data-stu-id="869fe-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="869fe-123">Espaces réservés d’URL</span><span class="sxs-lookup"><span data-stu-id="869fe-123">URL placeholders</span></span>

<span data-ttu-id="869fe-124">Name</span><span class="sxs-lookup"><span data-stu-id="869fe-124">Name</span></span>        | <span data-ttu-id="869fe-125">Tapez</span><span class="sxs-lookup"><span data-stu-id="869fe-125">Type</span></span>    | <span data-ttu-id="869fe-126">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="869fe-126">Required</span></span> | <span data-ttu-id="869fe-127">Notes</span><span class="sxs-lookup"><span data-stu-id="869fe-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="869fe-128">string</span><span class="sxs-lookup"><span data-stu-id="869fe-128">string</span></span>  | <span data-ttu-id="869fe-129">Non</span><span class="sxs-lookup"><span data-stu-id="869fe-129">no</span></span>       | <span data-ttu-id="869fe-130">ID de package pour lequel obtenir des détails</span><span class="sxs-lookup"><span data-stu-id="869fe-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="869fe-131">string</span><span class="sxs-lookup"><span data-stu-id="869fe-131">string</span></span>  | <span data-ttu-id="869fe-132">Non</span><span class="sxs-lookup"><span data-stu-id="869fe-132">no</span></span>       | <span data-ttu-id="869fe-133">Version du package pour laquelle obtenir des détails</span><span class="sxs-lookup"><span data-stu-id="869fe-133">The package version to get details for</span></span>

<span data-ttu-id="869fe-134">Le serveur doit accepter les valeurs `{id}` et `{version}` avec n’importe quelle casse.</span><span class="sxs-lookup"><span data-stu-id="869fe-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="869fe-135">En outre, le serveur ne doit pas être sensible à la [normalisation](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)de la version.</span><span class="sxs-lookup"><span data-stu-id="869fe-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="869fe-136">En d’autres termes, le serveur doit accepter également les versions non normalisées.</span><span class="sxs-lookup"><span data-stu-id="869fe-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="869fe-137">Par exemple, le modèle de détails de package de NuGet. org ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="869fe-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="869fe-138">Si l’implémentation du client doit afficher un lien vers les détails du package pour NuGet. version 4.3.0, elle génère l’URL suivante et la fournit à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="869fe-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
