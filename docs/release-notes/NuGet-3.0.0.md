---
title: Notes de publication NuGet 3.0
description: Notes de publication pour NuGet 3.0.0 notamment et problèmes connus, correctifs de bogues, fonctionnalités ajoutées, dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551861"
---
# <a name="nuget-30-release-notes"></a>Notes de publication NuGet 3.0

[Notes de publication de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [Notes de publication de NuGet 3.1](../release-notes/nuget-3.1.md)

NuGet 3.0 a été publiée le 20 juillet 2015 comme extension de bundle dans Visual Studio 2015. Nous avons introduit pour fournir cette version avec Visual Studio afin que l’expérience de NuGet 3.0 mise à jour complète serait disponible pour les nouveaux utilisateurs de Visual Studio. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Nous recommandons aux développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, car nous publions une mise à jour peu après la publication de Visual Studio 2015 qui contient la prise en charge pour le développement de Windows 10.

Au total, nous avons fermé 240 problèmes dans la version 3.0, et vous pouvez consulter le [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problèmes connus

Il existe un nombre de problèmes connus fournies par cette version, et tous ces éléments sont fixes dans notre version 3.1 planifiées pour coïncider avec la version de Windows 10 sur 29 juillet.  Vous êtes en mesure de mettre à jour votre extension de Visual Studio à partir de la galerie sur ou après cette date pour résoudre ces problèmes connus.

*  Traduction n’est pas fournie pour l’étiquette « Ne plus afficher ce » sur la fenêtre d’aperçu et de l’étiquette « Auteurs » dans la fenêtre de la description du package.
*  Lorsque vous travaillez sur un projet à l’aide de TFS contrôle de source, NuGet ne peut pas présenter le Gestionnaire de package interface utilisateur si le fichier Nuget.Config est marqué comme étant en lecture seule.
   * **Solution de contournement** extraire le fichier à partir de TFS.
*  Texte dans la « barre de redémarrage » dans la fenêtre Powershell de NuGet jaune n’est pas visible lorsque vous utilisez le thème foncé Visual Studio.
   * **Solution de contournement** utiliser le thème clair de Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Résumé des principaux problèmes résolus

* [Mise à jour fréquentes réseau appelle au moment de l’actualisation de la fenêtre du Gestionnaire de package](https://github.com/NuGet/Home/issues/515)
* [Retardé défilement lors de la modification à installé vue dans le Gestionnaire de package](https://github.com/NuGet/Home/issues/519)
* [Les appels réseau doivent être exécutés sur un thread d’arrière-plan](https://github.com/NuGet/Home/issues/516)
* [Case à cocher « Ne pas afficher la fenêtre d’aperçu » ajouté](https://github.com/NuGet/Home/issues/566)
* [Ajout de limitation pour réduire l’utilisation du processeur de processus](https://github.com/NuGet/Home/issues/356)
* Gestion des références de bibliothèque de classes portable améliorés
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Service de la saisie semi-automatique a été respecte la casse](https://github.com/NuGet/Home/issues/198)
* [Mise à jour de réintroduire les informations d’identification de l’authentification de base](https://github.com/NuGet/Home/issues/456)
* [Journalisation des erreurs améliorée](https://github.com/NuGet/Home/issues/407)
* [Messages d’erreur powershell améliorée lors de l’appel de Package de mise à jour](https://github.com/NuGet/Home/issues/5)
* [Fixe le lien « En savoir plus sur les Options » pour éviter un blocage sur Windows 10](https://github.com/NuGet/Home/issues/822)
* [N’oubliez pas de paramètre de la case à cocher de la version préliminaire](https://github.com/NuGet/Home/issues/732)
* [Performances améliorées de regroupement en mettant en cache les résultats sur plusieurs projets dans une solution](https://github.com/NuGet/Home/issues/721)
* [Plusieurs Packages peuvent être regroupés en parallèle](https://github.com/NuGet/Home/issues/713)
* [Supprimer le package d’installation-forcer la commande](https://github.com/NuGet/Home/issues/697)

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus de progression et de publicités que nous préparons fournir la prise en charge pour le développement de Windows 10.