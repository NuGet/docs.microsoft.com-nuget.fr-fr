---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande nuget.exe setapikey
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780017"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="53840-103">commande setapikey (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="53840-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="53840-104">**S’applique à : consommation de** packages, publication &bullet; des **versions prises en charge :** toutes</span><span class="sxs-lookup"><span data-stu-id="53840-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="53840-105">Enregistre une clé API pour une URL de serveur donnée dans `NuGet.Config` afin qu’elle n’ait pas besoin d’être entrée pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="53840-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="53840-106">Utilisation</span><span class="sxs-lookup"><span data-stu-id="53840-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="53840-107">où `<source>` identifie le serveur et `<key>` est la clé à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="53840-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="53840-108">Si `<source>` est omis, NuGet.org est utilisé par défaut.</span><span class="sxs-lookup"><span data-stu-id="53840-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="53840-109">La clé API n’est pas utilisée pour l’authentification auprès du flux privé.</span><span class="sxs-lookup"><span data-stu-id="53840-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="53840-110">Reportez-vous à la [ `nuget sources` commande](../cli-reference/cli-ref-sources.md) pour gérer les informations d’identification pour l’authentification auprès de la source.</span><span class="sxs-lookup"><span data-stu-id="53840-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="53840-111">Les clés API peuvent être obtenues à partir des serveurs NuGet individuels.</span><span class="sxs-lookup"><span data-stu-id="53840-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="53840-112">Pour créer et gérer des APIKeys pour nuget.org, consultez la rubrique [acquisition d’une clé API](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span><span class="sxs-lookup"><span data-stu-id="53840-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="53840-113">Options</span><span class="sxs-lookup"><span data-stu-id="53840-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="53840-114">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="53840-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="53840-115">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="53840-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="53840-116">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="53840-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="53840-117">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="53840-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="53840-118">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="53840-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="53840-119">URL du serveur où la clé d’API est valide.</span><span class="sxs-lookup"><span data-stu-id="53840-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="53840-120">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="53840-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="53840-121">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="53840-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="53840-122">Exemples</span><span class="sxs-lookup"><span data-stu-id="53840-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
