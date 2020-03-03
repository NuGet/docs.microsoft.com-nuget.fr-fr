---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231225"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="d861a-103">commande setapikey (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="d861a-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="d861a-104">**S’applique à : consommation de** packages, publication &bullet; **versions prises en charge :** tout</span><span class="sxs-lookup"><span data-stu-id="d861a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d861a-105">Enregistre une clé API pour une URL de serveur donnée dans `NuGet.Config` afin qu’il n’ait pas besoin d’être entré pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d861a-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d861a-106">Usage</span><span class="sxs-lookup"><span data-stu-id="d861a-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="d861a-107">où `<source>` identifie le serveur et `<key>` est la clé à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="d861a-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="d861a-108">Si `<source>` est omis, nuget.org est utilisé par défaut.</span><span class="sxs-lookup"><span data-stu-id="d861a-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="d861a-109">La clé API n’est pas utilisée pour l’authentification auprès du flux privé.</span><span class="sxs-lookup"><span data-stu-id="d861a-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="d861a-110">Reportez-vous à [`nuget sources` commande](../cli-reference/cli-ref-sources.md) pour gérer les informations d’identification pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="d861a-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="d861a-111">Les clés API peuvent être obtenues à partir des serveurs NuGet individuels.</span><span class="sxs-lookup"><span data-stu-id="d861a-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="d861a-112">Pour créer et gérer des APIKeys pour nuget.org, reportez-vous à la rubrique [Publish-API-Key](../../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="d861a-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="d861a-113">Options</span><span class="sxs-lookup"><span data-stu-id="d861a-113">Options</span></span>

| <span data-ttu-id="d861a-114">Option</span><span class="sxs-lookup"><span data-stu-id="d861a-114">Option</span></span> | <span data-ttu-id="d861a-115">Description</span><span class="sxs-lookup"><span data-stu-id="d861a-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d861a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d861a-116">ConfigFile</span></span> | <span data-ttu-id="d861a-117">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="d861a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d861a-118">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d861a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d861a-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d861a-119">ForceEnglishOutput</span></span> | <span data-ttu-id="d861a-120">*(3.5 +)* Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais.</span><span class="sxs-lookup"><span data-stu-id="d861a-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d861a-121">Aide</span><span class="sxs-lookup"><span data-stu-id="d861a-121">Help</span></span> | <span data-ttu-id="d861a-122">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="d861a-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="d861a-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d861a-123">NonInteractive</span></span> | <span data-ttu-id="d861a-124">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d861a-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d861a-125">Commentaires</span><span class="sxs-lookup"><span data-stu-id="d861a-125">Verbosity</span></span> | <span data-ttu-id="d861a-126">Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="d861a-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d861a-127">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d861a-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d861a-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="d861a-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
