---
title: Notes de publication de NuGet 3.4.2
description: Notes de publication pour NuGet 3.4.2 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549149"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="6bfbe-103">Notes de publication de NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="6bfbe-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="6bfbe-104">[Notes de publication de NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [Notes de publication de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="6bfbe-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="6bfbe-105">NuGet 3.4.2 a été publiée le 8 avril 2016 pour résoudre plusieurs problèmes qui ont été identifiées dans le 3.4 et 3.4.1, mise en production.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="6bfbe-106">NuGet.exe 3.4.2 RC est désormais disponible</span><span class="sxs-lookup"><span data-stu-id="6bfbe-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="6bfbe-107">Vous pouvez télécharger la version release candidate de nuget.exe 3.4.2 [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="6bfbe-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6bfbe-108">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="6bfbe-108">Updates and Improvements</span></span>

* <span data-ttu-id="6bfbe-109">Nous avons considérablement amélioré les performances des mises à jour dans un scénario spécifique, où les mises à jour sur les packages avec des graphiques de dépendance approfondie a pris beaucoup de temps et est en attente de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="6bfbe-110">la restauration NuGet sans le trafic réseau est 2,5 à 3 fois plus rapides dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="6bfbe-111">En plus de cette modification, nous avons résolu un problème où nous étions en appuyant sur le réseau à deux reprises lors de l’extraction de la mise à jour compter dans l’interface utilisateur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="6bfbe-112">Cela a été partiellement responsable pour certains clients de problèmes de délai d’attente, l’expérience de 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="6bfbe-113">Prise en charge pour le paramètre de no_proxy</span><span class="sxs-lookup"><span data-stu-id="6bfbe-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="6bfbe-114">Correctifs</span><span class="sxs-lookup"><span data-stu-id="6bfbe-114">Fixes</span></span>

* <span data-ttu-id="6bfbe-115">Correction d’un problème où nuget.org source est manquant dans les paramètres de NuGet ou de configuration après la mise à jour à 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="6bfbe-116">Correction d’un problème où un changement de casse pour FindPackagesById dans 3.4.1 interrompt Artifactory.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="6bfbe-117">Correction d’un problème à la norme FIPS qui provoquait des échecs avec la restauration de NuGet avec nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="6bfbe-118">Correction d’un incident lors de l’exploration des sources avec l’URL de l’icône non valide.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="6bfbe-119">Résolution des problèmes avec la fusion de versions et les entrées « Toutes les sources ».</span><span class="sxs-lookup"><span data-stu-id="6bfbe-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="6bfbe-120">Problèmes connus dans 3.4.2 Windows x86 de ligne de commande (RC)</span><span class="sxs-lookup"><span data-stu-id="6bfbe-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="6bfbe-121">Ces problèmes seront corrigés anticipée semaine prochaine avant que nous nous heurtons à RTM.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="6bfbe-122">La restauration nuget en cours d’exécution sur une solution échoue si le fichier solution est placé dans une hiérarchie de dossiers plus faible que les fichiers de projet.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="6bfbe-123">Exécution de commande de suppression de nuget sur un package en utilisant le flux V2 échoue.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="6bfbe-124">Utilisez plutôt les flux V3.</span><span class="sxs-lookup"><span data-stu-id="6bfbe-124">Use V3 feed instead.</span></span>


<span data-ttu-id="6bfbe-125">Pour obtenir la liste complète des correctifs et améliorations dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="6bfbe-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>