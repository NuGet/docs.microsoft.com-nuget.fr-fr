---
title: Commande de NuGet CLI init | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Référence de la commande init nuget.exe"
keywords: "référence d’init NuGet, commande init"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>commande d’init (NuGet CLI)

**S’applique à :** la création de package &bullet; **versions prises en charge :** 3.3 +

Copie tous les packages à partir d’un dossier dans un dossier de destination à l’aide de façon hiérarchique comme indiqué pour le [ajouter commande](#add) ci-dessus. Autrement dit, à l’aide de `init` est équivalente à l’aide du `add` commande sur chaque package dans le dossier.

Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC ; Les référentiels de package HTTP telles que nuget.org ou serveurs privés ne sont pas pris en charge.

## <a name="usage"></a>Utilisation

```
nuget init <source> <destination> [options]
```

où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou un chemin d’accès UNC dans lequel les packages seront copiés.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Expand | Ajoute tous les fichiers dans chaque package est ajouté à la source du package ; identique à `-Expand` avec la `add` commande. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
