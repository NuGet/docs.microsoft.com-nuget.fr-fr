---
title: Notes de version RC de NuGet 3.0
description: Notes de publication pour NuGet 3.0 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551717"
---
# <a name="nuget-30-rc-release-notes"></a>Notes de version RC de NuGet 3.0

[Notes de publication de NuGet 3.0 bêta](../release-notes/nuget-3.0-beta.md) | [Notes de publication de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC a été publiée avec la version de Visual Studio 2015 RC le 29 avril 2015. Cette version comporte un nombre de correctifs de bogues importants, des améliorations des performances et des mises à jour pour prendre en charge les nouvelles infrastructures.  Il est uniquement disponible pour Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Concentrés sur les performances

La stabilité et les performances des requêtes de NuGet continuent à être un sujet brûlant nous nous concentrons sur.  Avec cette version, vous devez commencer à voir les opérations de recherche très rapide dans le site Web et NuGet UI.  Nous surveillons le service et la façon dont vous utilisez le service afin que nous pouvons continuer à ajuster ces opérations.

## <a name="significant-issues-resolved"></a>Problèmes importants résolus

Pour stabiliser les clients NuGet, nous avons résolu plusieurs problèmes dans le cadre de cette version.  Ici est qu’une brève liste de certains des problèmes plus importantes résolus :

* Dans le cadre du changement de nom de l’infrastructure de K pour ASP.NET 5, monikers du framework ont été mis à jour pour gérer dnx et dnxcore [lien](https://github.com/NuGet/Home/issues/215)
* Ajouté la documentation d’aide à partir des liens dans l’interface utilisateur de Visual Studio [lien](https://github.com/NuGet/Home/issues/232)
* Meilleure gestion des références complexes dans `.nuspec` avec des références de framework délimitée par des virgules [lien](https://github.com/NuGet/Home/issues/276)
* Correction de prise en charge de cultures japonais [lien](https://github.com/NuGet/Home/issues/253)
* Client mis à jour pour permettre aux projets ASP.NET 5 à utiliser les nouveaux points de terminaison v3 [lien](https://github.com/NuGet/Home/issues/219)
* Dossier de packages de mise à jour pour une meilleure handle avec contrôle de code source [lien](https://github.com/NuGet/Home/issues/56)
* Correction de prise en charge des packages satellites [lien](https://github.com/NuGet/Home/issues/17)
* Prise en charge des fichiers de contenu spécifiques à l’infrastructure de correction [lien](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Remaniement de présence de GitHub

Nous avons apporté des changements pour nos [référentiels de code sur GitHub source](http://github.com/nuget/home).  Si vous rencontrez des problèmes avec le client NuGet Visual Studio, les commandes Powershell ou la ligne de commande exécutable vous connecter ces problèmes et suivre leur progression sur notre [liste de problèmes de référentiel GitHub accueil](http://github.com/nuget/home/issues).  Nous effectuons le suivi des problèmes pour la galerie dans notre [GitHub NuGetGallery référentiel](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Restez connecté

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus de progression et de publicités pour NuGet 3.0 !