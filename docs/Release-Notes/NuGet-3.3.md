---
title: Notes de publication NuGet 3.3 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notes de publication pour 3.3 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
keywords: Notes de version 3.3 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ab5e1ca550297c608017cb56dff32f4bd4bbb885
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="a30b2-104">Notes de version 3.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="a30b2-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="a30b2-105">[Notes de publication NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [Notes de NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a30b2-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="a30b2-106">3.3 de NuGet a été publiée le 30 novembre 2015 avec un nombre important de l’interface d’utilisateur mises à jour et des fonctionnalités de ligne de commande ainsi un ensemble de corrections utiles aux clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="a30b2-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="a30b2-107">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="a30b2-107">New Features</span></span>

* <span data-ttu-id="a30b2-108">Les fournisseurs d’informations d’identification ont été introduites qui permettent aux clients de ligne de commande de NuGet être en mesure de fonctionner de manière transparente avec un flux authentifié.</span><span class="sxs-lookup"><span data-stu-id="a30b2-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="a30b2-109">[Fournisseur des informations d’identification des instructions sur la façon d’installer Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) et configurer NuGet à disposition des clients sont disponibles sur NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="a30b2-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a30b2-110">Nouvelles fonctionnalités de l’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="a30b2-110">New User Interface Features</span></span>

* <span data-ttu-id="a30b2-111">Onglets séparés de parcourir, installé et mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="a30b2-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="a30b2-112">Met à jour de badge disponible indiquant le nombre de packages avec des mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="a30b2-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="a30b2-113">Badges de package dans la liste des packages pour indiquer si le package est installé, ou une mise à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="a30b2-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="a30b2-114">Télécharger le nombre et l’auteur ajouté à la liste des packages</span><span class="sxs-lookup"><span data-stu-id="a30b2-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="a30b2-115">Numéro de version disponible la plus élevée et le numéro de version actuellement installée sur la liste des packages</span><span class="sxs-lookup"><span data-stu-id="a30b2-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="a30b2-116">Boutons d’action pour autoriser l’installation rapide, mettre à jour et désinstaller à partir de la liste des packages</span><span class="sxs-lookup"><span data-stu-id="a30b2-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="a30b2-117">Boutons d’action plus claire dans le volet de détails du package</span><span class="sxs-lookup"><span data-stu-id="a30b2-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="a30b2-118">Date de mise à jour de package dans le volet de détails du package</span><span class="sxs-lookup"><span data-stu-id="a30b2-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="a30b2-119">Consolider le panneau de configuration dans la vue de la Solution</span><span class="sxs-lookup"><span data-stu-id="a30b2-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="a30b2-120">Grille pouvant être trié de projets et les numéros de version installée sur la vue de la solution</span><span class="sxs-lookup"><span data-stu-id="a30b2-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="a30b2-121">Nouvelles fonctionnalités de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="a30b2-121">New Command-line Features</span></span>

<span data-ttu-id="a30b2-122">Dans cette version, nous avons présenté la `add` et `init` commandes pour initialiser les référentiels basés sur le dossier comme décrit dans la [nuget.exe référence](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a30b2-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="a30b2-123">Les dépôts qui sont créés et conservés dans ce dossier de la structure sera [offrent des avantages de performances significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) comme indiqué sur notre blog.</span><span class="sxs-lookup"><span data-stu-id="a30b2-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="a30b2-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="a30b2-124">ContentFiles</span></span>

<span data-ttu-id="a30b2-125">Le contenu est désormais prise en charge dans `project.json` géré des projets à partir de la nouvelle `contentFiles` dossier et `.nuspec` `contentFiles` notation de l’élément.</span><span class="sxs-lookup"><span data-stu-id="a30b2-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="a30b2-126">Ce contenu peut être spécifié directement par l’auteur du package pour les interactions avec les systèmes de projet.</span><span class="sxs-lookup"><span data-stu-id="a30b2-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="a30b2-127">Plus d’informations sur la configuration des fichiers dans un `.nuspec` document se trouve dans le [.nuspec référence](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="a30b2-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="a30b2-128">Gestion de Cache de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="a30b2-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="a30b2-129">NuGet de ligne de commande a été mis à jour pour inclure des informations sur la façon de gérer les caches locales sur une station de travail.</span><span class="sxs-lookup"><span data-stu-id="a30b2-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="a30b2-130">Plus d’informations sur la commande de variables locales est disponible dans le [référence de ligne de commande de NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="a30b2-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="a30b2-131">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a30b2-131">Fixed Issues</span></span>

<span data-ttu-id="a30b2-132">**Problèmes importants**</span><span class="sxs-lookup"><span data-stu-id="a30b2-132">**Notable Issues**</span></span>

* <span data-ttu-id="a30b2-133">Les packages NuGet de ligne de commande restaurée prise en charge pour la restauration avec un fichier de solution sur Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="a30b2-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="a30b2-134">Vous trouverez la liste complète des problèmes qui ont été traités dans la version 3.3 sur GitHub sous le [jalon 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="a30b2-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="a30b2-135">La liste des problèmes corrigés dans la version de ligne de commande 3.3 sont enregistrés dans le [3.3 jalon de ligne de commande](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="a30b2-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="a30b2-136">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="a30b2-136">Known Issues</span></span>

<span data-ttu-id="a30b2-137">Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a30b2-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>