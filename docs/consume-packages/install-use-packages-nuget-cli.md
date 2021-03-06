---
title: Gérer des packages NuGet à l’aide de l’interface CLI nuget.exe
description: Instructions d’utilisation de l’interface CLI nuget.exe pour gérer des packages NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237385"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Gérer des packages à l’aide de l’interface CLI nuget.exe

L’outil CLI facilite la mise à jour et la restauration des packages NuGet dans les projets et solutions. Cet outil fournit toutes les fonctionnalités NuGet sur Windows ainsi que la plupart des fonctionnalités sur Mac et Linux dans un environnement d’exécution Mono.

Vous pouvez utiliser l’interface CLI `nuget.exe` pour votre projet .NET Framework et les projets non-SDK-style (par exemple, un projet SDK-style ciblant les bibliothèques .NET Standard). Si vous utilisez un projet non-SDK-style qui a été migré vers `PackageReference`, utilisez l’interface CLI `dotnet` à la place. L’interface CLI `nuget.exe` a besoin d’un fichier [packages.config](../reference/packages-config.md) pour référencer les packages.

> [!NOTE]
> Dans la plupart des scénarios, il est préférable de [migrer les projets non-SDK-style](../consume-packages/migrate-packages-config-to-package-reference.md) qui utilisent `packages.config` vers PackageReference, et d’utiliser ensuite l’interface CLI `dotnet` au lieu de l’interface CLI `nuget.exe`. La migration n’est actuellement pas possible pour les projets C++ et ASP.NET.

Cet article explique l’utilisation de base de quelques-unes des commandes de la CLI `nuget.exe` les plus courantes. Pour la plupart de ces commandes, l’outil CLI recherche un fichier projet dans le répertoire actif, sauf si vous avez spécifié un fichier projet particulier dans la commande. Pour obtenir une liste complète des commandes et des arguments disponibles, consultez les [informations de référence sur l’interface CLI nuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Conditions préalables requises

- Installez l’interface CLI `nuget.exe` en la téléchargeant sur [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) : enregistrez ce fichier `.exe` dans un dossier approprié et ajoutez ce dossier à votre variable d’environnement PATH.

## <a name="install-a-package"></a>Installer un package

La commande [install](../reference/cli-reference/cli-ref-install.md) télécharge et installe un package dans un projet, par défaut dans le dossier actif, en utilisant les sources de packages spécifiées. Installez les nouveaux packages dans le dossier *packages* du répertoire racine de votre projet.

> [!IMPORTANT]
> La commande `install` ne modifie pas le fichier projet ni le fichier *packages.config* . Elle est similaire à la commande `restore` en ce sens qu’elle ajoute seulement les packages sur le disque, sans changer les dépendances du projet. Pour ajouter une dépendance, soit vous ajoutez un package via l’interface utilisateur ou la console du Gestionnaire de package dans Visual Studio, soit vous modifiez *packages.config* et exécutez ensuite `install` ou `restore`.

1. Ouvrez une ligne de commande et accédez au répertoire contenant votre fichier projet.

2. Utilisez la commande suivante pour installer un package NuGet dans le dossier *packages* .

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Pour installer le package `Newtonsoft.json` dans le dossier *packages* , utilisez cette commande :

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Vous pouvez aussi utiliser la commande suivante si vous souhaitez installer un package NuGet à l’aide d’un fichier `packages.config` existant dans le dossier *packages* . Cette commande n’ajoute pas le package aux dépendances de votre projet, elle l’installe localement.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Installer une version particulière d’un package

Si vous ne spécifiez pas de version dans la commande [install](../reference/cli-reference/cli-ref-install.md), NuGet installe la dernière version disponible du package. Vous pouvez toutefois installer une version particulière d’un package Nuget :

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Par exemple, pour ajouter la version 12.0.1 du package `Newtonsoft.json`, utilisez cette commande :

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Pour plus d’informations sur les limitations et le comportement de la commande `install`, consultez [Installer un package](#install-a-package).

## <a name="remove-a-package"></a>Supprimer un package

Pour supprimer un ou plusieurs packages, spécifiez les packages que vous souhaitez supprimer du dossier *packages* .

Pour réinstaller des packages supprimés, utilisez la commande `restore` ou `install`.

## <a name="list-packages"></a>Lister les packages

Vous pouvez lister les packages d’une source donnée à l’aide de la commande [list](../reference/cli-reference/cli-ref-list.md). Utilisez l’option `-Source` pour limiter l’étendue de la recherche.

```cli
nuget list -Source <source>
```

Par exemple, listez les packages contenus dans le dossier *packages* .

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Si vous utilisez un terme de recherche, la recherche porte sur les noms des packages, les balises et les descriptions des packages.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Mettre à jour un seul package

NuGet installe la dernière version du package quand vous utilisez la commande `install`, sauf si vous spécifiez une version particulière du package.

## <a name="update-all-packages"></a>Mettre à jour tous les packages

Utilisez la commande [update](../reference/cli-reference/cli-ref-update.md) pour mettre à jour l’ensemble des packages. Mettez à jour tous les packages dans un projet (en utilisant `packages.config`) avec leurs dernières versions disponibles. Il est recommandé d’exécuter `restore` avant `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Restaurer des packages

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Obtenir la version de la CLI

Utilisez la commande suivante :

```cli
nuget help
```

La première ligne de la sortie d'aide affiche la version. Pour éviter le défilement vers le haut, utilisez `nuget help | more` à la place.