---
title: Commande setapikey de NuGet CLI
description: Référence de la commande setapikey de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549218"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="d2193-103">commande setapikey (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="d2193-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="d2193-104">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="d2193-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d2193-105">Enregistre une clé API pour une URL de serveur donnée en `NuGet.Config` afin qu’il n’a pas besoin être entrés pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d2193-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d2193-106">Utilisation</span><span class="sxs-lookup"><span data-stu-id="d2193-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="d2193-107">où `<source>` identifie le serveur et `<key>` est la clé ou le mot de passe à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="d2193-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="d2193-108">Si `<source>` est omis, nuget.org est pris en compte.</span><span class="sxs-lookup"><span data-stu-id="d2193-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="d2193-109">Options</span><span class="sxs-lookup"><span data-stu-id="d2193-109">Options</span></span>

| <span data-ttu-id="d2193-110">Option</span><span class="sxs-lookup"><span data-stu-id="d2193-110">Option</span></span> | <span data-ttu-id="d2193-111">Description</span><span class="sxs-lookup"><span data-stu-id="d2193-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d2193-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d2193-112">ConfigFile</span></span> | <span data-ttu-id="d2193-113">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="d2193-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d2193-114">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d2193-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d2193-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d2193-115">ForceEnglishOutput</span></span> | <span data-ttu-id="d2193-116">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="d2193-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d2193-117">Help</span><span class="sxs-lookup"><span data-stu-id="d2193-117">Help</span></span> | <span data-ttu-id="d2193-118">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="d2193-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="d2193-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d2193-119">NonInteractive</span></span> | <span data-ttu-id="d2193-120">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="d2193-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d2193-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d2193-121">Verbosity</span></span> | <span data-ttu-id="d2193-122">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="d2193-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d2193-123">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d2193-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d2193-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="d2193-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
