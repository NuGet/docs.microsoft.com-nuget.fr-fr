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
# <a name="nuget-17-release-notes"></a>Notes de version 1.7 de NuGet

[Notes de publication NuGet 1.6](../release-notes/nuget-1.6.md) | [Notes de version 1.8 de NuGet](../release-notes/nuget-1.8.md)

NuGet 1.7 a été publiée le 4 avril 2012.

## <a name="known-installation-issue"></a>Problème connu d’Installation
Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.

La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.  Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="features"></a>Fonctionnalités

### <a name="support-opening-readmetxt-file-after-installation"></a>Prise en charge de l’ouverture du fichier Lisezmoi.txt après l’installation
Nouveau dans 1.7, si votre package inclut un `readme.txt` fichier à la racine du package, NuGet s’ouvre automatiquement ce fichier après avoir terminé l’installation de votre package.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Afficher les versions préliminaires des packages dans la boîte de dialogue Gérer NuGet packages
La boîte de dialogue Gérer les Packages NuGet inclut désormais une liste déroulante qui permet d’afficher les versions préliminaires des packages.

![Affichage des versions préliminaires des packages](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Afficher le bouton de restauration des packages lorsque les fichiers de package sont manquants
Lorsque vous ouvrez la console du Gestionnaire de Package ou le gestionnaire NuGet packages boîte de dialogue, NuGet vérifie si la solution actuelle a activé le mode de restauration des packages et si tous les fichiers de package sont absents dans le `packages` dossier. Si ces deux conditions sont remplies, NuGet vous informera et affiche un bouton de restauration pratique. Ce bouton déclenchera NuGet pour restaurer tous les packages manquants.

![Bouton de restauration de package dans la boîte de dialogue](./media/packagerestore-dialog.png)

![Bouton de restauration de package sur la console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Ajouter le fichier packages.config de niveau de la solution
Dans les versions précédentes de NuGet, chaque projet a une `packages.config` fichier qui effectue le suivi des packages NuGet sont installés dans le projet. Toutefois, aucun fichier similaire n’était au niveau de la solution pour effectuer le suivi des packages de solution au niveau. Par conséquent, il n’a aucun moyen de restaurer les packages au niveau de la solution.
Cette fonctionnalité est maintenant implémentée dans NuGet 1.7. Niveau de la solution `packages.config` fichier est placé sous le `.nuget` dossier de solution racine et stocke les packages uniquement au niveau solution.

### <a name="remove-new-package-command"></a>Supprimer la commande New-Package
En raison d’une faible utilisation, la commande New-Package a été supprimée. Les développeurs sont recommandées pour utiliser nuget.exe ou l’Explorateur de Package NuGet pratique pour créer des packages.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.7 a résolu le nombre de bogues autour de la restauration des packages de workflow et les scénarios de contrôle de Source/réseau.

Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.7, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
