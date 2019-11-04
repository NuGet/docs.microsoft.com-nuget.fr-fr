---
title: Commande de liste de l’interface CLI NuGet
description: Référence pour la commande de liste NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327736"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="41116-103">List, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="41116-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="41116-104">**S’applique à: consommation de** packages &bullet; , publication des **versions prises en charge:** toutes</span><span class="sxs-lookup"><span data-stu-id="41116-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="41116-105">Affiche la liste des packages d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="41116-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="41116-106">Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de `%AppData%\NuGet\NuGet.Config` configuration global, ( `~/.nuget/NuGet/NuGet.Config`Windows) ou, sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="41116-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="41116-107">Si `NuGet.Config` ne spécifie aucune source `list` , utilise le flux par défaut (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="41116-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="41116-108">Usage</span><span class="sxs-lookup"><span data-stu-id="41116-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="41116-109">où les termes de recherche facultatifs filtrent la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="41116-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="41116-110">Les termes de recherche sont appliqués aux noms des packages, des balises et des descriptions de package comme c’est le cas lorsque vous les utilisez sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="41116-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="41116-111">Options</span><span class="sxs-lookup"><span data-stu-id="41116-111">Options</span></span>

| <span data-ttu-id="41116-112">Option</span><span class="sxs-lookup"><span data-stu-id="41116-112">Option</span></span> | <span data-ttu-id="41116-113">Description</span><span class="sxs-lookup"><span data-stu-id="41116-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41116-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="41116-114">AllVersions</span></span> | <span data-ttu-id="41116-115">Répertorie toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="41116-115">List all versions of a package.</span></span> <span data-ttu-id="41116-116">Par défaut, seule la dernière version du package est affichée.</span><span class="sxs-lookup"><span data-stu-id="41116-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="41116-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="41116-117">ConfigFile</span></span> | <span data-ttu-id="41116-118">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="41116-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="41116-119">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="41116-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="41116-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="41116-120">ForceEnglishOutput</span></span> | <span data-ttu-id="41116-121">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="41116-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="41116-122">Help</span><span class="sxs-lookup"><span data-stu-id="41116-122">Help</span></span> | <span data-ttu-id="41116-123">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="41116-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="41116-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="41116-124">IncludeDelisted</span></span> | <span data-ttu-id="41116-125">*(3.2 +)* Affichez les packages qui ne sont pas répertoriés.</span><span class="sxs-lookup"><span data-stu-id="41116-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="41116-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="41116-126">NonInteractive</span></span> | <span data-ttu-id="41116-127">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41116-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="41116-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="41116-128">PreRelease</span></span> | <span data-ttu-id="41116-129">Contient des packages de version préliminaire dans la liste.</span><span class="sxs-lookup"><span data-stu-id="41116-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="41116-130">Source</span><span class="sxs-lookup"><span data-stu-id="41116-130">Source</span></span> | <span data-ttu-id="41116-131">Spécifie une liste de sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="41116-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="41116-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="41116-132">Verbosity</span></span> | <span data-ttu-id="41116-133">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="41116-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="41116-134">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="41116-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="41116-135">Exemples</span><span class="sxs-lookup"><span data-stu-id="41116-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
