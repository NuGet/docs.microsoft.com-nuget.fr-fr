---
title: Commande de variables locales de CLI de NuGet
description: Référence de la commande de variables locales de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794133"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="7e9f5-103">locals (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7e9f5-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="7e9f5-104">**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7e9f5-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7e9f5-105">Efface ou répertorie les ressources NuGet locales telles que la *http-cache*, *global-packages* dossier et le dossier temporaire.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="7e9f5-106">Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="7e9f5-107">Pour plus d’informations, consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="7e9f5-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7e9f5-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="7e9f5-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="7e9f5-109">où `<folder>` est un des `all`, `http-cache`, `packages-cache` *(3.5 et versions antérieures)*, `global-packages`, `temp` *(3.4 +)*, et `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="7e9f5-110">Options</span><span class="sxs-lookup"><span data-stu-id="7e9f5-110">Options</span></span>

| <span data-ttu-id="7e9f5-111">Option</span><span class="sxs-lookup"><span data-stu-id="7e9f5-111">Option</span></span> | <span data-ttu-id="7e9f5-112">Description</span><span class="sxs-lookup"><span data-stu-id="7e9f5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e9f5-113">Effacer</span><span class="sxs-lookup"><span data-stu-id="7e9f5-113">Clear</span></span> | <span data-ttu-id="7e9f5-114">Efface le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="7e9f5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7e9f5-115">ConfigFile</span></span> | <span data-ttu-id="7e9f5-116">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7e9f5-117">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7e9f5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7e9f5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="7e9f5-119">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7e9f5-120">Help</span><span class="sxs-lookup"><span data-stu-id="7e9f5-120">Help</span></span> | <span data-ttu-id="7e9f5-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="7e9f5-122">Liste</span><span class="sxs-lookup"><span data-stu-id="7e9f5-122">List</span></span> | <span data-ttu-id="7e9f5-123">Répertorie l’emplacement du dossier spécifié, ou les emplacements de tous les dossiers lorsqu’il est utilisé avec *tous les*.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="7e9f5-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7e9f5-124">NonInteractive</span></span> | <span data-ttu-id="7e9f5-125">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7e9f5-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7e9f5-126">Verbosity</span></span> | <span data-ttu-id="7e9f5-127">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="7e9f5-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7e9f5-128">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7e9f5-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7e9f5-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="7e9f5-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="7e9f5-130">Pour obtenir des exemples supplémentaires, consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="7e9f5-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
