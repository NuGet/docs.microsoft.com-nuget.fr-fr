---
title: Notes de publication NuGet 1.8
description: Notes de publication pour 1.8 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546619"
---
# <a name="nuget-18-release-notes"></a>Notes de publication NuGet 1.8

[Notes de publication de NuGet 1.7](../release-notes/nuget-1.7.md) | [Notes de publication de NuGet 2.0](../release-notes/nuget-2.0.md)

NuGet 1.8 a été publiée le 23 mai 2012.

## <a name="known-installation-issue"></a>Problème d’Installation connus
Si vous exécutez Visual Studio 2010 SP1, vous pouvez rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet si vous avez une version antérieure est installée.

La solution de contournement consiste à désinstaller simplement NuGet, puis l’installer à partir de la galerie d’extensions Visual Studio.  Consultez [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) pour plus d’informations, ou [rendez-vous directement sur le correctif logiciel VS](http://bit.ly/vsixcertfix).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis vous avez probablement besoin de redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 incompatibles avec Windows XP, correctif publié

Peu de temps après la publication de NuGet 1.8, nous avons appris qu’une modification de cryptographie dans 1.8 résilié utilisateurs sur Windows XP.

Nous avons publié depuis un correctif logiciel qui résout ce problème.  En mettant à jour NuGet via la galerie d’extensions Visual Studio, vous recevez ce correctif logiciel.

## <a name="features"></a>Fonctionnalités

### <a name="satellite-packages-for-localized-resources"></a>Packages satellites de ressources localisées
NuGet 1.8 prend désormais en charge la possibilité de créer des packages distincts pour les ressources localisées, semblables aux fonctionnalités d’assembly satellite du .NET Framework.  Un package satellite est créé dans la même façon que tout autre package NuGet avec l’ajout de quelques conventions :

* Le nom d’ID et le fichier du package satellite doit inclure un suffixe qui correspond à celui de la norme [culture des chaînes utilisées par le .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* Dans son `.nuspec` fichier, le package satellite doit définir à un élément de langage avec la même chaîne de culture utilisée dans l’ID
* Le package satellite doit définir une dépendance dans son `.nuspec` fichier à son package core, qui est simplement le package avec le même ID sans le suffixe de langage.  Le package principal doit être disponible dans le référentiel pour la réussite de l’installation.

Pour installer un package avec des ressources localisées, un développeur sélectionne explicitement la version localisée du package à partir du référentiel. À l’heure actuelle, la galerie NuGet ne donne pas de tout type de traitement spécial pour les packages satellites.

![Boîte de dialogue package manager avec le package de localisée](./media/dlg-w-loc-packs.png)

Étant donné que le package satellite répertorie une dépendance à son package de base, le satellite et les principaux packages sont extraites dans le dossier de packages NuGet et installés.

![Dossier de packages avec des packages localisés](./media/fldr-loc-packs.png)

En outre, lors de l’installation du package satellite, NuGet reconnaît également la convention d’affectation de noms de chaîne de culture et copie ensuite l’assembly de ressource localisée dans le sous-dossier approprié dans le package principal afin qu’elles peuvent être récupérées par le .NET Framework.

![Dossier de package principal avec le dossier de la ressource copiée](./media/fldr-copied-loc.png)

Un bogue existant à remarquer, avec des packages satellites est que NuGet ne copie pas les ressources localisées pour le `bin` dossier pour les projets de site Web.  Ce problème sera résolu dans la prochaine version de NuGet.

Pour obtenir un exemple complet qui montre comment créer et utiliser des packages satellites, consultez [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consentement de restauration de package
Dans NuGet 1.8, nous avons défini pour prendre en charge d’une contrainte importante lors de la restauration de package pour protéger la confidentialité des utilisateurs. Cette contrainte exige que les développeurs qui créent des projets et solutions qui sont à l’aide de la restauration de package à explicitement donner son consentement à la restauration de package va online pour télécharger des packages à partir de sources de package configuré.

Il existe 2 façons de fournir ce consentement. Vous trouverez le premier dans la boîte de dialogue configuration de gestionnaire package comme indiqué ci-dessous.  Cette méthode est principalement pour les ordinateurs de développement.

![Boîte de dialogue de configuration de package manager](./media/pr-consent-configdlg.png)

La deuxième méthode consiste à définir l’environnement variable « EnableNuGetPackageRestore » à la valeur « true ».  Cette méthode est destinée aux ordinateurs sans assistance tels que les serveurs CI ou de la build.

À présent, comme indiqué ci-dessus, nous avons uniquement défini pour cette fonctionnalité dans NuGet 1.8.  En pratique, cela signifie que pendant que nous avons ajouté l’ensemble de la logique pour activer la fonctionnalité, elle n’est pas actuellement appliquée dans cette version. Il est activé, toutefois, dans la prochaine version de NuGet, donc nous souhaitons vous faire part de celui-ci dès que possible afin que vous pouvez configurer vos environnements de façon appropriée et donc ne pas être affectées lorsque nous commencerons appliquer la contrainte de consentement.

Pour plus d’informations, consultez le [billet de blog de l’équipe](http://blog.nuget.org/20120518/package-restore-and-consent.html) sur cette fonctionnalité.

### <a name="nugetexe-performance-improvements"></a>Améliorations des performances de NuGet.exe
En modifiant la commande d’installation pour télécharger et installer des packages en parallèle, NuGet 1.8 apporte des améliorations considérables des performances de nuget.exe – et par la restauration de package d’extension.  Test de niveau élevé indique qu’améliorent les performances pour l’installation des 6 packages dans un projet d’environ 35 % dans NuGet 1.8.  Augmentation du nombre de packages à 25 illustre un gain de performances d’environ 60 %.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 1.8 inclut quelques correctifs de bogues en mettant l’accent sur la console du Gestionnaire de package et le flux de restauration de package, en particulier par rapport à l’intégration de Windows 8 Express et de consentement de restauration de package.
Pour obtenir une liste complète de travail éléments résolus dans NuGet 1.8, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
