---
title: Commande spec de l’interface CLI NuGet
description: Référence pour la commande nuget.exe spec
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779151"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="fe4c4-103">Spec, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="fe4c4-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="fe4c4-104">**S’applique à :** &bullet; **versions prises en charge** pour la création de package : All</span><span class="sxs-lookup"><span data-stu-id="fe4c4-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fe4c4-105">Génère un `.nuspec` fichier pour un nouveau package.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="fe4c4-106">Si l’exécution s’exécute dans le même dossier qu’un fichier projet ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` crée un `.nuspec` fichier sous forme de jeton.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="fe4c4-107">Pour plus d’informations, consultez [création d’un package](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="fe4c4-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fe4c4-108">Utilisation</span><span class="sxs-lookup"><span data-stu-id="fe4c4-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="fe4c4-109">où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="fe4c4-110">Options</span><span class="sxs-lookup"><span data-stu-id="fe4c4-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="fe4c4-111">Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="fe4c4-112">Remplace tout `.nuspec` fichier existant.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="fe4c4-113">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="fe4c4-114">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="fe4c4-115">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fe4c4-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="fe4c4-116">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="fe4c4-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="fe4c4-117">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fe4c4-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fe4c4-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="fe4c4-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
