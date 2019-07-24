---
title: Commande paramètres régionaux de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe variables locales
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327806"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="e6444-103">locals (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e6444-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="e6444-104">**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 3.3+</span><span class="sxs-lookup"><span data-stu-id="e6444-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="e6444-105">Efface ou répertorie les ressources NuGet locales, telles que le dossier *http-cache*, *Global-packages* et le dossier Temp.</span><span class="sxs-lookup"><span data-stu-id="e6444-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="e6444-106">La `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="e6444-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="e6444-107">Pour plus d’informations, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e6444-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="e6444-108">Usage</span><span class="sxs-lookup"><span data-stu-id="e6444-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="e6444-109">où `<folder>` est l' `plugins-cache` un `all` `packages-cache` `temp` `global-packages`   des, ,(3,5etversionsantérieures),,(3.4+)et(4.8+).`http-cache`</span><span class="sxs-lookup"><span data-stu-id="e6444-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="e6444-110">Options</span><span class="sxs-lookup"><span data-stu-id="e6444-110">Options</span></span>

| <span data-ttu-id="e6444-111">Option</span><span class="sxs-lookup"><span data-stu-id="e6444-111">Option</span></span> | <span data-ttu-id="e6444-112">Description</span><span class="sxs-lookup"><span data-stu-id="e6444-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6444-113">Effacer</span><span class="sxs-lookup"><span data-stu-id="e6444-113">Clear</span></span> | <span data-ttu-id="e6444-114">Efface le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="e6444-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="e6444-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e6444-115">ConfigFile</span></span> | <span data-ttu-id="e6444-116">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="e6444-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e6444-117">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e6444-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e6444-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e6444-118">ForceEnglishOutput</span></span> | <span data-ttu-id="e6444-119">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="e6444-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e6444-120">Help</span><span class="sxs-lookup"><span data-stu-id="e6444-120">Help</span></span> | <span data-ttu-id="e6444-121">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="e6444-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="e6444-122">Énumérer</span><span class="sxs-lookup"><span data-stu-id="e6444-122">List</span></span> | <span data-ttu-id="e6444-123">Répertorie l’emplacement du dossier spécifié, ou les emplacements de tous les dossiers lorsqu’ils sont utilisés avec *tous*.</span><span class="sxs-lookup"><span data-stu-id="e6444-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="e6444-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e6444-124">NonInteractive</span></span> | <span data-ttu-id="e6444-125">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6444-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e6444-126">Commentaires</span><span class="sxs-lookup"><span data-stu-id="e6444-126">Verbosity</span></span> | <span data-ttu-id="e6444-127">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="e6444-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e6444-128">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e6444-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e6444-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="e6444-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="e6444-130">Pour obtenir des exemples supplémentaires, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e6444-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
