---
title: Notes de publication de NuGet 3.4.2
description: Notes de publication pour NuGet 3.4.2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780252"
---
# <a name="nuget-342-release-notes"></a>Notes de publication de NuGet 3.4.2

Notes de publication de [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Notes de publication de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 a été publié le 8 avril 2016 pour résoudre plusieurs problèmes identifiés dans les versions 3,4 et 3.4.1.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC est désormais disponible

Vous pouvez télécharger la version Release candidate de nuget.exe 3.4.2 [ici](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Nous avons considérablement amélioré les performances des mises à jour dans un scénario spécifique, où les mises à jour sur les packages avec des graphiques de dépendance profonde prenaient beaucoup de temps et ont bloqué Visual Studio.
* la restauration NuGet sans trafic réseau est de 2,5 x – 3 fois plus rapide dans Visual Studio.
* En plus de cette modification, nous avons résolu un problème où nous avons atteint le réseau deux fois lors de l’extraction du nombre de mises à jour dans l’interface utilisateur de Visual Studio. Cela était partiellement responsable de certains problèmes de délai d’attente rencontrés par les clients dans 3.4/3.4.1.
* Ajout de la prise en charge du paramètre no_proxy

## <a name="fixes"></a>Correctifs

* Correction d’un problème où la source nuget.org était manquante dans les paramètres ou la configuration NuGet après une mise à jour à 3.4.1.
* Résolution d’un problème où une modification de la casse à FindPackagesById dans 3.4.1 rompt l’artefact.
* Correction d’un problème avec FIPS qui provoquait des échecs avec la restauration NuGet avec nuget.exe.
* Résolution d’un incident lors de l’exploration des sources avec une URL d’icône non valide.
* Résolution des problèmes liés à la fusion de versions et d’entrées à partir de’toutes les sources'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problèmes connus dans 3.4.2 Windows x86 CommandLine (RC)

Ces problèmes seront corrigés au début de la semaine prochaine avant que nous ayons atteint la version RTM.

*  L’exécution de la restauration NuGet sur une solution échoue si le fichier de solution est placé dans une hiérarchie de dossiers inférieure aux fichiers projet.
*  L’exécution de la commande NuGet Delete sur un package à l’aide du flux v2 échoue. Utilisez à la place le flux v3.


Pour obtenir la liste complète des correctifs et améliorations de cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).