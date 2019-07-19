---
title: Commande d’aide de l’interface CLI NuGet
description: Référence pour la commande d’aide de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327796"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="27da6-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="27da6-103">help or ?</span></span> <span data-ttu-id="27da6-104">(commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="27da6-104">command (NuGet CLI)</span></span>

<span data-ttu-id="27da6-105">**S’applique à:** toutes les &bullet; **versions prises en charge**: toutes</span><span class="sxs-lookup"><span data-stu-id="27da6-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="27da6-106">Affiche des informations d’aide générales et des informations d’aide sur des commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="27da6-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="27da6-107">Usage</span><span class="sxs-lookup"><span data-stu-id="27da6-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="27da6-108">où [commande] identifie une commande spécifique pour laquelle afficher l’aide.</span><span class="sxs-lookup"><span data-stu-id="27da6-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="27da6-109">Avec certaines commandes, pensez à spécifier *l’aide* en premier, comme `nuget help install`avec, car il existe un package nommé «Help» sur NuGet.org. Si vous donnez la commande `nuget install help`, vous n’obtiendrez pas d’aide sur la commande d’installation, mais vous installerez à la place le package nommé Help.</span><span class="sxs-lookup"><span data-stu-id="27da6-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="27da6-110">Options</span><span class="sxs-lookup"><span data-stu-id="27da6-110">Options</span></span>

| <span data-ttu-id="27da6-111">Option</span><span class="sxs-lookup"><span data-stu-id="27da6-111">Option</span></span> | <span data-ttu-id="27da6-112">Description</span><span class="sxs-lookup"><span data-stu-id="27da6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27da6-113">Tous</span><span class="sxs-lookup"><span data-stu-id="27da6-113">All</span></span> | <span data-ttu-id="27da6-114">Imprimer une aide détaillée pour toutes les commandes disponibles; ignoré si une commande spécifique est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="27da6-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="27da6-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="27da6-115">ConfigFile</span></span> | <span data-ttu-id="27da6-116">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="27da6-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="27da6-117">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="27da6-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="27da6-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="27da6-118">ForceEnglishOutput</span></span> | <span data-ttu-id="27da6-119">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="27da6-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="27da6-120">Aide</span><span class="sxs-lookup"><span data-stu-id="27da6-120">Help</span></span> | <span data-ttu-id="27da6-121">Affiche des informations d’aide pour la commande d’aide elle-même.</span><span class="sxs-lookup"><span data-stu-id="27da6-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="27da6-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="27da6-122">Markdown</span></span> | <span data-ttu-id="27da6-123">Imprimer une aide détaillée dans le format de démarque lorsqu’il est utilisé avec `-All`.</span><span class="sxs-lookup"><span data-stu-id="27da6-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="27da6-124">Sinon, ignoré.</span><span class="sxs-lookup"><span data-stu-id="27da6-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="27da6-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="27da6-125">NonInteractive</span></span> | <span data-ttu-id="27da6-126">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="27da6-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="27da6-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="27da6-127">Verbosity</span></span> | <span data-ttu-id="27da6-128">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="27da6-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="27da6-129">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="27da6-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="27da6-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="27da6-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
