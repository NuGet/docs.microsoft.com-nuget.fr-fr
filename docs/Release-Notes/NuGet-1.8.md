---
title: Notes de publication NuGet 1.8 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour 1.8 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de version 1.8 de NuGet, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e77c8a7cc2096e11571025b2a55bc6f20dfa4351
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-18-release-notes"></a>Notes de version 1.8 de NuGet

[Notes de publication NuGet 1.7](../release-notes/nuget-1.7.md) | [NuGet 2.0 Notes de publication](../release-notes/nuget-2.0.md)

NuGet 1.8 a été publiée le 23 mai 2012.

## <a name="known-installation-issue"></a>Problème connu d’Installation
Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.

La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.  Consultez [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) pour plus d’informations, ou [atteindre directement le correctif logiciel Visual Studio](http://bit.ly/vsixcertfix).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 Incompatible avec Windows XP, correctif logiciel publié

Peu de temps après la parution de NuGet 1.8, nous l’avons vu qu’une modification de la cryptographie 1.8 s’est arrêtée utilisateurs sous Windows XP.

Nous avons depuis publié un correctif qui résout ce problème.  En mettant à jour NuGet via la galerie d’extensions Visual Studio, vous recevrez ce correctif logiciel.

## <a name="features"></a>Fonctionnalités

### <a name="satellite-packages-for-localized-resources"></a>Packages de satellite des ressources localisées
1.8 de NuGet prend désormais en charge la capacité de créer des packages distincts pour les ressources localisées, semblables aux fonctionnalités d’assembly satellite du .NET Framework.  Un package de satellite est créé dans la même façon que tout autre package NuGet avec l’ajout de certaines conventions :

* Le nom du package satellite ID et le fichier doit inclure un suffixe correspondant à l’un de la norme [culture des chaînes utilisées par le .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* Dans son `.nuspec` fichier, le package satellite doit définir un élément de langage avec la même chaîne de culture utilisée dans l’ID
* Le package satellite doit définir une dépendance dans son `.nuspec` fichier à son package de base, qui est simplement le package avec le même ID moins le suffixe de la langue.  Le package de base doit être disponible dans le référentiel pour la réussite de l’installation.

Pour installer un package avec des ressources localisées, un développeur sélectionne explicitement la version localisée du package à partir du référentiel. À l’heure actuelle, la galerie NuGet ne donne pas de tout type de traitement spécial pour les packages de satellite.

![Boîte de dialogue package manager avec un package de localisée](./media/dlg-w-loc-packs.png)

Étant donné que le package satellite répertorie une dépendance à son package de base, le satellite et les principaux packages sont extraits dans le dossier de packages NuGet et installés.

![Dossier de packages avec des packages localisés](./media/fldr-loc-packs.png)

En outre, lors de l’installation du package de satellite, NuGet reconnaît également la convention d’affectation de noms de chaîne de culture et copie l’assembly de ressource localisée dans le sous-dossier approprié dans le package de base afin qu’elles peuvent être récupérées par le .NET Framework.

![Dossier de package principal avec le dossier de la ressource copiée](./media/fldr-copied-loc.png)

Un bogue existant à noter avec les packages de satellite est que NuGet ne copie pas les ressources localisées pour le `bin` dossier pour les projets de site Web.  Ce problème sera résolu dans la prochaine version de NuGet.

Pour obtenir un exemple complet qui montre comment créer et utiliser des packages de satellite, consultez [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Autorisation de restauration de package
NuGet 1.8, nous avons défini pour prendre en charge une contrainte importante lors de la restauration de package pour protéger la confidentialité de l’utilisateur. Cette contrainte exige que les développeurs qui créent des projets et solutions qui sont à l’aide de la restauration des packages explicitement consentir à la restauration du package va online pour télécharger des packages à partir de sources de package configuré.

Il existe 2 façons pour fournir ce consentement. Vous trouverez le premier dans la boîte de dialogue configuration de gestionnaire package comme indiqué ci-dessous.  Cette méthode est principalement destinée aux ordinateurs de développement.

![Boîte de dialogue de configuration de package manager](./media/pr-consent-configdlg.png)

La deuxième consiste à définir l’environnement de variable « EnableNuGetPackageRestore » à la valeur « true ».  Cette méthode est conçue pour les ordinateurs sans assistance tels que les serveurs de l’élément de configuration ou de la build.

À présent, comme indiqué ci-dessus, nous avons uniquement défini pour cette fonctionnalité dans NuGet 1.8.  En pratique, cela signifie que pendant que nous avons ajouté l’ensemble de la logique pour activer la fonctionnalité, elle n’est pas actuellement appliquée dans cette version. Il est activé, toutefois, dans la prochaine version de NuGet, donc nous souhaitons vous faire part de celui-ci dès que possible afin que vous pouvez configurer vos environnements de façon appropriée et par conséquent ne pas être affectée lorsque nous commençons appliquer la contrainte de consentement.

Pour plus d’informations, consultez la [billet de blog de l’équipe](http://blog.nuget.org/20120518/package-restore-and-consent.html) sur cette fonctionnalité.

### <a name="nugetexe-performance-improvements"></a>Améliorations des performances NuGet.exe
En modifiant la commande d’installation pour télécharger et installer des packages en parallèle, NuGet 1.8 apporte des améliorations de performances de nuget.exe – et par la restauration de package d’extension.  Test de niveau élevé indique qu’améliorent les performances pour l’installation des 6 packages dans un projet d’environ 35 % NuGet 1.8.  Augmentation du nombre de packages à 25 montre un gain de performances d’environ 60 %.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.8 comprend quelques correctifs de bogues en mettant l’accent sur la console du Gestionnaire de package et le flux de restauration de package, notamment en matière de consentement de restauration de package et l’intégration de Windows 8 Express.
Pour obtenir la liste complète de travail éléments corrigés dans NuGet 1.8, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
