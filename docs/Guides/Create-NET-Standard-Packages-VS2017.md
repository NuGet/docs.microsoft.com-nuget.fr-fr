---
title: "Créer des packages NuGet .NET Standard 2.0 avec Visual Studio 2017 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard 2.0 à l’aide de NuGet 4.x et Visual Studio 2017."
keywords: "créer un package, packages .NET Standard, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Créer des packages .NET Standard 2.0 avec Visual Studio 2017

*S’applique à NuGet 4.x+ et MSBuild 15.3+ tels que fournis avec Visual Studio 2017 Update 3. Pour les versions antérieures de Visual Studio 2017, ces instructions s’appliquent à .NET Standard versions 1.4 à 1.6 sous réserve de modifier la propriété \<TargetFramework\>. Consultez également [Créer des packages .NET Standard avec Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) si vous envisagez d’utiliser NuGet 3.x+.*

La [bibliothèque .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET. La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail. Elle permet aux développeurs de produire des bibliothèques de classes portables qui sont utilisables à travers tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.

Ce guide vous explique comment créer un package nuget ciblant .NET Standard Library 2.0 avec Visual Studio 2017 Update 3 et NuGet 4.0.

1. [Prérequis](#pre-requisites)
1. [Créer le projet de bibliothèque de classes](#create-the-netstandard-class-library-project)
1. [Modifier les métadonnées dans le fichier .csproj](#edit-metadata-in-the-csproj-file)
1. [Empaqueter le composant](#package-the-component)
1. [Rubriques connexes](#related-topics)

## <a name="pre-requisites"></a>Prérequis

Cette procédure pas à pas nécessite Visual Studio 2017 Update 3 avec la charge de travail **Développement multiplateforme .Net Core**. Vous pouvez installer l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser les éditions Professional et Enterprise.

La charge de travail requise s’affiche comme suit dans le programme d’installation de Visual Studio :

![Charge de travail Développement multiplateforme .Net Core dans le programme d’installation de Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Créer le projet de bibliothèque de classes .NET Standard

1. Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez **Bibliothèque de classes (.NET Standard)**, changez le nom en AppLogger et cliquez sur OK.

    ![Créer un projet de bibliothèque de classes](media/NuGet4-02-NewProject.png)

1. Définissez la configuration de build sur **Release**.
1. Cliquez avec le bouton droit sur le projet `AppLogger` dans l’Explorateur de solutions, sélectionnez **Propriétés**, sélectionnez l’onglet **Générer**, cochez la case **Fichier de documentation XML**, puis définissez le nom de fichier simplement sur `AppLogger.xml`. Ensuite, enregistrez le projet.

1. Ajoutez votre code au composant, à l’image du code suivant (qui se contente d’afficher des messages dans la console) :

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Générez le projet (avec la configuration Release) et vérifiez que les fichiers DLL et XML sont produits dans le dossier `bin\Release\netstandard2.0`.

## <a name="edit-metadata-in-the-csproj-file"></a>Modifier les métadonnées dans le fichier .csproj

Avec les projets NuGet 4.0 et .NET Core, les métadonnées des packages se trouvent directement dans le fichier `.csproj` au lieu de fichiers externes, tels qu’un fichier `.nuspec`. Une description complète de ces métadonnées est disponible dans [Cibles NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md#pack-target).

1. Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, sélectionnez **Modifier AppLogger.csproj**, puis modifiez le premier groupe de propriétés pour inclure les informations de package telles que les suivantes :

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Enregistrez le projet, puis cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour regénérer tous les fichiers du package, cette fois avec les métadonnées correctes.


## <a name="package-the-component"></a>Empaqueter le composant

NuGet 4.0 prend en charge une cible pack à l’aide de MSBuild version 15,1+ (MSBuild 15.3 dans le cadre de Visual Studio 2017 Update 3) quand le projet contient les métadonnées de package nécessaires, ajoutées dans la section précédente. Pour appeler MSBuild de cette manière, spécifiez simplement la cible pack sur la ligne de commande dans le même dossier que le fichier `.csproj` :

    msbuild /t:pack /p:Configuration=Release

Pour d’autres options avec `msbuild /t:pack`, telles que l’inclusion de fichiers de contenu, de symboles et de code source, consultez [Cibles NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md#pack-target).

Dans tous les cas, la commande ci-dessus génère `AppLogger.YOUR_NAME.1.0.0.nupkg` dans le dossier `bin\Release` par défaut, car elle génère cette configuration. Si vous omettez le commutateur `/p`, la configuration par défaut est `Debug`. 

Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :

![NuGet Package Explorer affichant le package AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> Un fichier `.nupkg` est simplement un fichier zip avec une extension différente. Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.

Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Rubriques connexes

- [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md) explique comment décrire votre package directement dans le fichier projet.
- [Cibles NuGet pack et restore en tant que cibles MSBuild](../schema/msbuild-targets.md) décrit toutes les options de création d’un package à l’aide de `msbuild /t:pack`.
- [Documentation de la bibliothèque .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portage vers .NET Core à partir du .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
