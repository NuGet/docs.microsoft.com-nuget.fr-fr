---
title: Commande de help NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour la commande de help nuget.exe"
keywords: "référence d’aide de NuGet, la commande aide"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b4255c353e412cf1d1a59590ee816b7887c90653
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="cdaad-104">aide ou ?</span><span class="sxs-lookup"><span data-stu-id="cdaad-104">help or ?</span></span> <span data-ttu-id="cdaad-105">commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cdaad-105">command (NuGet CLI)</span></span>

<span data-ttu-id="cdaad-106">**S’applique à :** tous les &bullet; **versions prises en charge**: tous les</span><span class="sxs-lookup"><span data-stu-id="cdaad-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="cdaad-107">Général des informations et des informations sur les commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cdaad-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="cdaad-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="cdaad-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="cdaad-109">où [commande] identifie une commande spécifique pour laquelle afficher l’aide.</span><span class="sxs-lookup"><span data-stu-id="cdaad-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="cdaad-110">Des commandes, tenez compte à spécifier *aide* tout d’abord, comme avec `nuget help install`, étant donné qu’un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, vous ne sera pas obtenir de l’aide sur la commande d’installation mais va installer le package nommé aide.</span><span class="sxs-lookup"><span data-stu-id="cdaad-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="cdaad-111">Options</span><span class="sxs-lookup"><span data-stu-id="cdaad-111">Options</span></span>

| <span data-ttu-id="cdaad-112">Option</span><span class="sxs-lookup"><span data-stu-id="cdaad-112">Option</span></span> | <span data-ttu-id="cdaad-113">Description</span><span class="sxs-lookup"><span data-stu-id="cdaad-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdaad-114">Tous</span><span class="sxs-lookup"><span data-stu-id="cdaad-114">All</span></span> | <span data-ttu-id="cdaad-115">Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est donnée.</span><span class="sxs-lookup"><span data-stu-id="cdaad-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="cdaad-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cdaad-116">ConfigFile</span></span> | <span data-ttu-id="cdaad-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="cdaad-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cdaad-118">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="cdaad-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="cdaad-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cdaad-119">ForceEnglishOutput</span></span> | <span data-ttu-id="cdaad-120">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="cdaad-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cdaad-121">Help</span><span class="sxs-lookup"><span data-stu-id="cdaad-121">Help</span></span> | <span data-ttu-id="cdaad-122">Affiche l’aide de la commande aide lui-même.</span><span class="sxs-lookup"><span data-stu-id="cdaad-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="cdaad-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="cdaad-123">Markdown</span></span> | <span data-ttu-id="cdaad-124">Imprimer une aide détaillée dans le format markdown lorsqu’il est utilisé avec `-All`.</span><span class="sxs-lookup"><span data-stu-id="cdaad-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="cdaad-125">Ignoré dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="cdaad-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="cdaad-126">Non interactif</span><span class="sxs-lookup"><span data-stu-id="cdaad-126">NonInteractive</span></span> | <span data-ttu-id="cdaad-127">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="cdaad-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cdaad-128">Commentaires</span><span class="sxs-lookup"><span data-stu-id="cdaad-128">Verbosity</span></span> | <span data-ttu-id="cdaad-129">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="cdaad-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cdaad-130">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cdaad-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cdaad-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="cdaad-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
