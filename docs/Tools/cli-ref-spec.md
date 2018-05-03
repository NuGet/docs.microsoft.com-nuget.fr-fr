---
title: Commande spec de NuGet CLI
description: Informations de référence pour la commande spec nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="68a23-103">commande spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="68a23-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="68a23-104">**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="68a23-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="68a23-105">Génère un `.nuspec` fichier pour un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="68a23-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="68a23-106">Si vous exécutez dans le même dossier dans un fichier de projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="68a23-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="68a23-107">Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="68a23-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="68a23-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="68a23-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="68a23-109">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="68a23-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="68a23-110">Options</span><span class="sxs-lookup"><span data-stu-id="68a23-110">Options</span></span>

| <span data-ttu-id="68a23-111">Option</span><span class="sxs-lookup"><span data-stu-id="68a23-111">Option</span></span> | <span data-ttu-id="68a23-112">Description</span><span class="sxs-lookup"><span data-stu-id="68a23-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68a23-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="68a23-113">AssemblyPath</span></span> | <span data-ttu-id="68a23-114">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="68a23-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="68a23-115">Force</span><span class="sxs-lookup"><span data-stu-id="68a23-115">Force</span></span> | <span data-ttu-id="68a23-116">Remplace l’existant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="68a23-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="68a23-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="68a23-117">ForceEnglishOutput</span></span> | <span data-ttu-id="68a23-118">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="68a23-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="68a23-119">Help</span><span class="sxs-lookup"><span data-stu-id="68a23-119">Help</span></span> | <span data-ttu-id="68a23-120">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="68a23-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="68a23-121">Non interactif</span><span class="sxs-lookup"><span data-stu-id="68a23-121">NonInteractive</span></span> | <span data-ttu-id="68a23-122">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="68a23-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="68a23-123">Commentaires</span><span class="sxs-lookup"><span data-stu-id="68a23-123">Verbosity</span></span> | <span data-ttu-id="68a23-124">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="68a23-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="68a23-125">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="68a23-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="68a23-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="68a23-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
