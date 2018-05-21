---
title: Commande de help NuGet CLI
description: Informations de référence pour la commande de help nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="0151e-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="0151e-103">help or ?</span></span> <span data-ttu-id="0151e-104">(commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0151e-104">command (NuGet CLI)</span></span>

<span data-ttu-id="0151e-105">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="0151e-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="0151e-106">Général des informations et des informations sur les commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0151e-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="0151e-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="0151e-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="0151e-108">où [commande] identifie une commande spécifique pour laquelle afficher l’aide.</span><span class="sxs-lookup"><span data-stu-id="0151e-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="0151e-109">Des commandes, tenez compte à spécifier *aide* tout d’abord, comme avec `nuget help install`, étant donné qu’un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, vous ne sera pas obtenir de l’aide sur la commande d’installation mais va installer le package nommé aide.</span><span class="sxs-lookup"><span data-stu-id="0151e-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="0151e-110">Options</span><span class="sxs-lookup"><span data-stu-id="0151e-110">Options</span></span>

| <span data-ttu-id="0151e-111">Option</span><span class="sxs-lookup"><span data-stu-id="0151e-111">Option</span></span> | <span data-ttu-id="0151e-112">Description</span><span class="sxs-lookup"><span data-stu-id="0151e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0151e-113">Tous</span><span class="sxs-lookup"><span data-stu-id="0151e-113">All</span></span> | <span data-ttu-id="0151e-114">Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est donnée.</span><span class="sxs-lookup"><span data-stu-id="0151e-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="0151e-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0151e-115">ConfigFile</span></span> | <span data-ttu-id="0151e-116">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="0151e-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0151e-117">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0151e-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0151e-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0151e-118">ForceEnglishOutput</span></span> | <span data-ttu-id="0151e-119">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="0151e-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0151e-120">Help</span><span class="sxs-lookup"><span data-stu-id="0151e-120">Help</span></span> | <span data-ttu-id="0151e-121">Affiche l’aide de la commande aide lui-même.</span><span class="sxs-lookup"><span data-stu-id="0151e-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="0151e-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="0151e-122">Markdown</span></span> | <span data-ttu-id="0151e-123">Imprimer une aide détaillée dans le format markdown lorsqu’il est utilisé avec `-All`.</span><span class="sxs-lookup"><span data-stu-id="0151e-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="0151e-124">Ignoré dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="0151e-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="0151e-125">Non interactif</span><span class="sxs-lookup"><span data-stu-id="0151e-125">NonInteractive</span></span> | <span data-ttu-id="0151e-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="0151e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0151e-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="0151e-127">Verbosity</span></span> | <span data-ttu-id="0151e-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="0151e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0151e-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0151e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0151e-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="0151e-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
