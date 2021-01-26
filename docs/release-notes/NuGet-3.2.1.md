---
title: Notes de publication de NuGet 3.2.1
description: Notes de publication pour NuGet 3.2.1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776526"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="0f1d3-103">Notes de publication de NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="0f1d3-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="0f1d3-104">Notes de publication de [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Notes de publication de NuGet 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="0f1d3-105">NuGet 3.2.1 pour la ligne de commande a été publiée le 12 octobre 2015 avec quelques optimisations et correctifs pour la version de 3,2 et est disponible à partir de [dist.NuGet.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="0f1d3-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="0f1d3-106">Améliorations</span><span class="sxs-lookup"><span data-stu-id="0f1d3-106">Improvements</span></span>

* <span data-ttu-id="0f1d3-107">NuGet utilise désormais le fichier de configuration avec la casse d’origine `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="0f1d3-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="0f1d3-108">Cela est important sur les systèmes d’exploitation qui respectent la casse [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="0f1d3-109">La restauration NuGet ignore maintenant les projets DNX ( `*.xproj` ) qui doivent être traités avec `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="0f1d3-110">Utilisation optimisée du réseau lors de l’utilisation des `index.json` données d’inscription et de package [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="0f1d3-111">Amélioration de la gestion du téléchargement des ressources pour être plus robuste avec les services v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="0f1d3-112">Correctifs</span><span class="sxs-lookup"><span data-stu-id="0f1d3-112">Fixes</span></span>

* <span data-ttu-id="0f1d3-113">Mise à jour de NuGet mises à jour correctement `.csproj` / `.vcxproj` références [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="0f1d3-114">Maintenant, vous empêchez la création d’un dossier. NuGet local lorsqu’un SpecialFolders. UserProfile est introuvable [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="0f1d3-115">Amélioration de la gestion des packages dans le cache local endommagés au cours du téléchargement [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="0f1d3-116">Une liste complète des problèmes adressés à la ligne de commande et à l’extension Visual Studio se trouve dans le [Jalon](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet GitHub 3.2.1.</span><span class="sxs-lookup"><span data-stu-id="0f1d3-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="0f1d3-117">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="0f1d3-117">Known Issues</span></span>

<span data-ttu-id="0f1d3-118">Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="0f1d3-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>