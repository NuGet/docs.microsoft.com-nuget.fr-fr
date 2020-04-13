---
title: Fichier project.json NuGet avec les projets UWP
description: Description de la façon dont le fichier project.json est utilisé pour suivre les dépendances NuGet dans les projets de plateforme Windows universelle (UWP).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494368"
---
# <a name="projectjson-and-uwp"></a>project.json et UWP

> [!Important]
> Ce contenu est déconseillé. Les projets doivent utiliser soit le format `packages.config`, soit le format PackageReference.

Ce document décrit la structure du package qui utilise les fonctionnalités de NuGet 3+ (Visual Studio 2015 et versions ultérieures). La propriété `minClientVersion` de votre `.nuspec` peut être utilisée pour indiquer que vous avez besoin des fonctionnalités décrites ici en lui affectant la valeur 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Ajout de la prise en charge de la plateforme Windows universelle à un package existant

Si vous disposez d’un package existant et que vous souhaitez ajouter la prise en charge des applications de la plateforme Windows universelle (UWP), alors vous n’avez pas besoin d’adopter le format d’empaquetage décrit ici. Vous devez uniquement adopter ce format si vous avez besoin des fonctionnalités qu’il décrit et que vous voulez travailler uniquement avec les clients qui ont effectué une mise à jour vers la version 3+ du client NuGet.

## <a name="i-already-target-netcore45"></a>Je cible déjà netcore45

Si vous ciblez déjà `netcore45` et que vous n’avez pas besoin des fonctionnalités décrites ici, aucune action n’est nécessaire. Les packages `netcore45` peuvent être consommés par les applications UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Je veux exploiter les API spécifiques de Windows 10

Dans ce cas, vous devez ajouter le moniker de la version cible de .Net Framework `uap10.0` (TFM ou TxM) à votre package. Créez un dossier dans votre package et ajoutez l’assembly qui a été compilé pour utiliser Windows 10 dans ce dossier.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Je n’ai pas besoin des API spécifiques de Windows 10, mais je veux utiliser les nouvelles fonctionnalités .NET ou je n’ai pas encore netcore45

Dans ce cas, ajoutez le TxM `dotnet` à votre package. Contrairement aux autres TxM, `dotnet` n’implique pas de surface d’exposition ni de plateforme. Il indique que votre package fonctionne sur n’importe quelle plateforme sur laquelle vos dépendances fonctionnent. Lors de la `dotnet` construction d’un paquet avec le TxM, vous êtes `.nuspec`susceptible d’avoir beaucoup plus de dépendances `System.Text`TxM spécifiques dans votre , que vous devez définir les paquets BCL dont vous dépendez, tels, , `System.Xml`, etc. Les emplacements sur lesquelles ces dépendances fonctionnent définissent l’endroit où votre colis fonctionne.

### <a name="how-do-i-find-out-my-dependencies"></a>Comment trouver mes dépendances

Il existe deux façons de déterminer les dépendances à répertorier :

1. Utilisez l’outil [Générateur de dépendances NuSpec](https://github.com/onovotny/ReferenceGenerator) **tiers**. Cet outil automatise le processus et met à jour votre fichier `.nuspec` avec les packages dépendants pendant la génération. Il est disponible par le biais d’un package NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Méthode plus difficile) Utilisez `ILDasm` pour examiner votre `.dll` pour voir quels assemblys sont en fait nécessaires au moment de l’exécution. Déterminez ensuite de quel package NuGet ils proviennent.

Consultez [`project.json`](project-json.md) le sujet pour plus de détails sur les `dotnet` fonctionnalités qui aident à la création d’un paquet qui prend en charge le TxM.

> [!Important]
> Si votre package est prévu pour fonctionner avec des projets de la bibliothèque de classes portables, nous vous recommandons fortement de créer un dossier `dotnet`, pour éviter les avertissements et les éventuels problèmes de compatibilité.

## <a name="directory-structure"></a>Structure de répertoires

Les packages NuGet qui utilisent ce format ont le dossier et les comportements connus suivants :

| Dossier | Comportements |
| --- | --- |
| Build | Contient des fichiers de cibles et de propriétés MSBuild dans ce dossier qui sont intégrées différemment au projet, mais à part cela, il n’y a aucun changement. |
| Outils | `install.ps1` et `uninstall.ps1` ne sont pas exécutés. `init.ps1` fonctionne comme il l’a toujours fait. |
| Contenu | Le contenu n’est pas copié automatiquement dans le projet de l’utilisateur. Une prise en charge de l’inclusion de contenu dans le projet est prévue dans une prochaine version. |
| Lib | Pour de nombreux packages, le dossier `lib` fonctionne de la même manière que dans NuGet 2.x, mais avec des options étendues pour les noms utilisables et une meilleure logique pour récupérer le sous-dossier approprié lors de la consommation de packages. Toutefois, lorsqu’il est utilisé conjointement avec `ref`, le dossier `lib` contient les assemblys qui implémentent la surface d’exposition définie par les assemblys inclus dans le dossier `ref`. |
| Ref | `ref` est un dossier facultatif qui contient des assemblys .NET définissant la surface publique (types et méthodes publics) sur laquelle se compile une application. Les assemblys inclus dans ce dossier n’ont peut-être aucune implémentation, ils sont purement utilisés pour définir la surface d’exposition du compilateur. Si le package n’a pas de dossier `ref`, alors le dossier `lib` est à la fois l’assembly de référence et l’assembly d’implémentation. |
| Runtimes | Le dossier `runtimes` est un dossier facultatif qui contient du code spécifique du système d’exploitation, comme l’architecture du processeur et d’autres fichiers binaires dépendant de la plateforme. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Fichiers de cibles et de propriétés MSBuild dans des packages

Les packages NuGet peuvent contenir des fichiers `.targets` et `.props` importés dans un projet MSBuild dans lequel le package est installé. Dans NuGet 2.x, il fallait injecter des instructions `<Import>` dans le fichier `.csproj` pour cela. Dans NuGet 3.0, il n’y a pas d’action d’« installation dans le projet » spécifique. Le processus de restauration du package écrit plutôt deux fichiers `[projectname].nuget.props` et `[projectname].NuGet.targets`.

MSBuild sait rechercher ces deux fichiers et les importe automatiquement au début et à la fin du processus de génération du projet. Ce comportement est très similaire à celui de NuGet 2.x, avec une différence majeure : *l’ordre des fichiers de cibles/propriétés n’est pas garanti dans ce cas*. Toutefois, MSBuild offre des moyens de définir l’ordre des cibles par le biais des attributs `BeforeTargets` et `AfterTargets` de la définition `<Target>` (consultez [Target, élément (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib et Ref

Le comportement du dossier `lib` n’a pas changé de manière significative dans NuGet v3. En revanche, tous les assemblys doivent se trouver dans des sous-dossiers nommés comme un TxM. Ils ne peuvent plus être placés directement sous le dossier `lib`. Un TxM est le nom d’une plateforme pour laquelle une ressource donnée dans un package est supposée travailler. Logiquement, il s’agit d’une extension de TFM (moniker de la version cible de .Net Framework). Notamment, `net45`, `net46`, `netcore50` et `dnxcore50` sont tous des exemples de TxM (consultez [Versions cibles de .Net Framework](../reference/target-frameworks.md). TxM peut faire référence à un framework (TFM) ainsi qu’à d’autres surfaces d’exposition propre à la plateforme. Par exemple, le TxM UWP (`uap10.0`) représente la surface d’exposition .NET, ainsi que la surface d’exposition Windows des applications UWP.

Un exemple de structure lib :

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

Le dossier `lib` contient les assemblys utilisés au moment de l’exécution. Pour la plupart des packages, un dossier sous `lib` pour chacun de TxM cibles est le seul élément requis.

## <a name="ref"></a>Ref

Il existe parfois des cas où un autre assembly doit être utilisé lors de la compilation (c’est le cas des assemblys de référence .NET aujourd’hui). Dans ces cas, utilisez un dossier de niveau supérieur appelé `ref` (comprenez « assemblys de référence »).

La plupart des auteurs de package n’ont pas besoin du dossier `ref`. Il s’avère utile pour les packages qui doivent fournir une surface d’exposition cohérente pour la compilation et IntelliSense, mais qui ont une implémentation différente pour différents TxM. Les principaux cas d’usage impliquent les packages `System.*` produits dans le cadre de la fourniture de .NET Core sur NuGet. Ces packages ont des implémentations différentes unifiées par un ensemble cohérent d’assemblys de référence.

Mécaniquement, les assemblys inclus dans le dossier `ref` sont les assemblys de référence passés au compilateur. Pour ceux qui ont utilisé csc.exe, il s’agit des assemblys que nous passons au commutateur de [l’option C# /reference](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).

La structure du dossier `ref` est la même que `lib`, par exemple :

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

Dans cet exemple, les assemblys inclus dans les répertoires `ref` sont tous identiques.

## <a name="runtimes"></a>Runtimes

Le dossier des runtimes contient des assemblys et des bibliothèques natives devant s’exécuter sur des « runtimes » spécifiques, qui sont généralement définis par le système d’exploitation et l’architecture du processeur. Ces temps d’exécution sont identifiés à l’aide `win` [d’identifiants Runtime (RIDs)](/dotnet/core/rid-catalog) tels que , `win-x86`, `win7-x86`, `win8-64`etc.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Programmes d’assistance natifs pour utiliser les API spécifiques à la plateforme

L’exemple suivant montre un package qui a une implémentation purement managée pour plusieurs plateformes, mais qui utilise des assistances natives sur Windows 8, où il peut appeler des API natives propres à Windows 8.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Avec le package ci-dessus, les événements suivants se produisent :

- En dehors de Windows 8, l’assembly `lib/net40/MyLibrary.dll` est utilisé.

- Sur Windows 8, `runtimes/win8-<architecture>/lib/MyLibrary.dll` est utilisé et `native/MyNativeHelper.dll` est copié dans la sortie de votre génération.

Dans l’exemple ci-dessus, l’assembly `lib/net40` est purement du code managé, tandis que les assemblys du dossier des runtimes utilisent p/invoke dans l’assembly d’assistance native pour appeler les API propres à Windows 8.

Un seul dossier `lib` est sélectionné, donc s’il existe un dossier propre au runtime, il est préféré à un `lib` non propre au runtime. Le dossier natif est additif ; s’il existe, il est copié dans la sortie de la génération.

## <a name="managed-wrapper"></a>Wrapper managé

Une autre façon d’utiliser les runtimes consiste à fournir un package qui est purement un wrapper managé sur un assembly natif. Dans ce scénario, vous créez un package comme le suivant :

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

Dans ce cas, il n’y a pas de dossier `lib` de niveau supérieur puisque qu’il n’y a pas d’implémentation de ce package qui ne repose pas sur l’assembly natif correspondant. Si l’assembly managé, `MyLibrary.dll`, était exactement le même dans les deux cas, alors nous pouvons le placer dans un dossier `lib` de niveau supérieur, mais étant donné que l’absence d’un assembly natif n’entraîne pas l’échec de l’installation du package s’il a été installé sur une plateforme autre que win-x86 ou win-x64, alors le dossier lib de niveau supérieur est utilisé sans qu’aucun assembly natif ne soit copié.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Création de packages pour NuGet 2 et NuGet 3

Si vous souhaitez créer un package consommable par des projets à l’aide de `packages.config` ainsi que des packages à l’aide de `project.json`, alors les conditions suivantes s’appliquent :

- Les dossiers ref et runtimes fonctionnent uniquement sur NuGet 3. Ils sont tous les deux ignorés par NuGet 2.

- Vous ne pouvez pas compter sur le fonctionnement de `install.ps1` ou `uninstall.ps1`. Ces fichiers s’exécutent lorsque vous utilisez `packages.config`, mais ils sont ignorés avec `project.json`. Par conséquent, votre package doit être utilisable sans qu’ils s’exécutent. `init.ps1` s’exécute toujours sur NuGet 3.

- L’installation des cibles et des propriétés est différente, alors vérifiez que votre package fonctionne comme prévu sur les deux clients.

- Les sous-répertoires de lib doivent être un TxM dans NuGet 3. Vous ne pouvez pas placer des bibliothèques à la racine du dossier `lib`.

- Le contenu n’est pas copié automatiquement avec NuGet 3. Les consommateurs de votre package peuvent copier les fichiers eux-mêmes ou utiliser un outil comme un exécuteur de tâches pour automatiser la copie des fichiers.

- Les transformations de fichiers sources et de configuration ne sont pas exécutées par NuGet 3.

Si vous prenez en charge NuGet 2 et 3, alors votre `minClientVersion` doit être la version la plus basse du client NuGet 2 sur laquelle fonctionne votre package. Dans le cas d’un package existant, aucune modification n’est nécessaire.
