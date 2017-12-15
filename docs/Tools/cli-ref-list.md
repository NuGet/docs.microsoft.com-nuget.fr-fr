---
title: Commande de liste NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Référence de la commande de liste de nuget.exe"
keywords: "référence de liste de NuGet, la liste packages commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>commande de la liste (NuGet CLI)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Affiche la liste des packages à partir d’une source donnée. Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config`, sont utilisés. Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).

## <a name="usage"></a>Utilisation

```
nuget list [search terms] [options]
```

où les termes de recherche facultatif filtre la liste affichée. Termes de recherche sont appliqués aux noms des packages, les balises et les descriptions de package.

## <a name="options"></a>Options
| Option | Description |
| --- | --- |
| AllVersions | Répertorier toutes les versions d’un package. Par défaut, la dernière version de package s’affiche. |
| ConfigFile | *(2.5 +)*  NuGet le fichier de configuration à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| IncludeDelisted | *(3.2 +)*  Afficher les packages non listées. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Version préliminaire | Inclut les versions préliminaires des packages dans la liste. |
| Source | Spécifie une liste des sources de packages à rechercher. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
