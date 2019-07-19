---
title: Commande Push de l’interface CLI NuGet
description: Référence pour la commande Push de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327626"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="01f31-103">Push, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="01f31-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="01f31-104">**S’applique à:** publication &bullet; de packages **versions prises en charge:** All; 4.1.0 + required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="01f31-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="01f31-105">Pour transmettre des packages à nuget.org, vous devez utiliser NuGet. exe v 4.1.0 +, qui implémente les [protocoles NuGet](../../api/nuget-protocols.md)requis.</span><span class="sxs-lookup"><span data-stu-id="01f31-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="01f31-106">Exécute un push d’un package vers une source de package et le publie.</span><span class="sxs-lookup"><span data-stu-id="01f31-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="01f31-107">La configuration par défaut de NuGet est obtenue `%AppData%\NuGet\NuGet.Config` en chargeant (Windows `~/.nuget/NuGet/NuGet.Config` ) ou (Mac/Linux), puis `Nuget.Config` en `.nuget\Nuget.Config` chargeant tous les fichiers ou à partir de la racine du lecteur jusqu’au répertoire actif (consultez [NuGet courant configurations](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="01f31-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="01f31-108">Usage</span><span class="sxs-lookup"><span data-stu-id="01f31-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="01f31-109">où `<packagePath>` identifie le package à envoyer au serveur.</span><span class="sxs-lookup"><span data-stu-id="01f31-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="01f31-110">Options</span><span class="sxs-lookup"><span data-stu-id="01f31-110">Options</span></span>

| <span data-ttu-id="01f31-111">Option</span><span class="sxs-lookup"><span data-stu-id="01f31-111">Option</span></span> | <span data-ttu-id="01f31-112">Description</span><span class="sxs-lookup"><span data-stu-id="01f31-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="01f31-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="01f31-113">ApiKey</span></span> | <span data-ttu-id="01f31-114">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="01f31-114">The API key for the target repository.</span></span> <span data-ttu-id="01f31-115">S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="01f31-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="01f31-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="01f31-116">ConfigFile</span></span> | <span data-ttu-id="01f31-117">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="01f31-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="01f31-118">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="01f31-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="01f31-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="01f31-119">DisableBuffering</span></span> | <span data-ttu-id="01f31-120">Désactive la mise en mémoire tampon lors d’un push vers un serveur HTTP (s) pour réduire l’utilisation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="01f31-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="01f31-121">ATTENTION: quand cette option est utilisée, l’authentification Windows intégrée peut ne pas fonctionner.</span><span class="sxs-lookup"><span data-stu-id="01f31-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="01f31-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="01f31-122">ForceEnglishOutput</span></span> | <span data-ttu-id="01f31-123">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="01f31-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="01f31-124">Help</span><span class="sxs-lookup"><span data-stu-id="01f31-124">Help</span></span> | <span data-ttu-id="01f31-125">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="01f31-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="01f31-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="01f31-126">NonInteractive</span></span> | <span data-ttu-id="01f31-127">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01f31-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="01f31-128">Nosymbols</span><span class="sxs-lookup"><span data-stu-id="01f31-128">NoSymbols</span></span> | <span data-ttu-id="01f31-129">*(3.5 +)* Si un package de symboles existe, il ne fera pas l’objet d’un push vers un serveur de symboles.</span><span class="sxs-lookup"><span data-stu-id="01f31-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="01f31-130">source</span><span class="sxs-lookup"><span data-stu-id="01f31-130">Source</span></span> | <span data-ttu-id="01f31-131">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="01f31-131">Specifies the server URL.</span></span> <span data-ttu-id="01f31-132">NuGet identifie une source de dossier local ou UNC et copie simplement le fichier ici au lieu de l’envoyer à l’aide du protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="01f31-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="01f31-133">En outre, à compter de NuGet 3.4.2, il s’agit d’un `NuGet.Config` paramètre obligatoire, sauf si le fichier spécifie une valeur *DefaultPushSource* (voir [configuration du comportement de NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="01f31-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="01f31-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="01f31-134">SkipDuplicate</span></span> | <span data-ttu-id="01f31-135">*(5.1 +)* Si un package et une version existent déjà, ignorez-le et poursuivez avec le package suivant dans l’envoi (push), le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="01f31-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="01f31-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="01f31-136">SymbolSource</span></span> | <span data-ttu-id="01f31-137">*(3.5 +)* Spécifie l’URL du serveur de symboles; nuget.smbsrc.net est utilisé lors du push vers nuget.org</span><span class="sxs-lookup"><span data-stu-id="01f31-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="01f31-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="01f31-138">SymbolApiKey</span></span> | <span data-ttu-id="01f31-139">*(3.5 +)* Spécifie la clé API pour l’URL spécifiée `-SymbolSource`dans.</span><span class="sxs-lookup"><span data-stu-id="01f31-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="01f31-140">Délai</span><span class="sxs-lookup"><span data-stu-id="01f31-140">Timeout</span></span> | <span data-ttu-id="01f31-141">Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="01f31-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="01f31-142">La valeur par défaut est 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="01f31-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="01f31-143">Commentaires</span><span class="sxs-lookup"><span data-stu-id="01f31-143">Verbosity</span></span> | <span data-ttu-id="01f31-144">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="01f31-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="01f31-145">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="01f31-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="01f31-146">Exemples</span><span class="sxs-lookup"><span data-stu-id="01f31-146">Examples</span></span>

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
