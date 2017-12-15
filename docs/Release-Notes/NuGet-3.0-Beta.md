---
title: "Notes de mise à jour de NuGet 3.0 bêta | Documents Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4153ff3f-f97f-4e54-b638-e844f70edf22
description: "Notes de version de NuGet 3.0 bêta, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 3.0 bêta, les correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46b2a81845f5ac06b8c80975c55fcfc33b86636e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-beta-release-notes"></a>Notes de mise à jour de NuGet 3.0 bêta

[Notes de mise à jour de NuGet 3.0 Preview](../release-notes/nuget-3.0-preview.md) | [Notes de version de NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 bêta a été publiée pour la version de Visual Studio 2015 CTP 6 23 février 2015. Cette version, on entend beaucoup à notre équipe, nous avons d’architecture et les performances des améliorations à partager et nous sommes heureux de démarrer le réglage des paramètres de performances sur notre service nuget.org.

Nous vous recommandons de désinstaller toute version antérieure de l’extension NuGet Visual Studio 2015 avant d’installer cette nouvelle version.  Si vous avez des problèmes avec cette version de l’extension, nous vous recommandons de vous revenir à la [version antérieure](http://nuget.codeplex.com/downloads/get/909582) pour une utilisation avec la version préliminaire de Visual Studio 2015.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Cette NuGet 3.0 bêta peut être installée dans la galerie d’extensions 6 Visual Studio 2015 CTP. Nous nous efforçons d’atteindre supprime de la version préliminaire de Visual Studio 2012 et Visual Studio 2013 très bientôt. Nous avons indiqué précédemment notre intention [interrompre les mises à jour pour Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), et nous avons apporté cette décision difficile.

## <a name="new-clientserver-api"></a>Nouveau Client/serveur API

Nous avons travaillé sur certains détails d’implémentation pour le protocole de NuGet client/serveur. Le travail que nous avons faites consiste à créer des « API v3 » pour NuGet, qui est conçue autour de haute disponibilité pour des scénarios critiques telles que la restauration des packages et installation des packages. La nouvelle API est basée sur REST et hypermédia et nous avons sélectionné [JSON-LD](http://json-ld.org) comme notre format de ressource.

Dans les bits de NuGet 3.0 bêta, vous verrez une nouvelle source de package appelée « api.nuget.org » dans la liste déroulante source de package.   Si vous sélectionnez cette source de package, nous allons utiliser notre nouvelle API plutôt à se connecter à nuget.org. Cette nouvelle source du package de base v3 API remplace dans NuGet 3.0 RC, la source du package « nuget.org « v2.  Nous vous recommandons de désactiver toutes les autres sources de package public et que vous laissez api.nuget.org uniquement comme référentiel package publics uniquement.

Nous avez mis beaucoup de temps dans la conception de nos API v3 et continuera à mettre à jour de l’API v2 standard pour les anciens clients la recherche accéder au référentiel public.

## <a name="updated-ui"></a>Mise à jour de l’interface utilisateur

Nous avons amélioré l’interface utilisateur dans cette version pour inclure une zone de liste déroulante qui vous permet de choisir une action à effectuer avec le package et le bouton Aperçu passé par une case à cocher dans la zone options de l’écran.  La zone options n’est plus réductible et fournit désormais un lien d’aide qui décrit les options disponibles.

![La nouvelle UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Enregistrement de l’opération

Nous avons supprimé de la fenêtre modale avec les informations de journalisation qui seraient rapidement s’affichent et masquer lors de l’installation ou la désinstallation.  Cette fenêtre n’ajouté aucune valeur lorsque vous souhaitez vraiment consulter les informations ou être en mesure de copier et coller à partir de celui-ci.  Au lieu de cela, nous allons maintenant rediriger toute la sortie de la journalisation dans le volet du Gestionnaire de Package de la fenêtre Sortie.  Nous pensons que cela est plus à l’aise et similaire à un rapport de build par défaut que vous souhaitez inspecter.


### <a name="focus-on-performance"></a>Concentrez-vous sur les performances

Nous avons apporté un grand nombre de modifications apportées au nom de l’amélioration des performances des recherches de NuGet et des extractions.  Il s’agissait de notre préoccupation principale à partir de nos clients, et nous voulions pour vous assurer que nous le traités dans cette version.  Nous avons réglé nos serveurs élaborés un nouveau CDN et amélioration de la requête Heureusement pour vous fournir les plus pertinentes de la logique de correspondance et les résultats de la recherche de package plus rapide.

Nous avant de lancer cette phase du développement de NuGet 3.0, nous paramétrage et surveillance du service nuget.org pour vous assurer que nous fournir une expérience améliorée.  Nous ne planifier de temps d’arrêt, mais sera être Ajout et modification des ressources dans le service.  Garder un œil sur nos [flux twitter](http://twitter.com/nuget) pour plus d’informations sur quand nous remplaçons la configuration du service.

## <a name="building-nuget-with-nuget"></a>NuGet de génération avec NuGet

Nous avons remanié maintenant de nos clients NuGet dans plusieurs composants qui sont eux-mêmes en cours de génération dans les packages NuGet. Réutilisation de notre propre bibliothèques nous oblige à créer des composants qui sont réutilisables et qui peut être empaqueté correctement.  Nous avons été en mesure de supprimer le code dupliqué et avez appris comment mieux configurer votre processus de développement pour prendre en charge la nécessité de créer des packages dans l’ensemble de nos solutions.  Recherchez un billet de blog bientôt où nous aborderons comment sont structurées les projets de code et le fonctionnement de nos processus de génération.

## <a name="stay-tuned"></a>Tenez-vous informé

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus d’avancement et les annonces de NuGet 3.0 !
