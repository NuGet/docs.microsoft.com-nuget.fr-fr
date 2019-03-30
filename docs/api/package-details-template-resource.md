---
title: Détails de l’API NuGet, modèle d’URL de package
description: Le modèle d’URL de package détails permet aux clients d’afficher dans leur interface utilisateur web lier à plus de détails de package
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638072"
---
# <a name="package-details-url-template"></a><span data-ttu-id="df28b-103">Modèle d’URL de détails de package</span><span class="sxs-lookup"><span data-stu-id="df28b-103">Package details URL template</span></span>

<span data-ttu-id="df28b-104">Il est possible pour un client générer une URL qui peut être utilisée par l’utilisateur pour afficher plus de détails de package dans son navigateur web.</span><span class="sxs-lookup"><span data-stu-id="df28b-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="df28b-105">Cela est utile lorsqu’une source de package souhaite afficher des informations supplémentaires sur un package qui ne correspondre pas dans la portée de ce que montre l’application cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="df28b-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="df28b-106">La ressource utilisée pour la création de cette URL est la `PackageDetailsUriTemplate` ressource trouvée dans le [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="df28b-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="df28b-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="df28b-107">Versioning</span></span>

<span data-ttu-id="df28b-108">Les éléments suivants `@type` les valeurs sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="df28b-108">The following `@type` values are used:</span></span>

<span data-ttu-id="df28b-109">Valeur@type </span><span class="sxs-lookup"><span data-stu-id="df28b-109">@type value</span></span>                     | <span data-ttu-id="df28b-110">Notes</span><span class="sxs-lookup"><span data-stu-id="df28b-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="df28b-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="df28b-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="df28b-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="df28b-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="df28b-113">Modèle d’URL</span><span class="sxs-lookup"><span data-stu-id="df28b-113">URL template</span></span>

<span data-ttu-id="df28b-114">L’URL de l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.</span><span class="sxs-lookup"><span data-stu-id="df28b-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="df28b-115">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="df28b-115">HTTP methods</span></span>

<span data-ttu-id="df28b-116">Bien que le client n’est pas destiné à effectuer des demandes à l’URL de détails du package pour le compte de l’utilisateur, la page web doit prendre en charge la `GET` méthode pour autoriser une URL consultée être ouvert dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="df28b-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="df28b-117">Construire l’URL</span><span class="sxs-lookup"><span data-stu-id="df28b-117">Construct the URL</span></span>

<span data-ttu-id="df28b-118">Étant donné un ID de package connus et la version, l’implémentation du client permettre construire une URL utilisée pour accéder à une interface web.</span><span class="sxs-lookup"><span data-stu-id="df28b-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="df28b-119">L’implémentation cliente doit afficher cette URL construit (ou un lien interactif) pour l’utilisateur lui permettant d’ouvrir un navigateur web à l’URL et pour en savoir plus sur le package.</span><span class="sxs-lookup"><span data-stu-id="df28b-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="df28b-120">Le contenu de la page de détails du package est déterminé par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="df28b-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="df28b-121">L’URL doit être une URL absolue et du modèle (protocole) doit être HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df28b-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="df28b-122">La valeur de la `@id` dans le service d’index est une chaîne d’URL contenant un jeton d’espace réservé suivant :</span><span class="sxs-lookup"><span data-stu-id="df28b-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="df28b-123">Espace réservé d’URL</span><span class="sxs-lookup"><span data-stu-id="df28b-123">URL placeholders</span></span>

<span data-ttu-id="df28b-124">Nom</span><span class="sxs-lookup"><span data-stu-id="df28b-124">Name</span></span>        | <span data-ttu-id="df28b-125">Type</span><span class="sxs-lookup"><span data-stu-id="df28b-125">Type</span></span>    | <span data-ttu-id="df28b-126">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="df28b-126">Required</span></span> | <span data-ttu-id="df28b-127">Notes</span><span class="sxs-lookup"><span data-stu-id="df28b-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="df28b-128">string</span><span class="sxs-lookup"><span data-stu-id="df28b-128">string</span></span>  | <span data-ttu-id="df28b-129">Non</span><span class="sxs-lookup"><span data-stu-id="df28b-129">no</span></span>       | <span data-ttu-id="df28b-130">L’ID de package pour obtenir des détails pour</span><span class="sxs-lookup"><span data-stu-id="df28b-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="df28b-131">string</span><span class="sxs-lookup"><span data-stu-id="df28b-131">string</span></span>  | <span data-ttu-id="df28b-132">Non</span><span class="sxs-lookup"><span data-stu-id="df28b-132">no</span></span>       | <span data-ttu-id="df28b-133">Pour obtenir des détails pour la version du package</span><span class="sxs-lookup"><span data-stu-id="df28b-133">The package version to get details for</span></span>

<span data-ttu-id="df28b-134">Le serveur doit accepter `{id}` et `{version}` valeurs avec n’importe quel boîtier.</span><span class="sxs-lookup"><span data-stu-id="df28b-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="df28b-135">En outre, le serveur ne doit pas être sensible aux indique si la version est [normalisée](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="df28b-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="df28b-136">En d’autres termes, le serveur doit accepter également accepter des versions non normalisée.</span><span class="sxs-lookup"><span data-stu-id="df28b-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="df28b-137">Par exemple, le modèle de détails du package nuget.org se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="df28b-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="df28b-138">Si l’implémentation cliente doit afficher un lien vers les détails du package pour NuGet.Versioning 4.3.0, il serait génère l’URL suivante et fournit à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="df28b-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
