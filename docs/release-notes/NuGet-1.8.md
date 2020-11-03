---
title: Notes de publication de NuGet 1,8
description: Notes de publication de NuGet 1,8, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9d55534ffe765137731b7fbf4be4bbaa618c769c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236835"
---
# <a name="nuget-18-release-notes"></a>Notes de publication de NuGet 1,8

Notes de publication de [NuGet 1,7](../release-notes/nuget-1.7.md)  |  [Notes de publication de NuGet 2,0](../release-notes/nuget-2.0.md)

NuGet 1,8 a été publié le 23 mai 2012.

## <a name="known-installation-issue"></a>Problème d’installation connu
Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.

La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.  <https://support.microsoft.com/kb/2581019>Pour plus d’informations, consultez pour plus d’informations ou [accédez directement au correctif vs](http://bit.ly/vsixcertfix).

Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1,8 incompatible avec Windows XP, correctif publié

Peu après la sortie de NuGet 1,8, nous avons appris qu’un changement de chiffrement dans 1,8 a endommagé les utilisateurs sur Windows XP.

Nous avons publié un correctif qui résout ce problème.  En mettant à jour NuGet par le biais de la Galerie d’extensions Visual Studio, vous recevez ce correctif.

## <a name="features"></a>Fonctionnalités

### <a name="satellite-packages-for-localized-resources"></a>Packages satellites pour les ressources localisées
NuGet 1,8 prend désormais en charge la possibilité de créer des packages distincts pour les ressources localisées, de la même façon que les fonctionnalités d’assembly satellite de l' .NET Framework.  Un package satellite est créé de la même façon que n’importe quel autre package NuGet, avec l’ajout de quelques conventions :

* L’ID de package et le nom de fichier du satellite doivent inclure un suffixe qui correspond à l’une des [chaînes de culture standard utilisées par le .NET Framework](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* Dans son `.nuspec` fichier, le package satellite doit définir un élément de langage avec la même chaîne de culture utilisée dans l’ID
* Le package satellite doit définir une dépendance dans son `.nuspec` fichier pour son package de base, qui est simplement le package avec le même ID, moins le suffixe du langage.  Le package de base doit être disponible dans le référentiel pour que l’installation réussisse.

Pour installer un package avec des ressources localisées, un développeur sélectionne explicitement le package localisé dans le référentiel. À l’heure actuelle, la galerie NuGet n’offre aucun traitement spécial aux packages satellites.

![Boîte de dialogue Gestionnaire de package avec exploitation localisé](./media/dlg-w-loc-packs.png)

Étant donné que le package satellite répertorie une dépendance à son package de base, les packages satellites et principaux sont extraits dans le dossier de packages NuGet et installés.

![Dossier Packages avec des packages localisés](./media/fldr-loc-packs.png)

En outre, lors de l’installation du package satellite, NuGet reconnaît également la Convention d’affectation de noms à la chaîne de culture, puis copie l’assembly de ressource localisé dans le sous-dossier approprié du package principal afin qu’il puisse être sélectionné par l' .NET Framework.

![Dossier de package principal avec dossier de ressources copié](./media/fldr-copied-loc.png)

L’un des bogues existants à noter avec les packages satellites est que NuGet ne copie pas les ressources localisées dans le `bin` dossier des projets de site Web.  Ce problème sera résolu dans la prochaine version de NuGet.

Pour obtenir un exemple complet montrant comment créer et utiliser des packages satellites, consultez [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) .

### <a name="package-restore-consent"></a>Consentement de la restauration des packages
Dans NuGet 1,8, nous avons mis au point le point de départ pour prendre en charge une contrainte importante sur la restauration des packages afin de protéger la confidentialité des utilisateurs. Cette contrainte oblige les développeurs à créer des projets et des solutions qui utilisent la restauration de packages pour consentir explicitement à la mise en ligne de la restauration de package pour télécharger des packages à partir de sources de package configurées.

Il existe deux façons de fournir ce consentement. Le premier se trouve dans la boîte de dialogue de configuration du gestionnaire de package, comme indiqué ci-dessous.  Cette méthode est principalement destinée aux développeurs.

![Boîte de dialogue de configuration du gestionnaire de package](./media/pr-consent-configdlg.png)

La deuxième méthode consiste à définir la variable d’environnement « EnableNuGetPackageRestore » sur la valeur « true ».  Cette méthode est destinée aux ordinateurs sans assistance tels que les serveurs d’intégration continue ou de Build.

À présent, comme indiqué ci-dessus, nous avons uniquement mis le départ de cette fonctionnalité dans NuGet 1,8.  Concrètement, cela signifie que pendant que nous avons ajouté toute la logique pour activer la fonctionnalité, elle n’est pas actuellement appliquée dans cette version. Toutefois, il est activé dans la prochaine version de NuGet. nous voulons donc en être conscient le plus rapidement possible afin de pouvoir configurer vos environnements de manière appropriée et, par conséquent, ne pas être impactés quand nous commençons d’appliquer la contrainte de consentement.

Pour plus d’informations, consultez le billet de blog de l' [équipe](http://blog.nuget.org/20120518/package-restore-and-consent.html) sur cette fonctionnalité.

### <a name="nugetexe-performance-improvements"></a>Améliorations des performances de nuget.exe
En modifiant la commande d’installation pour télécharger et installer des packages en parallèle, NuGet 1,8 améliore considérablement les performances des nuget.exe et de la restauration des packages d’extension.  Les tests de haut niveau montrent que les performances pour l’installation de 6 packages dans un projet s’améliorent d’environ 35% dans NuGet 1,8.  L’augmentation du nombre de packages à 25 représente un gain de performances d’environ 60%.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1,8 comprend un certain nombre de correctifs de bogues en mettant l’accent sur la console du gestionnaire de package et le flux de travail de restauration des packages, en particulier en ce qui concerne le consentement de restauration des packages et l’intégration de Windows 8 Express.
Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 1,8, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).