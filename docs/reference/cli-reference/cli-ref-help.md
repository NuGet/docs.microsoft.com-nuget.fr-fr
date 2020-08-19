---
title: Commande d’aide de l’interface CLI NuGet
description: Référence pour la commande d’aide nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623108"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Command (interface CLI NuGet)

**S’applique à :** toutes les &bullet; **versions prises en charge**: toutes

Affiche des informations d’aide générales et des informations d’aide sur des commandes spécifiques.

## <a name="usage"></a>Usage

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

où [commande] identifie une commande spécifique pour laquelle afficher l’aide.

> [!Warning]
> Avec certaines commandes, pensez à spécifier *l’aide* en premier, comme avec `nuget help install` , car il existe un package nommé « help » sur NuGet.org. Si vous donnez la commande `nuget install help` , vous n’obtiendrez pas d’aide sur la commande d’installation, mais vous installerez à la place le package nommé Help.

## <a name="options"></a>Options

- **`-All`**

  Imprimer une aide détaillée pour toutes les commandes disponibles ; ignoré si une commande spécifique est spécifiée.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-Markdown`**

  Imprimer une aide détaillée dans le format de démarque lorsqu’il est utilisé avec `-All` . Sinon, ignoré.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
