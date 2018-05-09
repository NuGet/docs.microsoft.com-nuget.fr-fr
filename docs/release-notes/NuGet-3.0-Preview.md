---
title: Notes de mise à jour de NuGet 3.0 Preview
description: Notes de publication pour l’aperçu de 3.0 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 67c217e52d975ed8f6889cd69f9b7e0d52b3a119
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-preview-release-notes"></a>Notes de mise à jour de NuGet 3.0 Preview

[Notes de version RC de NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [notes de mise à jour de NuGet 3.0 bêta](../release-notes/nuget-3.0-beta.md)

Version préliminaire de NuGet 3.0 a été publiée le 12 novembre 2014 en tant que partie de la version de Visual Studio 2015 Preview. Nous avons publié NuGet 3.0 Preview. Il s’agit d’une version big pour nous (quoiqu’une version d’évaluation), et nous sommes heureux de commencer à obtenir des commentaires sur nos modifications.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Cette version d’évaluation 3.0 NuGet est incluse dans Visual Studio 2015 Preview. Nous nous efforçons d’atteindre supprime de la version préliminaire de Visual Studio 2012 et Visual Studio 2013 très bientôt. Nous avons indiqué précédemment notre intention [interrompre les mises à jour pour Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), et nous avons apporté cette décision difficile.

## <a name="brand-new-ui"></a>Nouvelle interface utilisateur

La première chose que vous remarquerez sur la version préliminaire de NuGet 3.0 est notre interface utilisateur nouvelle. Il n’est plus une boîte de dialogue modale ; Il est désormais une fenêtre de document Visual Studio complète. Cela vous permet à ouvrir l’interface utilisateur pour plusieurs projets (et/ou la solution) en une seule fois, détacher la fenêtre vers un autre moniteur, ancrer toutefois vous le feriez comme, etc.

![La nouvelle UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Au-delà de différences de facilité d’utilisation en raison de l’abandon de la boîte de dialogue modale, nous avons également un grand nombre de nouvelles fonctionnalités dans la nouvelle interface utilisateur.

### <a name="version-selection"></a>Sélection de la version

Par exemple le plus demandé, fonctionnalité d’interface utilisateur pour permettre la sélection de la version de l’installation et de la mise à jour--il est désormais disponible.

![Sélection de Version de package](./media/NuGet-3.0-Preview/version-selection.png)

Si vous installez ou un package de mise à jour, la liste déroulante version vous permet de voir toutes les versions disponibles pour le package, avec certaines versions notables promues vers le haut de la liste de sélection simple. Vous n’avez plus besoin d’utiliser la PowerShell Console pour obtenir des versions spécifiques qui ne sont pas la dernière version.

### <a name="combined-installedonlineupdates-workflows"></a>Flux de travail combiné/en ligne/mises à jour installées

Notre interface utilisateur précédent avait les 3 onglets pour installé, en ligne et les mises à jour. Les packages répertoriés spécifiques à ces flux de travail et les actions disponibles sont spécifiques pour les flux de travail. Pendant que nous a permis logique, que nous avons entendu que beaucoup d'entre vous devriez souvent obtenir dépassé par cette séparation.

Nous disposons désormais d’une expérience, où vous pouvez installer, mettre à jour ou désinstaller un package, quelle que soit la façon dont vous avez obtenu le package sélectionné. Pour faciliter le flux de travail spécifiques, nous disposons désormais d’une liste déroulante de filtre qui vous permet de filtrer les packages visibles, mais ensuite les actions disponibles pour le package sont cohérentes.

![Désinstallation d’un Package](./media/NuGet-3.0-Preview/uninstall-package.png)

En utilisant le filtre « Installé », vous pouvez facilement voir vos packages installés, lesquels ont des mises à jour disponibles, et puis vous pouvez désinstaller ou mettre à jour le package en modifiant la sélection de la version pour voir modifier l’action disponible.

![Mettre à jour un Package](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidation de version

Il est courant d’utiliser le même package installé dans plusieurs projets dans votre solution. Parfois, les versions installées dans chaque projet peuvent dérive éloignés et il est nécessaire de consolider les versions en cours d’utilisation. Version préliminaire de NuGet 3.0 introduit une nouvelle fonctionnalité pour simplement ce scénario.

La fenêtre de gestion des solutions au niveau du package est accessible en cliquant sur la solution et en choisissant de gérer les Packages NuGet pour la Solution. À partir de là, si vous sélectionnez un package qui est installé dans plusieurs projets, mais avec différentes versions en cours d’utilisation, une nouvelle action de « Consolider » devient disponible. Dans la capture d’écran ci-dessous, `Newtonsoft.Json` a été installé dans le `SamplesClassLibrary` avec la version `6.0.4` et est installé dans `SamplesConsoleApp` avec la version `5.0.4`.

![Consolider des Versions](./media/NuGet-3.0-Preview/consolidate.png)

Voici le flux de travail pour la consolidation sur une version unique.

1. Sélectionnez le `Newtonsoft.Json` package dans la liste
1. Choisissez `Consolidate` à partir de la `Action` liste déroulante
1. Utilisez le `Version` menu déroulant pour sélectionner la version à être consolidés sur
1. Cochez les cases pour les projets qui doivent être consolidées sur cette version (Notez que les projets déjà sur la version sélectionnée seront grisés)
1. Cliquez sur le `Consolidate` bouton pour effectuer la consolidation

### <a name="operation-previews"></a>Aperçus d’opération

Quelle que soit l’opération que vous effectuez une--installation/mise à jour/désinstallation--la nouvelle interface utilisateur propose désormais un moyen de visualiser les modifications apportées à votre projet. Cet aperçu affiche de nouveaux packages qui seront installées, des packages qui seront mises à jour et des packages qui seront désinstallés, ainsi que des packages qui seront inchangées pendant l’opération.

Dans l’exemple ci-dessous, nous pouvons voir que l’installation Microsoft.AspNet.SignalR entraîne quelques modifications pour le projet.

![Afficher un aperçu de SignalR lors de l’installation](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Options d’installation

À l’aide de la PowerShell Console, vous avez un contrôle sur les deux options d’installation importants. Nous avons maintenant ces fonctionnalités dans l’interface utilisateur également. Vous pouvez désormais contrôler le comportement de résolution de dépendance pour le mode de sélection des versions des dépendances.

![Comportement des dépendances](./media/NuGet-3.0-Preview/dependency-behavior.png)

Vous pouvez également spécifier l’action à entreprendre lorsque les fichiers de contenu à partir de packages sont en conflit avec les fichiers déjà présents dans votre projet.

![Action de conflit de fichiers](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Défilement infinie

Nous avons utilisé pour obtenir un peu de commentaires sur notre interface utilisateur ayant les deux le défilement et de pagination paradigmes lors de l’énumération des packages. Il est assez courant d’avoir à faire défiler vers le bas de la liste courte et cliquez sur le numéro de page suivant, faites défiler vers le nouveau. Avec la nouvelle interface utilisateur, nous avons implémenté infinie défilement dans la liste des packages afin que vous devez uniquement faire défiler--n’y a plus de la pagination.

![Défilement infinie](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Qu’il fonctionne, rendre rapide, rendre Pretty

Nous sommes heureux d’atteindre cette nouvelle interface utilisateur vous permet d’essayer. Au cours de cette étape de la version préliminaire, nous avons suivant la bonne l’adage « faire qu’il fonctionne, rendre rapide, mettre en forme. » Dans cette version préliminaire, nous avons effectue la majeure partie de ce premier objectif--il fonctionne. Nous savons qu’il n’est pas assez rapide encore, et nous savons qu’il n’est pas tout à fait assez encore. Approbation de travailler sur ces objectifs entre aujourd'hui et la version RC. En attendant, nous aimerions avoir votre avis sur la *facilité d’utilisation* de l’interface utilisateur nouvelle--le flux de travail, les opérations et comment il *estime* à utiliser la nouvelle interface utilisateur.

Il existe deux fonctions que nous avons supprimé par rapport à l’interface utilisateur ancien. Un de ces n’est pas intentionnel, et autre n’a pas été simplement obtenir effectuée dans le temps.

#### <a name="searching-all-package-sources"></a>Recherche de Sources de Package « Tous »

L’interface utilisateur ancien autorisées vous permet d’effectuer une recherche de package par rapport à toutes vos sources de package. Nous avons supprimé cette fonctionnalité dans l’interface utilisateur et nous ne sera pas être sa mise en retour. Cette fonctionnalité permet d’effectuer des opérations de recherche sur toutes vos sources de package, imbriquer les résultats et tentez de classer les résultats en fonction de votre sélection de tri.

Nous avons détecté que la pertinence de la recherche est très difficile à imbriquer. Pourriez vous imaginez effectuant une recherche sur Google et Bing et a les résultats ensemble ? En outre, cette fonctionnalité a été lente, faciles à *accidentellement* utilisation et nous pensons qu’il a été rarement réellement utile. En raison de problèmes lorsque la fonctionnalité a été introduite, nous avons reçu un nombre de rapports de bogues sur ce qui peut ne jamais été résolu.

#### <a name="update-all"></a>Tout mettre à jour

Nous avons utilisé dispose d’un bouton « Tout mettre à jour » dans l’interface utilisateur ancien qui n’existait pas dans la nouvelle interface utilisateur encore. Nous sera réactiver réactiver cette fonctionnalité pour notre version RC.

## <a name="new-clientserver-api"></a>Nouveau Client/serveur API

En plus de toutes les nouvelles fonctionnalités de gestion des packages notre nouvelle interface utilisateur, nous avons également travaillé sur certains détails d’implémentation pour le protocole de NuGet client/serveur. Le travail que nous avons faites consiste à créer des « API v3 » pour NuGet, qui est conçue autour de haute disponibilité pour des scénarios critiques telles que la restauration des packages et installation des packages. La nouvelle API est basée sur REST et hypermédia et nous avons sélectionné [JSON-LD](http://json-ld.org) comme notre format de ressource.

Dans les bits de NuGet 3.0 Preview, vous consultez une nouvelle source de package appelée « preview.nuget.org » dans la liste déroulante source de package. Si vous sélectionnez cette source de package, nous allons utiliser notre nouvelle API plutôt à se connecter à nuget.org. Nous avons simplifié l’aperçu de la source disponibles dans l’interface utilisateur pendant que nous continuons à tester, passez en revue et améliorer la nouvelle API. Cette nouvelle source du package de base v3 API remplace dans NuGet 3.0 RC, la source du package « nuget.org « v2.

En dépit de l’investissement, que nous mettons en API v3, nous avons apporté toutes ces nouvelles fonctionnalités fonctionnent également avec notre existant protocole API v2, ce qui signifie qu’ils fonctionnent avec des sources de package existant autre que nuget.org également.

## <a name="new-features-coming"></a>Nouvelles fonctionnalités à venir

Entre maintenant et 3.0 RTM, nous travaillons également sur certaines nouvelles fonctionnalités de NuGet fondamentale, au-delà de ce que vous voyez dans l’interface utilisateur. Voici une courte liste des domaines d’investissement marquants :

1. Nous mettons en partenariat avec Visual Studio et MSBuild équipes pour obtenir [NuGet profond dans la plateforme](http://blog.nuget.org/20141014/in-the-platform.html).
1. Nous nous efforçons d’abandonner les conventions de package au moment de l’installation et l’appliquer à la place de ces conventions au moment de l’empaquetage en introduisant un nouveau faisant « autorité » [le manifeste du package](http://blog.nuget.org/20141023/package-manifests.html).
1. Nous travaillons à refactoriser NuGet codebase pour permettre la réutilisation des composants client et serveur dans des domaines différents au-delà de la gestion des packages dans Visual Studio.
1. Nous nous intéressons à la notion de « dépendances privés » où un package peut indiquer qu’il possède des dépendances sur d’autres packages pour les détails d’implémentation, et ces dépendances ne doivent pas être exposés en tant que dépendances de niveau supérieur.

## <a name="stay-tuned"></a>Tenez-vous informé

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus d’avancement et les annonces de NuGet 3.0 !