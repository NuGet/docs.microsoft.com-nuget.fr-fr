---
title: Commande de liste de l’interface CLI NuGet
description: Référence pour la commande de liste NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813336"
---
# <a name="list-command-nuget-cli"></a>List, commande (interface CLI NuGet)

**S’applique à : consommation de** packages, publication &bullet; **versions prises en charge :** tout

Affiche la liste des packages d’une source donnée. Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, sont utilisées. Si `NuGet.Config` spécifie aucune source, `list` utilise le flux par défaut (nuget.org).

## <a name="usage"></a>Contrôle

```cli
nuget list [search terms] [options]
```

où les termes de recherche facultatifs filtrent la liste affichée. Les termes de recherche sont appliqués aux noms des packages, des balises et des descriptions de package comme c’est le cas lorsque vous les utilisez sur nuget.org.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AllVersions | Répertorie toutes les versions d’un package. Par défaut, seule la dernière version du package est affichée. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Aide | Affiche des informations d’aide pour la commande. |
| IncludeDelisted | *(3.2 +)* Affichez les packages qui ne sont pas répertoriés. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| PreRelease | Contient des packages de version préliminaire dans la liste. |
| Source | Spécifie une liste de sources de packages à rechercher. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

Répertorier tous les packages à partir des flux configurés :
```
nuget list
```
Répertoriez les packages liés à Azure avec un niveau de détail détaillé :
```
nuget list Azure -Verbosity detailed
```
Répertorier toutes les versions des packages associés à Azure à partir de flux configurés :
```
nuget list Azure -AllVersions
```
Répertorie toutes les versions des packages liés à JSON à partir de la source/du flux spécifié :
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Répertorier les packages liés à JSON à partir de plusieurs sources/flux :
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

