---
title: Configuration de flux NuGet locaux | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "Guide pratique pour créer un flux local pour les packages NuGet en utilisant des dossiers sur votre réseau local"
keywords: flux NuGet, galerie NuGet, flux de packages local
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a><span data-ttu-id="ec6cf-104">Flux locaux</span><span class="sxs-lookup"><span data-stu-id="ec6cf-104">Local feeds</span></span>

<span data-ttu-id="ec6cf-105">Les flux de packages NuGet locaux sont simplement des structures de dossiers hiérarchiques sur votre réseau local (ou simplement sur votre propre ordinateur) dans lesquelles vous placez des packages.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-105">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="ec6cf-106">Vous pouvez ensuite les utiliser comme sources de packages avec toutes les autres opérations NuGet dans l’interface CLI, l’interface utilisateur du Gestionnaire de package et la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-106">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="ec6cf-107">Pour activer la source, ajoutez son chemin (tel que `\\myserver\packages`) à la liste des sources à l’aide de [l’interface utilisateur du Gestionnaire de package](../tools/package-manager-ui.md#package-sources) ou de la commande [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="ec6cf-107">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="ec6cf-108">Les structures de dossiers hiérarchiques sont prises en charge dans NuGet 3.3+.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-108">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="ec6cf-109">Les versions antérieures de NuGet utilisent un seul dossier contenant les packages, dont les performances sont bien inférieures à celles de la structure hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-109">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="ec6cf-110">Initialisation et gestion des dossiers hiérarchiques</span><span class="sxs-lookup"><span data-stu-id="ec6cf-110">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="ec6cf-111">L’arborescence des dossiers hiérarchiques versionnés présente la structure générale suivante :</span><span class="sxs-lookup"><span data-stu-id="ec6cf-111">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="ec6cf-112">NuGet crée cette structure automatiquement quand vous utilisez la commande [`nuget add`](../tools/cli-ref-add.md) pour copier un package dans le flux :</span><span class="sxs-lookup"><span data-stu-id="ec6cf-112">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="ec6cf-113">La commande `nuget add` fonctionne avec un package à la fois, ce qui peut être gênant quand vous configurez un flux avec plusieurs packages.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-113">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="ec6cf-114">Dans ce cas, utilisez la commande [`nuget init`](../tools/cli-ref-init.md) pour copier tous les packages d’un dossier dans le flux comme si vous exécutiez `nuget add` sur chacun d’eux tour à tour.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-114">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="ec6cf-115">Par exemple, la commande suivante copie tous les packages à partir de `c:\packages` vers une arborescence hiérarchique sur `\\myserver\packages` :</span><span class="sxs-lookup"><span data-stu-id="ec6cf-115">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="ec6cf-116">Comme dans le cas de la commande `add`, `init` crée un dossier pour chaque identificateur de package, chacun d’eux contenant un dossier avec numéro de version hébergeant le package approprié.</span><span class="sxs-lookup"><span data-stu-id="ec6cf-116">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
