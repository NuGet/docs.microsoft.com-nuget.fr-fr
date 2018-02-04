---
title: Notes de publication NuGet 1.7 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 1.7 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.7 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="25ca1-104">Notes de version 1.7 de NuGet</span><span class="sxs-lookup"><span data-stu-id="25ca1-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="25ca1-105">[Notes de publication NuGet 1.6](../release-notes/nuget-1.6.md) | [Notes de version 1.8 de NuGet](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="25ca1-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="25ca1-106">NuGet 1.7 a été publiée le 4 avril 2012.</span><span class="sxs-lookup"><span data-stu-id="25ca1-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="25ca1-107">Problème connu d’Installation</span><span class="sxs-lookup"><span data-stu-id="25ca1-107">Known Installation Issue</span></span>
<span data-ttu-id="25ca1-108">Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.</span><span class="sxs-lookup"><span data-stu-id="25ca1-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="25ca1-109">La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25ca1-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="25ca1-110">Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="25ca1-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="25ca1-111">Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="25ca1-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="25ca1-112">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="25ca1-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="25ca1-113">Prise en charge de l’ouverture du fichier Lisezmoi.txt après l’installation</span><span class="sxs-lookup"><span data-stu-id="25ca1-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="25ca1-114">Nouveau dans 1.7, si votre package inclut un `readme.txt` fichier à la racine du package, NuGet s’ouvre automatiquement ce fichier après avoir terminé l’installation de votre package.</span><span class="sxs-lookup"><span data-stu-id="25ca1-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="25ca1-115">Afficher les versions préliminaires des packages dans la boîte de dialogue Gérer NuGet packages</span><span class="sxs-lookup"><span data-stu-id="25ca1-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="25ca1-116">La boîte de dialogue Gérer les Packages NuGet inclut désormais une liste déroulante qui permet d’afficher les versions préliminaires des packages.</span><span class="sxs-lookup"><span data-stu-id="25ca1-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Affichage des versions préliminaires des packages](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="25ca1-118">Afficher le bouton de restauration des packages lorsque les fichiers de package sont manquants</span><span class="sxs-lookup"><span data-stu-id="25ca1-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="25ca1-119">Lorsque vous ouvrez la console du Gestionnaire de Package ou le gestionnaire NuGet packages boîte de dialogue, NuGet vérifie si la solution actuelle a activé le mode de restauration des packages et si tous les fichiers de package sont absents dans le `packages` dossier.</span><span class="sxs-lookup"><span data-stu-id="25ca1-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="25ca1-120">Si ces deux conditions sont remplies, NuGet vous informera et affiche un bouton de restauration pratique.</span><span class="sxs-lookup"><span data-stu-id="25ca1-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="25ca1-121">Ce bouton déclenchera NuGet pour restaurer tous les packages manquants.</span><span class="sxs-lookup"><span data-stu-id="25ca1-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Bouton de restauration de package dans la boîte de dialogue](./media/packagerestore-dialog.png)

![Bouton de restauration de package sur la console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="25ca1-124">Ajouter le fichier packages.config de niveau de la solution</span><span class="sxs-lookup"><span data-stu-id="25ca1-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="25ca1-125">Dans les versions précédentes de NuGet, chaque projet a une `packages.config` fichier qui effectue le suivi des packages NuGet sont installés dans le projet.</span><span class="sxs-lookup"><span data-stu-id="25ca1-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="25ca1-126">Toutefois, aucun fichier similaire n’était au niveau de la solution pour effectuer le suivi des packages de solution au niveau.</span><span class="sxs-lookup"><span data-stu-id="25ca1-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="25ca1-127">Par conséquent, il n’a aucun moyen de restaurer les packages au niveau de la solution.</span><span class="sxs-lookup"><span data-stu-id="25ca1-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="25ca1-128">Cette fonctionnalité est maintenant implémentée dans NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="25ca1-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="25ca1-129">Niveau de la solution `packages.config` fichier est placé sous le `.nuget` dossier de solution racine et stocke les packages uniquement au niveau solution.</span><span class="sxs-lookup"><span data-stu-id="25ca1-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="25ca1-130">Supprimer la commande New-Package</span><span class="sxs-lookup"><span data-stu-id="25ca1-130">Remove New-Package command</span></span>
<span data-ttu-id="25ca1-131">En raison d’une faible utilisation, la commande New-Package a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="25ca1-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="25ca1-132">Les développeurs sont recommandées pour utiliser nuget.exe ou l’Explorateur de Package NuGet pratique pour créer des packages.</span><span class="sxs-lookup"><span data-stu-id="25ca1-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="25ca1-133">Correctifs de bogues</span><span class="sxs-lookup"><span data-stu-id="25ca1-133">Bug Fixes</span></span>
<span data-ttu-id="25ca1-134">NuGet 1.7 a résolu le nombre de bogues autour de la restauration des packages de workflow et les scénarios de contrôle de Source/réseau.</span><span class="sxs-lookup"><span data-stu-id="25ca1-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="25ca1-135">Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.7, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="25ca1-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
