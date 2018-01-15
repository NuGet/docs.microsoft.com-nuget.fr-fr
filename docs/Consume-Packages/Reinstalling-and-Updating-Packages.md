---
title: "Réinstallation et mise à jour des packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2785879b-97f0-4a85-b3cc-bf4eaa5c39bf
description: "Informations détaillées sur la nécessité de réinstaller et mettre à jour des packages, comme lorsque des références de package sont rompues dans Visual Studio."
keywords: "Installation des packages NuGet, réinstallation des packages NuGet, restauration des packages NuGet, mise à jour des packages, restauration des packages, réparation des références rompues"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a198b371c86166e2bcdee7f6cf2a6c971bea0a3
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-reinstall-and-update-packages"></a>Réinstallation et mise à jour des packages

Il existe plusieurs situations (décrites ci-dessous dans [Quand réinstaller un package](#when-to-reinstall-a-package)), dans lesquelles les références à un package peuvent être rompues dans un projet Visual Studio. Dans ce cas, désinstaller et réinstaller la même version du package permet de restaurer ces références. Mettre à jour un package signifie simplement installer une version mise à jour, ce qui, souvent, permet de restaurer un package.

La mise à jour et la réinstallation des packages s’effectuent de la façon suivante :

| Méthode | Mise à jour | Réinstallation | 
| --- | --- | --- |
| Console du gestionnaire de package (décrite dans [Utilisation d’Update-Package](#using-update-package)) | Commande `Update-Package` | Commande `Update-Package -reinstall` |
| Interface utilisateur du gestionnaire de package | Sous l’onglet **Mises à jour**, sélectionnez un ou plusieurs packages, puis sélectionnez **Mettre à jour**. | Sous l’onglet **Installé**, sélectionnez un package, enregistrez son nom, puis sélectionnez **Désinstaller**. Basculez vers l’onglet **Parcourir**, recherchez le nom du package, sélectionnez-le, puis sélectionnez **Installer**. |
| Interface CLI de nuget.exe | Commande `nuget update` | Pour tous les packages, supprimez le dossier de package, puis exécutez `nuget install`. S’il n’y a qu’un seul package, supprimez le dossier de package et utilisez `nuget install <id>` pour réinstaller le même package. |

Dans cet article :

- [Quand réinstaller un package](#when-to-reinstall-a-package)
- [Restriction des versions de mise à niveau](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Quand réinstaller un package

1. **Références rompues après restauration des packages** : si vous avez toujours des références rompues après avoir ouvert un projet et restauré des packages NuGet, essayez de réinstaller chacun de ces packages.
1. **Projet ne fonctionnant plus après une suppression de fichiers** : NuGet ne vous empêche pas de supprimer des éléments ajoutés à partir des packages. Il est donc facile de modifier par inadvertance le contenu installé à partir d’un package et de rendre votre projet inutilisable. Pour restaurer le projet, réinstallez les packages concernés.
1. **Projet ne fonctionnant plus après une mise à jour de package** : si la mise à jour d’un package rend un projet inutilisable, cela est généralement dû à un package de dépendance qui a peut-être été aussi mis à jour. Pour restaurer l’état de la dépendance, réinstallez le package en question.
1. **Reciblage ou mise à niveau du projet** : cela peut être utile lorsqu’un projet a été reciblé ou mis à niveau, et si le package nécessite une réinstallation en raison de la modification de la version cible de .NET Framework. Dans ce cas, NuGet 2.7 (et versions ultérieures) affiche une erreur de build tout de suite après le reciblage du projet, et les avertissements de build suivants vous informent que le package doit être réinstallé. Pour la mise à niveau du projet, NuGet affiche une erreur dans le journal de mise à niveau du projet.
1. **Réinstallation d’un package durant son développement** : les auteurs de packages ont souvent besoin de réinstaller la même version d’un package qu’ils développent afin de tester son comportement. La commande `Install-Package` ne fournit pas d’option permettant de forcer une réinstallation. Vous devez donc utiliser `Update-Package -reinstall` à la place.

## <a name="constraining-upgrade-versions"></a>Restriction des versions de mise à niveau

Par défaut, la réinstallation et la mise à jour d’un package installent *toujours* la dernière version disponible dans la source du package.

Toutefois, dans les projets qui utilisent le format de référence `packages.config`, vous pouvez restreindre la plage des versions. Par exemple, si vous savez que votre application fonctionne uniquement avec la version 1.x d’un package, et pas avec les versions égales et supérieures à 2.0, peut-être en raison d’un changement majeur dans l’API du package, vous devrez restreindre les mises à niveau aux versions 1.x. Cette restriction empêche les mises à jour accidentelles d’endommager l’application.

Pour définir une restriction, ouvrez `packages.config` dans un éditeur de texte, recherchez la dépendance en question, puis ajoutez l’attribut `allowedVersions` avec une plage de versions. Par exemple, pour restreindre les mises à jour à la version 1.x, définissez `allowedVersions` sur `[1,2)` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Utilisation d’Update-Package

Si vous gardez à l’esprit les [éléments à prendre en considération](#considerations) décrits ci-dessous, vous pouvez facilement réinstaller un package à l’aide de la [commande Update-Package](../Tools/ps-ref-update-package.md) dans la console du gestionnaire de package Visual Studio (**Outils**  >  **Gestionnaire de package NuGet** > **Console du gestionnaire de package**) :

```ps
Update-Package -Id <package_name> –reinstall
```

L’utilisation de cette commande est beaucoup plus facile que de supprimer un package et de localiser ce même package dans la galerie NuGet avec la même version. Notez que le commutateur `-Id` est facultatif.

La même commande sans `-reinstall` met à jour un package vers une version plus récente, si nécessaire. La commande génère une erreur si le package en question n’est pas déjà installé dans un projet. Autrement dit, `Update-Package` n’installe pas directement les packages.

```ps
Update-Package <package_name>
```

Par défaut, `Update-Package` affecte tous les packages d’une solution. Pour limiter l’action à un projet spécifique, utilisez le commutateur `-ProjectName`, en utilisant le nom du projet tel qu’il apparaît dans l’Explorateur de solutions :

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```
Pour *mettre à jour* tous les packages d’un projet (ou les réinstaller à l’aide de `-reinstall`), utilisez `-ProjectName` sans spécifier un package particulier :

```ps
Update-Package -ProjectName MyProject
```

Pour mettre à jour tous les packages d’une solution, utilisez `Update-Package` tout seul, sans aucun autre argument ni commutateur. Utilisez ce formulaire avec précaution, car il peut mettre beaucoup de temps à effectuer toutes les mises à jour :

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

La mise à jour des packages d’un projet ou d’une solution à l’aide de `project.json` ou de [références de package dans des fichiers projet](../Consume-Packages/Package-References-in-Project-Files.md) est toujours effectuée vers la version la plus récente du package (à l’exclusion des packages de préversion). Les projets qui utilisent `packages.config` peuvent, si vous le souhaitez, limiter les versions de mise à jour, comme décrit ci-dessous dans [Restriction des versions de mise à niveau](#constraining-upgrade-versions).

Pour plus d’informations sur la commande, consultez la référence relative à [Update-Package](../Tools/ps-ref-update-package.md).

### <a name="considerations"></a>Éléments à prendre en considération

Les procédures suivantes peuvent être affectées lors de la réinstallation d’un package :

1. **Réinstallation de packages en fonction du reciblage de la version cible de .NET Framework**
    - Dans un cas simple, vous pouvez réinstaller un package à l’aide de `Update-Package –reinstall <package_name>`. Un package installé dans une ancienne version cible de .NET Framework est désinstallé, puis installé dans la version cible de .NET Framework actuelle du projet.
    - Dans certains cas, il peut arriver qu’un package ne prenne pas en charge la nouvelle version cible de .NET Framework.
        - Si un package prend en charge des bibliothèques de classes portables et si le projet est reciblé vers une combinaison de plateformes qui ne sont plus prises en charge par le package, les références au package seront manquantes après la réinstallation.
        - Cela peut se produire pour les packages que vous utilisez directement ou pour les packages installés en tant que dépendances. Il est possible que le package que vous utilisez directement prenne en charge la nouvelle version cible de .NET Framework, sans que ce soit le cas de ses dépendances.
        - Si la réinstallation des packages après le reciblage de votre application entraîne des erreurs de build ou de runtime, vous devrez peut-être rétablir l’ancienne version cible de .NET Framework ou chercher d’autres packages prenant en charge votre nouvelle version cible.

1. **Ajout de l’attribut requireReinstallation au fichier packages.config après la mise à niveau ou le reciblage du projet**
    - Si NuGet détecte que des packages ont été affectés par le reciblage ou la mise à niveau d’un projet, il ajoute un attribut `requireReinstallation="true"` dans `packages.config` pour toutes les références de package affectées. Pour cette raison, toutes les builds suivantes dans Visual Studio génèrent des avertissements de build pour ces packages afin de vous rappeler de les réinstaller.

1. **Réinstallation des packages avec des dépendances**
    - `Update-Package –reinstall` réinstalle la même version du package d’origine, mais installe la dernière version des dépendances, à moins que des restrictions de version n’aient été définies. Cela vous permet de mettre à jour uniquement les dépendances pour résoudre un problème. Toutefois, si cette opération restaure une version antérieure d’une dépendance, vous pouvez utiliser `Update-Package <dependency_name>` pour réinstaller cette dépendance sans affecter le package dépendant.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` réinstalle la même version du package d’origine, mais ne réinstalle pas les dépendances. Utilisez cette option lorsque la mise à jour des dépendances de package peuvent endommager les dépendances.

1. **Réinstallation de packages quand des versions dépendantes sont impliquées**
    - Comme expliqué ci-dessus, la réinstallation d’un package ne modifie pas les versions des autres packages installés qui en dépendent. Il est donc possible que la réinstallation d’une dépendance endommage le package dépendant.

