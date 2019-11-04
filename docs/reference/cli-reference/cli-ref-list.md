---
title: Commande de liste de l’interface CLI NuGet
description: Référence pour la commande de liste NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327736"
---
# <a name="list-command-nuget-cli"></a>List, commande (interface CLI NuGet)

**S’applique à: consommation de** packages &bullet; , publication des **versions prises en charge:** toutes

Affiche la liste des packages d’une source donnée. Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de `%AppData%\NuGet\NuGet.Config` configuration global, ( `~/.nuget/NuGet/NuGet.Config`Windows) ou, sont utilisées. Si `NuGet.Config` ne spécifie aucune source `list` , utilise le flux par défaut (NuGet.org).

## <a name="usage"></a>Usage

```cli
nuget list [search terms] [options]
```

où les termes de recherche facultatifs filtrent la liste affichée. Les termes de recherche sont appliqués aux noms des packages, des balises et des descriptions de package comme c’est le cas lorsque vous les utilisez sur nuget.org.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AllVersions | Répertorie toutes les versions d’un package. Par défaut, seule la dernière version du package est affichée. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| IncludeDelisted | *(3.2 +)* Affichez les packages qui ne sont pas répertoriés. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| PreRelease | Contient des packages de version préliminaire dans la liste. |
| Source | Spécifie une liste de sources de packages à rechercher. |
| Verbosity | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
