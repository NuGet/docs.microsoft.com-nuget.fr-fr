---
title: Notes de publication NuGet 3.4-RC
description: Notes de publication pour NuGet 3.4 RC est, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="bea0e-103">Notes de publication NuGet 3.4-RC</span><span class="sxs-lookup"><span data-stu-id="bea0e-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="bea0e-104">[Notes de publication NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 Notes de publication](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="bea0e-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="bea0e-105">NuGet 3.4-RC a été publiée le 3 mars 2016 en même temps que Visual Studio 2015 Update 2 RC et a été généré avec quelques principes dans esprit :</span><span class="sxs-lookup"><span data-stu-id="bea0e-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="bea0e-106">Prise en charge multiplateforme</span><span class="sxs-lookup"><span data-stu-id="bea0e-106">Cross-Platform support</span></span>
* <span data-ttu-id="bea0e-107">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="bea0e-107">Performance improvements</span></span>
* <span data-ttu-id="bea0e-108">Petites améliorations de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="bea0e-108">Minor UI improvements</span></span>

<span data-ttu-id="bea0e-109">Les fonctionnalités suivantes sont disponibles dans cette RC, avec plusieurs planifié pour la version finale 3.4.</span><span class="sxs-lookup"><span data-stu-id="bea0e-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="bea0e-110">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="bea0e-110">New Features</span></span>

* <span data-ttu-id="bea0e-111">Clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels</span><span class="sxs-lookup"><span data-stu-id="bea0e-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="bea0e-112">Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj</span><span class="sxs-lookup"><span data-stu-id="bea0e-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="bea0e-113">Prise en charge pour iOS et Android actions de génération dans l’élément de fichiers</span><span class="sxs-lookup"><span data-stu-id="bea0e-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="bea0e-114">Prise en charge des monikers netstandard et netstandardapp du framework</span><span class="sxs-lookup"><span data-stu-id="bea0e-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="bea0e-115">Nouvelles fonctionnalités de l’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="bea0e-115">New User Interface Features</span></span>

* <span data-ttu-id="bea0e-116">Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider</span><span class="sxs-lookup"><span data-stu-id="bea0e-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="bea0e-117">Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique</span><span class="sxs-lookup"><span data-stu-id="bea0e-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="bea0e-118">Ajouter un bouton d’actualisation qui permet une recherche à actualiser</span><span class="sxs-lookup"><span data-stu-id="bea0e-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bea0e-119">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="bea0e-119">Updates and Improvements</span></span>

* <span data-ttu-id="bea0e-120">Packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour à chaque build.</span><span class="sxs-lookup"><span data-stu-id="bea0e-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="bea0e-121">Au lieu de cela, ils mettent à jour uniquement quand il est contraint à restaurer, nettoyer, régénérer ou modifier `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bea0e-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="bea0e-122">sources de référentiel NuGet.org deviennent n’est plus dans une configuration de projet lorsque vous utilisez l’interface de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="bea0e-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="bea0e-123">NuGet n’est plus restaure les packages dans les projets partagés écritures, ni un fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="bea0e-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="bea0e-124">Nous avez amélioré de défaillance du réseau et recommencez la gestion des serveurs inaccessibles ou lente à répondre.</span><span class="sxs-lookup"><span data-stu-id="bea0e-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="bea0e-125">Les comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.</span><span class="sxs-lookup"><span data-stu-id="bea0e-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="bea0e-126">Nous prennent désormais en charge la dernière version `project.json` schéma de DNX.</span><span class="sxs-lookup"><span data-stu-id="bea0e-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="bea0e-127">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="bea0e-127">Known Issues</span></span>

<span data-ttu-id="bea0e-128">Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bea0e-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>