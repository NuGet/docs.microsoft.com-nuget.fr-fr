---
title: Création et publication d’un package NuGet avec l’interface CLI dotnet
description: Ce didacticiel explique pas à pas comment créer et publier un package NuGet avec l’interface de ligne de commande (CLI) .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: 02aa7bb9d27352bbecfc718ef5bd6ee33501018d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548427"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Démarrage rapide : Créer et publier un package (interface CLI dotnet)

La création d’un package NuGet à partir d’une bibliothèque de classes .NET est un processus simple, de même que sa publication sur nuget.org avec l’interface de ligne de commande (CLI) `dotnet`.

## <a name="prerequisites"></a>Prérequis

1. Installez le [Kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/download/), qui comprend l’interface CLI `dotnet`.

1. [Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte. La création d’un compte envoie un e-mail de confirmation. Vous devez confirmer le compte avant de pouvoir charger un package.

## <a name="create-a-class-library-project"></a>Créer un projet de bibliothèque de classes

Vous pouvez utiliser un projet de bibliothèque de classes .NET existant pour le code à empaqueter, ou bien en créer un de la façon suivante :

1. Créez un dossier nommé `AppLogger` et ouvrez-le.

1. Créez le projet à l’aide de la commande `dotnet new classlib`, qui donne le nom du dossier actif au projet.

## <a name="add-package-metadata-to-the-project-file"></a>Ajouter des métadonnées de package au fichier projet

Chaque package NuGet a besoin d’un manifeste décrivant son contenu et ses dépendances. Dans un package final, il s’agit d’un fichier `.nuspec` généré à partir des propriétés de métadonnées NuGet incluses dans le fichier projet.

1. Ouvrez votre fichier projet (`.csproj`) et ajoutez les propriétés minimales suivantes à l’intérieur de la balise `<PropertyGroup>` existante, en adaptant les valeurs :

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Donnez au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez. Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).

1. Ajoutez si vous le souhaitez certaines des propriétés facultatives décrites dans [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.

## <a name="run-the-pack-command"></a>Exécuter la commande pack

Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `dotnet pack`, qui génère également le projet automatiquement :

```cli
# Uses the project file in the current folder by default
dotnet pack
```

La sortie affiche le chemin d’accès du fichier `.nupkg` :

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Générer automatiquement le package à la création

Pour exécuter automatiquement `dotnet pack` pendant l’exécution de `dotnet build`, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publier le package

Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de la commande `dotnet nuget push`, avec une clé API acquise sur nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Obtenir une clé API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publier avec dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Erreurs de publication

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gérer le package publié

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Rubriques connexes

- [Créer un package](../create-packages/creating-a-package.md)
- [Publier un package](../create-packages/publish-a-package.md)
- [Packages de préversion](../create-packages/Prerelease-Packages.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md)
- [Gestion des versions de package](../reference/package-versioning.md)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
- [Signature de packages](../create-packages/Sign-a-package.md)
