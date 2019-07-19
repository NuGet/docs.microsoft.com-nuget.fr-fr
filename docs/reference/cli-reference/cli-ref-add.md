---
title: Commande Add de l’interface CLI NuGet
description: Référence pour la commande d’ajout de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327856"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="1cc79-103">add (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1cc79-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="1cc79-104">**S’applique à**: publication &bullet; de packages **prises en charge**: 3.3+</span><span class="sxs-lookup"><span data-stu-id="1cc79-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="1cc79-105">Ajoute un package spécifié à une source de package non-HTTP (dossier ou chemin d’accès UNC) dans une disposition hiérarchique, où les dossiers sont créés pour l’ID de package et le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="1cc79-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="1cc79-106">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1cc79-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="1cc79-107">Lors de la restauration ou de la mise à jour par rapport à la source du package, la disposition hiérarchique offre des performances nettement meilleures.</span><span class="sxs-lookup"><span data-stu-id="1cc79-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="1cc79-108">Pour développer tous les fichiers du package vers la source du package de destination, utilisez `-Expand` le commutateur.</span><span class="sxs-lookup"><span data-stu-id="1cc79-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="1cc79-109">Cela entraîne généralement l’affichage de sous-dossiers supplémentaires dans la destination, tels `tools` que `lib`et.</span><span class="sxs-lookup"><span data-stu-id="1cc79-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="1cc79-110">Usage</span><span class="sxs-lookup"><span data-stu-id="1cc79-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="1cc79-111">où `<packagePath>` est le nom du chemin d’accès au package à `<sourcePath>` ajouter et spécifie la source du package basée sur le dossier à laquelle le package sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="1cc79-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="1cc79-112">Les sources HTTP ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="1cc79-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="1cc79-113">Options</span><span class="sxs-lookup"><span data-stu-id="1cc79-113">Options</span></span>

| <span data-ttu-id="1cc79-114">Option</span><span class="sxs-lookup"><span data-stu-id="1cc79-114">Option</span></span> | <span data-ttu-id="1cc79-115">Description</span><span class="sxs-lookup"><span data-stu-id="1cc79-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1cc79-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1cc79-116">ConfigFile</span></span> | <span data-ttu-id="1cc79-117">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="1cc79-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1cc79-118">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1cc79-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1cc79-119">Expand</span><span class="sxs-lookup"><span data-stu-id="1cc79-119">Expand</span></span> | <span data-ttu-id="1cc79-120">Ajoute tous les fichiers du package à la source du package.</span><span class="sxs-lookup"><span data-stu-id="1cc79-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="1cc79-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1cc79-121">ForceEnglishOutput</span></span> | <span data-ttu-id="1cc79-122">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="1cc79-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1cc79-123">Help</span><span class="sxs-lookup"><span data-stu-id="1cc79-123">Help</span></span> | <span data-ttu-id="1cc79-124">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="1cc79-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="1cc79-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1cc79-125">NonInteractive</span></span> | <span data-ttu-id="1cc79-126">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1cc79-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1cc79-127">Commentaires</span><span class="sxs-lookup"><span data-stu-id="1cc79-127">Verbosity</span></span> | <span data-ttu-id="1cc79-128">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="1cc79-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1cc79-129">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1cc79-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1cc79-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="1cc79-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
