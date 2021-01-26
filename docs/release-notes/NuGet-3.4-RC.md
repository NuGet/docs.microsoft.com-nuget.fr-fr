---
title: Notes de publication de NuGet 3,4-RC
description: Notes de publication de NuGet 3,4 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780245"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="2a364-103">Notes de publication de NuGet 3,4-RC</span><span class="sxs-lookup"><span data-stu-id="2a364-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="2a364-104">Notes de publication de [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Notes de publication de NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="2a364-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="2a364-105">NuGet 3,4-RC a été publié le 3 mars 2016 en même temps que Visual Studio 2015 Update 2 RC et a été créé avec quelques principes à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="2a364-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="2a364-106">Prise en charge multiplateforme</span><span class="sxs-lookup"><span data-stu-id="2a364-106">Cross-Platform support</span></span>
* <span data-ttu-id="2a364-107">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="2a364-107">Performance improvements</span></span>
* <span data-ttu-id="2a364-108">Améliorations mineures de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="2a364-108">Minor UI improvements</span></span>

<span data-ttu-id="2a364-109">Les fonctionnalités suivantes sont disponibles dans cette version RC, avec davantage de planification pour la version finale 3,4.</span><span class="sxs-lookup"><span data-stu-id="2a364-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="2a364-110">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="2a364-110">New Features</span></span>

* <span data-ttu-id="2a364-111">Les clients NuGet prennent désormais en charge l’encodage de contenu gzip à partir des référentiels</span><span class="sxs-lookup"><span data-stu-id="2a364-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="2a364-112">Prise en charge des fichiers PDB des packages dans les projets xproj</span><span class="sxs-lookup"><span data-stu-id="2a364-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="2a364-113">Prise en charge des actions de génération iOS et Android dans l’élément contentFiles</span><span class="sxs-lookup"><span data-stu-id="2a364-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="2a364-114">Prise en charge des monikers netstandard et nestandardapp Framework</span><span class="sxs-lookup"><span data-stu-id="2a364-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="2a364-115">Nouvelles fonctionnalités de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="2a364-115">New User Interface Features</span></span>

* <span data-ttu-id="2a364-116">Amélioration significative des performances, en particulier sur les onglets installé, mises à jour et consolider</span><span class="sxs-lookup"><span data-stu-id="2a364-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="2a364-117">Les onglets installé et mis à jour sont désormais triés par ordre alphabétique</span><span class="sxs-lookup"><span data-stu-id="2a364-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="2a364-118">Ajout d’un bouton d’actualisation permettant d’actualiser une recherche</span><span class="sxs-lookup"><span data-stu-id="2a364-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="2a364-119">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="2a364-119">Updates and Improvements</span></span>

* <span data-ttu-id="2a364-120">Les packages référencés dans `project.json` et qui ont une version flottante ne sont pas mis à jour sur chaque Build.</span><span class="sxs-lookup"><span data-stu-id="2a364-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="2a364-121">Au lieu de cela, ils sont mis à jour uniquement lorsqu’ils sont forcés à restaurer, nettoyer, régénérer ou modifier `project.json` .</span><span class="sxs-lookup"><span data-stu-id="2a364-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="2a364-122">les sources de référentiel nuget.org ne sont plus contraints dans une configuration de projet lorsque vous utilisez l’interface utilisateur de configuration de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2a364-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="2a364-123">NuGet ne restaure plus les packages dans les projets partagés et n’écrit pas de fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="2a364-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="2a364-124">Nous avons amélioré les défaillances du réseau et les tentatives de traitement des serveurs inaccessibles ou lents à répondre.</span><span class="sxs-lookup"><span data-stu-id="2a364-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="2a364-125">Les comportements du clavier et de la souris sont améliorés dans l’interface utilisateur du gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a364-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="2a364-126">Nous prenons maintenant en charge le schéma le plus récent `project.json` dans DNX.</span><span class="sxs-lookup"><span data-stu-id="2a364-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2a364-127">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="2a364-127">Known Issues</span></span>

<span data-ttu-id="2a364-128">Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="2a364-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>