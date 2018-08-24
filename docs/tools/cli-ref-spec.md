---
title: Commande spec CLI NuGet
description: Référence pour la commande spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794149"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="44e0b-103">spécification de commande (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="44e0b-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="44e0b-104">**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="44e0b-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="44e0b-105">Génère un `.nuspec` fichier d’un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="44e0b-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="44e0b-106">Si vous exécutez dans le même dossier que le fichier projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="44e0b-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="44e0b-107">Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="44e0b-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="44e0b-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="44e0b-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="44e0b-109">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="44e0b-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="44e0b-110">Options</span><span class="sxs-lookup"><span data-stu-id="44e0b-110">Options</span></span>

| <span data-ttu-id="44e0b-111">Option</span><span class="sxs-lookup"><span data-stu-id="44e0b-111">Option</span></span> | <span data-ttu-id="44e0b-112">Description</span><span class="sxs-lookup"><span data-stu-id="44e0b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44e0b-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="44e0b-113">AssemblyPath</span></span> | <span data-ttu-id="44e0b-114">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="44e0b-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="44e0b-115">Force</span><span class="sxs-lookup"><span data-stu-id="44e0b-115">Force</span></span> | <span data-ttu-id="44e0b-116">Remplace tout existant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="44e0b-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="44e0b-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="44e0b-117">ForceEnglishOutput</span></span> | <span data-ttu-id="44e0b-118">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="44e0b-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="44e0b-119">Help</span><span class="sxs-lookup"><span data-stu-id="44e0b-119">Help</span></span> | <span data-ttu-id="44e0b-120">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="44e0b-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="44e0b-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="44e0b-121">NonInteractive</span></span> | <span data-ttu-id="44e0b-122">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="44e0b-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="44e0b-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="44e0b-123">Verbosity</span></span> | <span data-ttu-id="44e0b-124">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="44e0b-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="44e0b-125">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="44e0b-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44e0b-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="44e0b-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
