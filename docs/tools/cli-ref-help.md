---
title: Commande de help CLI NuGet
description: Référence de la commande d’aide de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546561"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="2e488-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="2e488-103">help or ?</span></span> <span data-ttu-id="2e488-104">(commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2e488-104">command (NuGet CLI)</span></span>

<span data-ttu-id="2e488-105">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="2e488-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="2e488-106">Présente général des informations d’aide et les informations d’aide sur les commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2e488-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2e488-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="2e488-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="2e488-108">où [commande] identifie une commande spécifique pour laquelle afficher l’aide.</span><span class="sxs-lookup"><span data-stu-id="2e488-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="2e488-109">Avec certaines commandes, n’oubliez pas de spécifier *aide* tout d’abord, comme avec `nuget help install`, car il existe un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, ne sont pas obtenir de l’aide sur la commande d’installation, mais au lieu de cela installera le package nommé aide.</span><span class="sxs-lookup"><span data-stu-id="2e488-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="2e488-110">Options</span><span class="sxs-lookup"><span data-stu-id="2e488-110">Options</span></span>

| <span data-ttu-id="2e488-111">Option</span><span class="sxs-lookup"><span data-stu-id="2e488-111">Option</span></span> | <span data-ttu-id="2e488-112">Description</span><span class="sxs-lookup"><span data-stu-id="2e488-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e488-113">Tous</span><span class="sxs-lookup"><span data-stu-id="2e488-113">All</span></span> | <span data-ttu-id="2e488-114">Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est indiquée.</span><span class="sxs-lookup"><span data-stu-id="2e488-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="2e488-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2e488-115">ConfigFile</span></span> | <span data-ttu-id="2e488-116">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="2e488-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2e488-117">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2e488-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2e488-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2e488-118">ForceEnglishOutput</span></span> | <span data-ttu-id="2e488-119">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="2e488-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2e488-120">Help</span><span class="sxs-lookup"><span data-stu-id="2e488-120">Help</span></span> | <span data-ttu-id="2e488-121">Affiche l’aide de la commande d’aide.</span><span class="sxs-lookup"><span data-stu-id="2e488-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="2e488-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="2e488-122">Markdown</span></span> | <span data-ttu-id="2e488-123">Imprimer une aide détaillée au format markdown lorsqu’il est utilisé avec `-All`.</span><span class="sxs-lookup"><span data-stu-id="2e488-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="2e488-124">Ignoré dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="2e488-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="2e488-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2e488-125">NonInteractive</span></span> | <span data-ttu-id="2e488-126">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="2e488-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2e488-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2e488-127">Verbosity</span></span> | <span data-ttu-id="2e488-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="2e488-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2e488-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2e488-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2e488-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="2e488-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
