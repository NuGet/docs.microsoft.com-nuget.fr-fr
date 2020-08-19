---
title: Commande paramètres régionaux de l’interface CLI NuGet
description: Référence pour la commande nuget.exe variables locales
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623056"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="f2957-103">commande variables locales (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="f2957-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="f2957-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation de packages : 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f2957-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="f2957-105">Efface ou répertorie les ressources NuGet locales, telles que le dossier *http-cache*, *Global-packages* et le dossier Temp.</span><span class="sxs-lookup"><span data-stu-id="f2957-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="f2957-106">La `locals` commande peut également être utilisée pour afficher une liste de ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="f2957-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="f2957-107">Pour plus d’informations, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f2957-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f2957-108">Usage</span><span class="sxs-lookup"><span data-stu-id="f2957-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="f2957-109">où `<folder>` est l’un des, `all` `http-cache` , `packages-cache` *(3,5 et versions antérieures)*, `global-packages` , `temp` *(3.4 +)* et `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="f2957-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="f2957-110">Options</span><span class="sxs-lookup"><span data-stu-id="f2957-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="f2957-111">Efface le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="f2957-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="f2957-112">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="f2957-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f2957-113">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f2957-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="f2957-114">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="f2957-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="f2957-115">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="f2957-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="f2957-116">Répertorie l’emplacement du dossier spécifié, ou les emplacements de tous les dossiers lorsqu’ils sont utilisés avec *tous*.</span><span class="sxs-lookup"><span data-stu-id="f2957-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="f2957-117">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2957-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="f2957-118">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="f2957-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="f2957-119">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f2957-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f2957-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="f2957-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="f2957-121">Pour obtenir des exemples supplémentaires, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f2957-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
