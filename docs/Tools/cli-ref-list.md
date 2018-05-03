---
title: Commande de liste NuGet CLI
description: Référence de la commande de liste de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="d3290-103">commande de la liste (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d3290-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="d3290-104">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="d3290-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d3290-105">Affiche la liste des packages à partir d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="d3290-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="d3290-106">Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="d3290-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="d3290-107">Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="d3290-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="d3290-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="d3290-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="d3290-109">où les termes de recherche facultatif filtre la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="d3290-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="d3290-110">Termes de recherche sont appliqués aux noms des packages, les balises et les descriptions de package, comme lors de leur utilisation sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d3290-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="d3290-111">Options</span><span class="sxs-lookup"><span data-stu-id="d3290-111">Options</span></span>

| <span data-ttu-id="d3290-112">Option</span><span class="sxs-lookup"><span data-stu-id="d3290-112">Option</span></span> | <span data-ttu-id="d3290-113">Description</span><span class="sxs-lookup"><span data-stu-id="d3290-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3290-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d3290-114">AllVersions</span></span> | <span data-ttu-id="d3290-115">Répertorier toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="d3290-115">List all versions of a package.</span></span> <span data-ttu-id="d3290-116">Par défaut, la dernière version de package s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d3290-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="d3290-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d3290-117">ConfigFile</span></span> | <span data-ttu-id="d3290-118">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="d3290-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d3290-119">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d3290-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d3290-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d3290-120">ForceEnglishOutput</span></span> | <span data-ttu-id="d3290-121">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="d3290-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d3290-122">Help</span><span class="sxs-lookup"><span data-stu-id="d3290-122">Help</span></span> | <span data-ttu-id="d3290-123">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="d3290-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="d3290-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="d3290-124">IncludeDelisted</span></span> | <span data-ttu-id="d3290-125">*(3.2 +)*  Afficher les packages non listées.</span><span class="sxs-lookup"><span data-stu-id="d3290-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="d3290-126">Non interactif</span><span class="sxs-lookup"><span data-stu-id="d3290-126">NonInteractive</span></span> | <span data-ttu-id="d3290-127">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="d3290-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d3290-128">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="d3290-128">PreRelease</span></span> | <span data-ttu-id="d3290-129">Inclut les versions préliminaires des packages dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d3290-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="d3290-130">Source</span><span class="sxs-lookup"><span data-stu-id="d3290-130">Source</span></span> | <span data-ttu-id="d3290-131">Spécifie une liste des sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="d3290-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="d3290-132">Commentaires</span><span class="sxs-lookup"><span data-stu-id="d3290-132">Verbosity</span></span> | <span data-ttu-id="d3290-133">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="d3290-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d3290-134">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d3290-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d3290-135">Exemples</span><span class="sxs-lookup"><span data-stu-id="d3290-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
