---
title: Notes de version 2.1 de NuGet
description: Notes de publication pour 2.1 NuGet, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044806"
---
# <a name="nuget-21-release-notes"></a>Notes de version 2.1 de NuGet

[Notes de publication NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet 2.2 Notes de publication](../release-notes/nuget-2.2.md)

NuGet 2.1 le 4 octobre 2012 a été publié.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config hiérarchique

NuGet 2.1 vous donne plus de souplesse dans le contrôle des paramètres de NuGet au moyen de remonter à la structure de dossiers la recherche de manière récursive `NuGet.Config` fichiers et puis en générant la configuration de l’ensemble de tous les fichiers trouvés.  Par exemple, considérez le scénario où une équipe possède un référentiel de packages interne pour la génération de l’élément de configuration des autres dépendances internes. La structure de dossiers pour un projet individuel peut se présenter comme suit :

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

En outre, si la restauration des packages est activée pour la solution, le dossier suivant sera également exister :

    C:\myteam\solution1\.nuget

Afin de disposer d’un référentiel de packages interne de l’équipe disponible pour tous les projets de l’équipe l’exécute, tout en ne pas rendre disponible pour chaque projet sur l’ordinateur, nous pouvons créer un nouveau fichier Nuget.Config et placez-le dans le dossier c:\myteam. Il n’existe aucun moyen de spécifier un dossier de packages par le projet.

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

Nous pouvons voir que la source a été ajoutée en exécutant la commande 'sources de nuget.exe' à partir de n’importe quel dossier sous c:\myteam comme indiqué ci-dessous :

![Sources de package à partir de la configuration de nuget parent](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` les fichiers sont recherchés dans l’ordre suivant :

1. `.nuget\Nuget.Config`
2. Récursive parcours du dossier de projet à la racine
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Les configurations sont à appliquer dans le *inverser l’ordre*, ce qui signifie que selon l’ordre ci-dessus, le Nuget.Config global est appliqué en premier, suivi par les fichiers de Nuget.Config détectés à partir de la racine pour le dossier du projet, suivi par `.nuget\Nuget.Config`.  Cela est particulièrement important si vous utilisez la `<clear/>` élément à supprimer d’un ensemble d’éléments de configuration.

## <a name="specify-packages-folder-location"></a>Spécifiez « packages » emplacement du dossier

Dans le passé, NuGet a géré les packages d’une solution à partir d’un dossier connu « packages » figurent sous le dossier racine de solution.  Pour les équipes de développement qui ont de nombreuses solutions différentes qui ont installé les packages NuGet, cela peut entraîner dans le même package en cours d’installation dans de nombreux endroits différents sur le système de fichiers.

NuGet 2.1 fournit un contrôle plus précis sur l’emplacement du dossier packages via le `repositoryPath` élément dans le `NuGet.Config` fichier.  Génération à partir de l’exemple précédent de la prise en charge de Nuget.Config hiérarchique, supposons que nous souhaitons tous les projets sous C:\myteam\ partage le même dossier de packages.  Pour ce faire, ajoutez simplement l’entrée suivante à `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Dans cet exemple, le partage `Nuget.Config` fichier Spécifie un dossier partagé des packages pour chaque projet est créé sous C:\myteam, quelle que soit la profondeur. Notez que si vous avez un dossier de packages existant sous la racine de votre solution, vous devez supprimer avant NuGet placera les packages dans le nouvel emplacement.

## <a name="support-for-portable-libraries"></a>Prise en charge pour les bibliothèques portables

[Les bibliothèques portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) est une fonctionnalité introduite avec 4 .NET qui vous permet de générer des assemblys qui peuvent fonctionner sans modification sur différentes plateformes de Microsoft, à partir de versions du.NET Framework pour Silverlight pour Windows Phone et Xbox même 360 (même si à ce stade, NuGet ne prend pas en charge la cible de la bibliothèque portable Xbox).  En étendant le [package conventions](../create-packages/supporting-multiple-target-frameworks.md) pour les profils et les versions du framework, NuGet 2.1 prend désormais en charge les bibliothèques portables en vous permettant de créer des packages qui ont composée framework et profil cible `lib` dossiers.

Par exemple, envisagez de plateformes cibles disponibles de la bibliothèque de classes portable suivantes.

![Boîte de dialogue Création bibliothèque portable](./media/releasenotes-21-plib.png)

Une fois la bibliothèque générée et la commande `nuget.exe pack MyPortableProject.csproj` est exécutée, la fonction portable nouvelle structure de dossiers de package de bibliothèque peut être consulté en examinant le contenu du package NuGet généré.

![Disposition de package de bibliothèque portable](./media/releasenotes-21-plib-layout.png)

Comme vous pouvez le voir, la convention de nom de dossier de bibliothèque portable suit le modèle de « portable-{framework 1} + {framework n} » dans lequel les identificateurs de framework suivent existants [conventions de nom et la version de framework](../reference/target-frameworks.md). Une exception pour les conventions de nom et la version se trouve dans l’identificateur de framework utilisé pour Windows Phone.  Ce moniker doit utiliser le nom d’infrastructure « wp » (wp7, wp71 ou wp8). À l’aide de 'silverlight-wp7', par exemple, entraîne une erreur.

Lorsque vous installez le package est créé à partir de cette structure de dossiers, NuGet peut appliquer maintenant ses règles framework et profil vers plusieurs cibles, comme spécifié dans le nom du dossier.  Derrière les règles de correspondance de NuGet est le principe que les cibles « plus spécifiques » aura priorité sur « moins spécifiques ».  Cela signifie que les monikers cibler une plateforme spécifique sera toujours préférés sur ceux qui sont portables s’ils sont tous deux compatibles avec un projet.  En outre, si plusieurs cibles portables sont compatibles avec un projet, NuGet préfèreront celui où l’ensemble des plateformes prises en charge est « le plus proche » au projet référençant le lot.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Ciblage Windows 8 et Windows Phone 8 projets

En plus d’ajouter la prise en charge les projets de bibliothèque portable, NuGet 2.1 fournit des monikers du framework pour les projets Windows 8 Store et Windows Phone 8, ainsi que certains nouveaux monikers générales du Windows Store et les projets Windows Phone qui seront gérer plus facilement entre les futures versions des plateformes respectifs.

Pour les applications du Windows Store de 8, les identificateurs de se présenter comme suit :

| NuGet 2.0 et versions antérieur | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45. NETCore45 | Win Windows, Windows 8, win8 |

<br/>
Pour les projets Windows Phone, les identificateurs de se présenter comme suit :

| Système d’exploitation du téléphone | NuGet 2.0 et versions antérieur | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | WP, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (non pris en charge) | wp8, WindowsPhone8 |

<br/>
Dans toutes les modifications décrites ci-dessus, les anciens noms de framework continueront à être entièrement pris en charge par NuGet 2.1.  Déplacement vers l’avant, les nouveaux noms convient car elles seront plus stables entre les futures versions des plateformes respectifs. Les nouveaux noms seront *pas* être pris en charge dans les versions de NuGet antérieures 2.1, toutefois, la planification en conséquence de la façon de rendre le commutateur.

## <a name="improved-search-in-package-manager-dialog"></a>Recherche améliorée dans la boîte de dialogue Gestionnaire de Package

Sur plusieurs itérations passées, les modifications ont été introduites dans la galerie NuGet qui sont considérablement améliorées la vitesse et la pertinence des recherches de package.  Toutefois, ces améliorations ont été limitées au site Web nuget.org.  NuGet 2.1 rend la recherche améliorée expérience disponible via la boîte de dialogue Gestionnaire de package NuGet.  Par exemple, imaginez que vous souhaitiez trouver le package de l’aperçu de la mise en cache Windows Azure.  Une requête de recherche raisonnable pour ce package peut être « Azure Cache ».  Dans les versions précédentes de la boîte de dialogue de gestionnaire de package, le package souhaité n'est pas encore répertorié dans la première page de résultats.  Toutefois, dans NuGet 2.1, le package souhaité maintenant s’affiche en haut des résultats de recherche.

![Recherche de boîte de dialogue Gestionnaire de package](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forcer la mise à jour du Package

Avant de NuGet 2.1, NuGet serait ignorer la mise à jour d’un package qu’il y a pas un numéro de version haute.  Cela introduit friction pour certains scénarios, en particulier dans le cas de build ou les scénarios de l’élément de configuration où l’équipe ne voulez pas incrémenter la version du package nombre avec chaque build.  Le comportement souhaité a été pour forcer une mise à jour indépendamment.  NuGet 2.1 préciser ce point avec l’indicateur « réinstaller ».  Par exemple, les versions précédentes de NuGet entraînerait les éléments suivants lorsque vous tentez de mettre à jour un package qui n’avait pas une version plus récente du package :

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Avec l’indicateur de réinstallation, le package sera mis à jour indépendamment de si une version plus récente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Un autre scénario dans lequel l’indicateur de réinstallation est un avantage est que de framework reciblage. Lors de la modification du framework cible d’un projet (par exemple, à partir de .NET 4 pour .NET 4.5), Package de mise à jour-réinstaller peut mettre à jour les références aux assemblys correctes pour tous les packages NuGet sont installés dans le projet.

## <a name="edit-package-sources-within-visual-studio"></a>Modifier les Sources de Package Visual Studio

Dans les versions précédentes de NuGet, mise à jour d’une source de package à partir de la boîte de dialogue options Visual Studio requis la suppression et l’ajout de nouveau la source du package.  NuGet 2.1 améliore ce flux de travail en prenant en charge la mise à jour en fonction de l’interface utilisateur de configuration de première classe.

![Boîte de dialogue de configuration de package manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correctifs de bogues

NuGet 2.1 inclut de nombreux correctifs de bogues. Pour obtenir la liste complète de travail éléments fixes dans NuGet 2.0, veuillez vue le [NuGet Issue Tracker pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
