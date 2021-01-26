---
title: Notes de publication de NuGet 3,0
description: Notes de publication pour NuGet 3.0.0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776555"
---
# <a name="nuget-30-release-notes"></a>Notes de publication de NuGet 3,0

Notes de publication de [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Notes de publication de NuGet 3,1](../release-notes/nuget-3.1.md)

NuGet 3,0 a été publié le 20 juillet 2015 en tant qu’extension de Visual Studio 2015. Nous avons poussé cette version avec Visual Studio afin que la mise à jour complète de l’expérience 3,0 NuGet soit disponible pour les nouveaux utilisateurs de Visual Studio. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Nous recommandons aux développeurs qui ont accès à la mise à jour de la Galerie Visual Studio d’accéder à la dernière version disponible, car nous publions une mise à jour peu après la publication de Visual Studio 2015 qui contient la prise en charge du développement Windows 10.

Au total, nous avons clôturé 240 problèmes dans la version 3,0, et vous pouvez consulter la [liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problèmes connus

Un certain nombre de problèmes connus ont été fournis avec cette version, et tous ces éléments ont été corrigés dans notre version de 3,1 planifiée pour coïncider avec la publication de Windows 10 le 29 juillet.  Vous pouvez mettre à jour votre extension Visual Studio à partir de la Galerie sur ou après cette date pour résoudre ces problèmes connus.

*  La traduction n’est pas fournie pour l’étiquette « ne plus afficher ce message » dans la fenêtre d’aperçu et l’étiquette « auteurs » dans la fenêtre Description du package.
*  Lorsque vous travaillez sur un projet à l’aide du contrôle de code source TFS, NuGet ne peut pas présenter l’interface utilisateur du gestionnaire de package si le fichier Nuget.Config est marqué en lecture seule.
   * **Solution de contournement** Consultez le fichier à partir de TFS.
*  Le texte de la « barre de redémarrage » jaune dans la fenêtre PowerShell NuGet n’est pas visible lorsque vous utilisez le thème Visual Studio Dark.
   * **Solution de contournement** Utilisez le thème Visual Studio Light.


## <a name="summary-of-top-issues-resolved"></a>Résumé des principaux problèmes résolus

* [Appels fréquents de mise à jour du réseau lors de l’actualisation de la fenêtre du gestionnaire de package](https://github.com/NuGet/Home/issues/515)
* [Défilement différé lors du passage à l’affichage installé dans le gestionnaire de package](https://github.com/NuGet/Home/issues/519)
* [Les appels réseau doivent être exécutés sur un thread d’arrière-plan](https://github.com/NuGet/Home/issues/516)
* [Ajout de la case à cocher « ne pas afficher la fenêtre d’aperçu »](https://github.com/NuGet/Home/issues/566)
* [Ajout de la limitation des processus pour réduire l’utilisation du processeur](https://github.com/NuGet/Home/issues/356)
* Amélioration de la gestion des références de bibliothèque de classes portables
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Le service de saisie semi-automatique respecte la casse](https://github.com/NuGet/Home/issues/198)
* [Mettre à jour pour réintroduire les informations d’identification d’authentification de base](https://github.com/NuGet/Home/issues/456)
* [Amélioration de la journalisation des erreurs](https://github.com/NuGet/Home/issues/407)
* [Amélioration des messages d’erreur PowerShell lors de l’appel de Update-Package](https://github.com/NuGet/Home/issues/5)
* [Correction du lien « en savoir plus sur les options » pour éviter les pannes sur Windows 10](https://github.com/NuGet/Home/issues/822)
* [Paramètre de case à cocher conserver les préversions](https://github.com/NuGet/Home/issues/732)
* [Amélioration des performances de collecte grâce à la mise en cache des résultats dans les projets d’une solution](https://github.com/NuGet/Home/issues/721)
* [Plusieurs packages peuvent être collectés en parallèle](https://github.com/NuGet/Home/issues/713)
* [Suppression de la commande Install-Package-force](https://github.com/NuGet/Home/issues/697)

Gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces à mesure que nous nous sommes prêts à fournir un support pour le développement Windows 10.