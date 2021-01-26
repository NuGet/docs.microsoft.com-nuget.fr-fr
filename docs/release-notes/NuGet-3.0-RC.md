---
title: Notes de publication de NuGet 3,0 RC
description: Notes de publication de NuGet 3,0 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776576"
---
# <a name="nuget-30-rc-release-notes"></a>Notes de publication de NuGet 3,0 RC

Notes de publication de [NuGet 3,0 Beta](../release-notes/nuget-3.0-beta.md)  |  [Notes de publication de NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3,0 RC a été publié le 29 avril 2015 avec la version Visual Studio 2015 RC. Cette version comporte un certain nombre de correctifs de bogues importants, des améliorations des performances et des mises à jour pour prendre en charge les nouvelles infrastructures.  Elle est uniquement disponible pour Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Focalisation continue sur les performances

La stabilité et les performances des requêtes NuGet continuent à être un sujet chaud sur lequel nous nous concentrons.  Avec cette version, vous devez commencer à voir des opérations de recherche très rapides dans l’interface utilisateur et le site Web NuGet.  Nous analysons le service et la façon dont vous utilisez le service afin de pouvoir continuer à ajuster ces opérations.

## <a name="significant-issues-resolved"></a>Problèmes importants résolus

Pour stabiliser les clients NuGet, nous avons résolu de nombreux problèmes dans le cadre de cette version.  Voici une brève liste de quelques-uns des problèmes les plus importants résolus :

* Dans le cadre du changement de nom de l’infrastructure K pour ASP.NET 5, les monikers de Framework ont été mis à jour pour gérer DNX et le [lien](https://github.com/NuGet/Home/issues/215) dnxcore
* Ajout de la documentation d’aide à partir des liens dans le [lien](https://github.com/NuGet/Home/issues/232) de l’interface utilisateur de Visual Studio
* Meilleure gestion des références complexes dans `.nuspec` avec le [lien](https://github.com/NuGet/Home/issues/276) références de Framework délimités par des virgules
* Correction de la prise en charge du [lien](https://github.com/NuGet/Home/issues/253) des cultures japonaises
* Client mis à jour pour autoriser les projets ASP.NET 5 à utiliser le nouveau [lien](https://github.com/NuGet/Home/issues/219) des points de terminaison v3
* Mise à jour pour mieux gérer le dossier Packages avec le [lien](https://github.com/NuGet/Home/issues/56) de contrôle de code source
* [Lien](https://github.com/NuGet/Home/issues/17) de prise en charge fixe pour les packages satellites
* [Lien](https://github.com/NuGet/Home/issues/18) de prise en charge corrigé pour les fichiers de contenu spécifiques à l’infrastructure

## <a name="github-presence-overhaul"></a>Révision de la présence GitHub

Nous avons apporté des modifications à nos [référentiels de code source sur GitHub](http://github.com/nuget/home).  Si vous rencontrez des problèmes avec le client NuGet Visual Studio, les commandes PowerShell ou l’exécutable de ligne de commande, vous pouvez consigner ces problèmes et surveiller leur progression dans notre [liste de problèmes de référentiels d’hébergement GitHub](http://github.com/nuget/home/issues).  Nous effectuons le suivi des problèmes de la galerie dans notre [référentiel NuGetGallery GitHub](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Restez informé

Gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces de NuGet 3,0 !