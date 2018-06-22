---
title: Notes de version de NuGet 3.0 RC
description: Notes de version de NuGet 3.0 RC, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819596"
---
# <a name="nuget-30-rc-release-notes"></a>Notes de version de NuGet 3.0 RC

[Notes de mise à jour de NuGet 3.0 bêta](../release-notes/nuget-3.0-beta.md) | [notes de mise à jour de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC le 29 avril 2015 a été publiée avec la version de Visual Studio 2015 RC. Cette version comporte un nombre de résolutions de bogues importantes, des améliorations de performances et des mises à jour pour prendre en charge les infrastructures de nouveau.  Il est uniquement disponible pour Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Se concentrer sur les performances

Stabilité et performances des requêtes de NuGet continuent de représenter une rubrique à chaud qui se concentre sur.  Avec cette version, vous devez commencer à voir les opérations de recherche très rapide dans le site Web et NuGet UI.  Nous surveillons le service et la façon dont vous utilisez le service afin que nous puissions continuer à paramétrer ces opérations.

## <a name="significant-issues-resolved"></a>Résolu des problèmes significatifs

Afin de stabiliser les clients NuGet, nous avons plusieurs problèmes résolus dans le cadre de cette version.  Voici juste une courte liste de certains des problèmes plus importants résolus :

* Dans le cadre de la modification du nom de l’infrastructure de K pour ASP.NET 5, monikers d’infrastructure ont été mis à jour pour gérer dnx et dnxcore [lien](https://github.com/NuGet/Home/issues/215)
* Ajouté la documentation d’aide à partir des liens dans l’interface utilisateur de Visual Studio [lien](https://github.com/NuGet/Home/issues/232)
* Une meilleure gestion des références complexes dans `.nuspec` avec références délimitée par des virgules de framework [lien](https://github.com/NuGet/Home/issues/276)
* Fixe la prise en charge pour les cultures japonais [lien](https://github.com/NuGet/Home/issues/253)
* Client mis à jour pour autoriser les projets ASP.NET 5 à utiliser les nouveaux points de terminaison v3 [lien](https://github.com/NuGet/Home/issues/219)
* Dossier de packages de mise à jour pour une meilleure handle avec contrôle de code source [lien](https://github.com/NuGet/Home/issues/56)
* Fixe la prise en charge pour les packages de satellites [lien](https://github.com/NuGet/Home/issues/17)
* Correction de la prise en charge pour les fichiers de contenu spécifiques à l’infrastructure [lien](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Révision de présence de GitHub

Nous avons apporté des modifications à notre [de source de référentiels de code sur GitHub](http://github.com/nuget/home).  Si vous rencontrez des problèmes avec le client NuGet Visual Studio, les commandes Powershell ou la ligne de commande exécutable vous pouvez connecter ces problèmes et surveiller leur progression sur notre [liste de problèmes de référentiel GitHub accueil](http://github.com/nuget/home/issues).  Nous surveillons problèmes pour la galerie dans notre [GitHub NuGetGallery référentiel](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Tenez-vous informé

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus d’avancement et les annonces de NuGet 3.0 !