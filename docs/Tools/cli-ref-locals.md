---
title: Commande de variables locales NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de variables locales de nuget.exe"
keywords: "référence de variables locales de NuGet, commande de variables locales"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="7d8df-104">commande de variables locales (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7d8df-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="7d8df-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7d8df-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7d8df-106">Efface ou des listes de ressources NuGet locales telles que le cache de requête http, le cache de packages et le dossier packages global d’échelle de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7d8df-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="7d8df-107">Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="7d8df-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="7d8df-108">Pour plus d’informations, consultez [gestion du NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="7d8df-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7d8df-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="7d8df-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="7d8df-110">où `<cache>` est un des `all`, `http-cache`, `packages-cache`, `global-packages`, et `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="7d8df-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="7d8df-111">Options</span><span class="sxs-lookup"><span data-stu-id="7d8df-111">Options</span></span>

| <span data-ttu-id="7d8df-112">Option</span><span class="sxs-lookup"><span data-stu-id="7d8df-112">Option</span></span> | <span data-ttu-id="7d8df-113">Description</span><span class="sxs-lookup"><span data-stu-id="7d8df-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7d8df-114">Effacer</span><span class="sxs-lookup"><span data-stu-id="7d8df-114">Clear</span></span> | <span data-ttu-id="7d8df-115">Efface le cache spécifié.</span><span class="sxs-lookup"><span data-stu-id="7d8df-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="7d8df-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7d8df-116">ConfigFile</span></span> | <span data-ttu-id="7d8df-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="7d8df-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7d8df-118">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7d8df-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7d8df-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7d8df-119">ForceEnglishOutput</span></span> | <span data-ttu-id="7d8df-120">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="7d8df-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7d8df-121">Help</span><span class="sxs-lookup"><span data-stu-id="7d8df-121">Help</span></span> | <span data-ttu-id="7d8df-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="7d8df-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="7d8df-123">Liste</span><span class="sxs-lookup"><span data-stu-id="7d8df-123">List</span></span> | <span data-ttu-id="7d8df-124">Répertorie l’emplacement du cache spécifié, ou les emplacements de tous les caches lorsqu’il est utilisé avec *tous les*.</span><span class="sxs-lookup"><span data-stu-id="7d8df-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="7d8df-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="7d8df-125">NonInteractive</span></span> | <span data-ttu-id="7d8df-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="7d8df-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7d8df-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="7d8df-127">Verbosity</span></span> | <span data-ttu-id="7d8df-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="7d8df-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7d8df-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7d8df-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7d8df-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="7d8df-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
