---
title: Commande d’aide de l’interface CLI NuGet
description: Référence pour la commande d’aide nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779355"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Command (interface CLI NuGet)

**S’applique à :** toutes les &bullet; **versions prises en charge**: toutes

Affiche des informations d’aide générales et des informations d’aide sur des commandes spécifiques.

## <a name="usage"></a>Utilisation

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
