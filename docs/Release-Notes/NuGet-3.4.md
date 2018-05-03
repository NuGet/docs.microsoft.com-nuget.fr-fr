---
title: Notes de publication NuGet 3.4
description: Notes de version de NuGet 3.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="3cea8-103">Notes de publication NuGet 3.4</span><span class="sxs-lookup"><span data-stu-id="3cea8-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="3cea8-104">[Notes de publication NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Notes de publication](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="3cea8-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="3cea8-105">NuGet 3.4 a été publiée le 30 mars 2016 en tant que partie de la version préliminaire de Visual Studio 15 et de Visual Studio 2015 Update 2 et a été généré avec quelques principes dans esprit :</span><span class="sxs-lookup"><span data-stu-id="3cea8-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="3cea8-106">Prise en charge multiplateforme</span><span class="sxs-lookup"><span data-stu-id="3cea8-106">Cross-Platform support</span></span>
* <span data-ttu-id="3cea8-107">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="3cea8-107">Performance improvements</span></span>
* <span data-ttu-id="3cea8-108">Petites améliorations de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="3cea8-108">Minor UI improvements</span></span>

<span data-ttu-id="3cea8-109">Les fonctionnalités suivantes ont été ajoutées précédemment dans la version RC et ont été mis à jour ou s’est terminées pour la version 3.4 :</span><span class="sxs-lookup"><span data-stu-id="3cea8-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="3cea8-110">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3cea8-110">New Features</span></span>

* <span data-ttu-id="3cea8-111">Clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels</span><span class="sxs-lookup"><span data-stu-id="3cea8-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="3cea8-112">Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj</span><span class="sxs-lookup"><span data-stu-id="3cea8-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="3cea8-113">Prise en charge pour iOS et Android actions de génération dans l’élément de fichiers</span><span class="sxs-lookup"><span data-stu-id="3cea8-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="3cea8-114">Prise en charge des monikers netstandard et netstandardapp du framework</span><span class="sxs-lookup"><span data-stu-id="3cea8-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="3cea8-115">Nouvelles fonctionnalités de l’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="3cea8-115">New User Interface Features</span></span>

* <span data-ttu-id="3cea8-116">Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider</span><span class="sxs-lookup"><span data-stu-id="3cea8-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="3cea8-117">Source d’agrégat de « Toutes les Sources de Package » n’est disponible avec la fusion de résultats de recherche correcte</span><span class="sxs-lookup"><span data-stu-id="3cea8-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="3cea8-118">Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique</span><span class="sxs-lookup"><span data-stu-id="3cea8-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="3cea8-119">Ajouter un bouton d’actualisation qui permet une recherche à actualiser</span><span class="sxs-lookup"><span data-stu-id="3cea8-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="3cea8-120">Options de génération plus récentes en haut de la liste des versions</span><span class="sxs-lookup"><span data-stu-id="3cea8-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3cea8-121">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="3cea8-121">Updates and Improvements</span></span>

* <span data-ttu-id="3cea8-122">Packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour à chaque build.</span><span class="sxs-lookup"><span data-stu-id="3cea8-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="3cea8-123">Au lieu de cela, ils mettent à jour uniquement quand il est contraint à restaurer, nettoyer, régénérer ou modifier `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3cea8-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="3cea8-124">sources de référentiel NuGet.org deviennent n’est plus dans une configuration de projet lorsque vous utilisez l’interface de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="3cea8-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="3cea8-125">NuGet n’est plus restaure les packages dans les projets partagés écritures, ni un fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="3cea8-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="3cea8-126">Nous avez amélioré de défaillance du réseau et recommencez la gestion des serveurs inaccessibles ou lente à répondre.</span><span class="sxs-lookup"><span data-stu-id="3cea8-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="3cea8-127">Les comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.</span><span class="sxs-lookup"><span data-stu-id="3cea8-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="3cea8-128">Nous prennent désormais en charge la dernière version `project.json` schéma de DNX.</span><span class="sxs-lookup"><span data-stu-id="3cea8-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="3cea8-129">Modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="3cea8-129">Breaking Changes</span></span>

* <span data-ttu-id="3cea8-130">Les numéros de version de package sont désormais normalisés au format *majeure*. *mineure*. *correctif*-*préliminaire* chacune de majeure, mineure et de correctif logiciel sont traitées en tant qu’entiers et supprimer les zéros non significatifs.</span><span class="sxs-lookup"><span data-stu-id="3cea8-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="3cea8-131">Les informations de version préliminaire sont traitées comme une chaîne et aucune modification lui n’est appliquées.</span><span class="sxs-lookup"><span data-stu-id="3cea8-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="3cea8-132">Ces nombres sont utilisés dans les requêtes par les clients NuGet et la recherche fournies par le service nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3cea8-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="3cea8-133">Vous trouverez plus de détails dans la documentation de NuGet sous [Versions de la version préliminaire](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3cea8-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="3cea8-134">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="3cea8-134">Known Issues</span></span>

* <span data-ttu-id="3cea8-135">**Problème :** Windows 10 v1511 utilisateurs peuvent rencontrer des problèmes ou même un blocage de Visual Studio avec Powershell dans Visual Studio dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="3cea8-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="3cea8-136">L’installation / désinstallation des packages qui ont install.ps1 / uninstall.ps1 scripts</span><span class="sxs-lookup"><span data-stu-id="3cea8-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="3cea8-137">Le chargement des projets qui ont un script init.ps1 (comme EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="3cea8-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="3cea8-138">Publication de contenu web</span><span class="sxs-lookup"><span data-stu-id="3cea8-138">Publishing web content</span></span>

* <span data-ttu-id="3cea8-139">**Solution de contournement :** vous assurer que votre installation de Windows 10 a les derniers correctifs appliqués, spécialement le janvier 2016 (KB 3124263) ou une mise à jour ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3cea8-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="3cea8-140">Plus de détails sont disponibles sur [problème GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="3cea8-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="3cea8-141">**Problème :** Les redirections du protocole NuGet v2 sont rompues.</span><span class="sxs-lookup"><span data-stu-id="3cea8-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="3cea8-142">Les dépôts NuGet personnalisés qui redirigent les demandes vers un autre hôte n’honorent pas ces demandes.</span><span class="sxs-lookup"><span data-stu-id="3cea8-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="3cea8-143">**Solution de contournement :** pour contourner ce problème, configurez l’URI de dépôt de packages dans les paramètres pour pointer vers l’emplacement de serveur redirigé.</span><span class="sxs-lookup"><span data-stu-id="3cea8-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="3cea8-144">Pour plus d’informations, consultez [requête de tirage GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="3cea8-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="3cea8-145">Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="3cea8-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>