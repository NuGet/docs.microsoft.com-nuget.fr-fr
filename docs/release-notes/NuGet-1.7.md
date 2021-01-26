---
title: Notes de publication de NuGet 1,7
description: Notes de publication de NuGet 1,7, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777071"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="a3ce2-103">Notes de publication de NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="a3ce2-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="a3ce2-104">Notes de publication de [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Notes de publication de NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="a3ce2-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="a3ce2-105">NuGet 1,7 a été publié le 4 avril 2012.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a3ce2-106">Problème d’installation connu</span><span class="sxs-lookup"><span data-stu-id="a3ce2-106">Known Installation Issue</span></span>
<span data-ttu-id="a3ce2-107">Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a3ce2-108">La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a3ce2-109">Consultez la rubrique <https://support.microsoft.com/kb/2581019> (éventuellement en anglais) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="a3ce2-110">Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="a3ce2-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="a3ce2-111">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="a3ce2-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="a3ce2-112">Prendre en charge l’ouverture d' readme.txt fichier après l’installation</span><span class="sxs-lookup"><span data-stu-id="a3ce2-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="a3ce2-113">Nouveauté de 1,7, si votre package contient un `readme.txt` fichier à la racine du package, NuGet ouvre automatiquement ce fichier une fois que l’installation de votre package est terminée.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="a3ce2-114">Afficher les packages de version préliminaire dans la boîte de dialogue gérer les packages NuGet</span><span class="sxs-lookup"><span data-stu-id="a3ce2-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="a3ce2-115">La boîte de dialogue gérer les packages NuGet inclut désormais une liste déroulante qui fournit l’option permettant d’afficher les packages de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Présentation des packages de version préliminaire](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="a3ce2-117">Afficher le bouton de restauration de package lorsque des fichiers de package sont manquants</span><span class="sxs-lookup"><span data-stu-id="a3ce2-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="a3ce2-118">Lorsque vous ouvrez la console du gestionnaire de package ou la boîte de dialogue packages NuGet du gestionnaire, NuGet vérifie si la solution actuelle a activé le mode de restauration de package et si des fichiers de package sont absents du `packages` dossier.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="a3ce2-119">Si ces deux conditions sont remplies, NuGet vous en informe et affiche un bouton de restauration pratique.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="a3ce2-120">Le fait de cliquer sur ce bouton déclenche NuGet pour restaurer tous les packages manquants.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Bouton restauration du package dans la boîte de dialogue](./media/packagerestore-dialog.png)

![Bouton de restauration de package sur la console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="a3ce2-123">Ajouter un fichier de packages.config au niveau de la solution</span><span class="sxs-lookup"><span data-stu-id="a3ce2-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="a3ce2-124">Dans les versions précédentes de NuGet, chaque projet a un `packages.config` fichier qui effectue le suivi des packages NuGet installés dans ce projet.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="a3ce2-125">Toutefois, il n’existait aucun fichier similaire au niveau de la solution pour effectuer le suivi des packages au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="a3ce2-126">Par conséquent, il n’existait aucun moyen de restaurer des packages au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="a3ce2-127">Cette fonctionnalité est désormais implémentée dans NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="a3ce2-128">Le fichier au niveau de la solution `packages.config` est placé sous le `.nuget` dossier sous la racine de la solution et stocke uniquement les packages au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="a3ce2-129">Commande supprimer New-Package</span><span class="sxs-lookup"><span data-stu-id="a3ce2-129">Remove New-Package command</span></span>
<span data-ttu-id="a3ce2-130">En raison d’une faible utilisation, la commande New-Package a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="a3ce2-131">Il est recommandé aux développeurs d’utiliser nuget.exe ou l’Explorateur de packages NuGet pratique pour créer des packages.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a3ce2-132">Résolutions de bogues</span><span class="sxs-lookup"><span data-stu-id="a3ce2-132">Bug Fixes</span></span>
<span data-ttu-id="a3ce2-133">NuGet 1,7 a corrigé de nombreux bogues autour du flux de travail de restauration des packages et des scénarios de contrôle du réseau/de la source.</span><span class="sxs-lookup"><span data-stu-id="a3ce2-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="a3ce2-134">Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,7, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a3ce2-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
