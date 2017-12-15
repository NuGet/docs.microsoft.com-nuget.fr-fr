---
title: Notes de publication NuGet 3.4 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Notes de version de NuGet 3.4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 3.4, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="7224a-104">Notes de publication NuGet 3.4</span><span class="sxs-lookup"><span data-stu-id="7224a-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="7224a-105">[Notes de publication NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Notes de publication](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="7224a-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="7224a-106">NuGet 3.4 a été publiée le 30 mars 2016 en tant que partie de la version préliminaire de Visual Studio 15 et de Visual Studio 2015 Update 2 et a été généré avec quelques principes dans esprit :</span><span class="sxs-lookup"><span data-stu-id="7224a-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="7224a-107">Prise en charge multiplateforme</span><span class="sxs-lookup"><span data-stu-id="7224a-107">Cross-Platform support</span></span>
*  <span data-ttu-id="7224a-108">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="7224a-108">Performance improvements</span></span>
*  <span data-ttu-id="7224a-109">Petites améliorations de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7224a-109">Minor UI improvements</span></span>

<span data-ttu-id="7224a-110">Les fonctionnalités suivantes ont été ajoutées précédemment dans la version RC et ont été mis à jour ou s’est terminées pour la version 3.4 :</span><span class="sxs-lookup"><span data-stu-id="7224a-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="7224a-111">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="7224a-111">New Features</span></span>

* <span data-ttu-id="7224a-112">Clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels</span><span class="sxs-lookup"><span data-stu-id="7224a-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7224a-113">Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj</span><span class="sxs-lookup"><span data-stu-id="7224a-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7224a-114">Prise en charge pour iOS et Android actions de génération dans l’élément de fichiers</span><span class="sxs-lookup"><span data-stu-id="7224a-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7224a-115">Prise en charge des monikers netstandard et netstandardapp du framework</span><span class="sxs-lookup"><span data-stu-id="7224a-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7224a-116">Nouvelles fonctionnalités de l’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7224a-116">New User Interface Features</span></span>

* <span data-ttu-id="7224a-117">Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider</span><span class="sxs-lookup"><span data-stu-id="7224a-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7224a-118">Source d’agrégat de « Toutes les Sources de Package » n’est disponible avec la fusion de résultats de recherche correcte</span><span class="sxs-lookup"><span data-stu-id="7224a-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="7224a-119">Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique</span><span class="sxs-lookup"><span data-stu-id="7224a-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7224a-120">Ajouter un bouton d’actualisation qui permet une recherche à actualiser</span><span class="sxs-lookup"><span data-stu-id="7224a-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="7224a-121">Options de génération plus récentes en haut de la liste des versions</span><span class="sxs-lookup"><span data-stu-id="7224a-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7224a-122">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="7224a-122">Updates and Improvements</span></span>

* <span data-ttu-id="7224a-123">Packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour à chaque build.</span><span class="sxs-lookup"><span data-stu-id="7224a-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7224a-124">Au lieu de cela, ils mettent à jour uniquement quand il est contraint à restaurer, nettoyer, régénérer ou modifier `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7224a-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7224a-125">sources de référentiel NuGet.org deviennent n’est plus dans une configuration de projet lorsque vous utilisez l’interface de configuration NuGet.</span><span class="sxs-lookup"><span data-stu-id="7224a-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7224a-126">NuGet n’est plus restaure les packages dans les projets partagés écritures, ni un fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="7224a-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7224a-127">Nous avez amélioré de défaillance du réseau et recommencez la gestion des serveurs inaccessibles ou lente à répondre.</span><span class="sxs-lookup"><span data-stu-id="7224a-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7224a-128">Les comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.</span><span class="sxs-lookup"><span data-stu-id="7224a-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7224a-129">Nous prennent désormais en charge la dernière version `project.json` schéma de DNX.</span><span class="sxs-lookup"><span data-stu-id="7224a-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="7224a-130">Modifications avec rupture</span><span class="sxs-lookup"><span data-stu-id="7224a-130">Breaking Changes</span></span>

* <span data-ttu-id="7224a-131">Les numéros de version de package sont désormais normalisés au format *majeure*. *mineure*. *correctif*-*préliminaire* chacune de majeure, mineure et de correctif logiciel sont traitées en tant qu’entiers et supprimer les zéros non significatifs.</span><span class="sxs-lookup"><span data-stu-id="7224a-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="7224a-132">Les informations de version préliminaire sont traitées comme une chaîne et aucune modification lui n’est appliquées.</span><span class="sxs-lookup"><span data-stu-id="7224a-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="7224a-133">Ces nombres sont utilisés dans les requêtes par les clients NuGet et la recherche fournies par le service nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7224a-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="7224a-134">Vous trouverez plus de détails dans la documentation de NuGet sous [Versions de la version préliminaire](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7224a-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="7224a-135">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="7224a-135">Known Issues</span></span>

* <span data-ttu-id="7224a-136">**Problème :** Windows 10 v1511 utilisateurs peuvent rencontrer des problèmes ou même un blocage de Visual Studio avec Powershell dans Visual Studio dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="7224a-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="7224a-137">L’installation / désinstallation des packages qui ont install.ps1 / uninstall.ps1 scripts</span><span class="sxs-lookup"><span data-stu-id="7224a-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="7224a-138">Le chargement des projets qui ont un script init.ps1 (comme EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="7224a-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="7224a-139">Publication de contenu web</span><span class="sxs-lookup"><span data-stu-id="7224a-139">Publishing web content</span></span>

* <span data-ttu-id="7224a-140">**Solution de contournement :** vous assurer que votre installation de Windows 10 a les derniers correctifs appliqués, spécialement le janvier 2016 (KB 3124263) ou une mise à jour ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7224a-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="7224a-141">Plus de détails sont disponibles sur [problème GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="7224a-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="7224a-142">**Problème :** Les redirections du protocole NuGet v2 sont rompues.</span><span class="sxs-lookup"><span data-stu-id="7224a-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="7224a-143">Les dépôts NuGet personnalisés qui redirigent les demandes vers un autre hôte n’honorent pas ces demandes.</span><span class="sxs-lookup"><span data-stu-id="7224a-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="7224a-144">**Solution de contournement :** pour contourner ce problème, configurez l’URI de dépôt de packages dans les paramètres pour pointer vers l’emplacement de serveur redirigé.</span><span class="sxs-lookup"><span data-stu-id="7224a-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="7224a-145">Pour plus d’informations, consultez [requête de tirage GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="7224a-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="7224a-146">Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7224a-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>