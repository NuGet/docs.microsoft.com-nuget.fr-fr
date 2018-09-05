---
title: Commande de NuGet CLI init
description: Référence de la commande init de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551408"
---
# <a name="init-command-nuget-cli"></a>Init, commande (CLI NuGet)

**S’applique à :** la création de package &bullet; **versions prises en charge :** 3.3 +

Copie tous les packages à partir d’un dossier dans un dossier de destination à l’aide d’une disposition hiérarchique comme indiqué pour le [ajouter commande](cli-ref-add.md). Autrement dit, à l’aide de `init` équivaut à utiliser le `add` commande sur chaque package dans le dossier.

Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC ; Référentiels de package HTTP comme nuget.org ou serveurs privés ne sont pas pris en charge.

## <a name="usage"></a>Utilisation

```cli
nuget init <source> <destination> [options]
```

où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou un chemin d’accès UNC dans lequel les packages sont copiés.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Expand | Ajoute tous les fichiers dans chaque package est ajouté à la source du package ; identique à `-Expand` avec la `add` commande. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
