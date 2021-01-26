---
title: Notes de publication de NuGet 3.4.2
description: Notes de publication pour NuGet 3.4.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780252"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="1b0d9-103">Notes de publication de NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="1b0d9-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="1b0d9-104">Notes de publication de [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Notes de publication de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="1b0d9-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="1b0d9-105">NuGet 3.4.2 a été publié le 8 avril 2016 pour résoudre plusieurs problèmes identifiés dans les versions 3,4 et 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="1b0d9-106">nuget.exe 3.4.2 RC est désormais disponible</span><span class="sxs-lookup"><span data-stu-id="1b0d9-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="1b0d9-107">Vous pouvez télécharger la version Release candidate de nuget.exe 3.4.2 [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="1b0d9-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="1b0d9-108">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="1b0d9-108">Updates and Improvements</span></span>

* <span data-ttu-id="1b0d9-109">Nous avons considérablement amélioré les performances des mises à jour dans un scénario spécifique, où les mises à jour sur les packages avec des graphiques de dépendance profonde prenaient beaucoup de temps et ont bloqué Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="1b0d9-110">la restauration NuGet sans trafic réseau est de 2,5 x – 3 fois plus rapide dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="1b0d9-111">En plus de cette modification, nous avons résolu un problème où nous avons atteint le réseau deux fois lors de l’extraction du nombre de mises à jour dans l’interface utilisateur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="1b0d9-112">Cela était partiellement responsable de certains problèmes de délai d’attente rencontrés par les clients dans 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="1b0d9-113">Ajout de la prise en charge du paramètre no_proxy</span><span class="sxs-lookup"><span data-stu-id="1b0d9-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="1b0d9-114">Correctifs</span><span class="sxs-lookup"><span data-stu-id="1b0d9-114">Fixes</span></span>

* <span data-ttu-id="1b0d9-115">Correction d’un problème où la source nuget.org était manquante dans les paramètres ou la configuration NuGet après une mise à jour à 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="1b0d9-116">Résolution d’un problème où une modification de la casse à FindPackagesById dans 3.4.1 rompt l’artefact.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="1b0d9-117">Correction d’un problème avec FIPS qui provoquait des échecs avec la restauration NuGet avec nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="1b0d9-118">Résolution d’un incident lors de l’exploration des sources avec une URL d’icône non valide.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="1b0d9-119">Résolution des problèmes liés à la fusion de versions et d’entrées à partir de’toutes les sources'.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="1b0d9-120">Problèmes connus dans 3.4.2 Windows x86 CommandLine (RC)</span><span class="sxs-lookup"><span data-stu-id="1b0d9-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="1b0d9-121">Ces problèmes seront corrigés au début de la semaine prochaine avant que nous ayons atteint la version RTM.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="1b0d9-122">L’exécution de la restauration NuGet sur une solution échoue si le fichier de solution est placé dans une hiérarchie de dossiers inférieure aux fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="1b0d9-123">L’exécution de la commande NuGet Delete sur un package à l’aide du flux v2 échoue.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="1b0d9-124">Utilisez à la place le flux v3.</span><span class="sxs-lookup"><span data-stu-id="1b0d9-124">Use V3 feed instead.</span></span>


<span data-ttu-id="1b0d9-125">Pour obtenir la liste complète des correctifs et améliorations de cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="1b0d9-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>