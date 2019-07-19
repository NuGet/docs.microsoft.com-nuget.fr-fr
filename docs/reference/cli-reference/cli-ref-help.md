---
title: Commande d’aide de l’interface CLI NuGet
description: Référence pour la commande d’aide de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327796"
---
# <a name="help-or--command-nuget-cli"></a>help or ? (commande, NuGet CLI)

**S’applique à:** toutes les &bullet; **versions prises en charge**: toutes

Affiche des informations d’aide générales et des informations d’aide sur des commandes spécifiques.

## <a name="usage"></a>Usage

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

où [commande] identifie une commande spécifique pour laquelle afficher l’aide.

> [!Warning]
> Avec certaines commandes, pensez à spécifier *l’aide* en premier, comme `nuget help install`avec, car il existe un package nommé «Help» sur NuGet.org. Si vous donnez la commande `nuget install help`, vous n’obtiendrez pas d’aide sur la commande d’installation, mais vous installerez à la place le package nommé Help.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Tous | Imprimer une aide détaillée pour toutes les commandes disponibles; ignoré si une commande spécifique est spécifiée. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Aide | Affiche des informations d’aide pour la commande d’aide elle-même. |
| Markdown | Imprimer une aide détaillée dans le format de démarque lorsqu’il est utilisé avec `-All`. Sinon, ignoré. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
