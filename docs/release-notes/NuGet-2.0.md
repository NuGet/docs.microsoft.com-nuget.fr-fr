---
title: Notes de publication NuGet 2.0
description: Notes de publication pour NuGet 2.0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547573"
---
# <a name="nuget-20-release-notes"></a>Notes de publication NuGet 2.0

[Notes de publication de NuGet 1.8](../release-notes/nuget-1.8.md) | [Notes de publication de NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet 2.0 a été publiée le 19 juin 2012.

## <a name="known-installation-issue"></a>Problème d’Installation connus
Si vous exécutez Visual Studio 2010 SP1, vous pouvez rencontrer une erreur d’installation lorsque vous tentez de mettre à niveau NuGet si vous avez une version antérieure est installée.

La solution de contournement consiste à désinstaller simplement NuGet, puis l’installer à partir de la galerie d’extensions Visual Studio.  Consultez [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) pour plus d’informations, ou [rendez-vous directement sur le correctif logiciel VS](http://bit.ly/vsixcertfix).

Remarque : Si Visual Studio ne vous autorisent à désinstaller l’extension (le bouton Désinstaller est désactivé), puis vous avez probablement besoin de redémarrer Visual Studio à l’aide de « Exécuter en tant qu’administrateur ».

## <a name="package-restore-consent-is-now-active"></a>Consentement de restauration de package est maintenant activé

Comme décrit dans cet [publier sur le consentement de restauration de package](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, vous devez désormais que consentement donné pour permettre la restauration de package pour vous connecter et télécharger les packages. Vérifiez que vous avez fourni le consentement par le biais de la boîte de dialogue configuration de gestionnaire package ou la variable d’environnement EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Dépendances de groupe par les frameworks cibles

Depuis la version 2.0, package de dépendances peuvent varier selon le profil de framework du projet cible. Pour cela, à l’aide d’une mise à jour `.nuspec` schéma. Le `<dependencies>` élément peut maintenant contenir un ensemble de `<group>` éléments. Chaque groupe contient zéro ou plusieurs `<dependency>` éléments et un `targetFramework` attribut. Toutes les dépendances à l’intérieur d’un groupe sont installés ensemble si le framework cible est compatible avec le profil de framework du projet cible. Exemple :

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

Notez qu’un groupe peut contenir **zéro** dépendances. Dans l’exemple ci-dessus, si le package est installé dans un projet qui cible Silverlight 3.0 ou version ultérieure, aucune dépendance ne sera installé. Si le package est installé dans un projet qui cible le .NET 4.0 ou version ultérieure, deux dépendances, jQuery et WebActivator, seront installés.  Si le package est installé dans un projet qui cible une version précoce de ces 2 infrastructures ou une autre infrastructure, RouteMagic 1.1.0 sera installé. Il n’existe aucun héritage entre les groupes. Si le framework de cible d’un projet correspond à la `targetFramework` attribut d’un groupe, uniquement les dépendances au sein de ce groupe sera installé.

Un package peut spécifier les dépendances de package dans un des deux formats : l’ancien format d’une liste plate de `<dependency>` éléments ou les groupes. Si le `<group>` format est utilisé, le package ne peut pas être installé dans les versions de NuGet antérieures à 2.0.

Notez que la combinaison des deux formats n’est pas autorisée. Par exemple, l’extrait suivant est **non valide** et sont rejetées par NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Regroupement des fichiers de contenu et scripts PowerShell par le framework cible

En plus des références d’assembly, les fichiers de contenu et scripts PowerShell peuvent également être regroupés par le framework cible. La même structure de dossiers se trouve dans le `lib` dossier pour la spécification du framework cible peut désormais être appliqué dans la même façon pour le `content` et `tools` dossiers. Exemple :

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

**Remarque**: étant donné que `init.ps1` est exécutée au niveau de la solution et est dépendant sur n’importe quel projet individuel, celui-ci doit être placé directement sous le `tools` dossier. Si placé dans un dossier propre à l’infrastructure, il sera ignoré.

En outre, une nouvelle fonctionnalité de NuGet 2.0 est qu’un dossier de framework peut être *vide*, auquel cas, NuGet n’ajoute pas les références d’assembly, ajouter des fichiers de contenu ou exécuter des scripts PowerShell pour la version du framework particulier. Dans l’exemple ci-dessus, le dossier `content\net40` est vide.

## <a name="improved-tab-completion-performance"></a>Performances de saisie semi-automatique tab améliorée
La fonctionnalité de saisie semi-automatique dans la Console du Gestionnaire de Package NuGet a été mis à jour pour améliorer considérablement les performances. Il y aura beaucoup moins de retard à partir du moment que la touche tab est enfoncée jusqu'à ce que la liste déroulante de suggestions s’affiche.

## <a name="bug-fixes"></a>Correctifs de bogues
NuGet 2.0 comprend plusieurs correctifs de bogues en mettant l’accent sur les performances et de consentement de restauration de package.
Pour obtenir une liste complète de travail éléments résolus dans NuGet 2.0, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
