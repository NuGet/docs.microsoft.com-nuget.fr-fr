---
title: Notes de publication de NuGet 3.0 bêta
description: Notes de publication pour NuGet 3.0 bêta, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550911"
---
# <a name="nuget-30-beta-release-notes"></a>Notes de publication de NuGet 3.0 bêta

[Notes de publication de NuGet 3.0 Preview](../release-notes/nuget-3.0-preview.md) | [Notes de version RC de NuGet 3.0](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 bêta a été publiée le 23 février 2015 pour la version de Visual Studio 2015 CTP 6. Cette version, on entend beaucoup à notre équipe, nous avons un nombre d’améliorations d’architecture et les performances de partager, et nous avons hâte de commencer le réglage des paramètres de performances sur notre service de nuget.org.

Nous vous recommandons fortement de désinstaller toute version antérieure de l’extension NuGet Visual Studio 2015 avant d’installer cette nouvelle version.  Si vous rencontrez des problèmes avec cette version de l’extension, nous vous recommandons de vous rétablissez le [version antérieure](http://nuget.codeplex.com/downloads/get/909582) pour une utilisation avec Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Cette NuGet 3.0 bêta peut être installée dans la galerie d’extensions 6 Visual Studio 2015 CTP. Nous travaillons à sortir supprime de la version préliminaire pour Visual Studio 2012 et Visual Studio 2013 très bientôt. Nous avons indiqué précédemment notre intention à [interrompre les mises à jour pour Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), et nous avons fait cette décision difficile.

## <a name="new-clientserver-api"></a>Nouveau Client/serveur API

Nous avons travaillé sur certains détails d’implémentation pour le protocole client/serveur de NuGet. Le travail réalisé consiste à créer des « V3 d’API » pour NuGet, qui est conçue autour de haute disponibilité pour des scénarios critiques telles que la restauration de package et installation des packages. La nouvelle API est basée sur REST et hypermédia et nous avons sélectionné [JSON-LD](http://json-ld.org) comme notre format de ressource.

Dans les bits NuGet 3.0 bêta, vous consultez une nouvelle source de package appelée « api.nuget.org » dans la liste déroulante source de package.   Si vous sélectionnez cette source de package, nous allons utiliser notre nouvelle API au lieu de cela pour vous connecter à nuget.org. Dans NuGet 3.0 RC, cette nouvelle source de package basé sur v3 d’API remplacera la source du package v2 « nuget.org ».  Nous vous recommandons de désactiver toutes les autres sources de package publique d’et que vous conservez api.nuget.org uniquement par votre référentiel de packages publics uniquement.

Nous avez beaucoup de temps dans la conception de notre API v3 et continuera à mettre à jour de l’API v2 standard pour les anciens clients qui cherchent à accéder au référentiel public.

## <a name="updated-ui"></a>Mise à jour de l’interface utilisateur

Nous avons amélioré l’interface utilisateur dans cette version pour inclure une zone de liste déroulante qui vous permet de choisir une action à effectuer avec le package et passé le bouton d’aperçu par une case à cocher dans la zone des options de l’écran.  La zone des options n’est plus réductible et fournit désormais un lien d’aide qui décrit les options disponibles.

![La nouvelle UI NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Enregistrement de l’opération

Nous avons supprimé la fenêtre modale avec les informations de journalisation qui s’affichent rapidement et Masquer pendant l’installation ou de désinstallation.  Cette fenêtre n’ajouté aucune valeur lorsque vous souhaitez vraiment voir les informations ou être en mesure de copier et coller à partir de celui-ci.  Au lieu de cela, nous allons maintenant rediriger toute la sortie de journalisation dans le volet du Gestionnaire de Package de la fenêtre Sortie.  Nous pensons que c’est plus à l’aise et semblable à un rapport de génération classique que vous souhaitez inspecter.


### <a name="focus-on-performance"></a>Vous concentrer sur les performances

Nous avons apporté un grand nombre de modifications apportées au nom de l’amélioration des performances des recherches de NuGet et des extractions.  C’était notre préoccupation numéro une de nos clients, et nous souhaitions pour être sûr que nous le résolus dans cette version.  Nous avons paramétré nos serveurs, créés un nouveau CDN et amélioré la logique pour fournir des J’espère que vous le plus pertinent de correspondance de requête et résultats de la recherche de package plus rapidement.

Comme nous continuons à parcourir cette phase du développement de NuGet 3.0, nous réglage et analyse du service de nuget.org pour vous assurer que nous fournir une expérience améliorée.  Nous ne plan s’engager dans le temps d’arrêt, mais sera être Ajout et modification des ressources dans le service.  Gardez un œil sur notre [flux twitter](http://twitter.com/nuget) pour plus d’informations sur quand nous remplaçons la configuration du service.

## <a name="building-nuget-with-nuget"></a>NuGet construction avec NuGet

Nous avons été ainsi remaniée nos clients NuGet en plusieurs composants qui sont eux-mêmes en cours de génération dans les packages NuGet. Réutilisation de nos propres bibliothèques nous oblige à créer des composants qui sont réutilisables et qui peut être empaqueté correctement.  Nous avons été en mesure de supprimer le code dupliqué et savez comment mieux configurer notre processus de développement pour prendre en charge de la nécessité de créer des packages dans l’ensemble de nos solutions.  Recherchez un billet de blog bientôt où nous nous pencherons sur la façon dont les projets de code sont structurées et comment notre processus de génération fonctionne.

## <a name="stay-tuned"></a>Restez connecté

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus de progression et de publicités pour NuGet 3.0 !
