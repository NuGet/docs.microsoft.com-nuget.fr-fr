---
title: Résolution des dépendances de package NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informations détaillées sur le processus par lequel les dépendances d’un package NuGet sont résolues , puis installées dans NuGet 2.x et NuGet 3.x+.
keywords: Dépendances de package NuGet, gestion des versions NuGet, versions des dépendances, graphique des versions, résolution des versions, restauration transitive
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: d387acd369c88a64abaa2cb94a913fe211df8da1
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a>Comment NuGet résout les dépendances de package

Lorsqu’un package est installé ou réinstallé, y compris dans le cadre d’un processus de [restauration](../consume-packages/package-restore.md), NuGet installe également tous les packages supplémentaires dont dépend ce premier package.

Ces dépendances immédiates peuvent également avoir leurs propres dépendances, et les dépendances peuvent ainsi continuer jusqu’à la profondeur souhaitée. Cela génère ce que l’on appelle un *graphique de dépendance*, qui décrit les relations entre les packages à tous les niveaux.

Lorsque plusieurs packages partagent une même dépendance, le même ID de package peut apparaître plusieurs fois dans le graphique, potentiellement avec des restrictions de version différentes. Néanmoins, un projet ne peut utiliser qu’une seule version d’un package donné ; NuGet doit donc choisir laquelle. Le processus exact varie selon le format de gestion des packages utilisé.

## <a name="dependency-resolution-with-packagereference"></a>Résolution des dépendances avec PackageReference

Lorsque des packages sont installés dans un projet au format PackageReference, NuGet ajoute des références à un graphique de packages plat dans le fichier correspondant, et résout les conflits à l’avance. Ce processus est appelé *restauration transitive*. Les processus de réinstallation et de restauration des packages reviennent donc à télécharger les packages répertoriés dans le graphique, ce qui permet d’obtenir des builds plus prévisibles, plus rapidement. Vous pouvez également tirer parti des versions génériques (flottantes), telles que 2.8.\*, afin d’éviter les appels à `nuget update` (qui sont coûteux et sujets aux erreurs) sur les ordinateurs clients et les serveurs de builds.

Lorsque le processus de restauration NuGet est exécuté avant une build, il résout d’abord les dépendances dans la mémoire, puis écrit le graphique résultant dans un fichier nommé `project.assets.json`, situé dans le dossier `obj` d’un projet qui utilise PackageReference. MSBuild lit alors ce fichier et le convertit en un ensemble de dossiers pouvant contenir des références, puis les ajoute à l’arborescence de projets en mémoire.

Le fichier de verrouillage est temporaire et ne doit pas être ajouté au contrôle de code source. Ce fichier est répertorié par défaut dans `.gitignore` et `.tfignore`. Consultez [Packages et contrôle de code source](packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Règles de résolution des dépendances

La restauration transitive applique quatre règles principales pour résoudre les dépendances : la plus ancienne version applicable, les versions flottantes, le package le plus proche et les dépendances cousines.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>La plus ancienne version applicable

La règle de la version la plus ancienne applicable restaure la version la plus ancienne possible d’un package, comme défini par ses dépendances. Elle s’applique également aux dépendances de l’application et de la bibliothèque de classes, sauf si déclarée comme [flottante](#floating-versions).

Dans la figure suivante, par exemple, 1.0-beta est considéré comme une version plus ancienne que 1.0. De fait, NuGet choisit la version 1.0 :

![Choix de la plus ancienne version applicable](media/projectJson-dependency-1.png)

Dans la figure suivante, la version 2.1 n’est pas disponible dans le flux. Toutefois, étant donné que la restriction de version est supérieure ou égale à 2.1, NuGet récupère la plus ancienne version suivante, dans ce cas 2.2 :

![Choix de la plus ancienne version suivante disponible dans le flux](media/projectJson-dependency-2.png)

Lorsqu’une application spécifie un numéro de version exact (tel que 1.2) qui n’est pas disponible dans le flux, NuGet échoue avec une erreur lorsque vous tentez d’installer ou de restaurer le package :

![NuGet génère une erreur lorsqu’une version de package exacte n’est pas disponible](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Versions flottantes (génériques)

Une version de dépendance flottante ou générique est spécifiée avec le caractère générique \*, comme dans 6.0.\*. Cette spécification signifie « utiliser la dernière version 6.0.x », et 4.\* signifie « utiliser la dernière version 4.x ». L’utilisation d’un caractère générique permet à un package de dépendance de continuer à évoluer, sans nécessiter la modification de l’application (ou du package) qui consomme.

Lorsque vous utilisez un caractère générique, NuGet résout la version la plus récente d’un package qui correspond au modèle de version. Par exemple, 6.0.\* obtient la version la plus récente d’un package commençant par 6.0 :

![Choix de la version 6.0.1 lorsqu’une version flottante 6.0.* est demandée](media/projectJson-dependency-4.png)

> [!Note]
> Pour plus d’informations sur le comportement des caractères génériques et les préversions, consultez [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Package le plus proche

Lorsque le graphique de package d’une application contient des versions différentes d’un même package, NuGet choisit le package qui est le plus proche de l’application dans le graphique, et ignore toutes les autres. Ce comportement permet à une application de remplacer n’importe quelle version de package dans le graphique de dépendance.

Dans l’exemple ci-dessous, l’application dépend directement du Package B ayant une restriction de version « supérieure ou égale à 2.0 ». L’application dépend également du Package A, qui, lui, dépend du Package B. Toutefois, sa restriction de version est « supérieure ou égale à 1.0 ». Étant donné que la dépendance du Package B 2.0 est plus proche de l’application dans le graphique, sa version est utilisée :

![Application utilisant la règle du package le plus proche](media/projectJson-dependency-5.png)

>[!Warning]
> La règle du package le plus proche peut entraîner le passage à une version antérieure du package, et rompre les autres dépendances du graphique. Par conséquent, lorsque cette règle est appliquée, un avertissement s’affiche pour l’utilisateur.

Cette règle permet également une plus grande efficacité avec les graphiques de dépendance volumineux (tels que ceux qui contiennent des packages BCL), car une fois qu’une dépendance donnée est ignorée, NuGet ignore également toutes les dépendances de la même branche du graphique. Dans le diagramme ci-dessous, par exemple, comme le Package C 2.0 est utilisé, NuGet ignore toutes les branches du graphique qui font référence à une version plus ancienne du Package C :

![Lorsque NuGet ignore un package dans le graphique, il ignore l’intégralité de la branche du package](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Dépendances cousines

Lorsque des versions de package différentes sont référencées à une même distance de l’application, NuGet utilise la plus ancienne version qui répond à toutes les exigences de version (comme avec la règle de [la plus ancienne version applicable](#lowest-applicable-version) et la règle de [version flottante](#floating-versions)). Dans l’image ci-dessous, par exemple, la version 2.0 du Package B respecte l’autre restriction « supérieure ou égale à 1.0 », et est donc utilisée :

![Résolution des dépendances cousines à l’aide de la plus ancienne version qui respecte toutes les restrictions](media/projectJson-dependency-7.png)

Dans certains cas, il n’est pas possible de répondre à toutes les conditions des versions. Comme indiqué ci-dessous, si le Package A nécessite exactement le Package B 1.0, et si le Package C nécessite le Package B « version supérieure ou égale à 2.0 », NuGet ne peut pas résoudre les dépendances et génère une erreur.

![Dépendances ne pouvant être résolues en raison d’une spécification de version exacte](media/projectJson-dependency-8.png)

Dans ce cas, le consommateur de niveau supérieur (l’application ou le package) doit ajouter sa propre dépendance directe au Package B pour que la règle de la [version la plus proche](#nearest-wins) soit appliquée.

## <a name="dependency-resolution-with-packagesconfig"></a>Résolution des dépendances avec packages.config

Avec `packages.config`, les dépendances d’un projet sont écrites dans `packages.config` sous forme d’une liste plate. Toutes les dépendances de ces packages sont écrites dans une même liste. Lorsque les packages sont installés, NuGet peut également modifier le fichier `.csproj`, `app.config`, `web.config`, et d’autres fichiers.

Avec `packages.config`, NuGet tente de résoudre les conflits de dépendance lors de l’installation de chaque package. Autrement dit, si le Package A est en cours d’installation et dépend du Package B, et si ce dernier est déjà répertorié dans `packages.config` comme une dépendance d’un autre élément, NuGet compare les versions du Package B demandé et tente de trouver une version respectant toutes les restrictions de version. Plus précisément, NuGet sélectionne la version la plus ancienne *majeure.mineure* qui répond aux dépendances.

Par défaut, NuGet 2.8 recherche la version corrective la plus ancienne (voir [Notes de publication NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Vous pouvez contrôler ce paramètre via l’attribut `DependencyVersion` de `Nuget.Config`, et le commutateur `-DependencyVersion` sur la ligne de commande.  

Le processus `packages.config` de résolution des dépendances devient complexe pour les graphiques de dépendance plus volumineux. Chaque nouvelle installation de package nécessite le parcours de l’ensemble du graphique, ce qui entraîne un risque de conflit de versions. En cas de conflit, l’installation est arrêtée, ce qui laisse le projet dans un état indéterminé, avec des modifications potentielles du fichier projet. Ce n’est pas un problème en cas d’utilisation d’autres formats de gestion des packages.

## <a name="managing-dependency-assets"></a>Gestion des ressources de dépendance

Le format PackageReference permet de choisir les ressources des dépendances qui seront acheminées dans le projet de niveau supérieur. Pour plus d’informations, consultez la section [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).

Lorsque le projet de niveau supérieur est un package, vous pouvez contrôler ce flux en utilisant les attributs `include` et `exclude` avec les dépendances répertoriées dans le fichier `.nuspec`. Consultez [Référence .nuspec - Dépendances](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Exclusion de références

Il existe des scénarios dans lesquels les assemblys qui portent le même nom peuvent être référencés plusieurs fois dans un même projet, ce qui génère des erreurs au moment de la conception et de la génération. Imaginez un projet qui contienne une version personnalisée de `C.dll`, et qui référence le Package C contenant également `C.dll`. En même temps, le projet dépend également du Package B qui dépend du Package C et de `C.dll`. Par conséquent, NuGet ne peut pas déterminer quel `C.dll` utiliser. Toutefois, vous ne pouvez pas supprimer la dépendance du projet au Package C, car le Package B en dépend également.

Pour résoudre ce problème, vous devez référencer directement le `C.dll` que vous souhaitez (ou utiliser un autre package qui référence celui qui convient), puis ajouter une dépendance au Package C qui exclut toutes ses ressources. Pour cela, suivez les étapes ci-dessous, selon le format de gestion des packages utilisé :

- [PackageReference](../consume-packages/package-references-in-project-files.md) : ajoutez `Exclude="All"` dans la dépendance :

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config` : supprimez la référence au Package C dans le fichier `.csproj` pour qu’il référence uniquement la version du `C.dll` souhaitée.
    
## <a name="dependency-updates-during-package-install"></a>Mises à jour des dépendances pendant l’installation du package 

Si une condition de version de la dépendance est déjà satisfaite, celle-ci n’est pas mise à jour lors de l’installation des autres packages. Par exemple, imaginons le Package A qui dépend du Package B et qui spécifie 1.0 comme numéro de version. Le référentiel source contient les versions 1.0, 1.1 et 1.2 du Package B. Si le Package A est installé dans un projet qui contient déjà le Package B version 1.0, ce dernier reste utilisé, car la contrainte de version est satisfaite. Toutefois, si le Package A avait demandé la version 1.1 ou ultérieure du Package B, le Package B 1.2 serait installé. 

## <a name="resolving-incompatible-package-errors"></a>Résolution des erreurs de package incompatible

Pendant une opération de restauration de package, vous pouvez rencontrer une erreur vous informant qu’un ou plusieurs packages ne sont pas compatibles ou qu’un package n’est pas compatible avec la version cible du .NET Framework du projet.

Cette erreur se produit lorsqu’un ou plusieurs des packages référencés dans votre projet n’indiquent pas qu’ils prennent en charge la version cible de .NET Framework du projet. Autrement dit, aucune DLL correspondant à une version cible de .NET Framework ne se trouve dans le dossier `lib` du package (consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour obtenir la liste des versions cibles). 

Par exemple, si un projet cible `netstandard1.6` et que vous essayez d’installer un package qui ne contient des DLL que dans les dossiers `lib\net20` et `\lib\net45`, des messages de ce type apparaîtront pour le package et, éventuellement, pour ses éléments dépendants :

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Pour résoudre les incompatibilités, effectuez l’une des opérations suivantes :

- Reciblez votre projet vers un framework pris en charge par les packages que vous souhaitez utiliser.
- Contactez l’auteur des packages et ajoutez ensemble la prise en charge du framework de votre choix. Chaque page qui répertorie des packages sur [nuget.org](https://www.nuget.org/) comprend le lien **Contact Owners** qui permet de contacter les propriétaires des packages.

