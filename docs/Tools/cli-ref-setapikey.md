---
title: Commande setapikey de NuGet CLI
description: Référence de la commande setapikey de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 968e22f32e51659590a6fe1e881bf5a9792a1331
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="cc85b-103">commande de setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cc85b-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="cc85b-104">**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="cc85b-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cc85b-105">Enregistre une clé d’API pour une URL de serveur donnée en `NuGet.Config` afin qu’il n’a pas besoin d’être entrés pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="cc85b-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="cc85b-106">Utilisation</span><span class="sxs-lookup"><span data-stu-id="cc85b-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="cc85b-107">où `<source>` identifie le serveur et `<key>` est la clé ou le mot de passe à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="cc85b-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="cc85b-108">Si `<source>` est omis, nuget.org est supposé.</span><span class="sxs-lookup"><span data-stu-id="cc85b-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="cc85b-109">Options</span><span class="sxs-lookup"><span data-stu-id="cc85b-109">Options</span></span>

| <span data-ttu-id="cc85b-110">Option</span><span class="sxs-lookup"><span data-stu-id="cc85b-110">Option</span></span> | <span data-ttu-id="cc85b-111">Description</span><span class="sxs-lookup"><span data-stu-id="cc85b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc85b-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cc85b-112">ConfigFile</span></span> | <span data-ttu-id="cc85b-113">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="cc85b-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cc85b-114">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="cc85b-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cc85b-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cc85b-115">ForceEnglishOutput</span></span> | <span data-ttu-id="cc85b-116">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="cc85b-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cc85b-117">Help</span><span class="sxs-lookup"><span data-stu-id="cc85b-117">Help</span></span> | <span data-ttu-id="cc85b-118">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="cc85b-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="cc85b-119">Non interactif</span><span class="sxs-lookup"><span data-stu-id="cc85b-119">NonInteractive</span></span> | <span data-ttu-id="cc85b-120">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="cc85b-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cc85b-121">Commentaires</span><span class="sxs-lookup"><span data-stu-id="cc85b-121">Verbosity</span></span> | <span data-ttu-id="cc85b-122">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="cc85b-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cc85b-123">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cc85b-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cc85b-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="cc85b-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
