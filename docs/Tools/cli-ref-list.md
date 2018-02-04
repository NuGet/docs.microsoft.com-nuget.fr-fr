---
title: Commande de liste NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de liste de nuget.exe"
keywords: "référence de liste de NuGet, la liste packages commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a>commande de la liste (NuGet CLI)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Affiche la liste des packages à partir d’une source donnée. Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config`, sont utilisés. Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).

## <a name="usage"></a>Utilisation

```cli
nuget list [search terms] [options]
```

où les termes de recherche facultatif filtre la liste affichée. Termes de recherche sont appliqués aux noms des packages, les balises et les descriptions de package.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AllVersions | Répertorier toutes les versions d’un package. Par défaut, la dernière version de package s’affiche. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| IncludeDelisted | *(3.2 +)*  Afficher les packages non listées. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Version préliminaire | Inclut les versions préliminaires des packages dans la liste. |
| Source | Spécifie une liste des sources de packages à rechercher. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
