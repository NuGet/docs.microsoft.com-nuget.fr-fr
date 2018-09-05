---
title: Afficher la commande CLI NuGet
description: Référence de la commande de liste de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549799"
---
# <a name="list-command-nuget-cli"></a>afficher la commande (CLI NuGet)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Affiche une liste des packages à partir d’une source donnée. Si aucune source n’est spécifié, toutes les sources définies dans le fichier de configuration globale, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, sont utilisés. Si `NuGet.Config` ne spécifie aucune source, puis `list` utilise le flux par défaut (nuget.org).

## <a name="usage"></a>Utilisation

```cli
nuget list [search terms] [options]
```

où les termes de recherche facultatif filtre la liste affichée. Termes de recherche sont appliquées aux noms des packages, les balises et descriptions des packages comme ils le sont lors de leur utilisation sur nuget.org.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AllVersions | Répertorier toutes les versions d’un package. Par défaut, seule la dernière version de package s’affiche. |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| IncludeDelisted | *(3.2 +)*  Afficher les packages non répertoriés. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Version préliminaire | Inclut les packages de version préliminaire dans la liste. |
| Source | Spécifie une liste des sources de packages à rechercher. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
