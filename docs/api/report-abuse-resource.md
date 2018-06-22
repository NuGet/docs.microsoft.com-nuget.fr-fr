---
title: Signaler un abus NuGet API, modèle d’URL
description: Le modèle d’URL de rapport abus permet aux clients d’afficher un lien Signaler un abus dans leur interface utilisateur.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818465"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="c8c23-103">Modèle d’URL de rapport abus</span><span class="sxs-lookup"><span data-stu-id="c8c23-103">Report abuse URL template</span></span>

<span data-ttu-id="c8c23-104">Il est possible pour un client générer une URL qui peut être utilisée par l’utilisateur pour signaler un abus sur un package spécifique.</span><span class="sxs-lookup"><span data-stu-id="c8c23-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="c8c23-105">Cela est utile lorsqu’une source de package souhaite activer toutes les expériences client (même 3e partie) déléguer les rapports d’abus à la source du package.</span><span class="sxs-lookup"><span data-stu-id="c8c23-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="c8c23-106">La ressource utilisée pour extraire le contenu du package est le `ReportAbuseUriTemplate` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c8c23-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c8c23-107">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="c8c23-107">Versioning</span></span>

<span data-ttu-id="c8c23-108">Les éléments suivants `@type` les valeurs sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="c8c23-108">The following `@type` values are used:</span></span>

<span data-ttu-id="c8c23-109">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="c8c23-109">@type value</span></span>                       | <span data-ttu-id="c8c23-110">Notes</span><span class="sxs-lookup"><span data-stu-id="c8c23-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="c8c23-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="c8c23-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="c8c23-112">La version initiale</span><span class="sxs-lookup"><span data-stu-id="c8c23-112">The initial release</span></span>
<span data-ttu-id="c8c23-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="c8c23-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="c8c23-114">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="c8c23-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="c8c23-115">Modèle d’URL</span><span class="sxs-lookup"><span data-stu-id="c8c23-115">URL template</span></span>

<span data-ttu-id="c8c23-116">L’URL de l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.</span><span class="sxs-lookup"><span data-stu-id="c8c23-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c8c23-117">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c23-117">HTTP methods</span></span>

<span data-ttu-id="c8c23-118">Bien que le client n’est pas destiné à effectuer des demandes à l’URL d’abus de rapports pour le compte de l’utilisateur, la page web doit prendre en charge la `GET` méthode pour autoriser les URL où vous avez cliquée pour être ouvert dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="c8c23-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="c8c23-119">Construire l’URL</span><span class="sxs-lookup"><span data-stu-id="c8c23-119">Construct the URL</span></span>

<span data-ttu-id="c8c23-120">Étant donné un ID de package connus et la version, l’implémentation du client permet de construire une URL utilisée pour accéder à une interface web.</span><span class="sxs-lookup"><span data-stu-id="c8c23-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="c8c23-121">L’implémentation cliente doit afficher cette URL construite (ou un lien cliquable) à l’utilisateur qui permet de les ouvrir un navigateur web à l’URL et que n’importe quel rapport abus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c8c23-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="c8c23-122">L’implémentation de la forme de rapport abus est déterminée par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="c8c23-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="c8c23-123">La valeur de la `@id` est une chaîne d’URL contenant l’un des jetons d’espace réservé suivant :</span><span class="sxs-lookup"><span data-stu-id="c8c23-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="c8c23-124">Espaces réservés d’URL</span><span class="sxs-lookup"><span data-stu-id="c8c23-124">URL placeholders</span></span>

<span data-ttu-id="c8c23-125">Name</span><span class="sxs-lookup"><span data-stu-id="c8c23-125">Name</span></span>        | <span data-ttu-id="c8c23-126">Type</span><span class="sxs-lookup"><span data-stu-id="c8c23-126">Type</span></span>    | <span data-ttu-id="c8c23-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="c8c23-127">Required</span></span> | <span data-ttu-id="c8c23-128">Notes</span><span class="sxs-lookup"><span data-stu-id="c8c23-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="c8c23-129">chaîne</span><span class="sxs-lookup"><span data-stu-id="c8c23-129">string</span></span>  | <span data-ttu-id="c8c23-130">Non</span><span class="sxs-lookup"><span data-stu-id="c8c23-130">no</span></span>       | <span data-ttu-id="c8c23-131">L’ID de package pour signaler un abus pour</span><span class="sxs-lookup"><span data-stu-id="c8c23-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="c8c23-132">chaîne</span><span class="sxs-lookup"><span data-stu-id="c8c23-132">string</span></span>  | <span data-ttu-id="c8c23-133">Non</span><span class="sxs-lookup"><span data-stu-id="c8c23-133">no</span></span>       | <span data-ttu-id="c8c23-134">La version du package pour signaler un abus pour</span><span class="sxs-lookup"><span data-stu-id="c8c23-134">The package version to report abuse for</span></span>

<span data-ttu-id="c8c23-135">Le `{id}` et `{version}` valeurs interprétée par l’implémentation de serveur doivent être insensible à la casse et n’ont aucune incidence si la version est normalisé.</span><span class="sxs-lookup"><span data-stu-id="c8c23-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="c8c23-136">Par exemple, le modèle d’abus nuget.org rapport ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="c8c23-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="c8c23-137">Si l’implémentation cliente doit afficher un lien vers le formulaire d’abus de rapport pour NuGet.Versioning 4.3.0, il génère l’URL suivante et fournir à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c8c23-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
