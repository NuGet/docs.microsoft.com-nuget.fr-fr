---
title: Notes de publication de NuGet 2,0
description: Notes de publication de NuGet 2,0, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776994"
---
# <a name="nuget-20-release-notes"></a>Notes de publication de NuGet 2,0

Notes de publication de [NuGet 1,8](../release-notes/nuget-1.8.md)  |  [Notes de publication de NuGet 2,1](../release-notes/nuget-2.1.md)

NuGet 2,0 a été publié le 19 juin 2012.

## <a name="known-installation-issue"></a>Problème d’installation connu
Si vous exécutez VS 2010 SP1, vous pouvez rencontrer une erreur d’installation lors de la tentative de mise à niveau de NuGet si une version antérieure est installée.

La solution consiste à désinstaller simplement NuGet, puis à l’installer à partir de la Galerie d’extensions Visual Studio.  <https://support.microsoft.com/kb/2581019>Pour plus d’informations, consultez pour plus d’informations ou [accédez directement au correctif vs](http://bit.ly/vsixcertfix).

Remarque : si Visual Studio ne vous permet pas de désinstaller l’extension (le bouton désinstaller est désactivé), vous devrez probablement redémarrer Visual Studio à l’aide de « exécuter en tant qu’administrateur ».

## <a name="package-restore-consent-is-now-active"></a>Le consentement de la restauration du package est maintenant actif

Comme décrit dans cette [publication sur le consentement de la restauration des packages](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 requiert désormais que le consentement soit donné pour activer la restauration du package en ligne et télécharger les packages. Vérifiez que vous avez fourni un consentement via la boîte de dialogue de configuration du gestionnaire de package ou la variable d’environnement EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Grouper les dépendances par frameworks cibles

À partir de la version 2,0, les dépendances de package peuvent varier en fonction du profil du Framework du projet cible. Cela s’effectue à l’aide d’un schéma mis à jour `.nuspec` . L' `<dependencies>` élément peut maintenant contenir un ensemble d' `<group>` éléments. Chaque groupe contient zéro `<dependency>` élément, un ou plusieurs éléments et un `targetFramework` attribut. Toutes les dépendances à l’intérieur d’un groupe sont installées ensemble si le Framework cible est compatible avec le profil de l’infrastructure de projet cible. Par exemple :

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

Notez qu’un groupe peut contenir **zéro** dépendance. Dans l’exemple ci-dessus, si le package est installé dans un projet qui cible Silverlight 3,0 ou une version ultérieure, aucune dépendance n’est installée. Si le package est installé dans un projet qui cible .NET 4,0 ou une version ultérieure, deux dépendances, jQuery et webactivateur, seront installées.  Si le package est installé dans un projet qui cible une version antérieure de ces 2 frameworks, ou de tout autre Framework, RouteMagic 1.1.0 sera installé. Il n’y a pas d’héritage entre les groupes. Si la version cible de .NET Framework d’un projet correspond à l' `targetFramework` attribut d’un groupe, seules les dépendances au sein de ce groupe seront installées.

Un package peut spécifier des dépendances de package dans l’un des deux formats suivants : l’ancien format d’une liste plate d' `<dependency>` éléments ou de groupes. Si le `<group>` format est utilisé, le package ne peut pas être installé dans les versions de NuGet antérieures à 2,0.

Notez que le mélange des deux formats n’est pas autorisé. Par exemple, l’extrait de code suivant n’est **pas valide** et sera rejeté par NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Regroupement de fichiers de contenu et de scripts PowerShell par le Framework cible

Outre les références d’assembly, les fichiers de contenu et les scripts PowerShell peuvent également être regroupés par Framework cible. La même structure de dossiers trouvée dans le dossier pour la spécification de la version `lib` cible de .NET Framework peut désormais être appliquée de la même façon aux `content` `tools` dossiers et. Par exemple :

```
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
```

**Remarque**: étant donné que `init.ps1` est exécuté au niveau de la solution et qu’il n’est pas dépendant d’un projet individuel, il doit être placé directement sous le `tools` dossier. S’il est placé dans un dossier spécifique à l’infrastructure, il sera ignoré.

En outre, une nouvelle fonctionnalité de NuGet 2,0 est qu’un dossier Framework peut être *vide*, auquel cas NuGet n’ajoute pas de références d’assembly, n’ajoute pas de fichiers de contenu ou n’exécute pas de scripts PowerShell pour la version de Framework particulière. Dans l’exemple ci-dessus, le dossier `content\net40` est vide.

## <a name="improved-tab-completion-performance"></a>Amélioration des performances de la saisie semi-automatique par tabulation
La fonctionnalité de saisie semi-automatique par tabulation dans la console du gestionnaire de package NuGet a été mise à jour pour améliorer les performances de manière significative. Il y aura bien moins de temps à partir du moment où la touche Tab est enfoncée jusqu’à ce que la liste déroulante de suggestions apparaisse.

## <a name="bug-fixes"></a>Résolutions de bogues
NuGet 2,0 comprend de nombreux correctifs de bogues, en mettant l’accent sur le consentement et les performances de la restauration des packages.
Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,0, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
