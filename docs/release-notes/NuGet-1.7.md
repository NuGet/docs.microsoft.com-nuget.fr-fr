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
# <a name="nuget-17-release-notes"></a>Notes de publication de NuGet 1,7

Notes de publication de [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Notes de publication de NuGet 1,8](../release-notes/nuget-1.8.md)

NuGet 1,7 a été publié le 4 avril 2012.

## <a name="known-installation-issue"></a>Problème d’installation connu
Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.

La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.  Consultez la rubrique <https://support.microsoft.com/kb/2581019> (éventuellement en anglais) pour plus d'informations.

Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».

## <a name="features"></a>Fonctionnalités

### <a name="support-opening-readmetxt-file-after-installation"></a>Prendre en charge l’ouverture d' readme.txt fichier après l’installation
Nouveauté de 1,7, si votre package contient un `readme.txt` fichier à la racine du package, NuGet ouvre automatiquement ce fichier une fois que l’installation de votre package est terminée.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Afficher les packages de version préliminaire dans la boîte de dialogue gérer les packages NuGet
La boîte de dialogue gérer les packages NuGet inclut désormais une liste déroulante qui fournit l’option permettant d’afficher les packages de version préliminaire.

![Présentation des packages de version préliminaire](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Afficher le bouton de restauration de package lorsque des fichiers de package sont manquants
Lorsque vous ouvrez la console du gestionnaire de package ou la boîte de dialogue packages NuGet du gestionnaire, NuGet vérifie si la solution actuelle a activé le mode de restauration de package et si des fichiers de package sont absents du `packages` dossier. Si ces deux conditions sont remplies, NuGet vous en informe et affiche un bouton de restauration pratique. Le fait de cliquer sur ce bouton déclenche NuGet pour restaurer tous les packages manquants.

![Bouton restauration du package dans la boîte de dialogue](./media/packagerestore-dialog.png)

![Bouton de restauration de package sur la console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Ajouter un fichier de packages.config au niveau de la solution
Dans les versions précédentes de NuGet, chaque projet a un `packages.config` fichier qui effectue le suivi des packages NuGet installés dans ce projet. Toutefois, il n’existait aucun fichier similaire au niveau de la solution pour effectuer le suivi des packages au niveau de la solution. Par conséquent, il n’existait aucun moyen de restaurer des packages au niveau de la solution.
Cette fonctionnalité est désormais implémentée dans NuGet 1,7. Le fichier au niveau de la solution `packages.config` est placé sous le `.nuget` dossier sous la racine de la solution et stocke uniquement les packages au niveau de la solution.

### <a name="remove-new-package-command"></a>Commande supprimer New-Package
En raison d’une faible utilisation, la commande New-Package a été supprimée. Il est recommandé aux développeurs d’utiliser nuget.exe ou l’Explorateur de packages NuGet pratique pour créer des packages.

## <a name="bug-fixes"></a>Résolutions de bogues
NuGet 1,7 a corrigé de nombreux bogues autour du flux de travail de restauration des packages et des scénarios de contrôle du réseau/de la source.

Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,7, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
