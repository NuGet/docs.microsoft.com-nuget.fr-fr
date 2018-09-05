---
title: Notes de publication de NuGet 3.0 RC2
description: Notes de publication pour NuGet 3.0 RC2, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545819"
---
# <a name="nuget-30-rc2-release-notes"></a>Notes de publication de NuGet 3.0 RC2

[Notes de version RC de NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [Notes de publication de NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 a été publiée le 3 juin 2015 en tant qu’une version intermédiaire à partir de la galerie d’extensions Visual Studio 2015 et [Codeplex](https://nuget.codeplex.com/releases/view/615507). Cette version comporte un nombre importants de correctifs de bogues et améliorations des performances que nous avons pensé étaient importantes de mise à jour avant la version de Visual Studio 2015 terminée. Cette version de l’extension NuGet est uniquement disponible pour Visual Studio 2015.

Au total, nous avons fermé 158 problèmes dans cette version, et vous pouvez consulter le [la liste complète des problèmes sur GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

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

Téléchargez ce [mettre à jour à l’extension NuGet](https://nuget.codeplex.com/releases/view/615507) à partir de Codeplex et gardez un œil [notre blog](http://blog.nuget.org) pour plus de progression et de publicités pour NuGet 3.0 !