---
title: Commande de help NuGet CLI
description: Informations de référence pour la commande de help nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a>aide ou ? commande (NuGet CLI)

**S’applique à :** tous les &bullet; **versions prises en charge**: tous les

Général des informations et des informations sur les commandes spécifiques.

## <a name="usage"></a>Utilisation

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

où [commande] identifie une commande spécifique pour laquelle afficher l’aide.

> [!Warning]
> Des commandes, tenez compte à spécifier *aide* tout d’abord, comme avec `nuget help install`, étant donné qu’un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, vous ne sera pas obtenir de l’aide sur la commande d’installation mais va installer le package nommé aide.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Tous | Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est donnée. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande aide lui-même. |
| Markdown | Imprimer une aide détaillée dans le format markdown lorsqu’il est utilisé avec `-All`. Ignoré dans le cas contraire. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
