---
title: Notes de publication NuGet 3.4-RC
description: Notes de publication pour NuGet 3.4 RC est, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820818"
---
# <a name="nuget-34-rc-release-notes"></a>Notes de publication NuGet 3.4-RC

[Notes de publication NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 Notes de publication](../release-notes/nuget-3.4.md)

NuGet 3.4-RC a été publiée le 3 mars 2016 en même temps que Visual Studio 2015 Update 2 RC et a été généré avec quelques principes dans esprit :

* Prise en charge multiplateforme
* Amélioration des performances
* Petites améliorations de l’interface utilisateur

Les fonctionnalités suivantes sont disponibles dans cette RC, avec plusieurs planifié pour la version finale 3.4.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels
* Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj
* Prise en charge pour iOS et Android actions de génération dans l’élément de fichiers
* Prise en charge des monikers netstandard et netstandardapp du framework

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités de l’Interface utilisateur

* Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider
* Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique
* Ajouter un bouton d’actualisation qui permet une recherche à actualiser

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour à chaque build. Au lieu de cela, ils mettent à jour uniquement quand il est contraint à restaurer, nettoyer, régénérer ou modifier `project.json`.
* sources de référentiel NuGet.org deviennent n’est plus dans une configuration de projet lorsque vous utilisez l’interface de configuration NuGet.
* NuGet n’est plus restaure les packages dans les projets partagés écritures, ni un fichier de verrouillage.
* Nous avez amélioré de défaillance du réseau et recommencez la gestion des serveurs inaccessibles ou lente à répondre.
* Les comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.
* Nous prennent désormais en charge la dernière version `project.json` schéma de DNX.

## <a name="known-issues"></a>Problèmes connus

Nous continuons à effectuer le suivi des problèmes sur notre liste de problèmes de GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)