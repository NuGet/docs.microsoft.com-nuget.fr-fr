---
title: Commande de recherche de l’interface CLI NuGet
description: Référence pour la commande de recherche de nuget.exe
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623268"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="ea96f-103">commande Search (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="ea96f-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="ea96f-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : 5.8 +</span><span class="sxs-lookup"><span data-stu-id="ea96f-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="ea96f-105">Recherche une source donnée à l’aide de la chaîne de requête fournie.</span><span class="sxs-lookup"><span data-stu-id="ea96f-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="ea96f-106">Si aucune source n’est spécifiée, toutes les sources définies dans% AppData% \NuGet\NuGet.config sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="ea96f-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="ea96f-107">Usage</span><span class="sxs-lookup"><span data-stu-id="ea96f-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="ea96f-108">où les termes de recherche sont appliqués aux noms des packages, aux balises et aux descriptions des packages, comme c’est le cas lorsque vous les utilisez sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ea96f-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="ea96f-109">Options</span><span class="sxs-lookup"><span data-stu-id="ea96f-109">Options</span></span>

| <span data-ttu-id="ea96f-110">Nom</span><span class="sxs-lookup"><span data-stu-id="ea96f-110">Name</span></span> | <span data-ttu-id="ea96f-111">Description</span><span class="sxs-lookup"><span data-stu-id="ea96f-111">Description</span></span> | <span data-ttu-id="ea96f-112">Usage</span><span class="sxs-lookup"><span data-stu-id="ea96f-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="ea96f-113">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="ea96f-113">PreRelease</span></span> | <span data-ttu-id="ea96f-114">Les packages de préversion ne sont pas inclus par défaut, mais peuvent être inclus à l’aide de cet argument</span><span class="sxs-lookup"><span data-stu-id="ea96f-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="ea96f-115">-Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="ea96f-115">-PreRelease</span></span> |
| <span data-ttu-id="ea96f-116">Source</span><span class="sxs-lookup"><span data-stu-id="ea96f-116">Source</span></span> | <span data-ttu-id="ea96f-117">Source (s) de package spécifique à rechercher au lieu d’interroger les sources par défaut dans __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="ea96f-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="ea96f-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="ea96f-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="ea96f-119">Take</span><span class="sxs-lookup"><span data-stu-id="ea96f-119">Take</span></span> | <span data-ttu-id="ea96f-120">Nombre de résultats à retourner.</span><span class="sxs-lookup"><span data-stu-id="ea96f-120">The number of results to return.</span></span> <span data-ttu-id="ea96f-121">La valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="ea96f-121">The default value is 20.</span></span> | <span data-ttu-id="ea96f-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="ea96f-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="ea96f-123">Commentaires</span><span class="sxs-lookup"><span data-stu-id="ea96f-123">Verbosity</span></span> | <span data-ttu-id="ea96f-124">Niveau de détail à afficher dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="ea96f-124">The level of detail to display in the output.</span></span> <span data-ttu-id="ea96f-125">La valeur par défaut est _normal_.</span><span class="sxs-lookup"><span data-stu-id="ea96f-125">The default is _normal_.</span></span> <span data-ttu-id="ea96f-126">(Voir la remarque ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="ea96f-126">(See the note below)</span></span>  | <span data-ttu-id="ea96f-127">-Verbosité `<quiet\|normal\|detailed>`</span><span class="sxs-lookup"><span data-stu-id="ea96f-127">-Verbosity `<quiet\|normal\|detailed>`</span></span> |
| <span data-ttu-id="ea96f-128">Aide</span><span class="sxs-lookup"><span data-stu-id="ea96f-128">Help</span></span> | <span data-ttu-id="ea96f-129">Affiche des informations d’aide pour la commande</span><span class="sxs-lookup"><span data-stu-id="ea96f-129">Displays help information for the command</span></span> | <span data-ttu-id="ea96f-130">-Aide</span><span class="sxs-lookup"><span data-stu-id="ea96f-130">-Help</span></span> |

<span data-ttu-id="ea96f-131">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ea96f-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

<span data-ttu-id="ea96f-132">__REMARQUE__</span><span class="sxs-lookup"><span data-stu-id="ea96f-132">__NOTE__</span></span>

<span data-ttu-id="ea96f-133">Niveaux de détail :</span><span class="sxs-lookup"><span data-stu-id="ea96f-133">Verbosity Levels:</span></span>

* <span data-ttu-id="ea96f-134">_Quiet_ : ID de package, version</span><span class="sxs-lookup"><span data-stu-id="ea96f-134">_quiet_ - Package ID, Version</span></span>
* <span data-ttu-id="ea96f-135">_normal_ : ID de package, version, téléchargements, aperçu de la description</span><span class="sxs-lookup"><span data-stu-id="ea96f-135">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
* <span data-ttu-id="ea96f-136">_detailed_ : ID de package, version, téléchargements, description complète, autres informations comme l’URL de la requête</span><span class="sxs-lookup"><span data-stu-id="ea96f-136">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="ea96f-137">Exemples</span><span class="sxs-lookup"><span data-stu-id="ea96f-137">Examples</span></span>

<span data-ttu-id="ea96f-138">Rechercher les packages liés à la *journalisation*à partir des sources par défaut :</span><span class="sxs-lookup"><span data-stu-id="ea96f-138">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="ea96f-139">Recherchez des packages liés à la *journalisation*avec un niveau de détail détaillé :</span><span class="sxs-lookup"><span data-stu-id="ea96f-139">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="ea96f-140">Recherchez les packages liés à la *journalisation*et Affichez uniquement les 5 premiers résultats :</span><span class="sxs-lookup"><span data-stu-id="ea96f-140">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="ea96f-141">Recherchez des packages *JSON*, y compris des versions préliminaires, à partir de la source/du flux spécifiés :</span><span class="sxs-lookup"><span data-stu-id="ea96f-141">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="ea96f-142">Rechercher des packages *JSON*à partir de plusieurs sources/flux :</span><span class="sxs-lookup"><span data-stu-id="ea96f-142">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
