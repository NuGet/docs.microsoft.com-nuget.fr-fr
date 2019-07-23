---
title: Notes de publication de NuGet 3,3
description: Notes de publication de NuGet 3,3, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317041"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="83cdc-103">Notes de publication de NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="83cdc-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="83cdc-104">[Notes de publication de NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [-notes de publication de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="83cdc-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="83cdc-105">NuGet 3,3 a été publié le 30 novembre, 2015 avec un nombre important de mises à jour de l’interface utilisateur et de fonctionnalités de ligne de commande, ainsi qu’une collection de correctifs utiles pour les clients NuGet.</span><span class="sxs-lookup"><span data-stu-id="83cdc-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="83cdc-106">Nouvelles fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="83cdc-106">New Features</span></span>

* <span data-ttu-id="83cdc-107">Des fournisseurs d’informations d’identification ont été introduits, qui permettent aux clients de ligne de commande NuGet de fonctionner de manière transparente avec un flux authentifié.</span><span class="sxs-lookup"><span data-stu-id="83cdc-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="83cdc-108">Les [instructions relatives à l’installation du fournisseur d’informations d’identification Visual Studio Team Services](../api/nuget-exe-credential-providers.md) et à la configuration des clients NuGet pour l’utiliser sont disponibles sur les documents NuGet.</span><span class="sxs-lookup"><span data-stu-id="83cdc-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="83cdc-109">Nouvelles fonctionnalités de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="83cdc-109">New User Interface Features</span></span>

* <span data-ttu-id="83cdc-110">Séparer les onglets disponibles parcourir, installer et mettre à jour</span><span class="sxs-lookup"><span data-stu-id="83cdc-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="83cdc-111">Badge des mises à jour disponibles indiquant le nombre de packages avec des mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="83cdc-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="83cdc-112">Badges de package dans la liste des packages pour indiquer si le package est installé ou si une mise à jour est disponible</span><span class="sxs-lookup"><span data-stu-id="83cdc-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="83cdc-113">Nombre de téléchargements et auteur ajoutés à la liste des packages</span><span class="sxs-lookup"><span data-stu-id="83cdc-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="83cdc-114">Numéro de version disponible le plus élevé et numéro de version actuellement installé dans la liste des packages</span><span class="sxs-lookup"><span data-stu-id="83cdc-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="83cdc-115">Boutons d’action pour permettre l’installation, la mise à jour et la désinstallation rapides dans la liste des packages</span><span class="sxs-lookup"><span data-stu-id="83cdc-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="83cdc-116">Boutons d’action plus clairs dans le panneau Détails du package</span><span class="sxs-lookup"><span data-stu-id="83cdc-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="83cdc-117">Date de mise à jour du package dans le panneau Détails du package</span><span class="sxs-lookup"><span data-stu-id="83cdc-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="83cdc-118">Panneau consolider dans la vue solution</span><span class="sxs-lookup"><span data-stu-id="83cdc-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="83cdc-119">Grille pouvant être triée des projets et numéros de version installés dans la vue de la solution</span><span class="sxs-lookup"><span data-stu-id="83cdc-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="83cdc-120">Nouvelles fonctionnalités de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="83cdc-120">New Command-line Features</span></span>

<span data-ttu-id="83cdc-121">Dans cette version, nous avons `add` introduit `init` les commandes et pour initialiser les référentiels basés sur des dossiers, comme décrit dans la [référence de NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="83cdc-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="83cdc-122">Les référentiels construits et gérés avec cette structure de dossiers offrent des [avantages significatifs](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) en matière de performances, comme indiqué sur notre blog.</span><span class="sxs-lookup"><span data-stu-id="83cdc-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="83cdc-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="83cdc-123">ContentFiles</span></span>

<span data-ttu-id="83cdc-124">Le contenu est désormais pris `project.json` en charge dans les projets `contentFiles` managés par le biais de la nouvelle notation de dossier et `.nuspec` `contentFiles` d’élément.</span><span class="sxs-lookup"><span data-stu-id="83cdc-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="83cdc-125">Ce contenu peut être spécifié plus directement par l’auteur du package pour les interactions avec les systèmes de projet.</span><span class="sxs-lookup"><span data-stu-id="83cdc-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="83cdc-126">Vous trouverez plus d’informations sur la configuration de `.nuspec` contentFiles dans un document dans la [référence. NuSpec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="83cdc-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="83cdc-127">Gestion du cache des variables locales NuGet</span><span class="sxs-lookup"><span data-stu-id="83cdc-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="83cdc-128">La ligne de commande NuGet a été mise à jour pour inclure des informations sur la gestion des caches locaux sur une station de travail.</span><span class="sxs-lookup"><span data-stu-id="83cdc-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="83cdc-129">Vous trouverez plus d’informations sur la commande variables locales dans la référence de la [ligne de commande NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="83cdc-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="83cdc-130">Problèmes résolus</span><span class="sxs-lookup"><span data-stu-id="83cdc-130">Fixed Issues</span></span>

<span data-ttu-id="83cdc-131">**Problèmes notables**</span><span class="sxs-lookup"><span data-stu-id="83cdc-131">**Notable Issues**</span></span>

* <span data-ttu-id="83cdc-132">Prise en charge de la restauration de la ligne de commande NuGet pour la restauration de packages avec un fichier solution sur mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="83cdc-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="83cdc-133">La liste complète des problèmes qui ont été résolus dans la version 3,3 se trouve sur GitHub, sous la [étape majeure de 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="83cdc-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="83cdc-134">La liste des problèmes corrigés dans la version de ligne de commande 3,3 est enregistrée dans le [jalon de ligne de commande 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="83cdc-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="83cdc-135">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="83cdc-135">Known Issues</span></span>

<span data-ttu-id="83cdc-136">Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="83cdc-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>