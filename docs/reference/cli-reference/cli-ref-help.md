---
title: Commande d’aide de l’interface CLI NuGet
description: Référence pour la commande d’aide nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623108"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="67408-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="67408-103">help or ?</span></span> <span data-ttu-id="67408-104">Command (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="67408-104">command (NuGet CLI)</span></span>

<span data-ttu-id="67408-105">**S’applique à :** toutes les &bullet; **versions prises en charge**: toutes</span><span class="sxs-lookup"><span data-stu-id="67408-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="67408-106">Affiche des informations d’aide générales et des informations d’aide sur des commandes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="67408-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="67408-107">Usage</span><span class="sxs-lookup"><span data-stu-id="67408-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="67408-108">où [commande] identifie une commande spécifique pour laquelle afficher l’aide.</span><span class="sxs-lookup"><span data-stu-id="67408-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="67408-109">Avec certaines commandes, pensez à spécifier *l’aide* en premier, comme avec `nuget help install` , car il existe un package nommé « help » sur NuGet.org. Si vous donnez la commande `nuget install help` , vous n’obtiendrez pas d’aide sur la commande d’installation, mais vous installerez à la place le package nommé Help.</span><span class="sxs-lookup"><span data-stu-id="67408-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="67408-110">Options</span><span class="sxs-lookup"><span data-stu-id="67408-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="67408-111">Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="67408-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="67408-112">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="67408-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="67408-113">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="67408-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="67408-114">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="67408-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="67408-115">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="67408-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="67408-116">Imprimer une aide détaillée dans le format de démarque lorsqu’il est utilisé avec `-All` .</span><span class="sxs-lookup"><span data-stu-id="67408-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="67408-117">Sinon, ignoré.</span><span class="sxs-lookup"><span data-stu-id="67408-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="67408-118">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="67408-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="67408-119">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="67408-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="67408-120">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="67408-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="67408-121">Exemples</span><span class="sxs-lookup"><span data-stu-id="67408-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
