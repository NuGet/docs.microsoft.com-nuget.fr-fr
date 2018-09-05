---
title: Notes de publication NuGet 3.3
description: Notes de version de NuGet 3.3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546645"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="578fb-103">Notes de publication NuGet 3.3</span><span class="sxs-lookup"><span data-stu-id="578fb-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="578fb-104">[Notes de publication NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [Notes de publication NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="578fb-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="578fb-105">NuGet 3.3 a été publiée le 30 novembre 2015 avec un nombre important de mises à jour d’interface utilisateur et des fonctionnalités de ligne de commande mais aussi un ensemble de correctifs utiles aux clients de NuGet.</span><span class="sxs-lookup"><span data-stu-id="578fb-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="578fb-106">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="578fb-106">New Features</span></span>

* <span data-ttu-id="578fb-107">Les fournisseurs d’informations d’identification ont été introduites qui permettent aux clients de ligne de commande de NuGet pouvoir travailler en toute transparence avec un flux authentifié.</span><span class="sxs-lookup"><span data-stu-id="578fb-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="578fb-108">[Obtenir des instructions sur l’installation de Visual Studio Team Services d’informations d’identification de fournisseur ](../api/nuget-exe-credential-providers.md) et configurer le package NuGet à disposition des clients sont disponibles sur NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="578fb-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="578fb-109">Nouvelles fonctionnalités d’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="578fb-109">New User Interface Features</span></span>

* <span data-ttu-id="578fb-110">Onglets distincts de parcourir, installé et les mises à jour disponible</span><span class="sxs-lookup"><span data-stu-id="578fb-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="578fb-111">Met à jour disponible badge indiquant le nombre de packages avec des mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="578fb-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="578fb-112">Badges de package dans la liste des packages pour indiquer si le package est installé ou a une mise à jour disponible</span><span class="sxs-lookup"><span data-stu-id="578fb-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="578fb-113">Télécharger le nombre et l’auteur a ajoutés à la liste des packages</span><span class="sxs-lookup"><span data-stu-id="578fb-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="578fb-114">Numéro de version disponible la plus élevée et le numéro de version actuellement installée sur la liste des packages</span><span class="sxs-lookup"><span data-stu-id="578fb-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="578fb-115">Boutons d’action pour autoriser l’installation rapide, mettre à jour et désinstaller à partir de la liste des packages</span><span class="sxs-lookup"><span data-stu-id="578fb-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="578fb-116">Boutons d’action plus claire dans le volet de détails du package</span><span class="sxs-lookup"><span data-stu-id="578fb-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="578fb-117">Date de mise à jour de package dans le volet de détails du package</span><span class="sxs-lookup"><span data-stu-id="578fb-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="578fb-118">Consolider le panneau de configuration dans la vue de la Solution</span><span class="sxs-lookup"><span data-stu-id="578fb-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="578fb-119">Grille triable de projets et les numéros des versions installées sur la vue de la solution</span><span class="sxs-lookup"><span data-stu-id="578fb-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="578fb-120">Nouvelles fonctionnalités de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="578fb-120">New Command-line Features</span></span>

<span data-ttu-id="578fb-121">Dans cette version, nous avons introduit la `add` et `init` commandes pour initialiser des référentiels basés sur le dossier comme décrit dans la [nuget.exe référence](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="578fb-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="578fb-122">Les dépôts qui sont conçus et entretenus avec ce dossier structure sera [offrent les avantages de performances significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) comme indiqué sur notre blog.</span><span class="sxs-lookup"><span data-stu-id="578fb-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="578fb-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="578fb-123">ContentFiles</span></span>

<span data-ttu-id="578fb-124">Contenu est désormais pris en charge `project.json` gérés projets via la nouvelle `contentFiles` dossier et `.nuspec` `contentFiles` notation de l’élément.</span><span class="sxs-lookup"><span data-stu-id="578fb-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="578fb-125">Ce contenu peut être spécifié plus directement par l’auteur du package pour les interactions avec les systèmes de projet.</span><span class="sxs-lookup"><span data-stu-id="578fb-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="578fb-126">Plus d’informations sur la configuration de contentFiles dans un `.nuspec` document se trouve dans le [.nuspec référence](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="578fb-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="578fb-127">Gestion de Cache de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="578fb-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="578fb-128">Le package NuGet de ligne de commande a été mis à jour pour inclure des informations sur la façon de gérer les caches locaux sur une station de travail.</span><span class="sxs-lookup"><span data-stu-id="578fb-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="578fb-129">Plus d’informations sur la commande de variables locales sont disponibles dans le [référence de ligne de commande NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="578fb-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="578fb-130">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="578fb-130">Fixed Issues</span></span>

<span data-ttu-id="578fb-131">**Problèmes notables**</span><span class="sxs-lookup"><span data-stu-id="578fb-131">**Notable Issues**</span></span>

* <span data-ttu-id="578fb-132">NuGet en ligne de commande restaurée prise en charge pour la restauration de packages avec un fichier de solution sur Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="578fb-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="578fb-133">Vous trouverez la liste complète des problèmes qui ont été traités dans la version 3.3 sur GitHub sous le [jalon 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="578fb-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="578fb-134">La liste des problèmes corrigés dans la version de ligne de commande 3.3 sont enregistrés dans le [3.3 jalon de ligne de commande](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="578fb-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="578fb-135">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="578fb-135">Known Issues</span></span>

<span data-ttu-id="578fb-136">Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="578fb-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>