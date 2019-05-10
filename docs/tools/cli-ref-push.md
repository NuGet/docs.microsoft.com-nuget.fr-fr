---
title: Commande NuGet CLI
description: Référence de la commande push de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877954"
---
# <a name="push-command-nuget-cli"></a>commande push (CLI NuGet)

**S’applique à :** publication du package &bullet; **versions prises en charge :** tous ; 4.1.0 requis pour nuget.org

> [!Important]
> Pour envoyer des packages sur nuget.org, vous devez utiliser nuget.exe v4.1.0 +, qui implémente le requis [protocoles NuGet](../api/nuget-protocols.md).

Exécute un push d’un package à une source de package et le publie.

Configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), puis en chargeant tout `Nuget.Config` ou `.nuget\Nuget.Config` fichiers à partir de la racine du lecteur et de fin dans le répertoire actif (consultez [configuration Comportement de NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Utilisation

```cli
nuget push <packagePath> [options]
```

où `<packagePath>` identifie le package à envoyer au serveur.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ApiKey | La clé API pour le référentiel cible. Si elle est absente, celle spécifiée dans le fichier de configuration est utilisé. |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| DisableBuffering | Désactive la mise en mémoire tampon lors de l’envoi à un serveur HTTP (s) afin de réduire les utilisations de la mémoire. Attention : lorsque cette option est utilisée, l’authentification Windows intégrée fonctionnera ne peut-être pas. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| NoSymbols | *(3.5 +)*  Si un package de symboles existe, il n’est pas adressée à un serveur de symboles. |
| Source | Spécifie l’URL du serveur. NuGet identifie un chemin UNC ou une source de dossier local et copie simplement le fichier au lieu d’envoyer à l’aide de HTTP.  En outre, à partir de NuGet 3.4.2, ce paramètre est obligatoire, sauf si le `NuGet.Config` fichier Spécifie un *DefaultPushSource* valeur (consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors de l’envoi sur nuget.org |
| SymbolApiKey | *(3.5 +)*  Spécifie la clé API pour l’URL spécifiée dans `-SymbolSource`. |
| Délai | Spécifie le délai d’attente, en secondes, pour envoyer vers un serveur. La valeur par défaut est 300 secondes (5 minutes). |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
