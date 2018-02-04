---
title: Commande setapikey de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande setapikey de nuget.exe"
keywords: "référence setapikey de NuGet, setapikey commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="1beb3-104">commande de setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1beb3-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="1beb3-105">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="1beb3-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1beb3-106">Enregistre une clé d’API pour une URL de serveur donnée en `NuGet.Config` afin qu’il n’a pas besoin d’être entrés pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="1beb3-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="1beb3-107">Utilisation</span><span class="sxs-lookup"><span data-stu-id="1beb3-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="1beb3-108">où `<source>` identifie le serveur et `<key>` est la clé ou le mot de passe à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="1beb3-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="1beb3-109">Si `<source>` est omis, nuget.org est supposé.</span><span class="sxs-lookup"><span data-stu-id="1beb3-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="1beb3-110">Options</span><span class="sxs-lookup"><span data-stu-id="1beb3-110">Options</span></span>

| <span data-ttu-id="1beb3-111">Option</span><span class="sxs-lookup"><span data-stu-id="1beb3-111">Option</span></span> | <span data-ttu-id="1beb3-112">Description</span><span class="sxs-lookup"><span data-stu-id="1beb3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1beb3-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1beb3-113">ConfigFile</span></span> | <span data-ttu-id="1beb3-114">Le fichier de configuration NuGet à modifier.</span><span class="sxs-lookup"><span data-stu-id="1beb3-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="1beb3-115">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1beb3-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1beb3-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1beb3-116">ForceEnglishOutput</span></span> | <span data-ttu-id="1beb3-117">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="1beb3-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1beb3-118">Help</span><span class="sxs-lookup"><span data-stu-id="1beb3-118">Help</span></span> | <span data-ttu-id="1beb3-119">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="1beb3-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="1beb3-120">Non interactif</span><span class="sxs-lookup"><span data-stu-id="1beb3-120">NonInteractive</span></span> | <span data-ttu-id="1beb3-121">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="1beb3-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1beb3-122">Commentaires</span><span class="sxs-lookup"><span data-stu-id="1beb3-122">Verbosity</span></span> | <span data-ttu-id="1beb3-123">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="1beb3-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1beb3-124">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1beb3-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1beb3-125">Exemples</span><span class="sxs-lookup"><span data-stu-id="1beb3-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
