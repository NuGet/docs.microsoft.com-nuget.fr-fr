---
title: Commande de NuGet CLI init | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande init nuget.exe"
keywords: "référence d’init NuGet, commande init"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="28c02-104">commande d’init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="28c02-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="28c02-105">**S’applique à :** la création de package &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="28c02-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="28c02-106">Copie tous les packages à partir d’un dossier dans un dossier de destination à l’aide de façon hiérarchique comme indiqué pour le [ajouter la commande](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="28c02-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="28c02-107">Autrement dit, à l’aide de `init` est équivalente à l’aide du `add` commande sur chaque package dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="28c02-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="28c02-108">Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC ; Les référentiels de package HTTP telles que nuget.org ou serveurs privés ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="28c02-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="28c02-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="28c02-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="28c02-110">où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou un chemin d’accès UNC dans lequel les packages sont copiés.</span><span class="sxs-lookup"><span data-stu-id="28c02-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="28c02-111">Options</span><span class="sxs-lookup"><span data-stu-id="28c02-111">Options</span></span>

| <span data-ttu-id="28c02-112">Option</span><span class="sxs-lookup"><span data-stu-id="28c02-112">Option</span></span> | <span data-ttu-id="28c02-113">Description</span><span class="sxs-lookup"><span data-stu-id="28c02-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28c02-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="28c02-114">ConfigFile</span></span> | <span data-ttu-id="28c02-115">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="28c02-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="28c02-116">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="28c02-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="28c02-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="28c02-117">ForceEnglishOutput</span></span> | <span data-ttu-id="28c02-118">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="28c02-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="28c02-119">Expand</span><span class="sxs-lookup"><span data-stu-id="28c02-119">Expand</span></span> | <span data-ttu-id="28c02-120">Ajoute tous les fichiers dans chaque package est ajouté à la source du package ; identique à `-Expand` avec la `add` commande.</span><span class="sxs-lookup"><span data-stu-id="28c02-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="28c02-121">Help</span><span class="sxs-lookup"><span data-stu-id="28c02-121">Help</span></span> | <span data-ttu-id="28c02-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="28c02-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="28c02-123">Non interactif</span><span class="sxs-lookup"><span data-stu-id="28c02-123">NonInteractive</span></span> | <span data-ttu-id="28c02-124">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="28c02-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="28c02-125">Commentaires</span><span class="sxs-lookup"><span data-stu-id="28c02-125">Verbosity</span></span> | <span data-ttu-id="28c02-126">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="28c02-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="28c02-127">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="28c02-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="28c02-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="28c02-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
