---
title: Commande init de l’interface CLI NuGet
description: Référence pour la commande nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623082"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="51260-103">Init, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="51260-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="51260-104">**S’applique à :** &bullet; **versions prises en charge** pour la création de package : 3.3 +</span><span class="sxs-lookup"><span data-stu-id="51260-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="51260-105">Copie tous les packages d’un dossier plat dans un dossier de destination à l’aide d’une disposition hiérarchique comme décrit pour la [commande Ajouter](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="51260-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="51260-106">Autrement dit, l’utilisation de équivaut `init` à utiliser la `add` commande sur chaque package dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="51260-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="51260-107">Comme avec `add` , la destination doit être un dossier local ou un chemin d’accès UNC ; Les référentiels de packages HTTP comme nuget.org ou les serveurs privés ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="51260-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="51260-108">Usage</span><span class="sxs-lookup"><span data-stu-id="51260-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="51260-109">où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou le chemin d’accès UNC dans lequel les packages sont copiés.</span><span class="sxs-lookup"><span data-stu-id="51260-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="51260-110">Options</span><span class="sxs-lookup"><span data-stu-id="51260-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="51260-111">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="51260-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="51260-112">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="51260-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="51260-113">Ajoute tous les fichiers de chaque package qui est ajouté à la source du package ; identique `-Expand` à la `add` commande.</span><span class="sxs-lookup"><span data-stu-id="51260-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="51260-114">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="51260-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="51260-115">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="51260-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="51260-116">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="51260-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="51260-117">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="51260-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="51260-118">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="51260-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="51260-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="51260-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
