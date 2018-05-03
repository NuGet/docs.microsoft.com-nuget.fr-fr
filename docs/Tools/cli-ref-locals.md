---
title: Commande de variables locales NuGet CLI
description: Référence de la commande de variables locales de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="8c0c9-103">commande de variables locales (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8c0c9-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="8c0c9-104">**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="8c0c9-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="8c0c9-105">Efface ou répertorie les ressources de NuGet locales telles que la *du cache http*, *global-packages* dossier et le dossier temporaire.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="8c0c9-106">Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="8c0c9-107">Pour plus d’informations, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8c0c9-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8c0c9-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="8c0c9-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="8c0c9-109">où `<folder>` est un des `all`, `http-cache`, `packages-cache` *(3.5 et versions antérieures)*, `global-packages`, et `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="8c0c9-110">Options</span><span class="sxs-lookup"><span data-stu-id="8c0c9-110">Options</span></span>

| <span data-ttu-id="8c0c9-111">Option</span><span class="sxs-lookup"><span data-stu-id="8c0c9-111">Option</span></span> | <span data-ttu-id="8c0c9-112">Description</span><span class="sxs-lookup"><span data-stu-id="8c0c9-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c0c9-113">Effacer</span><span class="sxs-lookup"><span data-stu-id="8c0c9-113">Clear</span></span> | <span data-ttu-id="8c0c9-114">Efface le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="8c0c9-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8c0c9-115">ConfigFile</span></span> | <span data-ttu-id="8c0c9-116">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8c0c9-117">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8c0c9-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8c0c9-118">ForceEnglishOutput</span></span> | <span data-ttu-id="8c0c9-119">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8c0c9-120">Help</span><span class="sxs-lookup"><span data-stu-id="8c0c9-120">Help</span></span> | <span data-ttu-id="8c0c9-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="8c0c9-122">Liste</span><span class="sxs-lookup"><span data-stu-id="8c0c9-122">List</span></span> | <span data-ttu-id="8c0c9-123">Répertorie l’emplacement du dossier spécifié, ou les emplacements de dossiers de tous les cas d’utilisation avec *tous les*.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="8c0c9-124">Non interactif</span><span class="sxs-lookup"><span data-stu-id="8c0c9-124">NonInteractive</span></span> | <span data-ttu-id="8c0c9-125">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8c0c9-126">Commentaires</span><span class="sxs-lookup"><span data-stu-id="8c0c9-126">Verbosity</span></span> | <span data-ttu-id="8c0c9-127">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="8c0c9-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8c0c9-128">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8c0c9-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8c0c9-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="8c0c9-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="8c0c9-130">Pour obtenir des exemples supplémentaires, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8c0c9-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
