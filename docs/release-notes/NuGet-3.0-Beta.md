---
title: Notes de publication de NuGet 3,0 Beta
description: Notes de publication de NuGet 3,0 Beta, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776625"
---
# <a name="nuget-30-beta-release-notes"></a>Notes de publication de NuGet 3,0 Beta

Notes de publication de [NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)  |  [Notes de publication de NuGet 3,0 RC](../release-notes/nuget-3.0-rc.md)

La version bêta de NuGet 3,0 a été publiée le 23 février 2015 pour la version Visual Studio 2015 CTP 6. Cette version signifie beaucoup pour notre équipe, car nous avons un certain nombre d’améliorations de l’architecture et des performances à partager, et nous sommes ravis de commencer à paramétrer les paramètres de performances sur notre service nuget.org.

Nous vous recommandons vivement de désinstaller toute version antérieure de l’extension de Visual Studio 2015 NuGet avant d’installer cette nouvelle version.  Si vous rencontrez des problèmes avec cette version de l’extension, nous vous recommandons de revenir à la [version antérieure](http://nuget.codeplex.com/downloads/get/909582) pour une utilisation avec visual studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Vous pouvez installer cette version bêta de NuGet 3,0 dans la Galerie d’extensions Visual Studio 2015 CTP 6. Nous travaillons à la préversion de Visual Studio 2012 et Visual Studio 2013 très bientôt. Nous avons précédemment partagé notre intention de mettre fin à [des mises à jour pour Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)et nous avons fait de cette décision difficile.

## <a name="new-clientserver-api"></a>Nouvelle API client/serveur

Nous travaillons sur des détails d’implémentation pour le protocole client/serveur de NuGet. Le travail que nous avons fait est de créer « API V3 » pour NuGet, conçu autour de la haute disponibilité pour les scénarios critiques, tels que la restauration de packages et l’installation de packages. La nouvelle API est basée sur REST et hypermédia et nous avons sélectionné [JSON-LD](http://json-ld.org) comme format de ressource.

Dans les bits NuGet 3,0 bêta, vous voyez une nouvelle source de package appelée « api.nuget.org » dans la liste déroulante source du package.   Si vous sélectionnez la source du package, nous allons utiliser notre nouvelle API plutôt que de vous connecter à nuget.org. Dans NuGet 3,0 RC, cette nouvelle source de package basée sur l’API V3 remplace la source de package « nuget.org » basée sur v2.  Nous vous recommandons de désactiver toutes les autres sources de package public et de conserver uniquement api.nuget.org comme référentiel de package public.

Nous avons beaucoup de temps à créer notre API V3 et continueront à gérer l’API v2 standard pour les anciens clients cherchant à accéder au référentiel public.

## <a name="updated-ui"></a>Interface utilisateur mise à jour

Nous avons amélioré l’interface utilisateur dans cette version pour inclure une zone de liste déroulante qui vous permettra de choisir une action à effectuer avec le package et de faire passer le bouton Aperçu dans une case à cocher dans la zone Options de l’écran.  La zone options n’est plus réductible et fournit maintenant un lien d’aide décrivant les options disponibles.

![Nouvelle interface utilisateur NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Journalisation des opérations

Nous avons supprimé la fenêtre modale avec des informations de journalisation qui apparaîtraient rapidement et sont masquées lors de l’installation ou de la désinstallation de.  Cette fenêtre n’a ajouté aucune valeur lorsque vous souhaitez vraiment voir les informations ou pouvoir les copier et les coller.  Au lieu de cela, nous redirigeons maintenant l’ensemble de la journalisation de la sortie dans le volet gestionnaire de package de la fenêtre sortie.  Nous pensons que cela est plus agréable et similaire à un rapport de build classique que vous souhaiteriez inspecter.


### <a name="focus-on-performance"></a>Concentrez-vous sur les performances

Nous avons apporté de nombreuses modifications au nom de l’amélioration des performances des recherches NuGet et des extractions.  C’était notre préoccupation numéro un de nos clients et nous voulons nous assurer que nous l’avons traitée dans cette version.  Nous avons réglé nos serveurs, développé un nouveau CDN et amélioré la logique de correspondance des requêtes pour vous permettre de vous fournir des résultats de recherche de package plus pertinents et plus rapides.

Pendant cette phase du développement de NuGet 3,0, nous allons ajuster et surveiller le service nuget.org pour nous assurer que nous offrons une expérience améliorée.  Nous ne prévoyons pas d’entreprendre de temps d’arrêt, mais vous ajouterez et modifierez les ressources du service.  Gardez un œil sur notre [flux Twitter](http://twitter.com/nuget) pour plus d’informations sur la modification de la configuration du service.

## <a name="building-nuget-with-nuget"></a>Génération de NuGet avec NuGet

Nous avons maintenant remanié nos clients NuGet en plusieurs composants qui sont eux-mêmes intégrés aux packages NuGet. Cette réutilisation de nos propres bibliothèques nous oblige à créer des composants réutilisables qui peuvent être empaquetés correctement.  Nous avons pu éliminer le code dupliqué et nous avons appris à mieux configurer notre processus de développement afin de prendre en charge le besoin de créer des packages dans nos solutions.  Recherchez un billet de blog bientôt là où nous parlerons de la structure des projets de code et de la façon dont le processus de génération fonctionne.

## <a name="stay-tuned"></a>Restez informé

Gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces de NuGet 3,0 !
