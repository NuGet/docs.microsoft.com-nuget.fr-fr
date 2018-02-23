---
title: Notes de publication NuGet 2.8 | Documents Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notes de version de NuGet 2.8, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr."
keywords: "Notes de publication NuGet 2.8, des correctifs de bogues, problèmes connus, ajouté des fonctionnalités, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39b885adc9e23eb815f65639875c4a4c27d61a4c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-28-release-notes"></a>Notes de publication NuGet 2.8

[Notes de publication NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Notes de publication](../release-notes/nuget-2.8.1.md)

NuGet 2.8 a été publié le 29 janvier 2014.

## <a name="acknowledgements"></a>Remerciements

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) : lors de la vérification de l’Id de packages de dépendance des packages de livraison.
1. [Martin Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -supprimer le suffixe $metadata lorsque persistening flux d’informations d’identification.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - prise en charge de la spécification de fichier de projet pour la commande de mise à jour de nuget.exe.
1. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -ne pas passés avec - IncludeReferencedProjects des jetons de remplacement.
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -résoudre nuget.push lever OutOfMemoryException lors de la distribution du package important.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -chemin d’accès cible incorrect correctif lorsque le projet fait référence à un autre projet CLI/C++.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -autoriser les packages doivent être installés en tant que dépendances de développement par défaut
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -supprimer implicites mises à niveau vers la dernière version du correctif logiciel
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Plusieurs bogues correctifs et améliorations pour NuGet.Server, la commande de mise en miroir de nuget.exe et d’autres.
    - Ce travail a été effectué sur plusieurs mois, avec Gregory collaboré avec nous sur le minutage de droite à intégrer dans master pour 2.8.

## <a name="patch-resolution-for-dependencies"></a>Résolution de correctif logiciel pour les dépendances

Lors de la résolution des dépendances du package, NuGet a implémenté historiquement une stratégie de sélection de la version majeure et mineure package le plus bas qui satisfait aux dépendances sur le package. Toutefois, contrairement à la version majeure et mineure, la version du correctif a été résolue toujours à la version la plus élevée. Bien que le comportement a été bien intentionné, il créé un manque de déterminisme pour l’installation de packages avec des dépendances. Prenons l'exemple suivant :

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Dans cet exemple, même si Developer1 et Developer2 installés PackageA@1.0.0, chaque terminée avec une version différente de PackageB. NuGet 2.8 modifie ce comportement par défaut tels que le comportement de résolution de dépendance pour les versions de correctif logiciel est cohérent avec le comportement pour les versions majeure et mineure. Dans l’exemple ci-dessus, puis, PackageB@1.0.0 sont installés à la suite de l’installation PackageA@1.0.0, quelle que soit la version plus récente de correctif.

## <a name="-dependencyversion-switch"></a>DependencyVersion - commutateur

Si les modifications de NuGet 2.8 le _par défaut_ comportement pour la résolution des dépendances, il ajoute également un contrôle plus précis sur le processus de résolution de dépendance via le commutateur - DependencyVersion dans la console Gestionnaire de package. Le commutateur permet la résolution des dépendances à la version la plus basse possible (comportement par défaut), la version la plus élevée possible, ou le mineur le plus élevé ou la version du correctif.  Ce commutateur fonctionne uniquement pour le package d’installation dans la commande powershell.

![Commutateur de DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Attribut de DependencyVersion

Outre le commutateur - DependencyVersion détaillés plu haut, NuGet est également autorisé pour la possibilité de définir un nouvel attribut dans le fichier Nuget.Config définir ce qu’est la valeur par défaut, si le commutateur - DependencyVersion n’est pas spécifié dans un appel à package d’installation. Cette valeur sera également être respectée par la boîte de dialogue Gestionnaire de Package NuGet pour les opérations de package d’installation. Pour définir cette valeur, ajoutez l’attribut ci-dessous à votre fichier Nuget.Config :

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Aperçu des opérations de NuGet avec - whatif

Certains packages NuGet peuvent avoir des graphiques de dépendance approfondie, et par conséquent, il peut être utile lors de l’installation, désinstaller ou mettre à jour de l’opération d’abord visualiser ce qui se produira. NuGet 2.8 ajoute le commutateur - whatif PowerShell standard pour le package d’installation, désinstaller-package et les commandes de package de mise à jour afin de permettre la visualisation de la fermeture d’ensemble des packages qui la commande sera appliquée. Par exemple, en cours d’exécution `install-package Microsoft.AspNet.WebApi -whatif` dans un site Web ASP.NET vide application donne le résultat suivant.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Package de vers une version antérieure

Il n’est pas rare d’installer une version préliminaire d’un package afin d’étudier les nouvelles fonctionnalités et décider ensuite de revenir à la dernière version stable. Avant de NuGet 2.8, il s’agissait d’un processus en plusieurs étapes de la version préliminaire package et ses dépendances, installation et la désinstallation puis la version antérieure. Avec NuGet 2.8, toutefois, le package de mise à jour maintenant annule la fermeture de l’ensemble du package (par exemple, arborescence des dépendances du package) à la version précédente.

## <a name="development-dependencies"></a>Dépendances de développement

Différents types de fonctionnalités peuvent être remis sous forme de packages NuGet - y compris les outils utilisés pour l’optimisation du processus de développement. Ces composants, s’ils peuvent vous aider dans le développement d’un nouveau package ne doivent pas être considéré comme une dépendance du nouveau package lorsqu’il est publié ultérieurement. NuGet 2.8 permet à un package pour s’identifier dans la `.nuspec` fichier comme un developmentDependency. Lors de l’installation, ces métadonnées sont également ajoutées à la `packages.config` fichier du projet dans lequel le package a été installé. Lorsque que `packages.config` fichier est analysé ultérieurement les dépendances de NuGet pendant `nuget.exe pack`, il exclut ces dépendances marquées en tant que dépendances de développement.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Fichiers de packages.config individuelles pour les différentes plateformes

Lors du développement d’applications pour plusieurs plateformes cibles, il est courant d’avoir des fichiers de projet différent pour chacun des environnements de build respectifs. Il est également courant de consommer les différents packages NuGet dans différents fichiers projet, comme packages ont des niveaux de prise en charge pour les différentes plateformes. NuGet 2.8 fournit la prise en charge améliorée pour ce scénario en créant différentes `packages.config` fichiers pour les fichiers de projet spécifiques à la plateforme différent.

![Plusieurs fichiers package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Stratégie de secours pour le Cache Local

Bien que les packages NuGet sont généralement consommées à partir d’une galerie à distance comme [la galerie NuGet](http://www.nuget.org/) à l’aide d’une connexion réseau, il existe plusieurs scénarios où le client n’est pas connecté. Sans connexion réseau, le client NuGet n’a pas pu installer correctement les packages - même lorsque ces packages étaient déjà présents sur l’ordinateur client dans le cache local NuGet. NuGet 2.8 ajoute un cache de secours automatique pour la console du Gestionnaire de package. Par exemple, lorsque la déconnexion de la carte réseau et l’installation de jQuery, la console affiche les informations suivantes :

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

La fonctionnalité de secours du cache ne nécessite pas d’arguments de commande spécifique. En outre, cache secours actuellement fonctionne uniquement dans la console du Gestionnaire de package, le comportement ne fonctionne pas actuellement dans la boîte de dialogue de gestionnaire de package.

## <a name="webmatrix-nuget-client-updates"></a>Met à jour du Client de NuGet WebMatrix

Avec NuGet 2.8, l’extension NuGet pour WebMatrix également mise à jour pour inclure de nombreux les principales fonctionnalités fournies par [NuGet 2.5](../release-notes/nuget-2.5.md). Nouvelles fonctionnalités incluent ceux tels que « Tout mettre à jour », « Version de NuGet Minimum » et consistant à autoriser le remplacement des fichiers de contenu.

Pour mettre à jour votre extension de gestionnaire de Package NuGet dans WebMatrix 3 :

1. Ouvrez WebMatrix 3
1. Cliquez sur l’icône des Extensions dans le ruban
1. Sélectionnez l’onglet mises à jour
1. Cliquez pour mettre à jour le Gestionnaire de Package NuGet pour 2.5.0
1. Fermez et redémarrez WebMatrix 3

Il s’agit première version de l’équipe NuGet de l’extension du Gestionnaire de Package NuGet pour WebMatrix.  Le code a été récemment fourni par Microsoft dans le projet de NuGet open source. Auparavant, l’intégration de NuGet a été intégrée à WebMatrix, et il ne peut pas être mis à jour hors bande à partir de WebMatrix.  Nous disposons désormais la possibilité d’obtenir la mise à jour en même temps que le reste des outils du client de NuGet.

## <a name="bug-fixes"></a>Correctifs de bogues

Amélioration des performances dans le package de mise à jour de l’une des correctifs de bogues majeures apportées était-réinstaller la commande.

Outre ces fonctionnalités et la correction des performances mentionnées précédemment, cette version de NuGet inclut également plusieurs autres correctifs de bogues. Il existait des problèmes de total 181 traités dans la mise en production. Pour obtenir la liste complète des travaux les éléments corrigés dans NuGet 2.8, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
