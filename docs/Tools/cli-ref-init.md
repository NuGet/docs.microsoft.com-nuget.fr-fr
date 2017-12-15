---
title: Commande de NuGet CLI init | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Référence de la commande init nuget.exe"
keywords: "référence d’init NuGet, commande init"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="d3c93-104">commande d’init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d3c93-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="d3c93-105">**S’applique à :** la création de package &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="d3c93-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d3c93-106">Copie tous les packages à partir d’un dossier dans un dossier de destination à l’aide de façon hiérarchique comme indiqué pour le [ajouter commande](#add) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d3c93-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="d3c93-107">Autrement dit, à l’aide de `init` est équivalente à l’aide du `add` commande sur chaque package dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="d3c93-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="d3c93-108">Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC ; Les référentiels de package HTTP telles que nuget.org ou serveurs privés ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d3c93-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="d3c93-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="d3c93-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="d3c93-110">où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou un chemin d’accès UNC dans lequel les packages seront copiés.</span><span class="sxs-lookup"><span data-stu-id="d3c93-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="d3c93-111">Options</span><span class="sxs-lookup"><span data-stu-id="d3c93-111">Options</span></span>

| <span data-ttu-id="d3c93-112">Option</span><span class="sxs-lookup"><span data-stu-id="d3c93-112">Option</span></span> | <span data-ttu-id="d3c93-113">Description</span><span class="sxs-lookup"><span data-stu-id="d3c93-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3c93-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d3c93-114">ConfigFile</span></span> | <span data-ttu-id="d3c93-115">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="d3c93-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d3c93-116">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d3c93-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d3c93-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d3c93-117">ForceEnglishOutput</span></span> | <span data-ttu-id="d3c93-118">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="d3c93-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d3c93-119">Expand</span><span class="sxs-lookup"><span data-stu-id="d3c93-119">Expand</span></span> | <span data-ttu-id="d3c93-120">Ajoute tous les fichiers dans chaque package est ajouté à la source du package ; identique à `-Expand` avec la `add` commande.</span><span class="sxs-lookup"><span data-stu-id="d3c93-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="d3c93-121">Help</span><span class="sxs-lookup"><span data-stu-id="d3c93-121">Help</span></span> | <span data-ttu-id="d3c93-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="d3c93-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="d3c93-123">Non interactif</span><span class="sxs-lookup"><span data-stu-id="d3c93-123">NonInteractive</span></span> | <span data-ttu-id="d3c93-124">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="d3c93-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d3c93-125">Commentaires</span><span class="sxs-lookup"><span data-stu-id="d3c93-125">Verbosity</span></span> | <span data-ttu-id="d3c93-126">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="d3c93-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="d3c93-127">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d3c93-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d3c93-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="d3c93-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
