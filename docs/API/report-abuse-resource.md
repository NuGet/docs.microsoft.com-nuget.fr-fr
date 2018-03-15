---
title: "Signaler un abus NuGet API, modèle d’URL | Documents Microsoft"
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
description: "Le modèle d’URL de rapport abus permet aux clients d’afficher un lien Signaler un abus dans leur interface utilisateur."
keywords: "API NuGet signaler un abus, réclamation de fichier API NuGet, modèle d’URL nuget.org rapport"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: efbe5704e6e6028f9382fea3fe5ec453f573a2e9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="09400-104">Modèle d’URL de rapport abus</span><span class="sxs-lookup"><span data-stu-id="09400-104">Report abuse URL template</span></span>

<span data-ttu-id="09400-105">Il est possible pour un client générer une URL qui peut être utilisée par l’utilisateur pour signaler un abus sur un package spécifique.</span><span class="sxs-lookup"><span data-stu-id="09400-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="09400-106">Cela est utile lorsqu’une source de package souhaite activer toutes les expériences client (même 3e partie) déléguer les rapports d’abus à la source du package.</span><span class="sxs-lookup"><span data-stu-id="09400-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="09400-107">La ressource utilisée pour extraire le contenu du package est le `ReportAbuseUriTemplate` ressource trouvée dans le [index service](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="09400-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="09400-108">Gestion de version</span><span class="sxs-lookup"><span data-stu-id="09400-108">Versioning</span></span>

<span data-ttu-id="09400-109">Les éléments suivants `@type` les valeurs sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="09400-109">The following `@type` values are used:</span></span>

<span data-ttu-id="09400-110">Valeur @type</span><span class="sxs-lookup"><span data-stu-id="09400-110">@type value</span></span>                       | <span data-ttu-id="09400-111">Notes</span><span class="sxs-lookup"><span data-stu-id="09400-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="09400-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="09400-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="09400-113">La version initiale</span><span class="sxs-lookup"><span data-stu-id="09400-113">The initial release</span></span>
<span data-ttu-id="09400-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="09400-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="09400-115">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="09400-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="09400-116">Modèle d’URL</span><span class="sxs-lookup"><span data-stu-id="09400-116">URL template</span></span>

<span data-ttu-id="09400-117">L’URL de l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs.</span><span class="sxs-lookup"><span data-stu-id="09400-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="09400-118">Méthodes HTTP</span><span class="sxs-lookup"><span data-stu-id="09400-118">HTTP methods</span></span>

<span data-ttu-id="09400-119">Bien que le client n’est pas destiné à effectuer des demandes à l’URL d’abus de rapports pour le compte de l’utilisateur, la page web doit prendre en charge la `GET` méthode pour autoriser les URL où vous avez cliquée pour être ouvert dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="09400-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="09400-120">Construire l’URL</span><span class="sxs-lookup"><span data-stu-id="09400-120">Construct the URL</span></span>

<span data-ttu-id="09400-121">Étant donné un ID de package connus et la version, l’implémentation du client permet de construire une URL utilisée pour accéder à une interface web.</span><span class="sxs-lookup"><span data-stu-id="09400-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="09400-122">L’implémentation cliente doit afficher cette URL construite (ou un lien cliquable) à l’utilisateur qui permet de les ouvrir un navigateur web à l’URL et que n’importe quel rapport abus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="09400-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="09400-123">L’implémentation de la forme de rapport abus est déterminée par l’implémentation du serveur.</span><span class="sxs-lookup"><span data-stu-id="09400-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="09400-124">La valeur de la `@id` est une chaîne d’URL contenant l’un des jetons d’espace réservé suivant :</span><span class="sxs-lookup"><span data-stu-id="09400-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="09400-125">Espaces réservés d’URL</span><span class="sxs-lookup"><span data-stu-id="09400-125">URL placeholders</span></span>

<span data-ttu-id="09400-126">Name</span><span class="sxs-lookup"><span data-stu-id="09400-126">Name</span></span>        | <span data-ttu-id="09400-127">Type</span><span class="sxs-lookup"><span data-stu-id="09400-127">Type</span></span>    | <span data-ttu-id="09400-128">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="09400-128">Required</span></span> | <span data-ttu-id="09400-129">Notes</span><span class="sxs-lookup"><span data-stu-id="09400-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="09400-130">chaîne</span><span class="sxs-lookup"><span data-stu-id="09400-130">string</span></span>  | <span data-ttu-id="09400-131">Non</span><span class="sxs-lookup"><span data-stu-id="09400-131">no</span></span>       | <span data-ttu-id="09400-132">L’ID de package pour signaler un abus pour</span><span class="sxs-lookup"><span data-stu-id="09400-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="09400-133">chaîne</span><span class="sxs-lookup"><span data-stu-id="09400-133">string</span></span>  | <span data-ttu-id="09400-134">Non</span><span class="sxs-lookup"><span data-stu-id="09400-134">no</span></span>       | <span data-ttu-id="09400-135">La version du package pour signaler un abus pour</span><span class="sxs-lookup"><span data-stu-id="09400-135">The package version to report abuse for</span></span>

<span data-ttu-id="09400-136">Le `{id}` et `{version}` valeurs interprétée par l’implémentation de serveur doivent être insensible à la casse et n’ont aucune incidence si la version est normalisé.</span><span class="sxs-lookup"><span data-stu-id="09400-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="09400-137">Par exemple, le modèle d’abus nuget.org rapport ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="09400-137">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="09400-138">Si l’implémentation cliente doit afficher un lien vers le formulaire d’abus de rapport pour NuGet.Versioning 4.3.0, il génère l’URL suivante et fournir à l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="09400-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
