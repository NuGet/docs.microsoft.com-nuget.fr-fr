---
title: Notes de publication de NuGet 3,4-RC
description: Notes de publication de NuGet 3,4 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780245"
---
# <a name="nuget-34-rc-release-notes"></a>Notes de publication de NuGet 3,4-RC

Notes de publication de [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Notes de publication de NuGet 3,4](../release-notes/nuget-3.4.md)

NuGet 3,4-RC a été publié le 3 mars 2016 en même temps que Visual Studio 2015 Update 2 RC et a été créé avec quelques principes à l’esprit :

* Prise en charge multiplateforme
* Amélioration des performances
* Améliorations mineures de l’interface utilisateur

Les fonctionnalités suivantes sont disponibles dans cette version RC, avec davantage de planification pour la version finale 3,4.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Les clients NuGet prennent désormais en charge l’encodage de contenu gzip à partir des référentiels
* Prise en charge des fichiers PDB des packages dans les projets xproj
* Prise en charge des actions de génération iOS et Android dans l’élément contentFiles
* Prise en charge des monikers netstandard et nestandardapp Framework

## <a name="new-user-interface-features"></a>Nouvelles fonctionnalités de l’interface utilisateur

* Amélioration significative des performances, en particulier sur les onglets installé, mises à jour et consolider
* Les onglets installé et mis à jour sont désormais triés par ordre alphabétique
* Ajout d’un bouton d’actualisation permettant d’actualiser une recherche

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Les packages référencés dans `project.json` et qui ont une version flottante ne sont pas mis à jour sur chaque Build. Au lieu de cela, ils sont mis à jour uniquement lorsqu’ils sont forcés à restaurer, nettoyer, régénérer ou modifier `project.json` .
* les sources de référentiel nuget.org ne sont plus contraints dans une configuration de projet lorsque vous utilisez l’interface utilisateur de configuration de NuGet.
* NuGet ne restaure plus les packages dans les projets partagés et n’écrit pas de fichier de verrouillage.
* Nous avons amélioré les défaillances du réseau et les tentatives de traitement des serveurs inaccessibles ou lents à répondre.
* Les comportements du clavier et de la souris sont améliorés dans l’interface utilisateur du gestionnaire de package Visual Studio.
* Nous prenons maintenant en charge le schéma le plus récent `project.json` dans DNX.

## <a name="known-issues"></a>Problèmes connus

Nous continuons à suivre les problèmes de notre liste de problèmes GitHub qui se trouvent à l’adresse suivante : [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)