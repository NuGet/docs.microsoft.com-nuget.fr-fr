---
title: Commande de liste de l’interface CLI NuGet
description: Référence pour la commande nuget.exe List
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623069"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b7f8a-103">List, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="b7f8a-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="b7f8a-104">**S’applique à : consommation de** packages, publication &bullet; des **versions prises en charge :** toutes</span><span class="sxs-lookup"><span data-stu-id="b7f8a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b7f8a-105">Affiche la liste des packages d’une source donnée.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b7f8a-106">Si aucune source n’est spécifiée, toutes les sources définies dans le fichier de configuration global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` , sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="b7f8a-107">Si `NuGet.Config` ne spécifie aucune source, `list` utilise le flux par défaut (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="b7f8a-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b7f8a-108">Usage</span><span class="sxs-lookup"><span data-stu-id="b7f8a-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="b7f8a-109">où les termes de recherche facultatifs filtrent la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b7f8a-110">Les [termes de recherche](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) sont appliqués aux noms des packages, des balises et des descriptions de package comme c’est le cas lorsque vous les utilisez sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-110">[Search terms](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="b7f8a-111">Options</span><span class="sxs-lookup"><span data-stu-id="b7f8a-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="b7f8a-112">Répertorie toutes les versions d’un package.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-112">List all versions of a package.</span></span> <span data-ttu-id="b7f8a-113">Par défaut, seule la dernière version du package est affichée.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b7f8a-114">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b7f8a-115">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b7f8a-116">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b7f8a-117">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="b7f8a-118">*(3.2 +)* Affichez les packages qui ne sont pas répertoriés.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b7f8a-119">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="b7f8a-120">Contient des packages de version préliminaire dans la liste.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="b7f8a-121">Spécifie une liste de sources de packages à rechercher.</span><span class="sxs-lookup"><span data-stu-id="b7f8a-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b7f8a-122">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="b7f8a-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="b7f8a-123">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b7f8a-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b7f8a-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="b7f8a-124">Examples</span></span>

<span data-ttu-id="b7f8a-125">Répertorier tous les packages à partir des flux configurés :</span><span class="sxs-lookup"><span data-stu-id="b7f8a-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="b7f8a-126">Répertoriez les packages liés à Azure avec un niveau de détail détaillé :</span><span class="sxs-lookup"><span data-stu-id="b7f8a-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="b7f8a-127">Répertorier toutes les versions des packages associés à Azure à partir de flux configurés :</span><span class="sxs-lookup"><span data-stu-id="b7f8a-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="b7f8a-128">Répertorie toutes les versions des packages liés à JSON à partir de la source/du flux spécifié :</span><span class="sxs-lookup"><span data-stu-id="b7f8a-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="b7f8a-129">Répertorier les packages liés à JSON à partir de plusieurs sources/flux :</span><span class="sxs-lookup"><span data-stu-id="b7f8a-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
