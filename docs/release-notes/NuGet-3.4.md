---
title: Notes de publication de NuGet 3,4
description: Notes de publication de NuGet 3,4, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776419"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="7fefd-103">Notes de publication de NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="7fefd-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="7fefd-104">Notes de publication [de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Notes de publication de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="7fefd-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="7fefd-105">NuGet 3,4 a été publié le 30 mars 2016 dans le cadre de la version préliminaire de Visual Studio 2015 Update 2 et de Visual Studio 15 preview. il a été créé avec quelques principes dans l’esprit :</span><span class="sxs-lookup"><span data-stu-id="7fefd-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="7fefd-106">Prise en charge multiplateforme</span><span class="sxs-lookup"><span data-stu-id="7fefd-106">Cross-Platform support</span></span>
* <span data-ttu-id="7fefd-107">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="7fefd-107">Performance improvements</span></span>
* <span data-ttu-id="7fefd-108">Améliorations mineures de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7fefd-108">Minor UI improvements</span></span>

<span data-ttu-id="7fefd-109">Les fonctionnalités suivantes ont été précédemment ajoutées à la version RC et ont été mises à jour ou terminées pour la version 3,4 :</span><span class="sxs-lookup"><span data-stu-id="7fefd-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="7fefd-110">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="7fefd-110">New Features</span></span>

* <span data-ttu-id="7fefd-111">Les clients NuGet prennent désormais en charge l’encodage de contenu gzip à partir des référentiels</span><span class="sxs-lookup"><span data-stu-id="7fefd-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7fefd-112">Prise en charge des fichiers PDB des packages dans les projets xproj</span><span class="sxs-lookup"><span data-stu-id="7fefd-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7fefd-113">Prise en charge des actions de génération iOS et Android dans l’élément contentFiles</span><span class="sxs-lookup"><span data-stu-id="7fefd-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7fefd-114">Prise en charge des monikers netstandard et nestandardapp Framework</span><span class="sxs-lookup"><span data-stu-id="7fefd-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7fefd-115">Nouvelles fonctionnalités de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="7fefd-115">New User Interface Features</span></span>

* <span data-ttu-id="7fefd-116">Amélioration significative des performances, en particulier sur les onglets installé, mises à jour et consolider</span><span class="sxs-lookup"><span data-stu-id="7fefd-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7fefd-117">La source de l’agrégat « toutes les sources de package » est disponible avec une fusion des résultats de recherche appropriée</span><span class="sxs-lookup"><span data-stu-id="7fefd-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="7fefd-118">Les onglets installé et mis à jour sont désormais triés par ordre alphabétique</span><span class="sxs-lookup"><span data-stu-id="7fefd-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7fefd-119">Ajout d’un bouton d’actualisation permettant d’actualiser une recherche</span><span class="sxs-lookup"><span data-stu-id="7fefd-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="7fefd-120">Dernières options de build en haut de la liste des versions</span><span class="sxs-lookup"><span data-stu-id="7fefd-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7fefd-121">Mises à jour et améliorations</span><span class="sxs-lookup"><span data-stu-id="7fefd-121">Updates and Improvements</span></span>

* <span data-ttu-id="7fefd-122">Les packages référencés dans `project.json` et qui ont une version flottante ne sont pas mis à jour sur chaque Build.</span><span class="sxs-lookup"><span data-stu-id="7fefd-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7fefd-123">Au lieu de cela, ils sont mis à jour uniquement lorsqu’ils sont forcés à restaurer, nettoyer, régénérer ou modifier `project.json` .</span><span class="sxs-lookup"><span data-stu-id="7fefd-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7fefd-124">les sources de référentiel nuget.org ne sont plus contraints dans une configuration de projet lorsque vous utilisez l’interface utilisateur de configuration de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7fefd-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7fefd-125">NuGet ne restaure plus les packages dans les projets partagés et n’écrit pas de fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="7fefd-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7fefd-126">Nous avons amélioré les défaillances du réseau et les tentatives de traitement des serveurs inaccessibles ou lents à répondre.</span><span class="sxs-lookup"><span data-stu-id="7fefd-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7fefd-127">Les comportements du clavier et de la souris sont améliorés dans l’interface utilisateur du gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7fefd-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7fefd-128">Nous prenons maintenant en charge le schéma le plus récent `project.json` dans DNX.</span><span class="sxs-lookup"><span data-stu-id="7fefd-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="7fefd-129">Dernières modifications</span><span class="sxs-lookup"><span data-stu-id="7fefd-129">Breaking Changes</span></span>

* <span data-ttu-id="7fefd-130">Les numéros de version de package sont maintenant normalisés au format *major*. *mineure*. *correctif logiciel* - *version préliminaire*   Chacune des valeurs majeures, minor et patch est traitée comme des entiers et supprime les zéros non significatifs.</span><span class="sxs-lookup"><span data-stu-id="7fefd-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="7fefd-131">Les informations de préversion sont traitées comme une chaîne et aucune modification n’est appliquée à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="7fefd-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="7fefd-132">Ces nombres sont utilisés dans les requêtes des clients NuGet et de la recherche fournie par le service nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7fefd-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="7fefd-133">Vous trouverez plus de détails dans les documents NuGet, sous les [versions préliminaires](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7fefd-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="7fefd-134">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="7fefd-134">Known Issues</span></span>

* <span data-ttu-id="7fefd-135">**Problème :** Les utilisateurs de Windows 10 v1511 inclut peuvent rencontrer des problèmes ou même un blocage de Visual Studio avec PowerShell dans Visual Studio dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="7fefd-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="7fefd-136">Installation/désinstallation de packages avec des scripts install.ps1/uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="7fefd-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="7fefd-137">Chargement de projets qui ont un script init.ps1 (comme EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="7fefd-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="7fefd-138">Publication de contenu Web</span><span class="sxs-lookup"><span data-stu-id="7fefd-138">Publishing web content</span></span>

* <span data-ttu-id="7fefd-139">**Solution de contournement :** Vérifiez que les derniers correctifs sont appliqués à votre installation de Windows 10, expecially le 2016 janvier (KB 3124263) ou une mise à jour ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7fefd-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="7fefd-140">Plus de détails sont disponibles sur le [problème GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="7fefd-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="7fefd-141">**Problème :** Les redirections du protocole NuGet v2 sont rompues.</span><span class="sxs-lookup"><span data-stu-id="7fefd-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="7fefd-142">Les dépôts NuGet personnalisés qui redirigent les demandes vers un autre hôte n’honorent pas ces demandes.</span><span class="sxs-lookup"><span data-stu-id="7fefd-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="7fefd-143">**Solution de contournement :**  Pour contourner ce problème, configurez l’URI du référentiel de packages dans les paramètres de façon à ce qu’il pointe vers l’emplacement du serveur Redirigé.</span><span class="sxs-lookup"><span data-stu-id="7fefd-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="7fefd-144">Pour plus d’informations, consultez [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="7fefd-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="7fefd-145">Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7fefd-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>