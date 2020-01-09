---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383967"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="b0186-103">commande setapikey (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="b0186-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="b0186-104">**S’applique à : consommation de** packages, publication &bullet; **versions prises en charge :** tout</span><span class="sxs-lookup"><span data-stu-id="b0186-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b0186-105">Enregistre une clé API pour une URL de serveur donnée dans `NuGet.Config` afin qu’il n’ait pas besoin d’être entré pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="b0186-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b0186-106">Contrôle</span><span class="sxs-lookup"><span data-stu-id="b0186-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="b0186-107">où `<source>` identifie le serveur et `<key>` est la clé ou le mot de passe à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="b0186-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="b0186-108">Si `<source>` est omis, nuget.org est utilisé par défaut.</span><span class="sxs-lookup"><span data-stu-id="b0186-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="b0186-109">La clé API n’est pas utilisée pour l’authentification auprès du flux privé.</span><span class="sxs-lookup"><span data-stu-id="b0186-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="b0186-110">Reportez-vous à [`nuget sources` commande](../cli-reference/cli-ref-sources.md) pour gérer les informations d’identification pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="b0186-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="b0186-111">Options</span><span class="sxs-lookup"><span data-stu-id="b0186-111">Options</span></span>

| <span data-ttu-id="b0186-112">Option</span><span class="sxs-lookup"><span data-stu-id="b0186-112">Option</span></span> | <span data-ttu-id="b0186-113">Description</span><span class="sxs-lookup"><span data-stu-id="b0186-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0186-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b0186-114">ConfigFile</span></span> | <span data-ttu-id="b0186-115">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="b0186-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b0186-116">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b0186-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b0186-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b0186-117">ForceEnglishOutput</span></span> | <span data-ttu-id="b0186-118">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="b0186-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b0186-119">Aide</span><span class="sxs-lookup"><span data-stu-id="b0186-119">Help</span></span> | <span data-ttu-id="b0186-120">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="b0186-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="b0186-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b0186-121">NonInteractive</span></span> | <span data-ttu-id="b0186-122">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b0186-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b0186-123">Commentaires</span><span class="sxs-lookup"><span data-stu-id="b0186-123">Verbosity</span></span> | <span data-ttu-id="b0186-124">Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="b0186-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b0186-125">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b0186-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b0186-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="b0186-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
