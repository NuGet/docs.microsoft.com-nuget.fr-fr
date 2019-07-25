---
title: Configuration de flux NuGet locaux
description: Guide pratique pour créer un flux local pour les packages NuGet en utilisant des dossiers sur votre réseau local
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317589"
---
# <a name="local-feeds"></a>Flux locaux

Les flux de packages NuGet locaux sont simplement des structures de dossiers hiérarchiques sur votre réseau local (ou simplement sur votre propre ordinateur) dans lesquelles vous placez des packages. Vous pouvez ensuite les utiliser comme sources de packages avec toutes les autres opérations NuGet dans l’interface CLI, l’interface utilisateur du Gestionnaire de package et la console du Gestionnaire de package.

Pour activer la source, ajoutez son chemin (tel que `\\myserver\packages`) à la liste des sources à l’aide de [l’interface utilisateur du Gestionnaire de package](../consume-packages/install-use-packages-visual-studio.md#package-sources) ou de la commande [`nuget sources`](../reference/cli-reference/cli-ref-sources.md).

> [!Note]
> Les structures de dossiers hiérarchiques sont prises en charge dans NuGet 3.3+. Les versions antérieures de NuGet utilisent un seul dossier contenant les packages, dont les performances sont bien inférieures à celles de la structure hiérarchique.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Initialisation et gestion des dossiers hiérarchiques

L’arborescence des dossiers hiérarchiques versionnés présente la structure générale suivante :

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet crée cette structure automatiquement quand vous utilisez la commande [`nuget add`](../reference/cli-reference/cli-ref-add.md) pour copier un package dans le flux :

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

La commande `nuget add` fonctionne avec un package à la fois, ce qui peut être gênant quand vous configurez un flux avec plusieurs packages.

Dans ce cas, utilisez la commande [`nuget init`](../reference/cli-reference/cli-ref-init.md) pour copier tous les packages d’un dossier dans le flux comme si vous exécutiez `nuget add` sur chacun d’eux tour à tour. Par exemple, la commande suivante copie tous les packages à partir de `c:\packages` vers une arborescence hiérarchique sur `\\myserver\packages` :

```cli
nuget init c:\packages \\myserver\packages
```

Comme dans le cas de la commande `add`, `init` crée un dossier pour chaque identificateur de package, chacun d’eux contenant un dossier avec numéro de version hébergeant le package approprié.
