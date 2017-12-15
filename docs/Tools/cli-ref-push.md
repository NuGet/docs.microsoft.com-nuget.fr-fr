---
title: Commande NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Référence de la commande de push de nuget.exe"
keywords: "référence de push de NuGet, commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>commande (NuGet CLI)

**S’applique à :** la publication du package &bullet; **versions prises en charge :** tous ; 4.1.0+ requis pour nuget.org

> [!Important]
> Pour envoyer les packages à nuget.org, vous devez utiliser nuget.exe v4.1.0 +, qui implémente le requis [NuGet protocoles](../api/nuget-protocols.md).

Exécute un push d’un package à une source de package et le publie.

Configuration par défaut de NuGet est obtenue en chargeant `%AppData%\NuGet\NuGet.Config`, puis charger les `Nuget.Config` ou `.nuget\Nuget.Config` fichiers commençant à la racine du lecteur et de fin dans le répertoire actif (consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Utilisation

```
nuget push <packagePath> [options]
```

où `<packagePath>` identifie le package à distribuer vers le serveur.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| apiKey | La clé d’API pour le référentiel cible. Si absent, celui spécifié dans *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ConfigFile | *(2.5 +)*  NuGet le fichier de configuration à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| DisableBuffering | Désactive la mise en mémoire tampon lors de la distribution à un serveur HTTP (s) pour réduire les utilisations de la mémoire. Attention : lorsque cette option est utilisée, l’authentification intégrée de Windows ne fonctionnent pas. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| NoSymbols | *(3.5 +)*  Si un package de symboles existe, il n’est pas adressée à un serveur de symboles. |
| Source | Spécifie l’URL du serveur. Avec NuGet 2.5 +, NuGet identifie un chemin UNC ou une source de dossier local et il suffit de copier le fichier au lieu d’envoyer à l’aide de HTTP.  Également, à partir de NuGet 3.4.2, ce paramètre est obligatoire, sauf si le `NuGet.Config` fichier Spécifie un *DefaultPushSource* valeur (consultez [NuGet de configuration de comportement](../Consume-Packages/Configuring-NuGet-Behavior.md)). |
| SymbolSource | *(3.5 +)*  Spécifie l’URL du serveur de symboles ; nuget.smbsrc.net est utilisé lors de la diffusion à nuget.org |
| SymbolApiKey | *(3.5 +)*  Spécifie la clé d’API pour l’URL spécifiée dans `-SymbolSource`. |
| Délai d'expiration | Spécifie le délai d’attente, en secondes, en exécutant un push sur un serveur. La valeur par défaut est 300 secondes (5 minutes). |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
