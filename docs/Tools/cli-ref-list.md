---
title: Commande de liste NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Référence de la commande de liste de nuget.exe"
keywords: "référence de liste de NuGet, la liste packages commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="e12fc-104">commande de la liste (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e12fc-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="e12fc-105">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="e12fc-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e12fc-106">Affiche la liste des packages à partir d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="e12fc-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="e12fc-107">Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config`, sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="e12fc-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="e12fc-108">Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="e12fc-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="e12fc-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="e12fc-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="e12fc-110">où les termes de recherche facultatif filtre la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="e12fc-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="e12fc-111">Termes de recherche sont appliqués aux noms des packages, les balises et les descriptions de package.</span><span class="sxs-lookup"><span data-stu-id="e12fc-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="e12fc-112">Options</span><span class="sxs-lookup"><span data-stu-id="e12fc-112">Options</span></span>
| <span data-ttu-id="e12fc-113">Option</span><span class="sxs-lookup"><span data-stu-id="e12fc-113">Option</span></span> | <span data-ttu-id="e12fc-114">Description</span><span class="sxs-lookup"><span data-stu-id="e12fc-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e12fc-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="e12fc-115">AllVersions</span></span> | <span data-ttu-id="e12fc-116">Répertorier toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="e12fc-116">List all versions of a package.</span></span> <span data-ttu-id="e12fc-117">Par défaut, la dernière version de package s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e12fc-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="e12fc-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e12fc-118">ConfigFile</span></span> | <span data-ttu-id="e12fc-119">*(2.5 +)*  NuGet le fichier de configuration à appliquer.</span><span class="sxs-lookup"><span data-stu-id="e12fc-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="e12fc-120">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e12fc-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e12fc-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e12fc-121">ForceEnglishOutput</span></span> | <span data-ttu-id="e12fc-122">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="e12fc-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e12fc-123">Help</span><span class="sxs-lookup"><span data-stu-id="e12fc-123">Help</span></span> | <span data-ttu-id="e12fc-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="e12fc-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="e12fc-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="e12fc-125">IncludeDelisted</span></span> | <span data-ttu-id="e12fc-126">*(3.2 +)*  Afficher les packages non listées.</span><span class="sxs-lookup"><span data-stu-id="e12fc-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="e12fc-127">Non interactif</span><span class="sxs-lookup"><span data-stu-id="e12fc-127">NonInteractive</span></span> | <span data-ttu-id="e12fc-128">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="e12fc-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e12fc-129">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="e12fc-129">PreRelease</span></span> | <span data-ttu-id="e12fc-130">Inclut les versions préliminaires des packages dans la liste.</span><span class="sxs-lookup"><span data-stu-id="e12fc-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="e12fc-131">Source</span><span class="sxs-lookup"><span data-stu-id="e12fc-131">Source</span></span> | <span data-ttu-id="e12fc-132">Spécifie une liste des sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="e12fc-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="e12fc-133">Commentaires</span><span class="sxs-lookup"><span data-stu-id="e12fc-133">Verbosity</span></span> | <span data-ttu-id="e12fc-134">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="e12fc-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="e12fc-135">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e12fc-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e12fc-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="e12fc-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
