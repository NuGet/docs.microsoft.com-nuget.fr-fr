---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327606"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="92c5a-103">commande setapikey (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="92c5a-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="92c5a-104">**S’applique à: consommation de** packages &bullet; , publication des **versions prises en charge:** toutes</span><span class="sxs-lookup"><span data-stu-id="92c5a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="92c5a-105">Enregistre une clé API pour une URL de serveur donnée `NuGet.Config` dans afin qu’elle n’ait pas besoin d’être entrée pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="92c5a-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="92c5a-106">Usage</span><span class="sxs-lookup"><span data-stu-id="92c5a-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="92c5a-107">où `<source>` identifie le serveur et `<key>` représente la clé ou le mot de passe à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="92c5a-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="92c5a-108">Si `<source>` est omis, NuGet.org est utilisé par défaut.</span><span class="sxs-lookup"><span data-stu-id="92c5a-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="92c5a-109">Options</span><span class="sxs-lookup"><span data-stu-id="92c5a-109">Options</span></span>

| <span data-ttu-id="92c5a-110">Option</span><span class="sxs-lookup"><span data-stu-id="92c5a-110">Option</span></span> | <span data-ttu-id="92c5a-111">Description</span><span class="sxs-lookup"><span data-stu-id="92c5a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92c5a-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="92c5a-112">ConfigFile</span></span> | <span data-ttu-id="92c5a-113">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="92c5a-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="92c5a-114">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="92c5a-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="92c5a-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="92c5a-115">ForceEnglishOutput</span></span> | <span data-ttu-id="92c5a-116">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="92c5a-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="92c5a-117">Help</span><span class="sxs-lookup"><span data-stu-id="92c5a-117">Help</span></span> | <span data-ttu-id="92c5a-118">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="92c5a-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="92c5a-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="92c5a-119">NonInteractive</span></span> | <span data-ttu-id="92c5a-120">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92c5a-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="92c5a-121">Commentaires</span><span class="sxs-lookup"><span data-stu-id="92c5a-121">Verbosity</span></span> | <span data-ttu-id="92c5a-122">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="92c5a-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="92c5a-123">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="92c5a-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="92c5a-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="92c5a-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
