---
title: Commande de liste de l’interface CLI NuGet
description: Référence pour la commande nuget.exe List
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780057"
---
# <a name="list-command-nuget-cli"></a>List, commande (interface CLI NuGet)

**S’applique à : consommation de** packages, publication &bullet; des **versions prises en charge :** toutes

Affiche la liste des packages d’une source donnée. Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` , sont utilisées. Si `NuGet.Config` ne spécifie aucune source, `list` utilise le flux par défaut (NuGet.org).

## <a name="usage"></a>Utilisation

```cli
nuget list [search terms] [options]
```

où les termes de recherche facultatifs filtrent la liste affichée. Les [termes de recherche](../../consume-packages/finding-and-choosing-packages.md#search-syntax) sont appliqués aux noms des packages, des balises et des descriptions de package comme c’est le cas lorsque vous les utilisez sur NuGet.org. 

## <a name="options"></a>Options

- **`-AllVersions`**

  Répertorie toutes les versions d’un package. Par défaut, seule la dernière version du package est affichée.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-IncludeDelisted`**

  *(3.2 +)* Affichez les packages qui ne sont pas répertoriés.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-PreRelease`**

  Contient des packages de version préliminaire dans la liste.

- **`-Source`**

  Source du package à rechercher. Vous pouvez spécifier plusieurs sources à l’aide de l' `-Source` option plusieurs fois.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

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
