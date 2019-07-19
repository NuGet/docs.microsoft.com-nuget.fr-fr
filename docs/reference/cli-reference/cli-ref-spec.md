---
title: Commande spec de l’interface CLI NuGet
description: Référence pour la commande de spécification NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327566"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="276ee-103">Spec, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="276ee-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="276ee-104">**S’applique à:** &bullet; **versions prises en charge** pour la création de package: All</span><span class="sxs-lookup"><span data-stu-id="276ee-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="276ee-105">Génère un `.nuspec` fichier pour un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="276ee-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="276ee-106">Si l’exécution s’exécute dans le même dossier qu’un`.csproj`fichier `.vbproj`projet `.fsproj`(, `spec` ,), crée `.nuspec` un fichier sous forme de jeton.</span><span class="sxs-lookup"><span data-stu-id="276ee-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="276ee-107">Pour plus d’informations, consultez [création d’un package](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="276ee-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="276ee-108">Usage</span><span class="sxs-lookup"><span data-stu-id="276ee-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="276ee-109">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="276ee-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="276ee-110">Options</span><span class="sxs-lookup"><span data-stu-id="276ee-110">Options</span></span>

| <span data-ttu-id="276ee-111">Option</span><span class="sxs-lookup"><span data-stu-id="276ee-111">Option</span></span> | <span data-ttu-id="276ee-112">Description</span><span class="sxs-lookup"><span data-stu-id="276ee-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="276ee-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="276ee-113">AssemblyPath</span></span> | <span data-ttu-id="276ee-114">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="276ee-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="276ee-115">Appliqués</span><span class="sxs-lookup"><span data-stu-id="276ee-115">Force</span></span> | <span data-ttu-id="276ee-116">Remplace tout fichier existant `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="276ee-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="276ee-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="276ee-117">ForceEnglishOutput</span></span> | <span data-ttu-id="276ee-118">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="276ee-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="276ee-119">Help</span><span class="sxs-lookup"><span data-stu-id="276ee-119">Help</span></span> | <span data-ttu-id="276ee-120">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="276ee-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="276ee-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="276ee-121">NonInteractive</span></span> | <span data-ttu-id="276ee-122">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="276ee-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="276ee-123">Commentaires</span><span class="sxs-lookup"><span data-stu-id="276ee-123">Verbosity</span></span> | <span data-ttu-id="276ee-124">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="276ee-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="276ee-125">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="276ee-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="276ee-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="276ee-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
