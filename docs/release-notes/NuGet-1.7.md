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
# <a name="nuget-17-release-notes"></a>Notes de publication NuGet 1.7

[Notes de publication de NuGet 1.6](../release-notes/nuget-1.6.md) | [Notes de publication de NuGet 1.8](../release-notes/nuget-1.8.md)

NuGet 1.7 a été publiée le 4 avril 2012.

## <a name="known-installation-issue"></a>Problème d’Installation connus
Si vous exécutez Visual Studio 2010 SP1, vous pouvez rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet si vous avez une version antérieure est installée.

La solution de contournement consiste à désinstaller simplement NuGet, puis l’installer à partir de la galerie d’extensions Visual Studio.  Pour plus d’informations, consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis vous avez probablement besoin de redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="features"></a>Fonctionnalités

### <a name="support-opening-readmetxt-file-after-installation"></a>Prise en charge de l’ouverture du fichier readme.txt après l’installation
Nouveautés de 1.7, si votre package comprend un `readme.txt` fichier à la racine du package, NuGet s’ouvre automatiquement ce fichier après avoir terminé l’installation de votre package.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Afficher les packages de version préliminaire dans la boîte de dialogue Gérer NuGet packages
La boîte de dialogue Gérer les Packages NuGet inclut désormais une liste déroulante qui fournit l’option pour afficher les packages de version préliminaire.

![Affichage des packages de version préliminaire](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Afficher le bouton de la restauration des packages lorsque les fichiers de package sont manquants
Lorsque vous ouvrez la console du Gestionnaire de Package ou le Gestionnaire de package NuGet packages boîte de dialogue, NuGet vérifie si la solution actuelle a activé le mode de restauration des packages et si des fichiers de package sont manquants dans le `packages` dossier. Si ces deux conditions sont remplies, NuGet vous informe et affiche un bouton pratique de la restauration. Cliquez sur ce bouton déclenchera NuGet pour restaurer tous les packages manquants.

![Bouton de restauration de package sur la boîte de dialogue](./media/packagerestore-dialog.png)

![Bouton de restauration de package sur la console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Ajouter le fichier packages.config de niveau de la solution
Dans les versions précédentes de NuGet, chaque projet a un `packages.config` fichier qui effectue le suivi de quels packages NuGet sont installés dans ce projet. Toutefois, il n’a aucun fichier similaire au niveau de la solution pour effectuer le suivi des packages au niveau de la solution. Par conséquent, il n’existait aucun moyen de restaurer les packages au niveau de la solution.
Cette fonctionnalité est maintenant implémentée dans NuGet 1.7. Niveau de la solution `packages.config` le fichier est placé sous le `.nuget` dossier sous solution racine et stockera les packages uniquement au niveau de solution.

### <a name="remove-new-package-command"></a>Supprimer la commande New-Package
En raison d’une faible utilisation, la commande New-Package a été supprimée. Les développeurs sont recommandées pour utiliser nuget.exe ou l’Explorateur de Package NuGet pratique pour créer des packages.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.7 a résolu plusieurs bogues autour de la restauration des packages le flux de travail et les scénarios de contrôle de Source/réseau.

Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.7, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
