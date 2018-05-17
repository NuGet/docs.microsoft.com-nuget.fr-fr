---
title: Notes de version 3.3 de NuGet
description: Notes de publication pour 3.3 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="4ff7b-103">Notes de version 3.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="4ff7b-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="4ff7b-104">[Notes de publication NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [Notes de NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="4ff7b-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="4ff7b-105">3.3 de NuGet a été publiée le 30 novembre 2015 avec un nombre important de l’interface d’utilisateur mises à jour et des fonctionnalités de ligne de commande ainsi un ensemble de corrections utiles aux clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="4ff7b-106">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="4ff7b-106">New Features</span></span>

* <span data-ttu-id="4ff7b-107">Les fournisseurs d’informations d’identification ont été introduites qui permettent aux clients de ligne de commande de NuGet être en mesure de fonctionner de manière transparente avec un flux authentifié.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="4ff7b-108">[Fournisseur des informations d’identification des instructions sur la façon d’installer Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) et configurer NuGet à disposition des clients sont disponibles sur NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="4ff7b-109">Nouvelles fonctionnalités de l’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="4ff7b-109">New User Interface Features</span></span>

* <span data-ttu-id="4ff7b-110">Onglets séparés de parcourir, installé et mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="4ff7b-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="4ff7b-111">Met à jour de badge disponible indiquant le nombre de packages avec des mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="4ff7b-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="4ff7b-112">Badges de package dans la liste des packages pour indiquer si le package est installé, ou une mise à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="4ff7b-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="4ff7b-113">Télécharger le nombre et l’auteur ajouté à la liste des packages</span><span class="sxs-lookup"><span data-stu-id="4ff7b-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="4ff7b-114">Numéro de version disponible la plus élevée et le numéro de version actuellement installée sur la liste des packages</span><span class="sxs-lookup"><span data-stu-id="4ff7b-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="4ff7b-115">Boutons d’action pour autoriser l’installation rapide, mettre à jour et désinstaller à partir de la liste des packages</span><span class="sxs-lookup"><span data-stu-id="4ff7b-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="4ff7b-116">Boutons d’action plus claire dans le volet de détails du package</span><span class="sxs-lookup"><span data-stu-id="4ff7b-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="4ff7b-117">Date de mise à jour de package dans le volet de détails du package</span><span class="sxs-lookup"><span data-stu-id="4ff7b-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="4ff7b-118">Consolider le panneau de configuration dans la vue de la Solution</span><span class="sxs-lookup"><span data-stu-id="4ff7b-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="4ff7b-119">Grille pouvant être trié de projets et les numéros de version installée sur la vue de la solution</span><span class="sxs-lookup"><span data-stu-id="4ff7b-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="4ff7b-120">Nouvelles fonctionnalités de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="4ff7b-120">New Command-line Features</span></span>

<span data-ttu-id="4ff7b-121">Dans cette version, nous avons présenté la `add` et `init` commandes pour initialiser les référentiels basés sur le dossier comme décrit dans la [nuget.exe référence](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="4ff7b-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="4ff7b-122">Les dépôts qui sont créés et conservés dans ce dossier de la structure sera [offrent des avantages de performances significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) comme indiqué sur notre blog.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="4ff7b-123">Fichiers</span><span class="sxs-lookup"><span data-stu-id="4ff7b-123">ContentFiles</span></span>

<span data-ttu-id="4ff7b-124">Le contenu est désormais prise en charge dans `project.json` géré des projets à partir de la nouvelle `contentFiles` dossier et `.nuspec` `contentFiles` notation de l’élément.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="4ff7b-125">Ce contenu peut être spécifié directement par l’auteur du package pour les interactions avec les systèmes de projet.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="4ff7b-126">Plus d’informations sur la configuration des fichiers dans un `.nuspec` document se trouve dans le [.nuspec référence](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="4ff7b-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="4ff7b-127">Gestion de Cache de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="4ff7b-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="4ff7b-128">NuGet de ligne de commande a été mis à jour pour inclure des informations sur la façon de gérer les caches locales sur une station de travail.</span><span class="sxs-lookup"><span data-stu-id="4ff7b-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="4ff7b-129">Plus d’informations sur la commande de variables locales est disponible dans le [référence de ligne de commande de NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="4ff7b-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="4ff7b-130">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="4ff7b-130">Fixed Issues</span></span>

<span data-ttu-id="4ff7b-131">**Problèmes importants**</span><span class="sxs-lookup"><span data-stu-id="4ff7b-131">**Notable Issues**</span></span>

* <span data-ttu-id="4ff7b-132">Les packages NuGet de ligne de commande restaurée prise en charge pour la restauration avec un fichier de solution sur Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="4ff7b-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="4ff7b-133">Vous trouverez la liste complète des problèmes qui ont été traités dans la version 3.3 sur GitHub sous le [jalon 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="4ff7b-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="4ff7b-134">La liste des problèmes corrigés dans la version de ligne de commande 3.3 sont enregistrés dans le [3.3 jalon de ligne de commande](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="4ff7b-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="4ff7b-135">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="4ff7b-135">Known Issues</span></span>

<span data-ttu-id="4ff7b-136">Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="4ff7b-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>