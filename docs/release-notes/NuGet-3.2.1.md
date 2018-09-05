---
title: Notes de publication NuGet 3.2.1
description: Notes de publication pour NuGet 3.2.1 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548188"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="502c2-103">Notes de publication NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="502c2-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="502c2-104">[Notes de publication de NuGet 3.2](../release-notes/nuget-3.2.md) | [Notes de publication NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="502c2-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="502c2-105">NuGet 3.2.1 pour la ligne de commande a été publiée le 12 octobre 2015, avec un certain nombre d’optimisations et les correctifs pour la version 3.2 et est disponible à partir de [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="502c2-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="502c2-106">Améliorations</span><span class="sxs-lookup"><span data-stu-id="502c2-106">Improvements</span></span>

* <span data-ttu-id="502c2-107">NuGet utilise désormais le fichier de configuration avec la casse d’origine de `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="502c2-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="502c2-108">Ceci est important sur les systèmes d’exploitation respectant la casse [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="502c2-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="502c2-109">Restauration NuGet ignore maintenant les projets dnx (`*.xproj`) qui doit être traité avec `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="502c2-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="502c2-110">Optimisé l’utilisation du réseau lorsque vous travaillez avec `index.json` et les données de l’inscription du package [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="502c2-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="502c2-111">Téléchargement de ressources gérant de manière à être plus robuste avec les services v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="502c2-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="502c2-112">Correctifs</span><span class="sxs-lookup"><span data-stu-id="502c2-112">Fixes</span></span>

* <span data-ttu-id="502c2-113">Mise à jour de NuGet met correctement à jour `.csproj` / `.vcxproj` références [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="502c2-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="502c2-114">Maintenant empêchant toute un dossier local .nuget création lorsqu’un SpecialFolders.UserProfile ne peut pas être localisé [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="502c2-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="502c2-115">Une gestion des packages dans le cache local sont endommagés pendant le téléchargement améliorée [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="502c2-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="502c2-116">Obtenir la liste complète des problèmes résolus pour la ligne de commande et de Visual Studio se trouve dans NuGet GitHub [3.2.1 jalon](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="502c2-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="502c2-117">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="502c2-117">Known Issues</span></span>

<span data-ttu-id="502c2-118">Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="502c2-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>