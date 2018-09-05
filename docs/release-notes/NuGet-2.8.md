---
title: Notes de publication NuGet 2.8
description: Notes de publication pour NuGet 2.8, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547457"
---
# <a name="nuget-28-release-notes"></a>Notes de publication NuGet 2.8

[Notes de publication de NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [Notes de publication de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 a été publié le 29 janvier 2014.

## <a name="acknowledgements"></a>Remerciements

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) - lors de la compression des packages, vérification des Id des packages de dépendances.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -supprimer le suffixe $metadata lors persistening flux des informations d’identification.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - prise en charge de la spécification de fichier de projet pour la commande de mise à jour de nuget.exe.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -ne pas passés avec - IncludeReferencedProjects de jetons de remplacement.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -corriger nuget.push lever exception OutOfMemoryException lors de l’envoi du package volumineux.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -chemin d’accès cible incorrect de correctif lorsque le projet fait référence à un autre projet CLI/C++.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -autoriser les packages doivent être installés en tant que dépendances de développement par défaut
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -supprimer implicites mises à niveau vers la dernière version de correctif
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Plusieurs bogues de correctifs et améliorations pour le NuGet.Server, la commande de mise en miroir de nuget.exe et autres.
    - Ce travail a été effectué sur plusieurs mois, avec Gregory collaboré avec nous sur le minutage de droite à intégrer dans la branche maître pour 2.8.

## <a name="patch-resolution-for-dependencies"></a>Résolution des correctifs pour les dépendances

Lors de la résolution des dépendances de package, NuGet a implémenté par le passé d’une stratégie de sélection de la version majeure et mineure package le plus bas qui satisfait aux dépendances sur le package. Toutefois, contrairement à la version majeure et mineure, la version du correctif a été résolue toujours vers la version la plus élevée. Bien que le comportement a été bien intentionné, il créé un manque de déterminisme pour installer des packages avec des dépendances. Prenons l'exemple suivant :

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Dans cet exemple, même si Developer1 et Developer2 installés PackageA@1.0.0, chaque finalement obtenu avec une version différente de PackageB. NuGet 2.8 modifie ce comportement par défaut tels que le comportement de résolution de dépendance pour les versions de correctifs est cohérent avec le comportement pour les versions majeures et mineures. Dans l’exemple ci-dessus, puis, PackageB@1.0.0 sont installés à la suite de l’installation PackageA@1.0.0, quelle que soit la version plus récente du correctif.

## <a name="-dependencyversion-switch"></a>-DependencyVersion commutateur

Si les modifications de NuGet 2.8 le _par défaut_ comportement pour la résolution des dépendances, il ajoute également un contrôle plus précis sur le processus de résolution de dépendance via le commutateur - DependencyVersion dans la console du Gestionnaire de package. Le commutateur permet la résolution des dépendances à la version la plus basse possible (comportement par défaut), la version la plus élevée possible, ou le plus élevé version mineure ou patch.  Ce commutateur fonctionne uniquement pour le package d’installation dans la commande powershell.

![DependencyVersion commutateur](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Attribut de DependencyVersion

Outre le commutateur - DependencyVersion détaillé plus haut, NuGet a permis la possibilité de définir un nouvel attribut dans le fichier Nuget.Config à définir ce qui est la valeur par défaut, si le commutateur - DependencyVersion n’est pas spécifié dans un appel à package d’installation. Cette valeur sera également être respectée par la boîte de dialogue Gestionnaire de Package NuGet pour les opérations de package d’installation. Pour définir cette valeur, ajoutez l’attribut ci-dessous à votre fichier Nuget.Config :

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Aperçu des opérations de NuGet avec - whatif

Certains packages NuGet peuvent avoir des graphiques de dépendance approfondie, et par conséquent, il peut s’avérer utile lors d’une installation, la désinstallation ou la mise à jour pour voir tout d’abord ce qui se produira. NuGet 2.8 ajoute le commutateur - whatif PowerShell standard pour le package d’installation, désinstaller-package et les commandes de package de mise à jour afin de permettre la visualisation de la fermeture complète des packages à laquelle la commande sera appliquée. Par exemple, en cours d’exécution `install-package Microsoft.AspNet.WebApi -whatif` dans un site Web ASP.NET vide application donne le résultat suivant.

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

Il n’est pas rare pour installer une version préliminaire d’un package afin d’étudier les nouvelles fonctionnalités et décider ensuite de revenir à la dernière version stable. Avant NuGet 2.8, c’était un processus en plusieurs étapes de la version préliminaire package et ses dépendances, installation et la désinstallation puis la version antérieure. Avec NuGet 2.8, toutefois, le package de mise à jour maintenant annule la fermeture de l’ensemble du package (par exemple, arborescence des dépendances du package) à la version précédente.

## <a name="development-dependencies"></a>Dépendances de développement

Différents types de fonctionnalités peuvent être fournis sous forme de packages NuGet - y compris les outils qui sont utilisés pour optimiser le processus de développement. Ces composants, pendant qu’ils peuvent vous aider à développer un nouveau package, pas prenez une dépendance du nouveau package lorsqu’il est publié plus tard. NuGet 2.8 permet à un package pour s’identifier dans la `.nuspec` fichier comme un developmentDependency. Lors de l’installation, ces métadonnées seront également ajoutées à la `packages.config` fichier du projet dans lequel le package a été installé. Lorsque que `packages.config` fichier est analysé ultérieurement pour les dépendances NuGet pendant `nuget.exe pack`, il exclut ces dépendances marquées en tant que dépendances de développement.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Fichiers packages.config individuels pour différentes plateformes

Lors du développement d’applications pour plusieurs plateformes cibles, il est courant d’avoir des fichiers de projet différent pour chacun des environnements de build respectifs. Il est également courant de consommer différents packages NuGet dans différents fichiers projet, comme les packages ont différents niveaux de prise en charge pour les différentes plateformes. NuGet 2.8 fournit la prise en charge améliorée pour ce scénario en créant différents `packages.config` fichiers pour les fichiers de projet spécifiques à la plateforme différent.

![Plusieurs fichiers package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Action de secours dans le Cache Local

Bien que les packages NuGet sont généralement consommées depuis une galerie à distance comme [la galerie NuGet](http://www.nuget.org/) à l’aide d’une connexion réseau, il existe de nombreux scénarios où le client n’est pas connecté. Sans une connexion réseau, le client NuGet n’a pas pu installer correctement les packages - même lorsque ces packages étaient déjà présents sur l’ordinateur client dans le cache NuGet local. NuGet 2.8 ajoute automatique du cache secours à la console du Gestionnaire de package. Par exemple, lorsque la déconnexion de la carte réseau et l’installation de jQuery, la console affiche les informations suivantes :

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

La fonctionnalité de cache de secours ne nécessite pas d’argument de commande spécifique. En outre, cache de secours fonctionne actuellement uniquement dans la console du Gestionnaire de package : le comportement ne fonctionne pas actuellement dans la boîte de dialogue de gestionnaire de package.

## <a name="webmatrix-nuget-client-updates"></a>Met à jour du Client NuGet de WebMatrix

Avec NuGet 2.8, l’extension NuGet pour WebMatrix également mise à jour pour inclure la plupart des principales fonctionnalités fournies avec [NuGet 2.5](../release-notes/nuget-2.5.md). Les nouvelles fonctionnalités incluent ceux tels que « Update All », « Version de NuGet Minimum » et permettant le remplacement des fichiers de contenu.

Pour mettre à jour votre extension de gestionnaire de Package NuGet dans WebMatrix 3 :

1. Ouvrez WebMatrix 3
1. Cliquez sur l’icône des Extensions dans le ruban
1. Sélectionnez l’onglet mises à jour
1. Cliquez pour mettre à jour le Gestionnaire de Package NuGet à 2.5.0
1. Fermez et redémarrez WebMatrix 3

Il s’agit première version de l’équipe NuGet de l’extension du Gestionnaire de Package NuGet pour WebMatrix.  Le code a été récemment envoyé par Microsoft dans le projet NuGet open source. Auparavant, l’intégration de NuGet a été intégrée à WebMatrix, et il ne peut pas être mis à jour hors bande à partir de WebMatrix.  Nous disposons désormais la fonctionnalité mettre à jour plus en même temps que le reste des outils clients de NuGet.

## <a name="bug-fixes"></a>Correctifs de bogues

Parmi les principaux correctifs de bogues apportées était l’amélioration des performances dans le package de mise à jour-réinstaller la commande.

Outre ces fonctionnalités et le correctif de performances mentionnés ci-dessus, cette version de NuGet inclut également plusieurs autres correctifs de bogues. Vous rencontrez des problèmes de total 181 résolus dans la version. Pour obtenir la liste complète des travaux éléments résolus dans NuGet 2.8, veuillez vue le [NuGet Issue Tracker pour cette version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
