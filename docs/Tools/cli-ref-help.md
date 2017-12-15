---
title: Commande de help NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Informations de référence pour la commande de help nuget.exe"
keywords: "référence d’aide de NuGet, la commande aide"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>aide ou ? commande (NuGet CLI)

**S’applique à :** tous les &bullet; **versions prises en charge**: tous les

Général des informations et des informations sur les commandes spécifiques.

## <a name="usage"></a>Utilisation

```
nuget help [command] [options]
nuget ? [command] [options]
```

où [commande] identifie une commande spécifique pour laquelle afficher l’aide.

> [!Warning]
> Des commandes, tenez compte à spécifier *aide* tout d’abord, comme avec `nuget help install`, étant donné qu’un package nommé « help » sur nuget.org. Si vous attribuez à la commande `nuget install help`, vous n'allez pas obtenir de l’aide sur la commande d’installation mais va installer le package nommé aide.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Tout | Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est donnée. |
| ConfigFile | *(2.5 +)*  NuGet le fichier de configuration à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande aide lui-même. |
| Markdown | Imprimer une aide détaillée dans le format markdown lorsqu’il est utilisé avec `-All`. Ignoré dans le cas contraire. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
