---
title: Commande de liste NuGet CLI
description: Référence de la commande de liste de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818436"
---
# <a name="list-command-nuget-cli"></a>commande de la liste (NuGet CLI)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Affiche la liste des packages à partir d’une source donnée. Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, sont utilisés. Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).

## <a name="usage"></a>Utilisation

```cli
nuget list [search terms] [options]
```

où les termes de recherche facultatif filtre la liste affichée. Termes de recherche sont appliqués aux noms des packages, les balises et les descriptions de package, comme lors de leur utilisation sur nuget.org.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AllVersions | Répertorier toutes les versions d’un package. Par défaut, la dernière version de package s’affiche. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| IncludeDelisted | *(3.2 +)*  Afficher les packages non listées. |
| NonInteractive | Supprime les invites de saisie utilisateur ou les confirmations. |
| Version préliminaire | Inclut les versions préliminaires des packages dans la liste. |
| Source | Spécifie une liste des sources de packages à rechercher. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
