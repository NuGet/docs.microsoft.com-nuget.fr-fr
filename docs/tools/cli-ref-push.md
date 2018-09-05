---
title: Commande NuGet CLI
description: Référence de la commande push de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548341"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="3596a-103">commande push (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="3596a-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="3596a-104">**S’applique à :** publication du package &bullet; **versions prises en charge :** tous ; 4.1.0 requis pour nuget.org</span><span class="sxs-lookup"><span data-stu-id="3596a-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="3596a-105">Pour envoyer des packages sur nuget.org, vous devez utiliser nuget.exe v4.1.0 +, qui implémente le requis [protocoles NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3596a-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="3596a-106">Exécute un push d’un package à une source de package et le publie.</span><span class="sxs-lookup"><span data-stu-id="3596a-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="3596a-107">Configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), puis en chargeant tout `Nuget.Config` ou `.nuget\Nuget.Config` fichiers à partir de la racine du lecteur et de fin dans le répertoire actif (consultez [configuration Comportement de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="3596a-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="3596a-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="3596a-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="3596a-109">où `<packagePath>` identifie le package à envoyer au serveur.</span><span class="sxs-lookup"><span data-stu-id="3596a-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="3596a-110">Options</span><span class="sxs-lookup"><span data-stu-id="3596a-110">Options</span></span>

| <span data-ttu-id="3596a-111">Option</span><span class="sxs-lookup"><span data-stu-id="3596a-111">Option</span></span> | <span data-ttu-id="3596a-112">Description</span><span class="sxs-lookup"><span data-stu-id="3596a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3596a-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3596a-113">ApiKey</span></span> | <span data-ttu-id="3596a-114">La clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="3596a-114">The API key for the target repository.</span></span> <span data-ttu-id="3596a-115">Si elle est absente, celle spécifiée dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3596a-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="3596a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3596a-116">ConfigFile</span></span> | <span data-ttu-id="3596a-117">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="3596a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3596a-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3596a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3596a-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="3596a-119">DisableBuffering</span></span> | <span data-ttu-id="3596a-120">Désactive la mise en mémoire tampon lors de l’envoi à un serveur HTTP (s) afin de réduire les utilisations de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="3596a-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="3596a-121">Attention : lorsque cette option est utilisée, l’authentification Windows intégrée fonctionnera ne peut-être pas.</span><span class="sxs-lookup"><span data-stu-id="3596a-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="3596a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3596a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="3596a-123">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="3596a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3596a-124">Help</span><span class="sxs-lookup"><span data-stu-id="3596a-124">Help</span></span> | <span data-ttu-id="3596a-125">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="3596a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="3596a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3596a-126">NonInteractive</span></span> | <span data-ttu-id="3596a-127">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="3596a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3596a-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="3596a-128">NoSymbols</span></span> | <span data-ttu-id="3596a-129">*(3.5 +)*  Si un package de symboles existe, il n’est pas adressée à un serveur de symboles.</span><span class="sxs-lookup"><span data-stu-id="3596a-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="3596a-130">Source</span><span class="sxs-lookup"><span data-stu-id="3596a-130">Source</span></span> | <span data-ttu-id="3596a-131">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="3596a-131">Specifies the server URL.</span></span> <span data-ttu-id="3596a-132">NuGet identifie un chemin UNC ou une source de dossier local et copie simplement le fichier au lieu d’envoyer à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="3596a-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="3596a-133">En outre, à partir de NuGet 3.4.2, ce paramètre est obligatoire, sauf si le `NuGet.Config` fichier Spécifie un *DefaultPushSource* valeur (consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="3596a-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="3596a-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="3596a-134">SymbolSource</span></span> | <span data-ttu-id="3596a-135">*(3.5 +)*  Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors de l’envoi sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="3596a-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="3596a-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="3596a-136">SymbolApiKey</span></span> | <span data-ttu-id="3596a-137">*(3.5 +)*  Spécifie la clé API pour l’URL spécifiée dans `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="3596a-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="3596a-138">Délai d'expiration</span><span class="sxs-lookup"><span data-stu-id="3596a-138">Timeout</span></span> | <span data-ttu-id="3596a-139">Spécifie le délai d’attente, en secondes, pour envoyer vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="3596a-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="3596a-140">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="3596a-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="3596a-141">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3596a-141">Verbosity</span></span> | <span data-ttu-id="3596a-142">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="3596a-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3596a-143">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3596a-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3596a-144">Exemples</span><span class="sxs-lookup"><span data-stu-id="3596a-144">Examples</span></span>

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
