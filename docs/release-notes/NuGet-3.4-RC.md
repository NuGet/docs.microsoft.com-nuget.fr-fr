---
title: Notes de publication NuGet 3.4-RC
description: Notes de publication pour NuGet 3.4 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546752"
---
# <a name="nuget-34-rc-release-notes"></a>Notes de publication NuGet 3.4-RC

[Notes de publication NuGet 3.3](../release-notes/nuget-3.3.md) | [Notes de publication de NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC a été publiée le 3 mars 2016 en même temps que Visual Studio 2015 Update 2 RC et a été généré avec quelques principes dans l’esprit :

* Prise en charge multiplateforme
* Amélioration des performances
* Améliorations mineures de l’interface utilisateur

Les fonctionnalités suivantes sont disponibles dans la version RC, prévu pour la version finale 3.4 d’autres.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les clients NuGet prennent désormais en charge encodage de contenu gzip à partir de référentiels
* Prise en charge pour les fichiers PDB à partir de packages dans des projets xproj
* Actions dans l’élément contentFiles de génération de prise en charge pour iOS et Android
* Prise en charge des monikers netstandard et netstandardapp du framework

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités d’Interface utilisateur

* Améliorations significatives des performances en particulier sur les onglets installé, les mises à jour et les consolider
* Installé et onglets de mises à jour sont maintenant triés par ordre alphabétique
* Ajouter un bouton d’actualisation qui permet une recherche à être actualisé

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Les packages référencés dans `project.json` qui ont flottante version ne sera pas mise à jour sur chaque build. Au lieu de cela, ils mettent à jour uniquement lorsqu’il est forcé à restaurer, nettoyer, régénérer ou modifier `project.json`.
* sources de référentiel NuGet.org sont forcés n’est plus dans une configuration de projet lorsque vous utilisez l’interface utilisateur de configuration NuGet.
* NuGet n’est plus restaure les packages dans les projets partagés ni écrit un fichier de verrouillage.
* Nous avez amélioré défaillance réseau et réessayez de gestion pour les serveurs inaccessibles ou ralentir pour répondre.
* Comportements de clavier et souris sont améliorées dans le Gestionnaire de Package Visual Studio UI.
* Nous prennent désormais en charge la dernière version `project.json` schéma dans DNX.

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes sur notre liste de problèmes GitHub qui se trouve à : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)