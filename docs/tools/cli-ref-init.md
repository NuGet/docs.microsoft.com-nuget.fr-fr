---
title: Commande de NuGet CLI init
description: Référence de la commande init de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551408"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="1beaa-103">Init, commande (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="1beaa-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="1beaa-104">**S’applique à :** la création de package &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="1beaa-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="1beaa-105">Copie tous les packages à partir d’un dossier dans un dossier de destination à l’aide d’une disposition hiérarchique comme indiqué pour le [ajouter commande](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="1beaa-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="1beaa-106">Autrement dit, à l’aide de `init` équivaut à utiliser le `add` commande sur chaque package dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="1beaa-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="1beaa-107">Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC ; Référentiels de package HTTP comme nuget.org ou serveurs privés ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1beaa-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="1beaa-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="1beaa-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="1beaa-109">où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou un chemin d’accès UNC dans lequel les packages sont copiés.</span><span class="sxs-lookup"><span data-stu-id="1beaa-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="1beaa-110">Options</span><span class="sxs-lookup"><span data-stu-id="1beaa-110">Options</span></span>

| <span data-ttu-id="1beaa-111">Option</span><span class="sxs-lookup"><span data-stu-id="1beaa-111">Option</span></span> | <span data-ttu-id="1beaa-112">Description</span><span class="sxs-lookup"><span data-stu-id="1beaa-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1beaa-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1beaa-113">ConfigFile</span></span> | <span data-ttu-id="1beaa-114">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="1beaa-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1beaa-115">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1beaa-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1beaa-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1beaa-116">ForceEnglishOutput</span></span> | <span data-ttu-id="1beaa-117">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="1beaa-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1beaa-118">Expand</span><span class="sxs-lookup"><span data-stu-id="1beaa-118">Expand</span></span> | <span data-ttu-id="1beaa-119">Ajoute tous les fichiers dans chaque package est ajouté à la source du package ; identique à `-Expand` avec la `add` commande.</span><span class="sxs-lookup"><span data-stu-id="1beaa-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="1beaa-120">Help</span><span class="sxs-lookup"><span data-stu-id="1beaa-120">Help</span></span> | <span data-ttu-id="1beaa-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="1beaa-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="1beaa-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1beaa-122">NonInteractive</span></span> | <span data-ttu-id="1beaa-123">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="1beaa-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1beaa-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1beaa-124">Verbosity</span></span> | <span data-ttu-id="1beaa-125">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="1beaa-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1beaa-126">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1beaa-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1beaa-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="1beaa-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
