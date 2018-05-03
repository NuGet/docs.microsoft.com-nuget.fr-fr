---
title: Notes de publication NuGet 2.0
description: Notes de version de NuGet 2.0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a>Notes de publication NuGet 2.0

[Notes de publication NuGet 1.8](../release-notes/nuget-1.8.md) | [Notes de version 2.1 de NuGet](../release-notes/nuget-2.1.md)

NuGet 2.0 a été publiée le 19 juin 2012.

## <a name="known-installation-issue"></a>Problème connu d’Installation
Si vous exécutez Visual Studio 2010 SP1, vous susceptible de rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet, si vous disposez d’une version plus ancienne est installée.

La solution de contournement consiste à simplement désinstaller NuGet et l’installer à partir de la galerie d’extensions Visual Studio.  Consultez [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) pour plus d’informations, ou [atteindre directement le correctif logiciel Visual Studio](http://bit.ly/vsixcertfix).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis il est probable que devez redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="package-restore-consent-is-now-active"></a>Autorisation de restauration de package est désormais active

Comme décrit dans cette [publier sur le consentement de restauration de package](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, vous devez désormais consentement donné pour permettre la restauration de package pour vous connecter et télécharger les packages. Veuillez vous assurer que vous avez fourni le consentement via la boîte de dialogue package manager configuration ou de la variable d’environnement EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Dépendances de groupe par l’infrastructure cible

Depuis la version 2.0, package de dépendances peuvent varier en fonction du profil de framework du projet cible. Pour cela, à l’aide d’une mise à jour `.nuspec` schéma. Le `<dependencies>` élément peut désormais contenir un ensemble de `<group>` éléments. Chaque groupe contient zéro ou plusieurs `<dependency>` éléments et un `targetFramework` attribut. Toutes les dépendances à l’intérieur d’un groupe sont installées ensemble si le framework cible est compatible avec le profil de framework du projet cible. Par exemple :

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Notez qu’un groupe peut contenir **zéro** dépendances. Dans l’exemple ci-dessus, si le package est installé dans un projet qui cible Silverlight 3.0 ou version ultérieure, aucune dépendance ne sera installé. Si le package est installé dans un projet qui cible le .NET 4.0 ou version ultérieure, deux dépendances, jQuery et WebActivator, seront installés.  Si le package est installé dans un projet qui cible une version antérieure de ces 2 infrastructures ou toute autre infrastructure, RouteMagic 1.1.0 sera installé. Il n’existe aucun héritage entre les groupes. Si le framework cible d’un projet correspond à la `targetFramework` attribut d’un groupe, seuls les dépendances au sein de ce groupe sera installé.

Un package peut spécifier les dépendances de package dans deux formats : l’ancien format de liste plate de `<dependency>` éléments ou les groupes. Si le `<group>` format est utilisé, le package ne peut pas être installé dans les versions antérieures à 2.0 de NuGet.

Notez que la combinaison des deux formats n’est pas autorisé. Par exemple, l’extrait suivant est **non valide** et sont rejetées par NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Regroupement des fichiers de contenu et des scripts PowerShell par le framework cible

En plus des références d’assembly, les fichiers de contenu et des scripts PowerShell peuvent également être regroupés par le framework cible. La même structure de dossier se trouve dans le `lib` dossier pour la spécification du framework cible peut désormais être appliqué dans la même façon à la `content` et `tools` dossiers. Par exemple :

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Remarque**: car `init.ps1` est exécutée au niveau de la solution et est dépendant sur n’importe quel projet individuel, il doit être placé directement sous le `tools` dossier. Si placé dans un dossier spécifique de l’infrastructure, il sera ignoré.

En outre, une nouvelle fonctionnalité de NuGet 2.0 est que le dossier d’une infrastructure peut être *vide*, dans ce cas, NuGet n’ajoute pas les références d’assembly, ajoutez les fichiers de contenu ou exécuter des scripts PowerShell pour la version du framework particulier. Dans l’exemple ci-dessus, le dossier `content\net40` est vide.

## <a name="improved-tab-completion-performance"></a>Performances de saisie semi-automatique tab améliorée
La fonctionnalité de saisie semi-automatique d’onglet dans la Console du Gestionnaire de Package NuGet a été mis à jour pour améliorer considérablement les performances. Il y a beaucoup moins retard de l’heure de que la touche tab est enfoncée jusqu'à ce que la liste déroulante de suggestions s’affiche.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 2.0 comprend plusieurs correctifs de bogues en mettant l’accent sur les performances et de consentement de restauration de package.
Pour obtenir la liste complète de travail éléments fixes dans NuGet 2.0, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
