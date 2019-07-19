---
title: Commande init de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327776"
---
# <a name="init-command-nuget-cli"></a>Init, commande (interface CLI NuGet)

**S’applique à:** &bullet; **versions prises en charge** pour la création de package: 3.3+

Copie tous les packages d’un dossier plat dans un dossier de destination à l’aide d’une disposition hiérarchique comme décrit pour la [commande Ajouter](cli-ref-add.md). Autrement dit, l' `init` utilisation de équivaut à utiliser `add` la commande sur chaque package dans le dossier.

Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC; Les référentiels de packages HTTP comme nuget.org ou les serveurs privés ne sont pas pris en charge.

## <a name="usage"></a>Usage

```cli
nuget init <source> <destination> [options]
```

où `<source>` est le dossier contenant les packages `<destination>` et est le dossier local ou le chemin d’accès UNC dans lequel les packages sont copiés.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Expand | Ajoute tous les fichiers de chaque package qui est ajouté à la source du package; identique à la `add`commande. `-Expand` |
| Aide | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
