---
title: Notes de publication NuGet 3.4.2 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 3.4.2, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 3.4.2 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-342-release-notes"></a>Notes de mise à jour de NuGet 3.4.2

[Notes de publication NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Notes de publication](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 a été publiée le 8 avril 2016 pour résoudre plusieurs problèmes ont été identifiés dans le 3.4 et 3.4.1 release.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC est désormais disponible

Vous pouvez télécharger la version release candidate de nuget.exe 3.4.2 [ici](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Mises à jour et améliorations

* Nous avons considérablement amélioré les performances des mises à jour dans un scénario spécifique, où les mises à jour sur les packages avec des graphiques de dépendance approfondie a pris beaucoup de temps et est en attente de Visual Studio.
* restauration de NuGet sans le trafic réseau est 2,5 à 3 x plus rapide dans Visual Studio.
* En plus de cette modification, nous avons résolu d’un problème où nous étions en appuyant sur le réseau à deux reprises lors de l’extraction de la mise à jour compter dans l’interface utilisateur de Visual Studio. Cela a été partiellement chargé de certains clients de problèmes de délai d’attente, l’expérience de 3.4/3.4.1.
* Prise en charge pour le paramètre de no_proxy

## <a name="fixes"></a>Correctifs

* Correction d’un problème où nuget.org source est manquant dans les paramètres de NuGet ou la configuration après la mise à jour vers 3.4.1.
* Correction d’un problème où une modification de la casse FindPackagesById dans 3.4.1 sauts Artifactory.
* Correction d’un problème à la norme FIPS qui a provoqué des échecs de restauration NuGet avec nuget.exe.
* Correction d’un incident lorsque vous parcourez des sources avec l’URL de l’icône non valide.
* Résolution des problèmes avec la fusion des versions et les entrées ' Toutes les sources'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problèmes connus dans la section 3.4.2 Windows x86 de ligne de commande (RC)

Ces problèmes seront résolus anticipée semaine suivante avant que nous atteinte RTM.

*  Restauration de nuget en cours d’exécution sur une solution échoue si le fichier solution est placé dans une hiérarchie de dossiers plus faible que les fichiers de projet.
*  Commande de suppression de nuget en cours d’exécution sur un package à l’aide de l’alimentation V2 échoue. Utilisez à la place des flux de V3.


Pour obtenir la liste complète des correctifs et améliorations apportées dans cette version, consultez la liste des problèmes [ici](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).