---
title: Commande de variables locales de CLI de NuGet
description: Référence de la commande de variables locales de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545026"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="473c2-103">locals (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="473c2-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="473c2-104">**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="473c2-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="473c2-105">Efface ou répertorie les ressources NuGet locales telles que la *http-cache*, *global-packages* dossier et le dossier temporaire.</span><span class="sxs-lookup"><span data-stu-id="473c2-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="473c2-106">Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="473c2-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="473c2-107">Pour plus d’informations, consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="473c2-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="473c2-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="473c2-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="473c2-109">où `<folder>` est un des `all`, `http-cache`, `packages-cache` *(3.5 et versions antérieures)*, `global-packages`, `temp` *(3.4 +)*, et `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="473c2-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="473c2-110">Options</span><span class="sxs-lookup"><span data-stu-id="473c2-110">Options</span></span>

| <span data-ttu-id="473c2-111">Option</span><span class="sxs-lookup"><span data-stu-id="473c2-111">Option</span></span> | <span data-ttu-id="473c2-112">Description</span><span class="sxs-lookup"><span data-stu-id="473c2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="473c2-113">Effacer</span><span class="sxs-lookup"><span data-stu-id="473c2-113">Clear</span></span> | <span data-ttu-id="473c2-114">Efface le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="473c2-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="473c2-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="473c2-115">ConfigFile</span></span> | <span data-ttu-id="473c2-116">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="473c2-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="473c2-117">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="473c2-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="473c2-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="473c2-118">ForceEnglishOutput</span></span> | <span data-ttu-id="473c2-119">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="473c2-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="473c2-120">Help</span><span class="sxs-lookup"><span data-stu-id="473c2-120">Help</span></span> | <span data-ttu-id="473c2-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="473c2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="473c2-122">Liste</span><span class="sxs-lookup"><span data-stu-id="473c2-122">List</span></span> | <span data-ttu-id="473c2-123">Répertorie l’emplacement du dossier spécifié, ou les emplacements de tous les dossiers lorsqu’il est utilisé avec *tous les*.</span><span class="sxs-lookup"><span data-stu-id="473c2-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="473c2-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="473c2-124">NonInteractive</span></span> | <span data-ttu-id="473c2-125">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="473c2-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="473c2-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="473c2-126">Verbosity</span></span> | <span data-ttu-id="473c2-127">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="473c2-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="473c2-128">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="473c2-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="473c2-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="473c2-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="473c2-130">Pour obtenir des exemples supplémentaires, consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="473c2-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
