---
title: Commande de help CLI NuGet
description: Référence de la commande d’aide de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546561"
---
# <a name="help-or--command-nuget-cli"></a>help or ? (commande, NuGet CLI)

**S’applique à :** tous les &bullet; **versions prises en charge**: tous les

Présente général des informations d’aide et les informations d’aide sur les commandes spécifiques.

## <a name="usage"></a>Utilisation

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

où [commande] identifie une commande spécifique pour laquelle afficher l’aide.

> [!Warning]
> Avec certaines commandes, n’oubliez pas de spécifier *aide* tout d’abord, comme avec `nuget help install`, car il existe un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, ne sont pas obtenir de l’aide sur la commande d’installation, mais au lieu de cela installera le package nommé aide.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Tous | Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est indiquée. |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande d’aide. |
| Markdown | Imprimer une aide détaillée au format markdown lorsqu’il est utilisé avec `-All`. Ignoré dans le cas contraire. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
