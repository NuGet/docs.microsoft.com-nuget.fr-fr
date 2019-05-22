---
title: Commande NuGet CLI
description: Référence de la commande push de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975004"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="a914b-103">commande push (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="a914b-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="a914b-104">**S’applique à :** publication du package &bullet; **versions prises en charge :** tous ; 4.1.0 requis pour nuget.org</span><span class="sxs-lookup"><span data-stu-id="a914b-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="a914b-105">Pour envoyer des packages sur nuget.org, vous devez utiliser nuget.exe v4.1.0 +, qui implémente le requis [protocoles NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a914b-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="a914b-106">Exécute un push d’un package à une source de package et le publie.</span><span class="sxs-lookup"><span data-stu-id="a914b-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="a914b-107">Configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), puis en chargeant tout `Nuget.Config` ou `.nuget\Nuget.Config` fichiers à partir de la racine du lecteur et de fin dans le répertoire actif (consultez [configuration Comportement de NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="a914b-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="a914b-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="a914b-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="a914b-109">où `<packagePath>` identifie le package à envoyer au serveur.</span><span class="sxs-lookup"><span data-stu-id="a914b-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="a914b-110">Options</span><span class="sxs-lookup"><span data-stu-id="a914b-110">Options</span></span>

| <span data-ttu-id="a914b-111">Option</span><span class="sxs-lookup"><span data-stu-id="a914b-111">Option</span></span> | <span data-ttu-id="a914b-112">Description</span><span class="sxs-lookup"><span data-stu-id="a914b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a914b-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="a914b-113">ApiKey</span></span> | <span data-ttu-id="a914b-114">La clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="a914b-114">The API key for the target repository.</span></span> <span data-ttu-id="a914b-115">Si elle est absente, celle spécifiée dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a914b-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="a914b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a914b-116">ConfigFile</span></span> | <span data-ttu-id="a914b-117">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="a914b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a914b-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a914b-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a914b-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="a914b-119">DisableBuffering</span></span> | <span data-ttu-id="a914b-120">Désactive la mise en mémoire tampon lors de l’envoi à un serveur HTTP (s) afin de réduire les utilisations de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="a914b-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="a914b-121">Attention : lorsque cette option est utilisée, l’authentification Windows intégrée fonctionnera ne peut-être pas.</span><span class="sxs-lookup"><span data-stu-id="a914b-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="a914b-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a914b-122">ForceEnglishOutput</span></span> | <span data-ttu-id="a914b-123">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="a914b-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a914b-124">Help</span><span class="sxs-lookup"><span data-stu-id="a914b-124">Help</span></span> | <span data-ttu-id="a914b-125">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="a914b-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="a914b-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a914b-126">NonInteractive</span></span> | <span data-ttu-id="a914b-127">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="a914b-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a914b-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="a914b-128">NoSymbols</span></span> | <span data-ttu-id="a914b-129">*(3.5 +)*  Si un package de symboles existe, il n’est pas adressée à un serveur de symboles.</span><span class="sxs-lookup"><span data-stu-id="a914b-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="a914b-130">Source</span><span class="sxs-lookup"><span data-stu-id="a914b-130">Source</span></span> | <span data-ttu-id="a914b-131">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="a914b-131">Specifies the server URL.</span></span> <span data-ttu-id="a914b-132">NuGet identifie un chemin UNC ou une source de dossier local et copie simplement le fichier au lieu d’envoyer à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="a914b-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="a914b-133">En outre, à partir de NuGet 3.4.2, ce paramètre est obligatoire, sauf si le `NuGet.Config` fichier Spécifie un *DefaultPushSource* valeur (consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="a914b-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="a914b-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="a914b-134">SkipDuplicate</span></span> | <span data-ttu-id="a914b-135">Si un package et la version existe déjà, ignorer et continuer avec le package suivant dans la notification push, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="a914b-135">If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="a914b-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="a914b-136">SymbolSource</span></span> | <span data-ttu-id="a914b-137">*(3.5 +)*  Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors de l’envoi sur nuget.org</span><span class="sxs-lookup"><span data-stu-id="a914b-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="a914b-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="a914b-138">SymbolApiKey</span></span> | <span data-ttu-id="a914b-139">*(3.5 +)*  Spécifie la clé API pour l’URL spécifiée dans `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="a914b-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="a914b-140">Délai</span><span class="sxs-lookup"><span data-stu-id="a914b-140">Timeout</span></span> | <span data-ttu-id="a914b-141">Spécifie le délai d’attente, en secondes, pour envoyer vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="a914b-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="a914b-142">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="a914b-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="a914b-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a914b-143">Verbosity</span></span> | <span data-ttu-id="a914b-144">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="a914b-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a914b-145">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a914b-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a914b-146">Exemples</span><span class="sxs-lookup"><span data-stu-id="a914b-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
