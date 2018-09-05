---
title: Ajouter des commandes CLI NuGet
description: Référence pour nuget.exe ajouter la commande
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545832"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="e97d5-103">add (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e97d5-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="e97d5-104">**S’applique aux**: publication du package &bullet; **versions prises en charge**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="e97d5-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="e97d5-105">Ajoute un package spécifié à une source de packages non HTTP (un dossier ou un chemin d’accès UNC) de façon hiérarchique, où les dossiers sont créés pour le numéro d’ID et la version de package.</span><span class="sxs-lookup"><span data-stu-id="e97d5-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="e97d5-106">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e97d5-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="e97d5-107">Lorsque vous restaurez ou la mise à jour par rapport à la source du package, disposition hiérarchique considérablement plus performante.</span><span class="sxs-lookup"><span data-stu-id="e97d5-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="e97d5-108">Pour développer tous les fichiers dans le package à la source de package de destination, utilisez la `-Expand` basculer.</span><span class="sxs-lookup"><span data-stu-id="e97d5-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="e97d5-109">Cela se produit généralement dans les sous-dossiers supplémentaires qui apparaissent dans la destination, tel que `tools` et `lib`.</span><span class="sxs-lookup"><span data-stu-id="e97d5-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="e97d5-110">Utilisation</span><span class="sxs-lookup"><span data-stu-id="e97d5-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="e97d5-111">où `<packagePath>` est le chemin d’accès au package à ajouter, et `<sourcePath>` spécifie la source de package basé sur le dossier dans lequel le package sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="e97d5-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="e97d5-112">Les sources HTTP ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e97d5-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="e97d5-113">Options</span><span class="sxs-lookup"><span data-stu-id="e97d5-113">Options</span></span>

| <span data-ttu-id="e97d5-114">Option</span><span class="sxs-lookup"><span data-stu-id="e97d5-114">Option</span></span> | <span data-ttu-id="e97d5-115">Description</span><span class="sxs-lookup"><span data-stu-id="e97d5-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e97d5-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e97d5-116">ConfigFile</span></span> | <span data-ttu-id="e97d5-117">Le fichier de configuration de NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="e97d5-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e97d5-118">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e97d5-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e97d5-119">Expand</span><span class="sxs-lookup"><span data-stu-id="e97d5-119">Expand</span></span> | <span data-ttu-id="e97d5-120">Ajoute tous les fichiers dans le package à la source du package.</span><span class="sxs-lookup"><span data-stu-id="e97d5-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="e97d5-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e97d5-121">ForceEnglishOutput</span></span> | <span data-ttu-id="e97d5-122">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="e97d5-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e97d5-123">Help</span><span class="sxs-lookup"><span data-stu-id="e97d5-123">Help</span></span> | <span data-ttu-id="e97d5-124">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="e97d5-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="e97d5-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e97d5-125">NonInteractive</span></span> | <span data-ttu-id="e97d5-126">Supprime les invites pour l’entrée de l’utilisateur ou de confirmations.</span><span class="sxs-lookup"><span data-stu-id="e97d5-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e97d5-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e97d5-127">Verbosity</span></span> | <span data-ttu-id="e97d5-128">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="e97d5-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e97d5-129">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e97d5-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e97d5-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="e97d5-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
