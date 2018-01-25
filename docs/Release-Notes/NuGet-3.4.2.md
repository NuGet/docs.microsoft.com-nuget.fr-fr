---
title: Notes de publication NuGet 3.4.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 3.4.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 3.4.2 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="3abee-104">Notes de mise à jour de NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="3abee-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="3abee-105">[Notes de publication NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Notes de publication](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="3abee-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="3abee-106">NuGet 3.4.2 a été publiée le 8 avril 2016 pour résoudre plusieurs problèmes ont été identifiés dans le 3.4 et 3.4.1 release.</span><span class="sxs-lookup"><span data-stu-id="3abee-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="3abee-107">NuGet.exe 3.4.2 RC est désormais disponible</span><span class="sxs-lookup"><span data-stu-id="3abee-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="3abee-108">Vous pouvez télécharger la version release candidate de nuget.exe 3.4.2 [ici](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="3abee-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3abee-109">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="3abee-109">Updates and Improvements</span></span>

* <span data-ttu-id="3abee-110">Nous avons considérablement amélioré les performances des mises à jour dans un scénario spécifique, où les mises à jour sur les packages avec des graphiques de dépendance approfondie a pris beaucoup de temps et est en attente de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3abee-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="3abee-111">restauration de NuGet sans le trafic réseau est 2,5 à 3 x plus rapide dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3abee-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="3abee-112">En plus de cette modification, nous avons résolu d’un problème où nous étions en appuyant sur le réseau à deux reprises lors de l’extraction de la mise à jour compter dans l’interface utilisateur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3abee-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="3abee-113">Cela a été partiellement chargé de certains clients de problèmes de délai d’attente, l’expérience de 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="3abee-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="3abee-114">Prise en charge pour le paramètre de no_proxy</span><span class="sxs-lookup"><span data-stu-id="3abee-114">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="3abee-115">Correctifs</span><span class="sxs-lookup"><span data-stu-id="3abee-115">Fixes</span></span>

* <span data-ttu-id="3abee-116">Correction d’un problème où nuget.org source est manquant dans les paramètres de NuGet ou la configuration après la mise à jour vers 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="3abee-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="3abee-117">Correction d’un problème où une modification de la casse FindPackagesById dans 3.4.1 sauts Artifactory.</span><span class="sxs-lookup"><span data-stu-id="3abee-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="3abee-118">Correction d’un problème à la norme FIPS qui a provoqué des échecs de restauration NuGet avec nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="3abee-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="3abee-119">Correction d’un incident lorsque vous parcourez des sources avec l’URL de l’icône non valide.</span><span class="sxs-lookup"><span data-stu-id="3abee-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="3abee-120">Résolution des problèmes avec la fusion des versions et les entrées ' Toutes les sources'.</span><span class="sxs-lookup"><span data-stu-id="3abee-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="3abee-121">Problèmes connus dans la section 3.4.2 Windows x86 de ligne de commande (RC)</span><span class="sxs-lookup"><span data-stu-id="3abee-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="3abee-122">Ces problèmes seront résolus anticipée semaine suivante avant que nous atteinte RTM.</span><span class="sxs-lookup"><span data-stu-id="3abee-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="3abee-123">Restauration de nuget en cours d’exécution sur une solution échoue si le fichier solution est placé dans une hiérarchie de dossiers plus faible que les fichiers de projet.</span><span class="sxs-lookup"><span data-stu-id="3abee-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="3abee-124">Commande de suppression de nuget en cours d’exécution sur un package à l’aide de l’alimentation V2 échoue.</span><span class="sxs-lookup"><span data-stu-id="3abee-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="3abee-125">Utilisez à la place des flux de V3.</span><span class="sxs-lookup"><span data-stu-id="3abee-125">Use V3 feed instead.</span></span>


<span data-ttu-id="3abee-126">Pour obtenir la liste complète des correctifs et améliorations apportées dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="3abee-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>