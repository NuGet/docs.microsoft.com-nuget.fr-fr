---
title: Notes de publication de NuGet 3.0 Preview
description: Notes de publication pour NuGet 3.0 Preview, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546463"
---
# <a name="nuget-30-preview-release-notes"></a>Notes de publication de NuGet 3.0 Preview

[Notes de version de RC NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [Notes de publication de NuGet 3.0 bêta](../release-notes/nuget-3.0-beta.md)

Version préliminaire de NuGet 3.0 a été publiée le 12 novembre 2014 en tant que partie de la version de Visual Studio 2015 Preview. Nous avons publié la version préliminaire de NuGet 3.0. Il s’agit d’une publication importante pour nous (quoiqu’une version préliminaire), et nous avons hâte de commencer à recevoir des commentaires sur nos modifications.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Cette version d’évaluation NuGet 3.0 est incluse dans Visual Studio 2015 Preview. Nous travaillons à sortir supprime de la version préliminaire pour Visual Studio 2012 et Visual Studio 2013 très bientôt. Nous avons indiqué précédemment notre intention à [interrompre les mises à jour pour Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), et nous avons fait cette décision difficile.

## <a name="brand-new-ui"></a>Toute nouvelle interface utilisateur

La première chose que vous remarquerez sur NuGet 3.0 Preview est notre toute nouvelle IU. Il n’est plus une boîte de dialogue modale ; Il est désormais une fenêtre de document Visual Studio complet. Cela vous permet d’ouvrir l’interface utilisateur pour plusieurs projets (et/ou la solution) en une seule fois, détacher la fenêtre vers un autre moniteur, ancrer mais vous le feriez comme, etc.

![La nouvelle UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Outre les différences d’utilisation en raison de l’abandon de la boîte de dialogue modale, nous avons également un grand nombre de nouvelles fonctionnalités dans la nouvelle interface utilisateur.

### <a name="version-selection"></a>Sélection de la version

Peut-être le meilleur demandé la fonctionnalité d’interface utilisateur est de permettre la sélection de version pour l’installation de package et de mise à jour--elle est désormais disponible.

![Sélection de Version de package](./media/NuGet-3.0-Preview/version-selection.png)

Si vous installez ou que la mise à jour un package, la liste déroulante de version vous permet de voir toutes les versions disponibles pour le package, avec certaines versions notables promues vers le haut de la liste de sélection simple. Vous n’avez plus besoin d’utiliser la PowerShell Console pour obtenir des versions spécifiques qui ne sont pas la dernière version.

### <a name="combined-installedonlineupdates-workflows"></a>Combiner des flux de travail/en ligne/mises à jour installées

Notre interface utilisateur précédent avait 3 onglets pour installé, en ligne et les mises à jour. Les packages répertoriés ont été spécifiques à ces flux de travail et les actions disponibles ont été spécifiques pour les flux de travail. Bien que ça me semblait logique, que nous avons entendu dire que beaucoup d'entre vous devriez souvent obtenir dépassé par cette séparation.

Nous disposons désormais d’une expérience combinée, où vous pouvez installer, mettre à jour ou désinstaller un package, quel que soit la façon dont vous avez obtenu le package sélectionné. Pour faciliter le flux de travail spécifiques, nous disposons désormais d’une liste déroulante de filtre qui vous permet de filtrer les packages visibles, mais ensuite les actions disponibles pour le package sont cohérentes.

![Désinstaller un Package](./media/NuGet-3.0-Preview/uninstall-package.png)

En utilisant le filtre « Installé », vous pouvez facilement voir vos packages installés, que celles qui ont des mises à jour disponibles, et ensuite vous pouvez désinstaller ou mettre à jour le package en modifiant la sélection de la version pour voir modifier l’action disponible.

![Mettre à jour un Package](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidation de version

Il est courant d’utiliser le même package installé dans plusieurs projets dans votre solution. Parfois, les versions installées dans chaque projet peuvent passer et il est nécessaire de consolider les versions en cours d’utilisation. Version préliminaire de NuGet 3.0 introduit une nouvelle fonctionnalité pour ce cas précis.

La fenêtre de gestion de package au niveau de la solution sont accessibles en cliquant sur la solution et en choisissant de gérer les Packages NuGet pour la Solution. À partir de là, si vous sélectionnez un package est installé dans plusieurs projets, mais avec différentes versions en cours d’utilisation, une nouvelle action « Consolider » devient disponible. Dans la capture d’écran ci-dessous, `Newtonsoft.Json` a été installé dans le `SamplesClassLibrary` avec version `6.0.4` et installés dans `SamplesConsoleApp` avec la version `5.0.4`.

![Consolider des Versions](./media/NuGet-3.0-Preview/consolidate.png)

Voici le flux de travail pour la consolidation sur une version unique.

1. Sélectionnez le `Newtonsoft.Json` package dans la liste
1. Choisissez `Consolidate` à partir de la `Action` liste déroulante
1. Utilisez le `Version` liste déroulante pour sélectionner la version à être consolidés sur
1. Cochez les cases pour les projets qui doivent être consolidés sur cette version (Notez que les projets déjà sur la version sélectionnée seront grisés)
1. Cliquez sur le `Consolidate` bouton pour effectuer la consolidation

### <a name="operation-previews"></a>Aperçus d’opération

Quel que soit l’opération que vous effectuez une--installation/mise à jour/désinstallation--la nouvelle interface utilisateur offre désormais un moyen pour prévisualiser les modifications qui vont être apportées à votre projet. Cette version d’évaluation affiche de nouveaux packages qui seront installés, packages qui seront mis à jour et les packages qui seront désinstallés, ainsi que des packages qui seront inchangés pendant l’opération.

Dans l’exemple ci-dessous, nous pouvons voir que l’installation Microsoft.AspNet.SignalR entraîne quelques modifications au projet.

![Aperçu de l’installation de SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Options d’installation

À l’aide de la PowerShell Console, vous avez un contrôle sur les deux options d’installation notables. Nous avons maintenant ces fonctionnalités dans l’interface utilisateur ainsi. Vous pouvez maintenant contrôler le comportement de résolution de dépendance pour la sélection des versions des dépendances.

![Comportement de dépendance](./media/NuGet-3.0-Preview/dependency-behavior.png)

Vous pouvez également spécifier l’action à entreprendre lorsque des fichiers de contenu à partir de packages sont en conflit avec les fichiers déjà présents dans votre projet.

![Action de conflit de fichiers](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Le défilement infini

Nous avons utilisé pour obtenir un peu de commentaires sur notre interface utilisateur ayant les deux le défilement et de pagination paradigmes lors de l’énumération des packages. Il était assez courant d’avoir à faire défiler vers le bas de la liste courte et cliquez sur le numéro de page suivant, puis faites défiler vers le nouveau. Avec la nouvelle interface utilisateur, nous avons implémenté un défilement infini dans la liste des packages afin qu’il vous suffit de faire défiler--la pagination n’est plus.

![Le défilement infini](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Rendre le travail, votre expérience, rapide, rendent Pretty

Nous sommes heureux d’obtenir cette nouvelle interface utilisateur pour essayer. Au cours de cette étape de la version préliminaire, nous avons été suivant la bonne l’adage « faire en fonctionnent, rendent rapide, faire ça. » Dans cette version préliminaire, nous avons accompli la majeure partie de cet objectif premier--il fonctionne. Nous savons qu’il n’est pas assez rapide encore, et nous savons qu’il n’est pas tout à fait assez encore. Approbation que nous allons travailler sur ces objectifs entre maintenant et la version RC. En attendant, nous aimerions avoir votre avis sur le *convivialité* de l’interface utilisateur nouvelle--le flux de travail, les opérations et comment il *semble* à utiliser la nouvelle interface utilisateur.

Il existe deux fonctions que nous avons supprimé par rapport à l’interface utilisateur ancien. Un d’eux est intentionnel et autres celui n’a pas simplement obtenir effectuée à temps.

#### <a name="searching-all-package-sources"></a>Recherche de Sources de Package « Tout »

L’interface utilisateur ancien autorisés vous permettent d’effectuer une recherche de package par rapport à toutes vos sources de package. Nous avons supprimé cette fonctionnalité dans l’interface utilisateur et nous n’être remettant il. Cette fonctionnalité permet d’effectuer des opérations de recherche sur toutes vos sources de package, d’imbriquer les résultats et tentez de classer les résultats en fonction de votre sélection de tri.

Nous avons constaté que la recherche de pertinence est vraiment difficile à imbriquer. Pourriez imaginer effectuant une recherche sur Google et Bing et fusionnez les résultats ensemble ? En outre, cette fonctionnalité a été lente et faciles à *accidentellement* utilisation et nous pensons il s’agissait rarement réellement utile. En raison des problèmes lorsque la fonctionnalité introduite, nous avons reçu un nombre de rapports de bogues sur celui-ci pourrait jamais ont été résolus.

#### <a name="update-all"></a>Tout mettre à jour

Nous avons utilisé pour avoir un bouton « Tout mettre à jour » dans l’ancienne interface utilisateur qui n’y figure pas dans la nouvelle interface utilisateur encore. Nous sera ressusciter cette fonctionnalité pour notre version RC.

## <a name="new-clientserver-api"></a>Nouveau Client/serveur API

En plus de toutes les nouvelles fonctionnalités de notre nouvelle interface utilisateur de gestion de package, nous avons également travaillé sur certains détails d’implémentation pour le protocole client/serveur de NuGet. Le travail réalisé consiste à créer des « V3 d’API » pour NuGet, qui est conçue autour de haute disponibilité pour des scénarios critiques telles que la restauration de package et installation des packages. La nouvelle API est basée sur REST et hypermédia et nous avons sélectionné [JSON-LD](http://json-ld.org) comme notre format de ressource.

Dans les bits de la version préliminaire de NuGet 3.0, vous consultez une nouvelle source de package appelée « preview.nuget.org » dans la liste déroulante source de package. Si vous sélectionnez cette source de package, nous allons utiliser notre nouvelle API au lieu de cela pour vous connecter à nuget.org. Nous avons apporté l’aperçu de la source disponibles dans l’interface utilisateur pendant que nous continuons à tester, de réviser et d’améliorer la nouvelle API. Dans NuGet 3.0 RC, cette nouvelle source de package basé sur v3 d’API remplacera la source du package v2 « nuget.org ».

En dépit de l’investissement que nous mettons vers v3 d’API, nous avons apporté toutes ces nouvelles fonctionnalités fonctionnent également avec notre protocole v2 des API existant, ce qui signifie qu’ils fonctionneront avec des sources de package existant autre que nuget.org également.

## <a name="new-features-coming"></a>Nouvelles fonctionnalités à venir

Entre maintenant et 3.0 RTM, nous travaillons également sur certaines nouvelles fonctionnalités de NuGet fondamentale, au-delà de ce que vous voyez dans l’interface utilisateur. Voici une courte liste de domaines d’investissement marquants :

1. Nous avons établi un partenariat avec Visual Studio et MSBuild pour obtenir les équipes [NuGet approfondie de la plateforme](http://blog.nuget.org/20141014/in-the-platform.html).
1. Nous nous efforçons d’abandonner les conventions de package utilisé au moment de l’installation et l’appliquer à la place de ces conventions au moment de l’empaquetage en introduisant un nouvel « autorité » [manifeste du package](http://blog.nuget.org/20141023/package-manifests.html).
1. Nous travaillons à refactoriser le package NuGet codebase pour rendre les composants client et serveur réutilisables dans des domaines différents au-delà de la gestion de package dans Visual Studio.
1. Nous nous intéressons à la notion de « dépendances privés » où un package peut indiquer qu’il a des dépendances sur d’autres packages pour les détails d’implémentation, et ces dépendances ne doivent pas être exposés en tant que dépendances de niveau supérieur.

## <a name="stay-tuned"></a>Restez connecté

Veuillez garder un œil sur [notre blog](http://blog.nuget.org) pour plus de progression et de publicités pour NuGet 3.0 !