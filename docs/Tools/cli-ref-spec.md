---
title: Commande spec de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Informations de référence pour la commande spec nuget.exe"
keywords: "référence technique de NuGet, commande spec"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="26de7-104">commande spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="26de7-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="26de7-105">**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="26de7-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="26de7-106">Génère un `.nuspec` fichier pour un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="26de7-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="26de7-107">Si vous exécutez dans le même dossier dans un fichier de projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="26de7-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="26de7-108">Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="26de7-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="26de7-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="26de7-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="26de7-110">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="26de7-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="26de7-111">Options</span><span class="sxs-lookup"><span data-stu-id="26de7-111">Options</span></span>

| <span data-ttu-id="26de7-112">Option</span><span class="sxs-lookup"><span data-stu-id="26de7-112">Option</span></span> | <span data-ttu-id="26de7-113">Description</span><span class="sxs-lookup"><span data-stu-id="26de7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26de7-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="26de7-114">AssemblyPath</span></span> | <span data-ttu-id="26de7-115">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="26de7-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="26de7-116">Force</span><span class="sxs-lookup"><span data-stu-id="26de7-116">Force</span></span> | <span data-ttu-id="26de7-117">Remplace l’existant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="26de7-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="26de7-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="26de7-118">ForceEnglishOutput</span></span> | <span data-ttu-id="26de7-119">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="26de7-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="26de7-120">Help</span><span class="sxs-lookup"><span data-stu-id="26de7-120">Help</span></span> | <span data-ttu-id="26de7-121">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="26de7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="26de7-122">Non interactif</span><span class="sxs-lookup"><span data-stu-id="26de7-122">NonInteractive</span></span> | <span data-ttu-id="26de7-123">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="26de7-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="26de7-124">Commentaires</span><span class="sxs-lookup"><span data-stu-id="26de7-124">Verbosity</span></span> | <span data-ttu-id="26de7-125">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="26de7-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="26de7-126">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="26de7-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="26de7-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="26de7-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
