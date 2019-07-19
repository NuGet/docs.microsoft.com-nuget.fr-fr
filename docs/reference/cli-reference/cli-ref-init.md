---
title: Commande init de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327776"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="492d0-103">Init, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="492d0-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="492d0-104">**S’applique à:** &bullet; **versions prises en charge** pour la création de package: 3.3+</span><span class="sxs-lookup"><span data-stu-id="492d0-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="492d0-105">Copie tous les packages d’un dossier plat dans un dossier de destination à l’aide d’une disposition hiérarchique comme décrit pour la [commande Ajouter](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="492d0-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="492d0-106">Autrement dit, l' `init` utilisation de équivaut à utiliser `add` la commande sur chaque package dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="492d0-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="492d0-107">Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC; Les référentiels de packages HTTP comme nuget.org ou les serveurs privés ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="492d0-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="492d0-108">Usage</span><span class="sxs-lookup"><span data-stu-id="492d0-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="492d0-109">où `<source>` est le dossier contenant les packages `<destination>` et est le dossier local ou le chemin d’accès UNC dans lequel les packages sont copiés.</span><span class="sxs-lookup"><span data-stu-id="492d0-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="492d0-110">Options</span><span class="sxs-lookup"><span data-stu-id="492d0-110">Options</span></span>

| <span data-ttu-id="492d0-111">Option</span><span class="sxs-lookup"><span data-stu-id="492d0-111">Option</span></span> | <span data-ttu-id="492d0-112">Description</span><span class="sxs-lookup"><span data-stu-id="492d0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="492d0-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="492d0-113">ConfigFile</span></span> | <span data-ttu-id="492d0-114">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="492d0-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="492d0-115">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="492d0-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="492d0-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="492d0-116">ForceEnglishOutput</span></span> | <span data-ttu-id="492d0-117">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="492d0-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="492d0-118">Expand</span><span class="sxs-lookup"><span data-stu-id="492d0-118">Expand</span></span> | <span data-ttu-id="492d0-119">Ajoute tous les fichiers de chaque package qui est ajouté à la source du package; identique à la `add`commande. `-Expand`</span><span class="sxs-lookup"><span data-stu-id="492d0-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="492d0-120">Aide</span><span class="sxs-lookup"><span data-stu-id="492d0-120">Help</span></span> | <span data-ttu-id="492d0-121">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="492d0-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="492d0-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="492d0-122">NonInteractive</span></span> | <span data-ttu-id="492d0-123">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="492d0-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="492d0-124">Commentaires</span><span class="sxs-lookup"><span data-stu-id="492d0-124">Verbosity</span></span> | <span data-ttu-id="492d0-125">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="492d0-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="492d0-126">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="492d0-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="492d0-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="492d0-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
