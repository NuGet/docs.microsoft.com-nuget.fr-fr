---
title: Notes de version de NuGet 3.0 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de publication pour NuGet 3.0.0, notamment de problèmes connus, des correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "NuGet 3.0.0 notes de publication, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ef8557c37105eb7915919c7b15d41d024921761f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-release-notes"></a>Notes de version 3.0 de NuGet

[Notes de mise à jour de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Notes de publication](../release-notes/nuget-3.1.md)

NuGet 3.0 a été publiée le 20 juillet 2015 comme extension de regroupement dans Visual Studio 2015. Nous avons envoyé à fournir cette version avec Visual Studio afin que l’expérience de NuGet 3.0 mise à jour terminée, ne serait disponible pour les nouveaux utilisateurs de Visual Studio. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Nous vous recommandons des développeurs qui ont accès à la mise à jour de la galerie Visual Studio à la version la plus récente est disponible, comme nous publions une mise à jour peu après la publication de Visual Studio 2015 qui contient la prise en charge pour le développement de Windows 10.

Au total, nous avons fermé 240 problèmes dans la version 3.0, et vous pouvez passer en revue les [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problèmes connus

Un certain nombre de problèmes connus fourni avec cette version, et tous ces éléments ont été corrigés dans notre version 3.1 planifiées pour coïncider avec la version de Windows 10 sur 29 juillet.  Vous ne pourrez pas mettre à jour votre extension de Visual Studio à partir de la galerie sur ou après cette date pour résoudre ces problèmes connus.

*  Traduction n’est pas fournie pour l’étiquette « Ne plus afficher cette boîte de dialogue » dans la fenêtre d’aperçu et de l’étiquette « Auteurs » dans la fenêtre de la description du package.
*  Lorsque vous travaillez sur un projet à l’aide de TFS contrôle de source, NuGet ne peuvent pas présenter le Gestionnaire de package interface utilisateur si le fichier Nuget.Config est marqué comme étant en lecture seule.
   * **Solution de contournement** à extraire le fichier à partir de TFS.
*  Texte dans le jaune « redémarrage barre » dans la fenêtre NuGet Powershell n’est pas visible lorsque vous utilisez le thème sombre de Visual Studio.
   * **Solution de contournement** utiliser ce thème clair Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Résumé des principaux problèmes résolus

* [Mise à jour fréquentes réseau appelle au moment de l’actualisation de la fenêtre du Gestionnaire de package](https://github.com/NuGet/Home/issues/515)
* [Retardé de défilement lorsque la modification à installé vue dans le Gestionnaire de package](https://github.com/NuGet/Home/issues/519)
* [Les appels réseau doivent être exécutés sur un thread d’arrière-plan](https://github.com/NuGet/Home/issues/516)
* [Case à cocher « Ne pas afficher la fenêtre d’aperçu » ajouté](https://github.com/NuGet/Home/issues/566)
* [Processus ajouté la limitation pour réduire l’utilisation du processeur](https://github.com/NuGet/Home/issues/356)
* Une référence de bibliothèque de classes portable gestion améliorée
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [La saisie semi-automatique service a été respectant la casse](https://github.com/NuGet/Home/issues/198)
* [Mise à jour pour rétablir les informations d’identification de l’authentification de base](https://github.com/NuGet/Home/issues/456)
* [Journalisation des erreurs améliorées](https://github.com/NuGet/Home/issues/407)
* [Powershell amélioré les messages d’erreur lors de l’appel de Package de mise à jour](https://github.com/NuGet/Home/issues/5)
* [Fixe le lien « En savoir plus sur les Options » pour empêcher le blocage sur Windows 10](https://github.com/NuGet/Home/issues/822)
* [N’oubliez pas de paramètre de la case à cocher de la version préliminaire](https://github.com/NuGet/Home/issues/732)
* [Performances améliorées de collecte en mettant en cache les résultats pour des projets d’une solution](https://github.com/NuGet/Home/issues/721)
* [Plusieurs Packages peuvent être regroupés en parallèle](https://github.com/NuGet/Home/issues/713)
* [Supprimer le package d’installation-forcer la commande](https://github.com/NuGet/Home/issues/697)

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) de progression et des annonces plus que nous se préparer à fournir la prise en charge pour le développement de Windows 10.