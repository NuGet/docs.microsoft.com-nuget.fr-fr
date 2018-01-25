---
title: Commande NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de push de nuget.exe"
keywords: "référence de push de NuGet, commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 50883bc85ab96cba54fb4ce0bd344e8148c4fab1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="6db5b-104">commande (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6db5b-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="6db5b-105">**S’applique à :** la publication du package &bullet; **versions prises en charge :** tous ; 4.1.0+ requis pour nuget.org</span><span class="sxs-lookup"><span data-stu-id="6db5b-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="6db5b-106">Pour envoyer les packages à nuget.org, vous devez utiliser nuget.exe v4.1.0 +, qui implémente le requis [NuGet protocoles](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="6db5b-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="6db5b-107">Exécute un push d’un package à une source de package et le publie.</span><span class="sxs-lookup"><span data-stu-id="6db5b-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="6db5b-108">Configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config`, puis charger les `Nuget.Config` ou `.nuget\Nuget.Config` fichiers commençant à la racine du lecteur et de fin dans le répertoire actif (consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="6db5b-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="6db5b-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="6db5b-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="6db5b-110">où `<packagePath>` identifie le package à distribuer vers le serveur.</span><span class="sxs-lookup"><span data-stu-id="6db5b-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="6db5b-111">Options</span><span class="sxs-lookup"><span data-stu-id="6db5b-111">Options</span></span>

| <span data-ttu-id="6db5b-112">Option</span><span class="sxs-lookup"><span data-stu-id="6db5b-112">Option</span></span> | <span data-ttu-id="6db5b-113">Description</span><span class="sxs-lookup"><span data-stu-id="6db5b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6db5b-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="6db5b-114">ApiKey</span></span> | <span data-ttu-id="6db5b-115">La clé d’API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="6db5b-115">The API key for the target repository.</span></span> <span data-ttu-id="6db5b-116">Si absent, celui spécifié dans *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="6db5b-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="6db5b-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6db5b-117">ConfigFile</span></span> | <span data-ttu-id="6db5b-118">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="6db5b-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6db5b-119">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="6db5b-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="6db5b-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="6db5b-120">DisableBuffering</span></span> | <span data-ttu-id="6db5b-121">Désactive la mise en mémoire tampon lors de la distribution à un serveur HTTP (s) pour réduire les utilisations de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="6db5b-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="6db5b-122">Attention : lorsque cette option est utilisée, l’authentification intégrée de Windows ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="6db5b-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="6db5b-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6db5b-123">ForceEnglishOutput</span></span> | <span data-ttu-id="6db5b-124">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="6db5b-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6db5b-125">Help</span><span class="sxs-lookup"><span data-stu-id="6db5b-125">Help</span></span> | <span data-ttu-id="6db5b-126">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="6db5b-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="6db5b-127">Non interactif</span><span class="sxs-lookup"><span data-stu-id="6db5b-127">NonInteractive</span></span> | <span data-ttu-id="6db5b-128">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="6db5b-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6db5b-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="6db5b-129">NoSymbols</span></span> | <span data-ttu-id="6db5b-130">*(3.5 +)*  Si un package de symboles existe, il n’est pas adressée à un serveur de symboles.</span><span class="sxs-lookup"><span data-stu-id="6db5b-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="6db5b-131">Source</span><span class="sxs-lookup"><span data-stu-id="6db5b-131">Source</span></span> | <span data-ttu-id="6db5b-132">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="6db5b-132">Specifies the server URL.</span></span> <span data-ttu-id="6db5b-133">NuGet identifie un chemin UNC ou une source de dossier local et simplement copie le fichier au lieu d’envoyer à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="6db5b-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="6db5b-134">Également, à partir de NuGet 3.4.2, ce paramètre est obligatoire, sauf si le `NuGet.Config` fichier Spécifie un *DefaultPushSource* valeur (consultez [NuGet de configuration de comportement](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="6db5b-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="6db5b-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="6db5b-135">SymbolSource</span></span> | <span data-ttu-id="6db5b-136">*(3.5 +)*  Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors de la diffusion à nuget.org</span><span class="sxs-lookup"><span data-stu-id="6db5b-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="6db5b-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="6db5b-137">SymbolApiKey</span></span> | <span data-ttu-id="6db5b-138">*(3.5 +)*  Spécifie la clé d’API pour l’URL spécifiée dans `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="6db5b-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="6db5b-139">Délai d'expiration</span><span class="sxs-lookup"><span data-stu-id="6db5b-139">Timeout</span></span> | <span data-ttu-id="6db5b-140">Spécifie le délai d’attente, en secondes, en exécutant un push sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="6db5b-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="6db5b-141">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="6db5b-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="6db5b-142">Commentaires</span><span class="sxs-lookup"><span data-stu-id="6db5b-142">Verbosity</span></span> | <span data-ttu-id="6db5b-143">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="6db5b-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6db5b-144">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6db5b-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6db5b-145">Exemples</span><span class="sxs-lookup"><span data-stu-id="6db5b-145">Examples</span></span>

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
