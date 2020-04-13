---
title: Configuration de flux NuGet locaux
description: Guide pratique pour créer un flux local pour les packages NuGet en utilisant des dossiers sur votre réseau local
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317589"
---
# <a name="local-feeds"></a><span data-ttu-id="ce771-103">Flux locaux</span><span class="sxs-lookup"><span data-stu-id="ce771-103">Local feeds</span></span>

<span data-ttu-id="ce771-104">Les flux de packages NuGet locaux sont simplement des structures de dossiers hiérarchiques sur votre réseau local (ou simplement sur votre propre ordinateur) dans lesquelles vous placez des packages.</span><span class="sxs-lookup"><span data-stu-id="ce771-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="ce771-105">Vous pouvez ensuite les utiliser comme sources de packages avec toutes les autres opérations NuGet dans l’interface CLI, l’interface utilisateur du Gestionnaire de package et la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="ce771-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="ce771-106">Pour activer la source, ajoutez son chemin (tel que `\\myserver\packages`) à la liste des sources à l’aide de [l’interface utilisateur du Gestionnaire de package](../consume-packages/install-use-packages-visual-studio.md#package-sources) ou de la commande [`nuget sources`](../reference/cli-reference/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="ce771-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="ce771-107">Les structures de dossiers hiérarchiques sont prises en charge dans NuGet 3.3+.</span><span class="sxs-lookup"><span data-stu-id="ce771-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="ce771-108">Les versions antérieures de NuGet utilisent un seul dossier contenant les packages, dont les performances sont bien inférieures à celles de la structure hiérarchique.</span><span class="sxs-lookup"><span data-stu-id="ce771-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="ce771-109">Initialisation et gestion des dossiers hiérarchiques</span><span class="sxs-lookup"><span data-stu-id="ce771-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="ce771-110">L’arborescence des dossiers hiérarchiques versionnés présente la structure générale suivante :</span><span class="sxs-lookup"><span data-stu-id="ce771-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="ce771-111">NuGet crée cette structure automatiquement [`nuget add`](../reference/cli-reference/cli-ref-add.md) lorsque vous utilisez la commande pour copier un paquet sur le flux :</span><span class="sxs-lookup"><span data-stu-id="ce771-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="ce771-112">La commande `nuget add` fonctionne avec un package à la fois, ce qui peut être gênant quand vous configurez un flux avec plusieurs packages.</span><span class="sxs-lookup"><span data-stu-id="ce771-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="ce771-113">Dans de tels [`nuget init`](../reference/cli-reference/cli-ref-init.md) cas, utilisez la commande pour copier tous les `nuget add` paquets dans un dossier sur le flux comme si vous couriez sur chacun individuellement.</span><span class="sxs-lookup"><span data-stu-id="ce771-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="ce771-114">Par exemple, la commande suivante copie tous les packages à partir de `c:\packages` vers une arborescence hiérarchique sur `\\myserver\packages` :</span><span class="sxs-lookup"><span data-stu-id="ce771-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="ce771-115">Comme dans le cas de la commande `add`, `init` crée un dossier pour chaque identificateur de package, chacun d’eux contenant un dossier avec numéro de version hébergeant le package approprié.</span><span class="sxs-lookup"><span data-stu-id="ce771-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
