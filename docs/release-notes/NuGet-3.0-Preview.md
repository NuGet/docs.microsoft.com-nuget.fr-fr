---
title: Notes de publication de NuGet 3,0 Preview
description: Notes de publication de NuGet 3,0 Preview, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780332"
---
# <a name="nuget-30-preview-release-notes"></a>Notes de publication de NuGet 3,0 Preview

Notes de publication de [NuGet 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Notes de publication de NuGet 3,0 Beta](../release-notes/nuget-3.0-beta.md)

La version préliminaire de NuGet 3,0 a été publiée le 12 novembre 2014 dans le cadre de la version préliminaire de Visual Studio 2015. Nous avons publié la version préliminaire de NuGet 3,0. C’est une grande version pour nous (bien qu’une version préliminaire) et nous sommes ravis de commencer à obtenir des commentaires sur nos modifications.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Cette version préliminaire de NuGet 3,0 est incluse dans la version préliminaire de Visual Studio 2015. Nous travaillons à la préversion de Visual Studio 2012 et Visual Studio 2013 très bientôt. Nous avons précédemment partagé notre intention de mettre fin à [des mises à jour pour Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)et nous avons fait de cette décision difficile.

## <a name="brand-new-ui"></a>Nouvelle interface utilisateur

La première chose que vous remarquez à propos de NuGet 3,0 Preview est notre nouvelle interface utilisateur. Il ne s’agit plus d’une boîte de dialogue modale. Il s’agit maintenant d’une fenêtre de document Visual Studio complète. Cela vous permet d’ouvrir l’interface utilisateur de plusieurs projets (et/ou de la solution) à la fois, de détacher la fenêtre sur un autre moniteur, de l’ancrer, si vous le souhaitez, etc.

![Nouvelle interface utilisateur NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Au-delà des différences d’utilisabilité en raison de l’abandon de la boîte de dialogue modale, nous disposons également d’un grand nombre de nouvelles fonctionnalités dans la nouvelle interface utilisateur.

### <a name="version-selection"></a>Sélection de la version

La fonctionnalité la plus demandée de l’interface utilisateur est peut-être de permettre la sélection de version pour l’installation et la mise à jour du package. cela est désormais disponible.

![Sélection de la version du package](./media/NuGet-3.0-Preview/version-selection.png)

Si vous installez ou mettez à jour un package, la liste déroulante version vous permet de voir toutes les versions disponibles pour le package, avec certaines versions notables promues en haut de la liste pour faciliter la sélection. Vous n’avez plus besoin d’utiliser la console PowerShell pour récupérer des versions spécifiques qui ne sont pas les plus récentes.

### <a name="combined-installedonlineupdates-workflows"></a>Flux de travail de mise à jour/installation combinés

Notre interface utilisateur précédente comportait 3 onglets pour l’installation, la mise en ligne et les mises à jour. Les packages listés étaient spécifiques à ces flux de travail et les actions disponibles étaient également spécifiques aux flux de travail. Bien que cela semblait logique, nous avons appris qu’un grand nombre d’entre vous auraient souvent été démontés par cette séparation.

Nous avons maintenant une expérience combinée, dans laquelle vous pouvez installer, mettre à jour ou désinstaller un package, quelle que soit la façon dont vous avez sélectionné le package. Pour faciliter la gestion des flux de travail, nous disposons désormais d’une liste déroulante de filtre qui vous permet de filtrer les packages visibles, mais les actions disponibles pour le package sont cohérentes.

![Désinstaller un package](./media/NuGet-3.0-Preview/uninstall-package.png)

À l’aide du filtre « installé », vous pouvez facilement voir vos packages installés, ceux qui ont des mises à jour disponibles, puis vous pouvez désinstaller ou mettre à jour le package en modifiant la sélection de version pour voir modifier l’action disponible.

![Mettre à jour un package](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidation des versions

Il est courant d’installer le même package dans plusieurs projets au sein de votre solution. Parfois, les versions installées dans chaque projet peuvent être décomposées et il est nécessaire de consolider les versions en cours d’utilisation. La version préliminaire de NuGet 3,0 introduit une nouvelle fonctionnalité uniquement pour ce scénario.

Vous pouvez accéder à la fenêtre de gestion des packages au niveau de la solution en cliquant avec le bouton droit sur la solution et en sélectionnant gérer les packages NuGet pour la solution. À partir de là, si vous sélectionnez un package qui est installé dans plusieurs projets, mais avec des versions différentes en cours d’utilisation, une nouvelle action « consolider » devient disponible. Dans la capture d’écran ci-dessous, `Newtonsoft.Json` a été installé dans la `SamplesClassLibrary` version de `6.0.4` et installée dans `SamplesConsoleApp` avec la version `5.0.4` .

![Consolider les versions](./media/NuGet-3.0-Preview/consolidate.png)

Voici le flux de travail pour la consolidation sur une seule version.

1. Sélectionner le `Newtonsoft.Json` package dans la liste
1. Choisir `Consolidate` dans la `Action` liste déroulante
1. Utilisez la `Version` liste déroulante pour sélectionner la version à consolider
1. Cochez les cases des projets qui doivent être consolidés sur cette version (Notez que les projets déjà présents sur la version sélectionnée seront grisés)
1. Cliquez sur le `Consolidate` bouton pour effectuer la consolidation.

### <a name="operation-previews"></a>Aperçus des opérations

Quelle que soit l’opération que vous effectuez (installation/mise à jour/désinstallation), la nouvelle interface utilisateur offre désormais un moyen d’afficher un aperçu des modifications qui seront apportées à votre projet. Cette version préliminaire affiche tous les nouveaux packages qui seront installés, les packages qui seront mis à jour et les packages qui seront désinstallés, ainsi que les packages qui seront inchangés au cours de l’opération.

Dans l’exemple ci-dessous, nous pouvons voir que l’installation de Microsoft. AspNet. Signalr entraînera un certain nombre de modifications apportées au projet.

![Aperçu de l’installation de Signalr](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Options d'installation

À l’aide de la console PowerShell, vous avez eu le contrôle sur deux options d’installation notables. Nous avons également apporté ces fonctionnalités dans l’interface utilisateur. Vous pouvez maintenant contrôler le comportement de résolution de dépendance pour la sélection des versions des dépendances.

![Comportement de dépendance](./media/NuGet-3.0-Preview/dependency-behavior.png)

Vous pouvez également spécifier l’action à exécuter lorsque les fichiers de contenu des packages sont en conflit avec les fichiers qui se trouvent déjà dans votre projet.

![Action de conflit de fichiers](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Défilement infini

Nous avons utilisé pour obtenir des commentaires sur notre interface utilisateur avec les paradigmes de défilement et de pagination lors de la liste des packages. Il était assez courant de faire défiler vers le bas de la liste, de cliquer sur le numéro de la page suivante, puis de faire défiler à nouveau. Avec la nouvelle interface utilisateur, nous avons implémenté un défilement infini dans la liste des packages afin que vous n’ayez besoin de faire défiler aucune autre pagination.

![Défilement infini](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Le faire fonctionner, le rendre plus rapide, en faire un joli

Nous sommes ravis d’obtenir cette nouvelle interface utilisateur pour vous aider à essayer. Au cours de cette étape majeure de la préversion, nous avons effectué la bonne vieille adage de «faire fonctionner. Dans cette version préliminaire, nous avons accompli la plus grande partie de ce premier objectif : cela fonctionne. Nous savons qu’il n’est pas encore très rapide et que nous savons qu’il n’est pas tout à fait un peu plus grand. Faites confiance au fait que nous allons travailler sur ces objectifs entre maintenant et la version RC. En attendant, nous aimerions connaître vos commentaires sur la *facilité* d’utilisation de la nouvelle interface utilisateur, les flux de travail, les opérations et la façon dont elle *semble* utiliser la nouvelle interface utilisateur.

Nous avons supprimé plusieurs fonctions par rapport à l’ancienne interface utilisateur. L’une d’entre elles était intentionnelle et l’autre n’a pas été effectuée dans le temps.

#### <a name="searching-all-package-sources"></a>Recherche de « toutes les sources de package »

L’ancienne interface utilisateur vous permettait d’effectuer une recherche dans les packages sur toutes vos sources de package. Nous avons supprimé cette fonctionnalité dans l’interface utilisateur et nous ne la revenons pas. Cette fonctionnalité permet d’effectuer des opérations de recherche sur toutes les sources de package, d’imbriquer les résultats ensemble et de tenter de classer les résultats en fonction de votre sélection de tri.

Nous avons constaté que la pertinence de la recherche est vraiment difficile à assembler ensemble. Pourriez-vous imaginer effectuer une recherche sur Google et Bing et tisser les résultats ensemble ? En outre, cette fonctionnalité était lente, facile à utiliser *accidentellement* et nous pensons qu’elle était rarement utile. En raison des problèmes que la fonctionnalité a introduits, nous avons reçu un certain nombre de rapports de bogues qui n’ont jamais été résolus.

#### <a name="update-all"></a>Tout mettre à jour

Nous avons utilisé un bouton « mettre à jour tout » dans l’ancienne interface utilisateur qui n’existe pas encore dans la nouvelle interface utilisateur. Nous allons résusciter cette fonctionnalité pour notre version RC.

## <a name="new-clientserver-api"></a>Nouvelle API client/serveur

En plus de toutes les nouvelles fonctionnalités de notre nouvelle interface utilisateur de gestion des packages, nous avons également travaillé sur des détails d’implémentation pour le protocole client/serveur de NuGet. Le travail que nous avons fait est de créer « API V3 » pour NuGet, conçu autour de la haute disponibilité pour les scénarios critiques, tels que la restauration de packages et l’installation de packages. La nouvelle API est basée sur REST et hypermédia et nous avons sélectionné [JSON-LD](http://json-ld.org) comme format de ressource.

Dans les versions préliminaires de NuGet 3,0, vous voyez une nouvelle source de package appelée « preview.nuget.org » dans la liste déroulante source du package. Si vous sélectionnez la source du package, nous allons utiliser notre nouvelle API plutôt que de vous connecter à nuget.org. Nous avons rendu la source de la version préliminaire disponible dans l’interface utilisateur pendant que nous continuons à tester, à modifier et à améliorer la nouvelle API. Dans NuGet 3,0 RC, cette nouvelle source de package basée sur l’API V3 remplace la source de package « nuget.org » basée sur v2.

En dépit de l’investissement que nous plaçons dans l’API V3, nous avons fait que toutes ces nouvelles fonctionnalités fonctionnent également avec notre protocole API v2 existant, ce qui signifie qu’elles fonctionnent avec les sources de package existantes autres que nuget.org.

## <a name="new-features-coming"></a>Nouvelles fonctionnalités

Entre aujourd’hui et 3,0 RTM, nous travaillons également sur certaines nouvelles fonctionnalités élémentaires de NuGet, au-delà de ce que vous voyez dans l’interface utilisateur. Voici une brève liste de zones d’investissement importantes :

1. Nous travaillons en partenariat avec les équipes Visual Studio et MSBuild pour découvrir [NuGet plus en profondeur dans la plateforme](http://blog.nuget.org/20141014/in-the-platform.html).
1. Nous travaillons à l’abandon des conventions de package au moment de l’installation et appliquons plutôt ces conventions au moment de l’empaquetage en introduisant un nouveau [manifeste de package](http://blog.nuget.org/20141023/package-manifests.html)« faisant autorité ».
1. Nous travaillons actuellement à refactoriser le code base NuGet pour rendre les composants client et serveur réutilisables dans des domaines différents au-delà de la gestion des packages dans Visual Studio.
1. Nous étudions la notion de « dépendances privées » dans laquelle un package peut indiquer qu’il a des dépendances avec d’autres packages uniquement pour les détails d’implémentation, et ces dépendances ne doivent pas être signalées comme des dépendances de niveau supérieur.

## <a name="stay-tuned"></a>Restez informé

Gardez un œil sur [notre blog](http://blog.nuget.org) pour en savoir plus sur la progression et les annonces de NuGet 3,0 !