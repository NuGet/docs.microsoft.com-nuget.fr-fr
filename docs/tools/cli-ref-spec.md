---
title: Commande spec de NuGet CLI
description: Informations de référence pour la commande spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817084"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="2a967-103">commande spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2a967-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="2a967-104">**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="2a967-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2a967-105">Génère un `.nuspec` fichier pour un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="2a967-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="2a967-106">Si vous exécutez dans le même dossier dans un fichier de projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="2a967-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="2a967-107">Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="2a967-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2a967-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="2a967-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="2a967-109">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="2a967-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="2a967-110">Options</span><span class="sxs-lookup"><span data-stu-id="2a967-110">Options</span></span>

| <span data-ttu-id="2a967-111">Option</span><span class="sxs-lookup"><span data-stu-id="2a967-111">Option</span></span> | <span data-ttu-id="2a967-112">Description</span><span class="sxs-lookup"><span data-stu-id="2a967-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a967-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="2a967-113">AssemblyPath</span></span> | <span data-ttu-id="2a967-114">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="2a967-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="2a967-115">Force</span><span class="sxs-lookup"><span data-stu-id="2a967-115">Force</span></span> | <span data-ttu-id="2a967-116">Remplace l’existant `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="2a967-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="2a967-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2a967-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2a967-118">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="2a967-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2a967-119">Help</span><span class="sxs-lookup"><span data-stu-id="2a967-119">Help</span></span> | <span data-ttu-id="2a967-120">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="2a967-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="2a967-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2a967-121">NonInteractive</span></span> | <span data-ttu-id="2a967-122">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="2a967-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2a967-123">Commentaires</span><span class="sxs-lookup"><span data-stu-id="2a967-123">Verbosity</span></span> | <span data-ttu-id="2a967-124">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="2a967-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2a967-125">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2a967-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2a967-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="2a967-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
