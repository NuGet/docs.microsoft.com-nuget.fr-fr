---
title: Commande de NuGet CLI init | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de la commande init nuget.exe
keywords: référence d’init NuGet, commande init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="467f3-104">commande d’init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="467f3-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="467f3-105">**S’applique à :** la création de package &bullet; **versions prises en charge :** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="467f3-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="467f3-106">Copie tous les packages à partir d’un dossier dans un dossier de destination à l’aide de façon hiérarchique comme indiqué pour le [ajouter la commande](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="467f3-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="467f3-107">Autrement dit, à l’aide de `init` est équivalente à l’aide du `add` commande sur chaque package dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="467f3-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="467f3-108">Comme avec `add`, la destination doit être un dossier local ou un chemin d’accès UNC ; Les référentiels de package HTTP telles que nuget.org ou serveurs privés ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="467f3-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="467f3-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="467f3-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="467f3-110">où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou un chemin d’accès UNC dans lequel les packages sont copiés.</span><span class="sxs-lookup"><span data-stu-id="467f3-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="467f3-111">Options</span><span class="sxs-lookup"><span data-stu-id="467f3-111">Options</span></span>

| <span data-ttu-id="467f3-112">Option</span><span class="sxs-lookup"><span data-stu-id="467f3-112">Option</span></span> | <span data-ttu-id="467f3-113">Description</span><span class="sxs-lookup"><span data-stu-id="467f3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="467f3-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="467f3-114">ConfigFile</span></span> | <span data-ttu-id="467f3-115">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="467f3-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="467f3-116">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="467f3-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="467f3-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="467f3-117">ForceEnglishOutput</span></span> | <span data-ttu-id="467f3-118">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="467f3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="467f3-119">Expand</span><span class="sxs-lookup"><span data-stu-id="467f3-119">Expand</span></span> | <span data-ttu-id="467f3-120">Ajoute tous les fichiers dans chaque package est ajouté à la source du package ; identique à `-Expand` avec la `add` commande.</span><span class="sxs-lookup"><span data-stu-id="467f3-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="467f3-121">Help</span><span class="sxs-lookup"><span data-stu-id="467f3-121">Help</span></span> | <span data-ttu-id="467f3-122">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="467f3-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="467f3-123">Non interactif</span><span class="sxs-lookup"><span data-stu-id="467f3-123">NonInteractive</span></span> | <span data-ttu-id="467f3-124">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="467f3-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="467f3-125">Commentaires</span><span class="sxs-lookup"><span data-stu-id="467f3-125">Verbosity</span></span> | <span data-ttu-id="467f3-126">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="467f3-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="467f3-127">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="467f3-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="467f3-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="467f3-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
