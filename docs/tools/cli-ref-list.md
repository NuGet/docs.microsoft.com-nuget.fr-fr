---
title: Afficher la commande CLI NuGet
description: Référence de la commande de liste de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549799"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b45d6-103">afficher la commande (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="b45d6-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="b45d6-104">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="b45d6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b45d6-105">Affiche une liste des packages à partir d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="b45d6-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b45d6-106">Si aucune source n’est spécifié, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="b45d6-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="b45d6-107">Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="b45d6-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b45d6-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="b45d6-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="b45d6-109">où les termes de recherche facultatif filtre la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="b45d6-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b45d6-110">Termes de recherche sont appliquées aux noms des packages, les balises et descriptions des packages comme ils le sont lors de leur utilisation sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b45d6-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="b45d6-111">Options</span><span class="sxs-lookup"><span data-stu-id="b45d6-111">Options</span></span>

| <span data-ttu-id="b45d6-112">Option</span><span class="sxs-lookup"><span data-stu-id="b45d6-112">Option</span></span> | <span data-ttu-id="b45d6-113">Description</span><span class="sxs-lookup"><span data-stu-id="b45d6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b45d6-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b45d6-114">AllVersions</span></span> | <span data-ttu-id="b45d6-115">Répertorier toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="b45d6-115">List all versions of a package.</span></span> <span data-ttu-id="b45d6-116">Par défaut, seule la dernière version de package s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b45d6-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="b45d6-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b45d6-117">ConfigFile</span></span> | <span data-ttu-id="b45d6-118">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="b45d6-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b45d6-119">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b45d6-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b45d6-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b45d6-120">ForceEnglishOutput</span></span> | <span data-ttu-id="b45d6-121">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="b45d6-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b45d6-122">Help</span><span class="sxs-lookup"><span data-stu-id="b45d6-122">Help</span></span> | <span data-ttu-id="b45d6-123">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="b45d6-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="b45d6-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="b45d6-124">IncludeDelisted</span></span> | <span data-ttu-id="b45d6-125">*(3.2 +)*  Afficher les packages non répertoriés.</span><span class="sxs-lookup"><span data-stu-id="b45d6-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="b45d6-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b45d6-126">NonInteractive</span></span> | <span data-ttu-id="b45d6-127">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="b45d6-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b45d6-128">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="b45d6-128">PreRelease</span></span> | <span data-ttu-id="b45d6-129">Inclut les packages de version préliminaire dans la liste.</span><span class="sxs-lookup"><span data-stu-id="b45d6-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="b45d6-130">Source</span><span class="sxs-lookup"><span data-stu-id="b45d6-130">Source</span></span> | <span data-ttu-id="b45d6-131">Spécifie une liste des sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="b45d6-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="b45d6-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b45d6-132">Verbosity</span></span> | <span data-ttu-id="b45d6-133">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="b45d6-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b45d6-134">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b45d6-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b45d6-135">Exemples</span><span class="sxs-lookup"><span data-stu-id="b45d6-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
