---
title: Commande NuGet CLI
description: Référence de la commande de push de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817189"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="cba98-103">commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cba98-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="cba98-104">**S’applique à :** la publication du package &bullet; **versions prises en charge :** tous ; 4.1.0+ requis pour nuget.org</span><span class="sxs-lookup"><span data-stu-id="cba98-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="cba98-105">Pour envoyer les packages à nuget.org, vous devez utiliser nuget.exe v4.1.0 +, qui implémente le requis [NuGet protocoles](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="cba98-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="cba98-106">Exécute un push d’un package à une source de package et le publie.</span><span class="sxs-lookup"><span data-stu-id="cba98-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="cba98-107">Configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Linux/Mac), puis en le chargeant tout `Nuget.Config` ou `.nuget\Nuget.Config` fichiers commençant à la racine du lecteur et de fin dans le répertoire actif (consultez [configuration Comportement de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="cba98-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="cba98-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="cba98-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="cba98-109">où `<packagePath>` identifie le package à distribuer vers le serveur.</span><span class="sxs-lookup"><span data-stu-id="cba98-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="cba98-110">Options</span><span class="sxs-lookup"><span data-stu-id="cba98-110">Options</span></span>

| <span data-ttu-id="cba98-111">Option</span><span class="sxs-lookup"><span data-stu-id="cba98-111">Option</span></span> | <span data-ttu-id="cba98-112">Description</span><span class="sxs-lookup"><span data-stu-id="cba98-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cba98-113">apiKey</span><span class="sxs-lookup"><span data-stu-id="cba98-113">ApiKey</span></span> | <span data-ttu-id="cba98-114">La clé d’API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="cba98-114">The API key for the target repository.</span></span> <span data-ttu-id="cba98-115">Sinon, l’élément spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="cba98-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="cba98-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cba98-116">ConfigFile</span></span> | <span data-ttu-id="cba98-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="cba98-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cba98-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="cba98-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cba98-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="cba98-119">DisableBuffering</span></span> | <span data-ttu-id="cba98-120">Désactive la mise en mémoire tampon lors de la distribution à un serveur HTTP (s) pour réduire les utilisations de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="cba98-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="cba98-121">Attention : lorsque cette option est utilisée, l’authentification intégrée de Windows ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="cba98-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="cba98-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cba98-122">ForceEnglishOutput</span></span> | <span data-ttu-id="cba98-123">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="cba98-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cba98-124">Help</span><span class="sxs-lookup"><span data-stu-id="cba98-124">Help</span></span> | <span data-ttu-id="cba98-125">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="cba98-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="cba98-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cba98-126">NonInteractive</span></span> | <span data-ttu-id="cba98-127">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="cba98-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cba98-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="cba98-128">NoSymbols</span></span> | <span data-ttu-id="cba98-129">*(3.5 +)*  Si un package de symboles existe, il n’est pas adressée à un serveur de symboles.</span><span class="sxs-lookup"><span data-stu-id="cba98-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="cba98-130">Source</span><span class="sxs-lookup"><span data-stu-id="cba98-130">Source</span></span> | <span data-ttu-id="cba98-131">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="cba98-131">Specifies the server URL.</span></span> <span data-ttu-id="cba98-132">NuGet identifie un chemin UNC ou une source de dossier local et simplement copie le fichier au lieu d’envoyer à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="cba98-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="cba98-133">Également, à partir de NuGet 3.4.2, ce paramètre est obligatoire, sauf si le `NuGet.Config` fichier Spécifie un *DefaultPushSource* valeur (consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="cba98-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="cba98-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="cba98-134">SymbolSource</span></span> | <span data-ttu-id="cba98-135">*(3.5 +)*  Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors de la diffusion à nuget.org</span><span class="sxs-lookup"><span data-stu-id="cba98-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="cba98-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="cba98-136">SymbolApiKey</span></span> | <span data-ttu-id="cba98-137">*(3.5 +)*  Spécifie la clé d’API pour l’URL spécifiée dans `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="cba98-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="cba98-138">Délai d'expiration</span><span class="sxs-lookup"><span data-stu-id="cba98-138">Timeout</span></span> | <span data-ttu-id="cba98-139">Spécifie le délai d’attente, en secondes, en exécutant un push sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="cba98-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="cba98-140">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="cba98-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="cba98-141">Commentaires</span><span class="sxs-lookup"><span data-stu-id="cba98-141">Verbosity</span></span> | <span data-ttu-id="cba98-142">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="cba98-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cba98-143">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cba98-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cba98-144">Exemples</span><span class="sxs-lookup"><span data-stu-id="cba98-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
