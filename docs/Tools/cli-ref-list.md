---
title: Commande de liste NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de liste de nuget.exe"
keywords: "référence de liste de NuGet, la liste packages commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="3826e-104">commande de la liste (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3826e-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="3826e-105">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="3826e-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3826e-106">Affiche la liste des packages à partir d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="3826e-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="3826e-107">Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config`, sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="3826e-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="3826e-108">Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="3826e-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="3826e-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="3826e-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="3826e-110">où les termes de recherche facultatif filtre la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="3826e-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="3826e-111">Termes de recherche sont appliqués aux noms des packages, les balises et les descriptions de package.</span><span class="sxs-lookup"><span data-stu-id="3826e-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="3826e-112">Options</span><span class="sxs-lookup"><span data-stu-id="3826e-112">Options</span></span>

| <span data-ttu-id="3826e-113">Option</span><span class="sxs-lookup"><span data-stu-id="3826e-113">Option</span></span> | <span data-ttu-id="3826e-114">Description</span><span class="sxs-lookup"><span data-stu-id="3826e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3826e-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3826e-115">AllVersions</span></span> | <span data-ttu-id="3826e-116">Répertorier toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="3826e-116">List all versions of a package.</span></span> <span data-ttu-id="3826e-117">Par défaut, la dernière version de package s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3826e-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="3826e-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3826e-118">ConfigFile</span></span> | <span data-ttu-id="3826e-119">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="3826e-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3826e-120">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3826e-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3826e-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3826e-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3826e-122">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="3826e-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3826e-123">Help</span><span class="sxs-lookup"><span data-stu-id="3826e-123">Help</span></span> | <span data-ttu-id="3826e-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="3826e-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3826e-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="3826e-125">IncludeDelisted</span></span> | <span data-ttu-id="3826e-126">*(3.2 +)*  Afficher les packages non listées.</span><span class="sxs-lookup"><span data-stu-id="3826e-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="3826e-127">Non interactif</span><span class="sxs-lookup"><span data-stu-id="3826e-127">NonInteractive</span></span> | <span data-ttu-id="3826e-128">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="3826e-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3826e-129">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="3826e-129">PreRelease</span></span> | <span data-ttu-id="3826e-130">Inclut les versions préliminaires des packages dans la liste.</span><span class="sxs-lookup"><span data-stu-id="3826e-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="3826e-131">Source</span><span class="sxs-lookup"><span data-stu-id="3826e-131">Source</span></span> | <span data-ttu-id="3826e-132">Spécifie une liste des sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="3826e-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="3826e-133">Commentaires</span><span class="sxs-lookup"><span data-stu-id="3826e-133">Verbosity</span></span> | <span data-ttu-id="3826e-134">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="3826e-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3826e-135">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3826e-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3826e-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="3826e-136">Examples</span></span>

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
