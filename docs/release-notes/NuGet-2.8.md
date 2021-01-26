---
title: Notes de publication de NuGet 2,8
description: Notes de publication de NuGet 2,8, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776718"
---
# <a name="nuget-28-release-notes"></a>Notes de publication de NuGet 2,8

Notes de publication de [NuGet 2.7.2](../release-notes/nuget-2.7.2.md)  |  [Notes de publication de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2,8 a été publié le 29 janvier 2014.

## <a name="acknowledgements"></a>Remerciements

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) : lors de l’empaquetage de packages, vérification de l’ID des packages de dépendance.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) : supprimez le suffixe $Metadata quand les informations d’identification du flux persistening.
3. [Filip de vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) -prend en charge la spécification du fichier projet pour la commande nuget.exe Update.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - jetons de remplacement [#3536](http://nuget.codeplex.com/workitem/3536) non passés avec-IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) -Fix NuGet. push levant une exception OutOfMemoryException lors du push d’un package volumineux.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) : corrigez le chemin cible incorrect lorsque le projet fait référence à un autre projet CLI/C++.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) -autoriser l’installation des packages en tant que dépendances de développement par défaut
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) -supprimer les mises à niveau implicites vers la dernière version du correctif
9. [Gregory vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Plusieurs correctifs de bogues et améliorations pour NuGet. Server, la commande nuget.exe Mirror et d’autres.
    - Ce travail a été effectué depuis plusieurs mois, avec Gregory avec nous sur le point de vue approprié pour une intégration à Master pour 2,8.

## <a name="patch-resolution-for-dependencies"></a>Résolution des correctifs pour les dépendances

Lors de la résolution des dépendances de packages, NuGet a implémenté historiquement une stratégie de sélection de la version de package principale et mineure la plus faible qui satisfait les dépendances du package. Toutefois, contrairement à la version majeure et la version mineure, la version du correctif a toujours été résolue à la version la plus élevée. Bien que le comportement ait été correctement intentionnel, il a créé un manque de déterminisme pour l’installation des packages avec des dépendances. Prenons l’exemple suivant :

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

Dans cet exemple, même si Developer1 et Developer2 sont installés PackageA@1.0.0 , chacun s’est terminé avec une version différente de PackageB. NuGet 2,8 modifie ce comportement par défaut de telle sorte que le comportement de résolution des dépendances pour les versions correctives est cohérent avec le comportement des versions majeure et mineure. Dans l’exemple ci-dessus, est PackageB@1.0.0 installé suite à l’installation de PackageA@1.0.0 , quelle que soit la version de patch la plus récente.

## <a name="-dependencyversion-switch"></a>Commutateur-DependencyVersion

Bien que NuGet 2,8 modifie le comportement _par défaut_ pour la résolution des dépendances, il ajoute également un contrôle plus précis sur le processus de résolution des dépendances via le commutateur-DependencyVersion dans la console du gestionnaire de package. Le commutateur permet de résoudre les dépendances sur la version la plus basse possible (comportement par défaut), la version la plus élevée possible, ou la version mineure ou correctif la plus élevée.  Ce commutateur fonctionne uniquement pour Install-Package dans la commande PowerShell.

![Commutateur DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Attribut DependencyVersion

Outre le commutateur-DependencyVersion détaillé ci-dessus, NuGet a également autorisé la possibilité de définir un nouvel attribut dans le fichier Nuget.Config définissant la valeur par défaut, si le commutateur-DependencyVersion n’est pas spécifié dans un appel de Install-Package. Cette valeur est également respectée par la boîte de dialogue du gestionnaire de package NuGet pour les opérations de package d’installation. Pour définir cette valeur, ajoutez l’attribut ci-dessous à votre fichier Nuget.Config :

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>Aperçu des opérations NuGet avec-WhatIf

Certains packages NuGet peuvent avoir des graphiques de dépendance profonde et, par conséquent, ils peuvent être utiles lors d’une opération d’installation, de désinstallation ou de mise à jour pour voir d’abord ce qui se passe. NuGet 2,8 ajoute le commutateur PowerShell-WhatIf standard aux commandes install-package, Uninstall-package et Update-Package pour permettre la visualisation de la totalité de la fermeture des packages auxquels la commande sera appliquée. Par exemple, `install-package Microsoft.AspNet.WebApi -whatif` l’exécution de dans une application Web ASP.net vide génère ce qui suit.

```
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
```

## <a name="downgrade-package"></a>Mettre à niveau le package

Il n’est pas rare d’installer une version préliminaire d’un package afin d’examiner les nouvelles fonctionnalités, puis de choisir de restaurer la dernière version stable. Avant NuGet 2,8, il s’agissait d’un processus à plusieurs étapes de la désinstallation du package de la version préliminaire et de ses dépendances, puis de l’installation de la version antérieure. Toutefois, avec NuGet 2,8, le package de mise à jour restaurera la fermeture complète du package (par exemple, l’arborescence des dépendances du package) à la version précédente.

## <a name="development-dependencies"></a>Dépendances de développement

De nombreux types de fonctionnalités différents peuvent être fournis sous forme de packages NuGet, y compris les outils utilisés pour optimiser le processus de développement. Ces composants, bien qu’ils puissent être Instrumentals dans le développement d’un nouveau package, ne doivent pas être considérés comme une dépendance du nouveau package lorsqu’il est publié ultérieurement. NuGet 2,8 permet à un package de s’identifier dans le `.nuspec` fichier en tant que developmentDependency. Une fois installée, ces métadonnées sont également ajoutées au `packages.config` fichier du projet dans lequel le package a été installé. Lorsque ce `packages.config` fichier est analysé ultérieurement pour les dépendances NuGet pendant `nuget.exe pack` , il exclut les dépendances marquées comme dépendances de développement.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Fichiers packages.config individuels pour différentes plateformes

Lors du développement d’applications pour plusieurs plateformes cibles, il est courant d’avoir différents fichiers projet pour chacun des environnements de génération respectifs. Il est également courant de consommer différents packages NuGet dans différents fichiers projet, car les packages ont des niveaux différents de prise en charge pour différentes plateformes. NuGet 2,8 fournit une prise en charge améliorée pour ce scénario en créant différents `packages.config` fichiers pour différents fichiers projet spécifiques à la plateforme.

![Fichiers package.config multiples](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Revenir au cache local

Bien que les packages NuGet soient généralement consommés à partir d’une galerie distante telle que [la galerie NuGet](http://www.nuget.org/) à l’aide d’une connexion réseau, il existe de nombreux scénarios dans lesquels le client n’est pas connecté. Sans connexion réseau, le client NuGet n’a pas pu installer correctement les packages, même si ces packages étaient déjà sur l’ordinateur du client dans le cache NuGet local. NuGet 2,8 ajoute le secours de cache automatique à la console du gestionnaire de package. Par exemple, lors de la déconnexion de la carte réseau et de l’installation de jQuery, la console affiche les informations suivantes :

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

La fonctionnalité de secours du cache ne requiert pas d’arguments de commande spécifiques. En outre, le secours du cache ne fonctionne actuellement que dans la console du gestionnaire de package : le comportement ne fonctionne pas dans la boîte de dialogue du gestionnaire de package.

## <a name="webmatrix-nuget-client-updates"></a>Mises à jour du client NuGet WebMatrix

Avec NuGet 2,8, l’extension NuGet pour WebMatrix a également été mise à jour pour inclure de nombreuses fonctionnalités majeures fournies avec [NuGet 2,5](../release-notes/nuget-2.5.md). Les nouvelles fonctionnalités incluent notamment « mettre à jour tout », « version minimale de NuGet » et permettre le remplacement de fichiers de contenu.

Pour mettre à jour votre extension du gestionnaire de package NuGet dans WebMatrix 3 :

1. Ouvrir WebMatrix 3
1. Cliquez sur l’icône extensions dans le ruban.
1. Sélectionner l’onglet mises à jour
1. Cliquez pour mettre à jour le gestionnaire de package NuGet vers 2.5.0
1. Fermer et redémarrer WebMatrix 3

Il s’agit de la première version de l’extension du gestionnaire de package NuGet de l’équipe NuGet pour WebMatrix.  Le code a récemment été fourni par Microsoft dans le projet NuGet Open source. Précédemment, l’intégration NuGet était intégrée à WebMatrix et n’a pas pu être mise à jour hors bande à partir de WebMatrix.  Nous avons maintenant la possibilité de le mettre à jour en même temps que le reste des outils clients de NuGet.

## <a name="bug-fixes"></a>Résolutions de bogues

L’un des principaux correctifs de bogues apportés était l’amélioration des performances dans la commande Update-Package-REINSTALL.

Outre ces fonctionnalités et les correctifs de performances susmentionnés, cette version de NuGet comprend également de nombreux autres correctifs de bogues. 181 problèmes ont été résolus dans la version. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,8, consultez le [suivi des problèmes NuGet pour cette version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
