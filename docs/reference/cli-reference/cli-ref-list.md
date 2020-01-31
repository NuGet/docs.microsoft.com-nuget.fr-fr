---
title: Commande de liste de l’interface CLI NuGet
description: Référence pour la commande de liste NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813336"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="2e2f2-103">List, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="2e2f2-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="2e2f2-104">**S’applique à : consommation de** packages, publication &bullet; **versions prises en charge :** tout</span><span class="sxs-lookup"><span data-stu-id="2e2f2-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2e2f2-105">Affiche la liste des packages d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="2e2f2-106">Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="2e2f2-107">Si `NuGet.Config` spécifie aucune source, `list` utilise le flux par défaut (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="2e2f2-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="2e2f2-108">Contrôle</span><span class="sxs-lookup"><span data-stu-id="2e2f2-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="2e2f2-109">où les termes de recherche facultatifs filtrent la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="2e2f2-110">Les termes de recherche sont appliqués aux noms des packages, des balises et des descriptions de package comme c’est le cas lorsque vous les utilisez sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="2e2f2-111">Options</span><span class="sxs-lookup"><span data-stu-id="2e2f2-111">Options</span></span>

| <span data-ttu-id="2e2f2-112">Option</span><span class="sxs-lookup"><span data-stu-id="2e2f2-112">Option</span></span> | <span data-ttu-id="2e2f2-113">Description</span><span class="sxs-lookup"><span data-stu-id="2e2f2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e2f2-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="2e2f2-114">AllVersions</span></span> | <span data-ttu-id="2e2f2-115">Répertorie toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-115">List all versions of a package.</span></span> <span data-ttu-id="2e2f2-116">Par défaut, seule la dernière version du package est affichée.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="2e2f2-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2e2f2-117">ConfigFile</span></span> | <span data-ttu-id="2e2f2-118">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2e2f2-119">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2e2f2-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2e2f2-120">ForceEnglishOutput</span></span> | <span data-ttu-id="2e2f2-121">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2e2f2-122">Aide</span><span class="sxs-lookup"><span data-stu-id="2e2f2-122">Help</span></span> | <span data-ttu-id="2e2f2-123">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="2e2f2-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="2e2f2-124">IncludeDelisted</span></span> | <span data-ttu-id="2e2f2-125">*(3.2 +)* Affichez les packages qui ne sont pas répertoriés.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="2e2f2-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2e2f2-126">NonInteractive</span></span> | <span data-ttu-id="2e2f2-127">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2e2f2-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="2e2f2-128">PreRelease</span></span> | <span data-ttu-id="2e2f2-129">Contient des packages de version préliminaire dans la liste.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="2e2f2-130">Source</span><span class="sxs-lookup"><span data-stu-id="2e2f2-130">Source</span></span> | <span data-ttu-id="2e2f2-131">Spécifie une liste de sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="2e2f2-132">Commentaires</span><span class="sxs-lookup"><span data-stu-id="2e2f2-132">Verbosity</span></span> | <span data-ttu-id="2e2f2-133">Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="2e2f2-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2e2f2-134">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2e2f2-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2e2f2-135">Exemples</span><span class="sxs-lookup"><span data-stu-id="2e2f2-135">Examples</span></span>

<span data-ttu-id="2e2f2-136">Répertorier tous les packages à partir des flux configurés :</span><span class="sxs-lookup"><span data-stu-id="2e2f2-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="2e2f2-137">Répertoriez les packages liés à Azure avec un niveau de détail détaillé :</span><span class="sxs-lookup"><span data-stu-id="2e2f2-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="2e2f2-138">Répertorier toutes les versions des packages associés à Azure à partir de flux configurés :</span><span class="sxs-lookup"><span data-stu-id="2e2f2-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="2e2f2-139">Répertorie toutes les versions des packages liés à JSON à partir de la source/du flux spécifié :</span><span class="sxs-lookup"><span data-stu-id="2e2f2-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="2e2f2-140">Répertorier les packages liés à JSON à partir de plusieurs sources/flux :</span><span class="sxs-lookup"><span data-stu-id="2e2f2-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

