---
title: NuGet CLI ajouter (commande)
description: Informations de référence pour le nuget.exe ajouter (commande)
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817608"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="47cba-103">add (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="47cba-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="47cba-104">**S’applique aux**: publication du package &bullet; **versions prises en charge**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="47cba-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="47cba-105">Ajoute un package spécifié à une source de package de non-HTTP (un dossier ou un chemin d’accès UNC) de façon hiérarchique, dans lequel les dossiers sont créés pour le numéro d’ID et la version de package.</span><span class="sxs-lookup"><span data-stu-id="47cba-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="47cba-106">Exemple :</span><span class="sxs-lookup"><span data-stu-id="47cba-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="47cba-107">Lorsque vous restaurez ou mise à jour par rapport à la source du package, disposition hiérarchique fournit améliorer considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="47cba-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="47cba-108">Pour développer tous les fichiers dans le package à la source de package de destination, utilisez la `-Expand` basculer.</span><span class="sxs-lookup"><span data-stu-id="47cba-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="47cba-109">Cela se produit généralement dans les sous-dossiers supplémentaires qui apparaissent dans la destination, tel que `tools` et `lib`.</span><span class="sxs-lookup"><span data-stu-id="47cba-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="47cba-110">Utilisation</span><span class="sxs-lookup"><span data-stu-id="47cba-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="47cba-111">où `<packagePath>` est le chemin d’accès au package à ajouter, et `<sourcePath>` spécifie la source du package de basé sur le dossier dans lequel le package sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="47cba-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="47cba-112">Les sources HTTP ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="47cba-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="47cba-113">Options</span><span class="sxs-lookup"><span data-stu-id="47cba-113">Options</span></span>

| <span data-ttu-id="47cba-114">Option</span><span class="sxs-lookup"><span data-stu-id="47cba-114">Option</span></span> | <span data-ttu-id="47cba-115">Description</span><span class="sxs-lookup"><span data-stu-id="47cba-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47cba-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="47cba-116">ConfigFile</span></span> | <span data-ttu-id="47cba-117">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="47cba-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="47cba-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="47cba-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="47cba-119">Expand</span><span class="sxs-lookup"><span data-stu-id="47cba-119">Expand</span></span> | <span data-ttu-id="47cba-120">Ajoute tous les fichiers dans le package à la source du package.</span><span class="sxs-lookup"><span data-stu-id="47cba-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="47cba-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="47cba-121">ForceEnglishOutput</span></span> | <span data-ttu-id="47cba-122">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="47cba-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="47cba-123">Help</span><span class="sxs-lookup"><span data-stu-id="47cba-123">Help</span></span> | <span data-ttu-id="47cba-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="47cba-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="47cba-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="47cba-125">NonInteractive</span></span> | <span data-ttu-id="47cba-126">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="47cba-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="47cba-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="47cba-127">Verbosity</span></span> | <span data-ttu-id="47cba-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="47cba-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="47cba-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="47cba-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="47cba-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="47cba-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
