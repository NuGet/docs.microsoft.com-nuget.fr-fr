---
title: Commande de variables locales NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de la commande de variables locales de nuget.exe
keywords: référence de variables locales de NuGet, commande de variables locales
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="9ef7c-104">commande de variables locales (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9ef7c-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="9ef7c-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="9ef7c-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="9ef7c-106">Efface ou répertorie les ressources de NuGet locales telles que la *du cache http*, *global-packages* dossier et le dossier temporaire.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="9ef7c-107">Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="9ef7c-108">Pour plus d’informations, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9ef7c-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9ef7c-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="9ef7c-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="9ef7c-110">où `<folder>` est un des `all`, `http-cache`, `packages-cache` *(3.5 et versions antérieures)*, `global-packages`, et `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="9ef7c-111">Options</span><span class="sxs-lookup"><span data-stu-id="9ef7c-111">Options</span></span>

| <span data-ttu-id="9ef7c-112">Option</span><span class="sxs-lookup"><span data-stu-id="9ef7c-112">Option</span></span> | <span data-ttu-id="9ef7c-113">Description</span><span class="sxs-lookup"><span data-stu-id="9ef7c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9ef7c-114">Effacer</span><span class="sxs-lookup"><span data-stu-id="9ef7c-114">Clear</span></span> | <span data-ttu-id="9ef7c-115">Efface le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="9ef7c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9ef7c-116">ConfigFile</span></span> | <span data-ttu-id="9ef7c-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9ef7c-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9ef7c-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9ef7c-119">ForceEnglishOutput</span></span> | <span data-ttu-id="9ef7c-120">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9ef7c-121">Help</span><span class="sxs-lookup"><span data-stu-id="9ef7c-121">Help</span></span> | <span data-ttu-id="9ef7c-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="9ef7c-123">Liste</span><span class="sxs-lookup"><span data-stu-id="9ef7c-123">List</span></span> | <span data-ttu-id="9ef7c-124">Répertorie l’emplacement du dossier spécifié, ou les emplacements de dossiers de tous les cas d’utilisation avec *tous les*.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="9ef7c-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="9ef7c-125">NonInteractive</span></span> | <span data-ttu-id="9ef7c-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9ef7c-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="9ef7c-127">Verbosity</span></span> | <span data-ttu-id="9ef7c-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="9ef7c-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9ef7c-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9ef7c-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9ef7c-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="9ef7c-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="9ef7c-131">Pour obtenir des exemples supplémentaires, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9ef7c-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
