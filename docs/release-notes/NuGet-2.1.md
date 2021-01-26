---
title: Notes de publication de NuGet 2,1
description: Notes de publication de NuGet 2,1, y compris les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777030"
---
# <a name="nuget-21-release-notes"></a>Notes de publication de NuGet 2,1

Notes de publication de [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Notes de publication de NuGet 2,2](../release-notes/nuget-2.2.md)

NuGet 2,1 a été publié le 4 octobre 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config hiérarchique

NuGet 2,1 vous offre une plus grande flexibilité dans le contrôle des paramètres NuGet grâce à la redirection récursive de la structure de dossiers à la recherche de `NuGet.Config` fichiers, puis à la génération de la configuration à partir de l’ensemble de tous les fichiers trouvés.  Par exemple, considérez le scénario dans lequel une équipe a un référentiel de packages interne pour les builds d’intégration continue d’autres dépendances internes. La structure de dossiers d’un projet individuel peut se présenter comme suit :

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

En outre, si la restauration des packages est activée pour la solution, le dossier suivant existera également :

```
C:\myteam\solution1\.nuget
```

Pour que le référentiel de packages interne de l’équipe soit disponible pour tous les projets sur lesquels l’équipe travaille, sans qu’il soit disponible pour chaque projet sur l’ordinateur, nous pouvons créer un fichier Nuget.Config et le placer dans le dossier c:\myteam. Il n’existe aucun moyen de dénombrer un dossier de packages par projet.

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

Nous pouvons maintenant voir que la source a été ajoutée en exécutant la commande’sources de nuget.exe 'à partir de n’importe quel dossier sous c:\myteam, comme indiqué ci-dessous :

![Sources de package de la configuration NuGet parente](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` les fichiers sont recherchés dans l’ordre suivant :

1. `.nuget\Nuget.Config`
2. Parcours récursif du dossier du projet vers la racine
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Les configurations sont appliquées dans l' *ordre inverse*, ce qui signifie qu’en fonction du classement ci-dessus, le Nuget.Config global est appliqué en premier, suivi des fichiers Nuget.Config détectés du dossier racine au dossier du projet, suivi de `.nuget\Nuget.Config` .  Cela est particulièrement important si vous utilisez l' `<clear/>` élément pour supprimer un ensemble d’éléments de la configuration.

## <a name="specify-packages-folder-location"></a>Spécifier l’emplacement du dossier « Packages »

Dans le passé, NuGet gérait les packages d’une solution à partir d’un dossier connu « packages » situé sous le dossier racine de la solution.  Pour les équipes de développement qui possèdent de nombreuses solutions pour lesquelles des packages NuGet sont installés, cela peut entraîner l’installation d’un même package à différents emplacements du système de fichiers.

NuGet 2,1 fournit un contrôle plus granulaire sur l’emplacement du dossier Packages par le biais de l' `repositoryPath` élément dans le `NuGet.Config` fichier.  En s’appuyant sur l’exemple précédent de prise en charge de Nuget.Config hiérarchique, supposons que nous souhaitons que tous les projets sous C:\myteam\ partagent le même dossier de packages.  Pour ce faire, ajoutez simplement l’entrée suivante à `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Dans cet exemple, le `Nuget.Config` fichier partagé spécifie un dossier de packages partagés pour chaque projet créé sous C:\myteam, quelle que soit sa profondeur. Notez que si vous avez un dossier Packages existant sous la racine de votre solution, vous devez le supprimer pour que NuGet place les packages dans le nouvel emplacement.

## <a name="support-for-portable-libraries"></a>Prise en charge des bibliothèques portables

Les [bibliothèques portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) sont une fonctionnalité introduite pour la première fois avec .net 4, qui vous permet de créer des assemblys qui peuvent fonctionner sans modification sur différentes plateformes Microsoft, des versions de The.NET Framework à Silverlight pour Windows Phone et même la Xbox 360 (à ce stade, NuGet ne prend pas en charge la cible de la bibliothèque portable Xbox).  En étendant les [conventions de package](../create-packages/supporting-multiple-target-frameworks.md) pour les versions et les profils du Framework, NuGet 2,1 prend désormais en charge les bibliothèques portables en vous permettant de créer des packages qui ont des dossiers d’infrastructure composée et de profil cible `lib` .

Par exemple, considérez les plateformes cibles disponibles suivantes de la bibliothèque de classes portable.

![Boîte de dialogue de création de bibliothèque portable](./media/releasenotes-21-plib.png)

Une fois la bibliothèque générée et la commande `nuget.exe pack MyPortableProject.csproj` exécutée, la nouvelle structure de dossiers de package de bibliothèque portable peut être consultée en examinant le contenu du package NuGet généré.

![Disposition de package de bibliothèque portable](./media/releasenotes-21-plib-layout.png)

Comme vous pouvez le voir, la Convention de nom de dossier de la bibliothèque portable suit le modèle « portable-{Framework 1} + {Framework n} », où les identificateurs de Framework suivent le [nom et les conventions de version](../reference/target-frameworks.md)existants de l’infrastructure. Une exception aux conventions de nom et de version se trouve dans l’identificateur de Framework utilisé pour Windows Phone.  Ce moniker doit utiliser le nom de Framework’WP' (WP7, wp71 ou wp8). L’utilisation de’Silverlight-WP7 ', par exemple, génère une erreur.

Lors de l’installation du package créé à partir de cette structure de dossiers, NuGet peut désormais appliquer ses règles d’infrastructure et de profil à plusieurs cibles, comme indiqué dans le nom du dossier.  Derrière les règles de correspondance de NuGet est le principe que les cibles « plus spécifiques » ont priorité sur les « moins spécifiques ».  Cela signifie que les monikers ciblant une plateforme spécifique sont toujours préférés aux ordinateurs portables s’ils sont tous les deux compatibles avec un projet.  En outre, si plusieurs cibles portables sont compatibles avec un projet, NuGet préfère celui où l’ensemble de plates-formes prises en charge est « le plus proche » du projet référençant le package.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Ciblage de projets Windows 8 et Windows Phone 8

Outre l’ajout de la prise en charge du ciblage des projets de bibliothèque portables, NuGet 2,1 fournit de nouveaux monikers de Framework pour les projets Windows 8 Store et Windows Phone 8, ainsi que certains nouveaux monikers généraux pour les projets Windows Store et Windows Phone qui seront plus faciles à gérer sur les futures versions des plateformes respectives.

Pour les applications du Windows Store de Windows 8, les identificateurs se présentent comme suit :

| NuGet 2,0 et versions antérieures | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45,. NETCore45 | Windows, Windows8, Win, WIN8 |

<br/>
Pour les projets Windows Phone, les identificateurs se présentent comme suit :

| SE téléphone | NuGet 2,0 et versions antérieures | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-WP | WP, WP7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (non pris en charge) | wp8, WindowsPhone8 |

<br/>
Dans toutes les modifications apportées ci-dessus, les anciens noms de Framework seront toujours entièrement pris en charge par NuGet 2,1.  À l’avenir, les nouveaux noms doivent être utilisés, car ils seront plus stables dans les futures versions des plateformes respectives. Toutefois, les nouveaux noms ne seront *pas* pris en charge dans les versions de NuGet antérieures à 2,1. par conséquent, planifiez en conséquence le moment où le basculement doit être effectué.

## <a name="improved-search-in-package-manager-dialog"></a>Recherche améliorée dans la boîte de dialogue du gestionnaire de package

Au cours des différentes itérations, des modifications ont été introduites dans la galerie NuGet, ce qui a amélioré la vitesse et la pertinence des recherches dans les packages.  Toutefois, ces améliorations étaient limitées au site Web nuget.org.  NuGet 2,1 rend l’expérience de recherche améliorée disponible par le biais de la boîte de dialogue Gestionnaire de package NuGet.  Par exemple, imaginez que vous souhaitiez trouver le package de la version préliminaire de Windows Azure Caching.  Une requête de recherche raisonnable pour ce package peut être « Azure cache ».  Dans les versions précédentes de la boîte de dialogue du gestionnaire de package, le package souhaité ne serait même pas listé sur la première page des résultats.  Toutefois, dans NuGet 2,1, le package souhaité s’affiche désormais en haut des résultats de la recherche.

![Recherche de boîte de dialogue du gestionnaire de package](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forcer la mise à jour du package

Avant NuGet 2,1, NuGet ignorerait la mise à jour d’un package alors qu’il n’existait pas de numéro de version élevé.  Cela a introduit un frottement pour certains scénarios, en particulier dans le cas de scénarios de génération ou d’élément de configuration où l’équipe ne souhaitait pas incrémenter le numéro de version de package avec chaque Build.  Le comportement souhaité consistait à forcer une mise à jour, quelle que soit la valeur.  NuGet 2,1 traite ceci avec l’indicateur « REINSTALL ».  Par exemple, les versions précédentes de NuGet se traduiraient par les éléments suivants lors de la tentative de mise à jour d’un package qui ne disposait pas d’une version plus récente du package :

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Avec l’indicateur de réinstallation, le package est mis à jour, qu’il y ait ou non une version plus récente.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Un autre scénario dans lequel l’indicateur de réinstallation s’avère bénéfique est le reciblage de Framework. Lors de la modification de la version cible du .NET Framework d’un projet (par exemple, de .NET 4 vers .NET 4,5), Update-Package-REINSTALL peut mettre à jour les références aux assemblys corrects pour tous les packages NuGet installés dans le projet.

## <a name="edit-package-sources-within-visual-studio"></a>Modifier des sources de package dans Visual Studio

Dans les versions précédentes de NuGet, la mise à jour d’une source de package à partir de la boîte de dialogue Options de Visual Studio nécessitait de supprimer et rajouter la source du package.  NuGet 2,1 améliore ce flux de travail en prenant en charge la mise à jour en tant que fonction de première classe de l’interface utilisateur de configuration.

![Boîte de dialogue de configuration du gestionnaire de package](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Résolutions de bogues

NuGet 2,1 comprend de nombreux correctifs de bogues. Pour obtenir la liste complète des éléments de travail corrigés dans NuGet 2,0, consultez le [suivi des problèmes NuGet pour cette version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
