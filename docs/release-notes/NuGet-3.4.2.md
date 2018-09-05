---
title: Notes de publication de NuGet 3.4.2
description: Notes de publication pour NuGet 3.4.2 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549149"
---
# <a name="nuget-342-release-notes"></a>Notes de publication de NuGet 3.4.2

[Notes de publication de NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [Notes de publication de NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 a été publiée le 8 avril 2016 pour résoudre plusieurs problèmes qui ont été identifiées dans le 3.4 et 3.4.1, mise en production.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC est désormais disponible

Vous pouvez télécharger la version release candidate de nuget.exe 3.4.2 [ici](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Nous avons considérablement amélioré les performances des mises à jour dans un scénario spécifique, où les mises à jour sur les packages avec des graphiques de dépendance approfondie a pris beaucoup de temps et est en attente de Visual Studio.
* la restauration NuGet sans le trafic réseau est 2,5 à 3 fois plus rapides dans Visual Studio.
* En plus de cette modification, nous avons résolu un problème où nous étions en appuyant sur le réseau à deux reprises lors de l’extraction de la mise à jour compter dans l’interface utilisateur de Visual Studio. Cela a été partiellement responsable pour certains clients de problèmes de délai d’attente, l’expérience de 3.4/3.4.1.
* Prise en charge pour le paramètre de no_proxy

## <a name="fixes"></a>Correctifs

* Correction d’un problème où nuget.org source est manquant dans les paramètres de NuGet ou de configuration après la mise à jour à 3.4.1.
* Correction d’un problème où un changement de casse pour FindPackagesById dans 3.4.1 interrompt Artifactory.
* Correction d’un problème à la norme FIPS qui provoquait des échecs avec la restauration de NuGet avec nuget.exe.
* Correction d’un incident lors de l’exploration des sources avec l’URL de l’icône non valide.
* Résolution des problèmes avec la fusion de versions et les entrées « Toutes les sources ».

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problèmes connus dans 3.4.2 Windows x86 de ligne de commande (RC)

Ces problèmes seront corrigés anticipée semaine prochaine avant que nous nous heurtons à RTM.

*  La restauration nuget en cours d’exécution sur une solution échoue si le fichier solution est placé dans une hiérarchie de dossiers plus faible que les fichiers de projet.
*  Exécution de commande de suppression de nuget sur un package en utilisant le flux V2 échoue. Utilisez plutôt les flux V3.


Pour obtenir la liste complète des correctifs et améliorations dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).