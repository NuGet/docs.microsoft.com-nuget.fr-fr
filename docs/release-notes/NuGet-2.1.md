---
title: Notes de publication NuGet 2.1
description: Notes de publication pour 2.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548595"
---
# <a name="nuget-21-release-notes"></a>Notes de publication NuGet 2.1

[Notes de publication de NuGet 2.0](../release-notes/nuget-2.0.md) | [Notes de publication de NuGet 2.2](../release-notes/nuget-2.2.md)

NuGet 2.1 a été publiée le 4 octobre 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config hiérarchique

NuGet 2.1 offre davantage de souplesse dans le contrôle des paramètres de NuGet par le biais de remonter à la structure de dossiers que vous recherchez de manière récursive `NuGet.Config` fichiers et puis en générant la configuration de l’ensemble de tous les fichiers trouvés.  Par exemple, considérez le scénario où une équipe a un référentiel de package interne pour les builds d’intégration continue d’autres dépendances internes. La structure de dossiers pour un projet individuel peut se présenter comme suit :

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

En outre, si la restauration de package est activée pour la solution, le dossier suivant sera également exister :

    C:\myteam\solution1\.nuget

Pour que le référentiel de package interne de l’équipe disponible pour tous les projets qui l’équipe travaille selon, tout en ne pas rendant disponibles pour chaque projet sur l’ordinateur, nous pouvons créer un nouveau fichier Nuget.Config et placez-le dans le dossier c:\myteam. Il n’existe aucun moyen de spécifier un dossier de packages par projet.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Nous pouvons voir que la source a été ajoutée en exécutant la commande « nuget.exe sources » à partir de n’importe quel dossier sous c:\myteam comme indiqué ci-dessous :

![Sources de package à partir de la configuration de nuget parent](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` les fichiers sont recherchés dans l’ordre suivant :

1. `.nuget\Nuget.Config`
2. Récursive remonter à partir du dossier du projet à la racine
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Les configurations sont qu’appliqué dans le *inverser l’ordre*, ce qui signifie que selon l’ordre ci-dessus, le fichier Nuget.Config global serait être appliquée en premier, suivi par les fichiers Nuget.Config découvertes à partir de la racine au dossier de projet, puis par `.nuget\Nuget.Config`.  Cela est particulièrement important si vous utilisez le `<clear/>` élément à supprimer un ensemble d’éléments de configuration.

## <a name="specify-packages-folder-location"></a>Spécifiez « packages » emplacement du dossier

Dans le passé, NuGet a géré les packages d’une solution à partir d’un dossier « packages » connus figurent sous le dossier racine de solution.  Pour les équipes de développement qui ont de nombreuses solutions différentes qui ont installé les packages NuGet, cela peut entraîner dans le même package en cours d’installation à différents emplacements sur le système de fichiers.

NuGet 2.1 fournit un contrôle plus précis sur l’emplacement du dossier packages via la `repositoryPath` élément dans le `NuGet.Config` fichier.  S’appuyant sur l’exemple précédent de la prise en charge hiérarchique de Nuget.Config, supposons que nous souhaitons avoir tous les projets sous C:\myteam\ partage le même dossier de packages.  Pour ce faire, ajoutez simplement l’entrée suivante à `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Dans cet exemple, le partage `Nuget.Config` fichier Spécifie un dossier de packages partagés pour chaque projet qui est créé sous C:\myteam, quelle que soit la profondeur. Notez que si vous avez un dossier packages en dessous de la racine de votre solution, vous devez la supprimer avant NuGet placera les packages dans le nouvel emplacement.

## <a name="support-for-portable-libraries"></a>Prise en charge pour les bibliothèques portables

[Les bibliothèques portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) est une fonctionnalité introduite avec .NET 4 qui vous permet de générer des assemblys qui peuvent fonctionner sans modification sur différentes plateformes Microsoft, à partir de versions du.NET Framework pour Silverlight pour Windows Phone et Xbox même 360 (même si à ce stade, NuGet ne prend pas en charge la cible de la bibliothèque portable Xbox).  En étendant la [package conventions](../create-packages/supporting-multiple-target-frameworks.md) pour les profils et les versions de framework, NuGet 2.1 prend désormais en charge les bibliothèques portables en vous permettant de créer des packages qui ont composée framework et profil cible `lib` dossiers.

Par exemple, envisagez de la bibliothèque de classes portable suivant disponible cibler des plateformes.

![Boîte de dialogue de création bibliothèque portable](./media/releasenotes-21-plib.png)

Une fois que la bibliothèque est créée et la commande `nuget.exe pack MyPortableProject.csproj` est exécutée, la fonction portable nouvelle structure de dossiers de package de bibliothèque peut être observé en examinant le contenu du package NuGet généré.

![Disposition de package de bibliothèque portable](./media/releasenotes-21-plib-layout.png)

Comme vous pouvez le voir, la convention de nom de dossier de bibliothèque portable suit le modèle « portable-{framework 1} + {framework n} » où les identificateurs de framework suivent existant [conventions de nom et la version de framework](../reference/target-frameworks.md). Une exception aux conventions de nom et la version se trouve dans l’identificateur de framework utilisé pour Windows Phone.  Ce moniker doit utiliser le nom de framework « wp » (wp7, wp71 ou wp8). À l’aide de « silverlight-wp7 », par exemple, entraîne une erreur.

Lorsque vous installez le package est créé à partir de cette structure de dossiers, NuGet peut maintenant appliquer ses règles framework et de profil à plusieurs cibles, tel que spécifié dans le nom du dossier.  Derrière les règles de correspondance de NuGet est le principe que « plus spécifiques » cibles ont priorité sur « moins spécifiques ».  Cela signifie que les monikers ciblant une plateforme spécifique sera toujours préférés sur celles portables si elles sont toutes deux compatibles avec un projet.  En outre, si plusieurs cibles portables sont compatibles avec un projet, NuGet préfèrent celui où l’ensemble des plateformes prises en charge est « plus proche » pour le projet référençant le package.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Ciblage Windows 8 et Windows Phone 8 projets

Outre l’ajout de la prise en charge les projets de bibliothèque portable, NuGet 2.1 fournit des monikers du framework pour les projets Windows 8 Store et Windows Phone 8, ainsi que certains nouveaux monikers générales pour le Windows Store et les projets Windows Phone qui sera plus faciles à gérer entre les futures versions des plateformes respectives.

Pour les applications Windows 8 Store, les identificateurs de se présenter comme suit :

| NuGet 2.0 et versions antérieur | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45. NETCore45 | Win Windows, Windows8, win8 |

<br/>
Pour les projets Windows Phone, les identificateurs de se présenter comme suit :

| Système d’exploitation du téléphone | NuGet 2.0 et versions antérieur | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | WP, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (non pris en charge) | wp8, WindowsPhone8 |

<br/>
Dans toutes les modifications ci-dessus, les anciens noms de framework continueront à être entièrement pris en charge par NuGet 2.1.  L’avenir, les nouveaux noms utiliser car elles seront plus stables entre les futures versions des plateformes respectives. Les nouveaux noms seront *pas* être pris en charge dans les versions de NuGet antérieures 2.1, toutefois, donc de planifier en conséquence pour le moment auquel effectuer la transition.

## <a name="improved-search-in-package-manager-dialog"></a>Recherche améliorée dans la boîte de dialogue Gestionnaire de Package

Sur plusieurs itérations passées, a été apportée à la galerie NuGet considérablement amélioré la vitesse et la pertinence des recherches de package.  Toutefois, ces améliorations ont été limitées au site Web nuget.org.  NuGet 2.1 rend la recherche améliorée expérience disponible via la boîte de dialogue Gestionnaire de package NuGet.  Par exemple, imaginez que vous souhaitiez trouver le package de l’aperçu de la mise en cache Windows Azure.  Une requête raisonnable pour ce package peut être « Azure Cache ».  Dans les versions précédentes de la boîte de dialogue de gestionnaire de package, le package souhaité ne serait pas même présentée sur la première page de résultats.  Toutefois, dans NuGet 2.1, le package souhaité maintenant s’affiche en haut des résultats de recherche.

![Recherche de boîte de dialogue Gestionnaire de package](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forcer la mise à jour de Package

Avant NuGet 2.1, NuGet ignorerait la mise à jour un package qu’il y a pas un numéro de version haute.  Cela introduit friction pour certains scénarios – en particulier dans le cas de build ou de scénarios d’intégration continue où l’équipe ne souhaite pas incrémenter la version du package numérique avec chaque build.  Le comportement souhaité a été pour forcer une mise à jour indépendamment.  NuGet 2.1 préciser ce point avec l’indicateur « réinstaller ».  Par exemple, les versions précédentes de NuGet génère les éléments suivants lorsque vous tentez de mettre à jour un package qui n’avait pas d’une version plus récente du package :

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Avec l’indicateur de réinstallation, le package sera mis à jour indépendamment de si une version plus récente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Un autre scénario dans lequel l’indicateur reinstall est un avantage est que de nouveau le ciblage du framework. Lors de la modification du framework cible d’un projet (par exemple, à partir de .NET 4 pour .NET 4.5), Update-Package-réinstaller peut mettre à jour les références aux assemblys corrects pour tous les packages NuGet installés dans le projet.

## <a name="edit-package-sources-within-visual-studio"></a>Modifier les Sources de Package dans Visual Studio

Dans les versions précédentes de NuGet, mise à jour une source de package à partir de la boîte de dialogue options Visual Studio requis de suppression et l’ajout de nouveau la source du package.  NuGet 2.1 améliore ce flux de travail en prenant en charge la mise à jour comme une fonction de première classe de l’interface utilisateur de configuration.

![Boîte de dialogue de configuration de package manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correctifs de bogues

NuGet 2.1 inclut plusieurs correctifs de bogues. Pour obtenir une liste complète de travail éléments résolus dans NuGet 2.0, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
