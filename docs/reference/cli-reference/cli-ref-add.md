---
title: Commande Add de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622900"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="a4fb8-103">Add, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="a4fb8-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="a4fb8-104">**S’applique à**: publication de packages &bullet; **versions prises en charge**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a4fb8-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="a4fb8-105">Ajoute un package spécifié à une source de package non-HTTP (dossier ou chemin d’accès UNC) dans une disposition hiérarchique, où les dossiers sont créés pour l’ID de package et le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="a4fb8-106">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a4fb8-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="a4fb8-107">Lors de la restauration ou de la mise à jour par rapport à la source du package, la disposition hiérarchique offre des performances nettement meilleures.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="a4fb8-108">Pour développer tous les fichiers du package vers la source du package de destination, utilisez le `-Expand` commutateur.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="a4fb8-109">Cela entraîne généralement l’affichage de sous-dossiers supplémentaires dans la destination, tels que `tools` et `lib` .</span><span class="sxs-lookup"><span data-stu-id="a4fb8-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="a4fb8-110">Usage</span><span class="sxs-lookup"><span data-stu-id="a4fb8-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="a4fb8-111">où `<packagePath>` est le nom du chemin d’accès au package à ajouter et `<sourcePath>` spécifie la source du package basée sur le dossier à laquelle le package sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="a4fb8-112">Les sources HTTP ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="a4fb8-113">Options</span><span class="sxs-lookup"><span data-stu-id="a4fb8-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a4fb8-114">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a4fb8-115">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="a4fb8-116">Ajoute tous les fichiers du package à la source du package.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a4fb8-117">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="a4fb8-118">Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a4fb8-119">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a4fb8-120">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="a4fb8-121">Spécifie la source du package, qui est un dossier ou un partage UNC auquel le nupkg sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="a4fb8-122">Les sources http ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="a4fb8-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a4fb8-123">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a4fb8-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a4fb8-124">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a4fb8-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a4fb8-125">Exemples</span><span class="sxs-lookup"><span data-stu-id="a4fb8-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
