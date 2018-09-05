---
title: Commande spec CLI NuGet
description: Référence pour la commande spec nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546447"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="12bc0-103">spécification de commande (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="12bc0-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="12bc0-104">**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="12bc0-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="12bc0-105">Génère un `.nuspec` fichier d’un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="12bc0-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="12bc0-106">Si vous exécutez dans le même dossier que le fichier projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="12bc0-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="12bc0-107">Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="12bc0-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="12bc0-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="12bc0-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="12bc0-109">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="12bc0-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="12bc0-110">Options</span><span class="sxs-lookup"><span data-stu-id="12bc0-110">Options</span></span>

| <span data-ttu-id="12bc0-111">Option</span><span class="sxs-lookup"><span data-stu-id="12bc0-111">Option</span></span> | <span data-ttu-id="12bc0-112">Description</span><span class="sxs-lookup"><span data-stu-id="12bc0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12bc0-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="12bc0-113">AssemblyPath</span></span> | <span data-ttu-id="12bc0-114">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="12bc0-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="12bc0-115">Force</span><span class="sxs-lookup"><span data-stu-id="12bc0-115">Force</span></span> | <span data-ttu-id="12bc0-116">Remplace tout existant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="12bc0-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="12bc0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="12bc0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="12bc0-118">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="12bc0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="12bc0-119">Help</span><span class="sxs-lookup"><span data-stu-id="12bc0-119">Help</span></span> | <span data-ttu-id="12bc0-120">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="12bc0-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="12bc0-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="12bc0-121">NonInteractive</span></span> | <span data-ttu-id="12bc0-122">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="12bc0-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="12bc0-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="12bc0-123">Verbosity</span></span> | <span data-ttu-id="12bc0-124">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="12bc0-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="12bc0-125">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="12bc0-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="12bc0-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="12bc0-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
