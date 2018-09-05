---
title: Notes de publication NuGet 1.7
description: Notes de publication pour 1.7 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551465"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="03b2c-103">Notes de publication NuGet 1.7</span><span class="sxs-lookup"><span data-stu-id="03b2c-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="03b2c-104">[Notes de publication de NuGet 1.6](../release-notes/nuget-1.6.md) | [Notes de publication de NuGet 1.8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="03b2c-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="03b2c-105">NuGet 1.7 a été publiée le 4 avril 2012.</span><span class="sxs-lookup"><span data-stu-id="03b2c-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="03b2c-106">Problème d’Installation connus</span><span class="sxs-lookup"><span data-stu-id="03b2c-106">Known Installation Issue</span></span>
<span data-ttu-id="03b2c-107">Si vous exécutez Visual Studio 2010 SP1, vous pouvez rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet si vous avez une version antérieure est installée.</span><span class="sxs-lookup"><span data-stu-id="03b2c-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="03b2c-108">La solution de contournement consiste à désinstaller simplement NuGet, puis l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03b2c-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="03b2c-109">Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="03b2c-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="03b2c-110">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis vous avez probablement besoin de redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="03b2c-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="03b2c-111">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="03b2c-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="03b2c-112">Prise en charge de l’ouverture du fichier readme.txt après l’installation</span><span class="sxs-lookup"><span data-stu-id="03b2c-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="03b2c-113">Nouveautés de 1.7, si votre package comprend un `readme.txt` fichier à la racine du package, NuGet s’ouvre automatiquement ce fichier après avoir terminé l’installation de votre package.</span><span class="sxs-lookup"><span data-stu-id="03b2c-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="03b2c-114">Afficher les packages de version préliminaire dans la boîte de dialogue Gérer NuGet packages</span><span class="sxs-lookup"><span data-stu-id="03b2c-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="03b2c-115">La boîte de dialogue Gérer les Packages NuGet inclut désormais une liste déroulante qui fournit l’option pour afficher les packages de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="03b2c-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Affichage des packages de version préliminaire](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="03b2c-117">Afficher le bouton de la restauration des packages lorsque les fichiers de package sont manquants</span><span class="sxs-lookup"><span data-stu-id="03b2c-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="03b2c-118">Lorsque vous ouvrez la console du Gestionnaire de Package ou le Gestionnaire de package NuGet packages boîte de dialogue, NuGet vérifie si la solution actuelle a activé le mode de restauration des packages et si des fichiers de package sont manquants dans le `packages` dossier.</span><span class="sxs-lookup"><span data-stu-id="03b2c-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="03b2c-119">Si ces deux conditions sont remplies, NuGet vous informe et affiche un bouton pratique de la restauration.</span><span class="sxs-lookup"><span data-stu-id="03b2c-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="03b2c-120">Cliquez sur ce bouton déclenchera NuGet pour restaurer tous les packages manquants.</span><span class="sxs-lookup"><span data-stu-id="03b2c-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Bouton de restauration de package sur la boîte de dialogue](./media/packagerestore-dialog.png)

![Bouton de restauration de package sur la console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="03b2c-123">Ajouter le fichier packages.config de niveau de la solution</span><span class="sxs-lookup"><span data-stu-id="03b2c-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="03b2c-124">Dans les versions précédentes de NuGet, chaque projet a un `packages.config` fichier qui effectue le suivi de quels packages NuGet sont installés dans ce projet.</span><span class="sxs-lookup"><span data-stu-id="03b2c-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="03b2c-125">Toutefois, il n’a aucun fichier similaire au niveau de la solution pour effectuer le suivi des packages au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="03b2c-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="03b2c-126">Par conséquent, il n’existait aucun moyen de restaurer les packages au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="03b2c-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="03b2c-127">Cette fonctionnalité est maintenant implémentée dans NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="03b2c-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="03b2c-128">Niveau de la solution `packages.config` le fichier est placé sous le `.nuget` dossier sous solution racine et stockera les packages uniquement au niveau de solution.</span><span class="sxs-lookup"><span data-stu-id="03b2c-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="03b2c-129">Supprimer la commande New-Package</span><span class="sxs-lookup"><span data-stu-id="03b2c-129">Remove New-Package command</span></span>
<span data-ttu-id="03b2c-130">En raison d’une faible utilisation, la commande New-Package a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="03b2c-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="03b2c-131">Les développeurs sont recommandées pour utiliser nuget.exe ou l’Explorateur de Package NuGet pratique pour créer des packages.</span><span class="sxs-lookup"><span data-stu-id="03b2c-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="03b2c-132">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="03b2c-132">Bug Fixes</span></span>
<span data-ttu-id="03b2c-133">NuGet 1.7 a résolu plusieurs bogues autour de la restauration des packages le flux de travail et les scénarios de contrôle de Source/réseau.</span><span class="sxs-lookup"><span data-stu-id="03b2c-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="03b2c-134">Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.7, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="03b2c-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
