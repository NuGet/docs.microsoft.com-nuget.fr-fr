---
title: Configuration de flux NuGet locaux
description: Guide pratique pour créer un flux local pour les packages NuGet en utilisant des dossiers sur votre réseau local
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 4710a6fd13bdd89492e2a7246d1e15f6c01a5368
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="local-feeds"></a><span data-ttu-id="f5272-103">Flux locaux</span><span class="sxs-lookup"><span data-stu-id="f5272-103">Local feeds</span></span>

<span data-ttu-id="f5272-104">Les flux de packages NuGet locaux sont simplement des structures de dossiers hiérarchiques sur votre réseau local (ou simplement sur votre propre ordinateur) dans lesquelles vous placez des packages.</span><span class="sxs-lookup"><span data-stu-id="f5272-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="f5272-105">Vous pouvez ensuite les utiliser comme sources de packages avec toutes les autres opérations NuGet dans l’interface CLI, l’interface utilisateur du Gestionnaire de package et la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="f5272-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="f5272-106">Pour activer la source, ajoutez son chemin (tel que `\\myserver\packages`) à la liste des sources à l’aide de [l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md#package-sources) ou de la commande [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="f5272-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="f5272-107">Les structures de dossiers hiérarchiques sont prises en charge dans NuGet 3.3+.</span><span class="sxs-lookup"><span data-stu-id="f5272-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="f5272-108">Les versions antérieures de NuGet utilisent un seul dossier contenant les packages, dont les performances sont bien inférieures à celles de la structure hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="f5272-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="f5272-109">Initialisation et gestion des dossiers hiérarchiques</span><span class="sxs-lookup"><span data-stu-id="f5272-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="f5272-110">L’arborescence des dossiers hiérarchiques versionnés présente la structure générale suivante :</span><span class="sxs-lookup"><span data-stu-id="f5272-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="f5272-111">NuGet crée cette structure automatiquement quand vous utilisez la commande [`nuget add`](../tools/cli-ref-add.md) pour copier un package dans le flux :</span><span class="sxs-lookup"><span data-stu-id="f5272-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="f5272-112">La commande `nuget add` fonctionne avec un package à la fois, ce qui peut être gênant quand vous configurez un flux avec plusieurs packages.</span><span class="sxs-lookup"><span data-stu-id="f5272-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="f5272-113">Dans ce cas, utilisez la commande [`nuget init`](../tools/cli-ref-init.md) pour copier tous les packages d’un dossier dans le flux comme si vous exécutiez `nuget add` sur chacun d’eux tour à tour.</span><span class="sxs-lookup"><span data-stu-id="f5272-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="f5272-114">Par exemple, la commande suivante copie tous les packages à partir de `c:\packages` vers une arborescence hiérarchique sur `\\myserver\packages` :</span><span class="sxs-lookup"><span data-stu-id="f5272-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="f5272-115">Comme dans le cas de la commande `add`, `init` crée un dossier pour chaque identificateur de package, chacun d’eux contenant un dossier avec numéro de version hébergeant le package approprié.</span><span class="sxs-lookup"><span data-stu-id="f5272-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
