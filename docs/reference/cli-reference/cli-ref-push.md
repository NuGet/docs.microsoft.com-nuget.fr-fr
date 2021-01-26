---
title: Commande Push de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Push
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779191"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="c65e0-103">Push, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="c65e0-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="c65e0-104">**S’applique à : publication de** packages &bullet; **versions prises en charge :** All ; 4.1.0 + required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c65e0-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="c65e0-105">Pour transmettre des packages à nuget.org, vous devez utiliser nuget.exe v 4.1.0 +, qui implémente les [protocoles NuGet](../../api/nuget-protocols.md)requis.</span><span class="sxs-lookup"><span data-stu-id="c65e0-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="c65e0-106">Exécute un push d’un package vers une source de package et le publie.</span><span class="sxs-lookup"><span data-stu-id="c65e0-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="c65e0-107">La configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), puis en chargeant tous les `Nuget.Config` `.nuget\Nuget.Config` fichiers ou à partir de la racine du lecteur jusqu’au répertoire actif (voir [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="c65e0-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="c65e0-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="c65e0-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="c65e0-109">où `<packagePath>` identifie le package à envoyer au serveur.</span><span class="sxs-lookup"><span data-stu-id="c65e0-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="c65e0-110">Options</span><span class="sxs-lookup"><span data-stu-id="c65e0-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="c65e0-111">Clé API pour le référentiel cible.</span><span class="sxs-lookup"><span data-stu-id="c65e0-111">The API key for the target repository.</span></span> <span data-ttu-id="c65e0-112">S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c65e0-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c65e0-113">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="c65e0-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c65e0-114">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c65e0-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="c65e0-115">Désactive la mise en mémoire tampon lors d’un push vers un serveur HTTP (s) pour réduire l’utilisation de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="c65e0-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="c65e0-116">ATTENTION : quand cette option est utilisée, l’authentification Windows intégrée peut ne pas fonctionner.</span><span class="sxs-lookup"><span data-stu-id="c65e0-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c65e0-117">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="c65e0-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c65e0-118">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="c65e0-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c65e0-119">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c65e0-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="c65e0-120">N’ajoute pas `api/v2/packages` à l’URL source.</span><span class="sxs-lookup"><span data-stu-id="c65e0-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="c65e0-121">*(3.5 +)* Si un package de symboles existe, il ne fera pas l’objet d’un push vers un serveur de symboles.</span><span class="sxs-lookup"><span data-stu-id="c65e0-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="c65e0-122">Spécifie l’URL du serveur.</span><span class="sxs-lookup"><span data-stu-id="c65e0-122">Specifies the server URL.</span></span> <span data-ttu-id="c65e0-123">NuGet identifie une source de dossier local ou UNC et copie simplement le fichier ici au lieu de l’envoyer à l’aide du protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="c65e0-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="c65e0-124">En outre, à compter de NuGet 3.4.2, il s’agit d’un paramètre obligatoire, sauf si le `NuGet.Config` fichier spécifie une valeur *DefaultPushSource* (voir [configuration du comportement de NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="c65e0-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="c65e0-125">*(5.1 +)* Si un package et une version existent déjà, ignorez-le et poursuivez avec le package suivant dans l’envoi (push), le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="c65e0-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="c65e0-126">*(3.5 +)* Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors du push vers nuget.org</span><span class="sxs-lookup"><span data-stu-id="c65e0-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="c65e0-127">*(3.5 +)* Spécifie la clé API pour l’URL spécifiée dans `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="c65e0-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="c65e0-128">Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur.</span><span class="sxs-lookup"><span data-stu-id="c65e0-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c65e0-129">La valeur par défaut est de 300 secondes (5 minutes).</span><span class="sxs-lookup"><span data-stu-id="c65e0-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c65e0-130">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c65e0-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="c65e0-131">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c65e0-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c65e0-132">Exemples</span><span class="sxs-lookup"><span data-stu-id="c65e0-132">Examples</span></span>

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
