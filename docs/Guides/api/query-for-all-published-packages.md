---
title: "Rechercher à l’aide d’une requête tous les packages publiés sur nuget.org | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "À l’aide de l’API NuGet, vous pouvez rechercher au moyen d’une requête tous les packages publiés sur nuget.org et rester à jour au fil du temps."
keywords: "énumérer tous les packages avec l’API NuGet, répliquer les packages avec l’API NuGet, derniers packages publiés sur nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ce25680f3b591e9c6b0234b6ac30b82205d10ad3
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="3d39e-104">Rechercher à l’aide d’une requête tous les packages publiés sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="3d39e-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="3d39e-105">Un modèle de requête courant sur l’API OData V2 héritée consistait à énumérer tous les packages publiés sur nuget.org, classés par date d’installation.</span><span class="sxs-lookup"><span data-stu-id="3d39e-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="3d39e-106">Les scénarios nécessitant ce type de requête sur nuget.org sont très variés :</span><span class="sxs-lookup"><span data-stu-id="3d39e-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="3d39e-107">Réplication complète de nuget.org</span><span class="sxs-lookup"><span data-stu-id="3d39e-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="3d39e-108">Détection de la disponibilité de nouvelles versions de packages</span><span class="sxs-lookup"><span data-stu-id="3d39e-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="3d39e-109">Recherche de packages dépendant de votre package</span><span class="sxs-lookup"><span data-stu-id="3d39e-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="3d39e-110">Pour effectuer cette opération, il fallait généralement trier l’entité de package OData par un horodatage et parcourir le jeu de résultats massif au moyen d’une pagination à l’aide des paramètres `skip` et `top` (taille de page).</span><span class="sxs-lookup"><span data-stu-id="3d39e-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="3d39e-111">Malheureusement, cette approche présente certains inconvénients :</span><span class="sxs-lookup"><span data-stu-id="3d39e-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="3d39e-112">Possibilité d’absence de packages, les requêtes étant exécutées sur des données dont l’ordre est souvent modifié</span><span class="sxs-lookup"><span data-stu-id="3d39e-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="3d39e-113">Lenteur du temps de réponse aux requêtes, celles-ci n’étant pas optimisées (les requêtes les plus optimisées sont celles qui prennent en charge un scénario principal pour le client NuGet officiel)</span><span class="sxs-lookup"><span data-stu-id="3d39e-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="3d39e-114">Utilisation d’une API dépréciée et non documentée, ce qui compromet la prise en charge future de ces requêtes</span><span class="sxs-lookup"><span data-stu-id="3d39e-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="3d39e-115">Impossibilité de relire l’historique dans l’ordre exact de son déroulement</span><span class="sxs-lookup"><span data-stu-id="3d39e-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="3d39e-116">Pour cette raison, vous pouvez suivre le guide ci-après pour résoudre les scénarios cités plus haut d’une manière plus fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="3d39e-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="3d39e-117">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3d39e-117">Overview</span></span>

<span data-ttu-id="3d39e-118">Ce guide repose sur une ressource de [l’API NuGet](../../api/overview.md) appelée **catalogue**.</span><span class="sxs-lookup"><span data-stu-id="3d39e-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="3d39e-119">Le catalogue est une API d’ajout uniquement qui permet à l’appelant d’afficher un historique complet des packages ajoutés, modifiés et supprimés dans nuget.org. Si vous êtes intéressé par tout ou partie des packages publiés sur nuget.org, le catalogue est un excellent moyen d’être constamment à jour de l’ensemble des packages disponibles.</span><span class="sxs-lookup"><span data-stu-id="3d39e-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="3d39e-120">Ce guide est conçu comme une procédure générale, mais si vous êtes intéressé par des détails précis du catalogue, consultez le [document de référence sur l’API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3d39e-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="3d39e-121">Les étapes suivantes peuvent être implémentées dans le langage de programmation de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3d39e-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="3d39e-122">Si vous souhaitez un exemple complet, jetez un œil à [l’exemple C#](#c-sample-code) mentionné plus bas.</span><span class="sxs-lookup"><span data-stu-id="3d39e-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="3d39e-123">Sinon, suivez le guide ci-dessous pour créer un lecteur de catalogue fiable.</span><span class="sxs-lookup"><span data-stu-id="3d39e-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="3d39e-124">Initialiser un curseur</span><span class="sxs-lookup"><span data-stu-id="3d39e-124">Initialize a cursor</span></span>

<span data-ttu-id="3d39e-125">La première étape de la création d’un lecteur de catalogue fiable consiste à implémenter un curseur.</span><span class="sxs-lookup"><span data-stu-id="3d39e-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="3d39e-126">Pour plus d’informations sur la conception d’un curseur de catalogue, consultez le [document de référence sur le catalogue](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="3d39e-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="3d39e-127">En bref, le curseur est un point dans le temps jusqu’auquel vous avez traité des événements dans le catalogue.</span><span class="sxs-lookup"><span data-stu-id="3d39e-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="3d39e-128">Les événements dans le catalogue représentent des publications de package et autres modifications de package.</span><span class="sxs-lookup"><span data-stu-id="3d39e-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="3d39e-129">Si vous vous intéressez à tous les packages publiés sur NuGet (depuis le tout début), vous initialisez votre curseur sur un horodatage de « valeur minimale » (par exemple, `DateTime.MinValue` dans .NET).</span><span class="sxs-lookup"><span data-stu-id="3d39e-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="3d39e-130">Si seuls vous intéressent les packages publiés à partir de maintenant, vous utilisez l’horodatage actuel comme valeur de curseur initiale.</span><span class="sxs-lookup"><span data-stu-id="3d39e-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="3d39e-131">Dans ce guide, nous allons initialiser notre curseur sur un horodatage remontant à une heure.</span><span class="sxs-lookup"><span data-stu-id="3d39e-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="3d39e-132">Pour l’instant, enregistrez simplement l’horodatage en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3d39e-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="3d39e-133">Déterminer l’URL de l’index du catalogue</span><span class="sxs-lookup"><span data-stu-id="3d39e-133">Determine catalog index URL</span></span>

<span data-ttu-id="3d39e-134">L’emplacement de chaque ressource (point de terminaison) dans l’API NuGet doit être découvert à l’aide de [l’index de service](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3d39e-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="3d39e-135">Étant donné que ce guide se concentre sur nuget.org, nous allons utiliser l’index de service de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3d39e-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="3d39e-136">Le document de service est un document JSON qui contient toutes les ressources sur nuget.org. Recherchez la ressource dont la propriété `@type` a pour valeur `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="3d39e-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="3d39e-137">La valeur de propriété `@id` associée est l’URL de l’index du catalogue.</span><span class="sxs-lookup"><span data-stu-id="3d39e-137">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="3d39e-138">Rechercher de nouvelles feuilles de catalogue</span><span class="sxs-lookup"><span data-stu-id="3d39e-138">Find new catalog leaves</span></span>

<span data-ttu-id="3d39e-139">À l’aide de la valeur de propriété `@id` trouvée à l’étape précédente, téléchargez l’index du catalogue :</span><span class="sxs-lookup"><span data-stu-id="3d39e-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="3d39e-140">Désérialisez [l’index du catalogue](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="3d39e-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="3d39e-141">Éliminez par filtrage tous les [objets de page de catalogue](../../api/catalog-resource.md#catalog-page-object-in-the-index) pour lesquels `commitTimeStamp` est inférieur ou égal à la valeur actuelle de votre curseur.</span><span class="sxs-lookup"><span data-stu-id="3d39e-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="3d39e-142">Pour chaque page de catalogue restante, téléchargez le document entier à l’aide de la propriété `@id`.</span><span class="sxs-lookup"><span data-stu-id="3d39e-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="3d39e-143">Désérialisez [la page du catalogue](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="3d39e-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="3d39e-144">Éliminez par filtrage tous les [objets de feuille de catalogue](../../api/catalog-resource.md#catalog-item-object-in-a-page) pour lesquels `commitTimeStamp` est inférieur ou égal à la valeur actuelle de votre curseur.</span><span class="sxs-lookup"><span data-stu-id="3d39e-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="3d39e-145">Après avoir téléchargé toutes les pages de catalogue non éliminées par filtrage, vous disposez d’un ensemble d’objets de feuille de catalogue représentant les packages qui ont été publiés, supprimés de la liste, répertoriés ou supprimés entre l’horodatage de votre curseur et maintenant.</span><span class="sxs-lookup"><span data-stu-id="3d39e-145">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="3d39e-146">Traiter les feuilles du catalogue</span><span class="sxs-lookup"><span data-stu-id="3d39e-146">Process catalog leaves</span></span>

<span data-ttu-id="3d39e-147">À ce stade, vous pouvez effectuer n’importe quel traitement personnalisé sur les éléments du catalogue.</span><span class="sxs-lookup"><span data-stu-id="3d39e-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="3d39e-148">Si vous avez uniquement besoin de l’ID et de la version du package, vous pouvez inspecter les propriétés `nuget:id` et `nuget:version` sur les objets d’élément de catalogue trouvés dans les pages.</span><span class="sxs-lookup"><span data-stu-id="3d39e-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="3d39e-149">Veillez à examiner la propriété `@type` pour savoir si l’élément de catalogue concerne un package existant ou un package supprimé.</span><span class="sxs-lookup"><span data-stu-id="3d39e-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="3d39e-150">Si vous êtes intéressé par les métadonnées relatives au package (par exemple, la description, les dépendances, la taille du fichier .nupkg, etc.), vous pouvez extraire le [document de feuille du catalogue](../../api/catalog-resource.md#catalog-leaf) à l’aide de la propriété `@id`.</span><span class="sxs-lookup"><span data-stu-id="3d39e-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="3d39e-151">Ce document contient, entre autres, toutes les métadonnées incluses dans la [ressource des métadonnées du package](../../api/registration-base-url-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3d39e-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="3d39e-152">Cette étape est celle où vous implémentez votre logique personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3d39e-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="3d39e-153">Les autres étapes de ce guide sont implémentées pratiquement de la même façon, quelle que soit l’opération que vous effectuez avec les feuilles de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3d39e-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="3d39e-154">Téléchargement du fichier .nupkg</span><span class="sxs-lookup"><span data-stu-id="3d39e-154">Downloading the .nupkg</span></span>

<span data-ttu-id="3d39e-155">Si vous souhaitez télécharger le fichier .nupkg des packages trouvés dans le catalogue, vous pouvez utiliser la [ressource de contenu de package](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3d39e-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="3d39e-156">Toutefois, notez qu’un court délai s’écoule entre le moment où un package est trouvé dans le catalogue et le moment où il est disponible dans la ressource de contenu du package.</span><span class="sxs-lookup"><span data-stu-id="3d39e-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="3d39e-157">Ainsi, si vous rencontrez `404 Not Found` quand vous tentez de télécharger un fichier .nupkg pour un package que vous avez trouvé dans le catalogue, réessayez simplement un peu plus tard.</span><span class="sxs-lookup"><span data-stu-id="3d39e-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="3d39e-158">La résolution de ce délai fait l’objet d’un suivi dans le sujet GitHub [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="3d39e-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="3d39e-159">Avancer le curseur</span><span class="sxs-lookup"><span data-stu-id="3d39e-159">Move the cursor forward</span></span>

<span data-ttu-id="3d39e-160">Une fois que vous avez correctement traité les éléments du catalogue, vous devez déterminer la nouvelle valeur de curseur à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="3d39e-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="3d39e-161">Pour ce faire, recherchez la valeur `commitTimeStamp` maximale (la plus récente chronologiquement) de tous les éléments de catalogue que vous avez traités.</span><span class="sxs-lookup"><span data-stu-id="3d39e-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="3d39e-162">Il s’agit de votre nouvelle valeur du curseur.</span><span class="sxs-lookup"><span data-stu-id="3d39e-162">This is your new cursor value.</span></span> <span data-ttu-id="3d39e-163">Enregistrez-la dans un magasin persistant, tel qu’une base de données, le système de fichiers ou le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="3d39e-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="3d39e-164">Quand vous souhaitez obtenir plus d’éléments de catalogue, démarrez simplement à la [première étape](#initialize-a-cursor) en initialisant la valeur de votre curseur à partir de ce magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="3d39e-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="3d39e-165">Si votre application lève une exception ou des erreurs, n’avancez pas le curseur.</span><span class="sxs-lookup"><span data-stu-id="3d39e-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="3d39e-166">Avancer le curseur signifie que vous n’avez plus besoin de traiter les éléments de catalogue situés avant le curseur.</span><span class="sxs-lookup"><span data-stu-id="3d39e-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="3d39e-167">Si, pour une raison quelconque, un bogue affecte le traitement des feuilles de catalogue, vous pouvez simplement reculer le curseur dans le temps et autoriser votre code à retraiter les anciens éléments de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3d39e-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="3d39e-168">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="3d39e-168">C# sample code</span></span>

<span data-ttu-id="3d39e-169">Le catalogue étant un ensemble de documents JSON disponibles via HTTP, vous pouvez interagir avec lui à l’aide de n’importe quel langage de programmation qui dispose d’un client HTTP et d’un désérialiseur JSON.</span><span class="sxs-lookup"><span data-stu-id="3d39e-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="3d39e-170">Des exemples C# sont disponibles dans le [dépôt NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="3d39e-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="3d39e-171">SDK du catalogue</span><span class="sxs-lookup"><span data-stu-id="3d39e-171">Catalog SDK</span></span>

<span data-ttu-id="3d39e-172">Pour consommer le catalogue, le plus simple consiste à utiliser le package du SDK du catalogue .NET (préversion) : [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="3d39e-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="3d39e-173">Ce package est disponible sur le flux `nuget-build` MyGet, pour lequel vous utilisez l’URL source de package NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3d39e-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="3d39e-174">Vous pouvez installer ce package sur un projet compatible avec `netstandard1.3` ou version supérieure (par exemple, .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="3d39e-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="3d39e-175">Un exemple d’utilisation de ce package est disponible sur GitHub dans le [projet NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="3d39e-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="3d39e-176">Résultat de l'exemple</span><span class="sxs-lookup"><span data-stu-id="3d39e-176">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="3d39e-177">Exemple minimal</span><span class="sxs-lookup"><span data-stu-id="3d39e-177">Minimal sample</span></span>

<span data-ttu-id="3d39e-178">Pour obtenir un exemple avec moins de dépendances qui illustre l’interaction avec le catalogue de façon plus détaillée, consultez [l’exemple de projet CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="3d39e-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="3d39e-179">Le projet cible `netcoreapp2.0` et dépend de [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pour la résolution de l’index de service) et de [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pour la désérialisation du JSON).</span><span class="sxs-lookup"><span data-stu-id="3d39e-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="3d39e-180">La logique principale du code est visible dans le [fichier Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="3d39e-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="3d39e-181">Résultat de l'exemple</span><span class="sxs-lookup"><span data-stu-id="3d39e-181">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
