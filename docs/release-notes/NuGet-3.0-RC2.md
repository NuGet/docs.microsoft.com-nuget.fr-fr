---
title: Notes de publication de NuGet 3,0 RC2
description: Notes de publication de NuGet 3,0 RC2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780274"
---
# <a name="nuget-30-rc2-release-notes"></a>Notes de publication de NuGet 3,0 RC2

Notes de publication de [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Notes de publication de NuGet 3,0](../release-notes/nuget-3.0.0.md)

NuGet 3,0 RC2 a été publié le 3 juin 2015 en tant que version intermédiaire disponible à partir de la Galerie d’extensions Visual Studio 2015 et de [CodePlex](https://nuget.codeplex.com/releases/view/615507). Cette version comporte un certain nombre de correctifs de bogues et d’améliorations des performances que nous avons pensés à libérer avant la version finale de Visual Studio 2015. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Au total, nous avons clôturé 158 problèmes dans cette version, et vous pouvez consulter la [liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

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

Téléchargez cette [mise à jour sur l’extension NuGet](https://nuget.codeplex.com/releases/view/615507) à partir de CodePlex et gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces de NuGet 3,0 !