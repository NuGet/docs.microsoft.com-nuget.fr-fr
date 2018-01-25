---
title: Commande spec de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour la commande spec nuget.exe"
keywords: "référence technique de NuGet, commande spec"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="173db-104">commande spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="173db-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="173db-105">**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="173db-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="173db-106">Génère un `.nuspec` fichier pour un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="173db-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="173db-107">Si vous exécutez dans le même dossier dans un fichier de projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="173db-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="173db-108">Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="173db-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="173db-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="173db-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="173db-110">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="173db-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="173db-111">Options</span><span class="sxs-lookup"><span data-stu-id="173db-111">Options</span></span>

| <span data-ttu-id="173db-112">Option</span><span class="sxs-lookup"><span data-stu-id="173db-112">Option</span></span> | <span data-ttu-id="173db-113">Description</span><span class="sxs-lookup"><span data-stu-id="173db-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="173db-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="173db-114">AssemblyPath</span></span> | <span data-ttu-id="173db-115">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="173db-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="173db-116">Force</span><span class="sxs-lookup"><span data-stu-id="173db-116">Force</span></span> | <span data-ttu-id="173db-117">Remplace l’existant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="173db-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="173db-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="173db-118">ForceEnglishOutput</span></span> | <span data-ttu-id="173db-119">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="173db-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="173db-120">Help</span><span class="sxs-lookup"><span data-stu-id="173db-120">Help</span></span> | <span data-ttu-id="173db-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="173db-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="173db-122">Non interactif</span><span class="sxs-lookup"><span data-stu-id="173db-122">NonInteractive</span></span> | <span data-ttu-id="173db-123">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="173db-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="173db-124">Commentaires</span><span class="sxs-lookup"><span data-stu-id="173db-124">Verbosity</span></span> | <span data-ttu-id="173db-125">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="173db-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="173db-126">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="173db-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="173db-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="173db-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
