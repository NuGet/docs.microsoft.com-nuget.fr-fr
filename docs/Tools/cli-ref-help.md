---
title: Commande de help NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informations de référence pour la commande de help nuget.exe
keywords: référence d’aide de NuGet, la commande aide
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 440861e53b4a9ff73a9d3e8a2a3dad7dbddc9584
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="a0621-104">aide ou ?</span><span class="sxs-lookup"><span data-stu-id="a0621-104">help or ?</span></span> <span data-ttu-id="a0621-105">commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a0621-105">command (NuGet CLI)</span></span>

<span data-ttu-id="a0621-106">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="a0621-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a0621-107">Général des informations et des informations sur les commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a0621-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="a0621-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="a0621-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="a0621-109">où [commande] identifie une commande spécifique pour laquelle afficher l’aide.</span><span class="sxs-lookup"><span data-stu-id="a0621-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="a0621-110">Des commandes, tenez compte à spécifier *aide* tout d’abord, comme avec `nuget help install`, étant donné qu’un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, vous ne sera pas obtenir de l’aide sur la commande d’installation mais va installer le package nommé aide.</span><span class="sxs-lookup"><span data-stu-id="a0621-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="a0621-111">Options</span><span class="sxs-lookup"><span data-stu-id="a0621-111">Options</span></span>

| <span data-ttu-id="a0621-112">Option</span><span class="sxs-lookup"><span data-stu-id="a0621-112">Option</span></span> | <span data-ttu-id="a0621-113">Description</span><span class="sxs-lookup"><span data-stu-id="a0621-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0621-114">Tous</span><span class="sxs-lookup"><span data-stu-id="a0621-114">All</span></span> | <span data-ttu-id="a0621-115">Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est donnée.</span><span class="sxs-lookup"><span data-stu-id="a0621-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="a0621-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0621-116">ConfigFile</span></span> | <span data-ttu-id="a0621-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="a0621-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a0621-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a0621-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a0621-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a0621-119">ForceEnglishOutput</span></span> | <span data-ttu-id="a0621-120">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="a0621-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a0621-121">Help</span><span class="sxs-lookup"><span data-stu-id="a0621-121">Help</span></span> | <span data-ttu-id="a0621-122">Affiche l’aide de la commande aide lui-même.</span><span class="sxs-lookup"><span data-stu-id="a0621-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="a0621-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="a0621-123">Markdown</span></span> | <span data-ttu-id="a0621-124">Imprimer une aide détaillée dans le format markdown lorsqu’il est utilisé avec `-All`.</span><span class="sxs-lookup"><span data-stu-id="a0621-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="a0621-125">Ignoré dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="a0621-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="a0621-126">Non interactif</span><span class="sxs-lookup"><span data-stu-id="a0621-126">NonInteractive</span></span> | <span data-ttu-id="a0621-127">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="a0621-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a0621-128">Commentaires</span><span class="sxs-lookup"><span data-stu-id="a0621-128">Verbosity</span></span> | <span data-ttu-id="a0621-129">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="a0621-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a0621-130">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a0621-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a0621-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="a0621-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
