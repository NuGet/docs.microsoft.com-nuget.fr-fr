---
title: Modèle d’URL du rapport d’abus, API NuGet
description: Le modèle URL du rapport d’abus permet aux clients d’afficher un lien signaler un abus dans leur interface utilisateur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775233"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="29c17-103">Modèle d’URL d’abus de rapport</span><span class="sxs-lookup"><span data-stu-id="29c17-103">Report abuse URL template</span></span>

<span data-ttu-id="29c17-104">Il est possible pour un client de créer une URL qui peut être utilisée par l’utilisateur pour signaler un abus sur un package spécifique.</span><span class="sxs-lookup"><span data-stu-id="29c17-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="29c17-105">Cela est utile quand une source de package souhaite activer toutes les expériences client (même tierces) pour déléguer des rapports d’abus à la source du package.</span><span class="sxs-lookup"><span data-stu-id="29c17-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="29c17-106">La ressource utilisée pour générer cette URL est la `ReportAbuseUriTemplate` ressource trouvée dans l' [index de service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="29c17-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="29c17-107">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="29c17-107">Versioning</span></span>

<span data-ttu-id="29c17-108">Les `@type` valeurs suivantes sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="29c17-108">The following `@type` values are used:</span></span>

<span data-ttu-id="29c17-109">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="29c17-109">@type value</span></span>                       | <span data-ttu-id="29c17-110">Notes</span><span class="sxs-lookup"><span data-stu-id="29c17-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="29c17-111">ReportAbuseUriTemplate/3.0.0-bêta</span><span class="sxs-lookup"><span data-stu-id="29c17-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="29c17-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="29c17-112">The initial release</span></span>
<span data-ttu-id="29c17-113">ReportAbuseUriTemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="29c17-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="29c17-114">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="29c17-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="29c17-115">URL template</span><span class="sxs-lookup"><span data-stu-id="29c17-115">URL template</span></span>

<span data-ttu-id="29c17-116">L’URL de l’API suivante est la valeur de la `@id` propriété associée à l’une des valeurs de ressource mentionnées ci-dessus `@type` .</span><span class="sxs-lookup"><span data-stu-id="29c17-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="29c17-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="29c17-117">HTTP methods</span></span>

<span data-ttu-id="29c17-118">Bien que le client ne soit pas destiné à effectuer des demandes à l’URL d’abus de rapport pour le compte de l’utilisateur, la page Web doit prendre en charge la `GET` méthode pour permettre l’ouverture facile d’une URL cliquée dans un navigateur Web.</span><span class="sxs-lookup"><span data-stu-id="29c17-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="29c17-119">Construire l’URL</span><span class="sxs-lookup"><span data-stu-id="29c17-119">Construct the URL</span></span>

<span data-ttu-id="29c17-120">Avec un ID de package connu et une version, l’implémentation cliente peut construire une URL utilisée pour accéder à une interface Web.</span><span class="sxs-lookup"><span data-stu-id="29c17-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="29c17-121">L’implémentation du client doit afficher cette URL construite (ou un lien de clic) pour permettre à l’utilisateur d’ouvrir un navigateur Web à l’URL et de faire tout rapport d’abus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29c17-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="29c17-122">L’implémentation du formulaire de rapport d’abus est déterminée par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="29c17-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="29c17-123">La valeur de `@id` est une chaîne d’URL contenant l’un des jetons d’espace réservé suivants :</span><span class="sxs-lookup"><span data-stu-id="29c17-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="29c17-124">Espaces réservés d’URL</span><span class="sxs-lookup"><span data-stu-id="29c17-124">URL placeholders</span></span>

<span data-ttu-id="29c17-125">Nom</span><span class="sxs-lookup"><span data-stu-id="29c17-125">Name</span></span>        | <span data-ttu-id="29c17-126">Type</span><span class="sxs-lookup"><span data-stu-id="29c17-126">Type</span></span>    | <span data-ttu-id="29c17-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="29c17-127">Required</span></span> | <span data-ttu-id="29c17-128">Notes</span><span class="sxs-lookup"><span data-stu-id="29c17-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="29c17-129">string</span><span class="sxs-lookup"><span data-stu-id="29c17-129">string</span></span>  | <span data-ttu-id="29c17-130">non</span><span class="sxs-lookup"><span data-stu-id="29c17-130">no</span></span>       | <span data-ttu-id="29c17-131">ID de package pour signaler un abus pour</span><span class="sxs-lookup"><span data-stu-id="29c17-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="29c17-132">string</span><span class="sxs-lookup"><span data-stu-id="29c17-132">string</span></span>  | <span data-ttu-id="29c17-133">non</span><span class="sxs-lookup"><span data-stu-id="29c17-133">no</span></span>       | <span data-ttu-id="29c17-134">Version du package pour signaler un abus pour</span><span class="sxs-lookup"><span data-stu-id="29c17-134">The package version to report abuse for</span></span>

<span data-ttu-id="29c17-135">Les `{id}` `{version}` valeurs et interprétées par l’implémentation de serveur doivent être insensibles à la casse et ne pas être sensibles au fait que la version est normalisée ou non.</span><span class="sxs-lookup"><span data-stu-id="29c17-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="29c17-136">Par exemple, le modèle de rapport d’abus de NuGet. org ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="29c17-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="29c17-137">Si l’implémentation du client doit afficher un lien vers le formulaire signaler un abus pour NuGet. version 4.3.0, elle génère l’URL suivante et la fournit à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="29c17-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
