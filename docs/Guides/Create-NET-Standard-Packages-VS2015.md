---
title: "Créer des packages NuGet .NET Standard avec Visual Studio 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard à l’aide de NuGet 3.x et Visual Studio 2015."
keywords: "créer un package, packages .NET Standard, table de mappage .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Créer des packages .NET Standard avec Visual Studio 2015

*S’applique à NuGet 3.x. Consultez [Créer des packages .NET Standard avec Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) si vous envisagez d’utiliser NuGet 4.x+.*

La [bibliothèque .NET Standard](/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET. La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail. Elle permet aux développeurs de produire des bibliothèques de classes portables qui sont utilisables à travers tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.

Ce guide vous explique comment créer un package nuget ciblant .NET Standard Library 1.4. Cette opération fonctionne sur .NET Framework 4.6.1, la plateforme Windows universelle 10, .NET Core et Mono/Xamarin. Pour plus d’informations, consultez la [table de mappage .NET Standard](#net-standard-mapping-table) plus loin dans cette rubrique.

1. [Prérequis](#pre-requisites)
1. [Créer le projet de bibliothèque de classes](#create-the-class-library-project)
1. [Créer et mettre à jour le fichier .nuspec](#create-and-update-the-nuspec-file)
1. [Empaqueter le composant](#package-the-component)
1. [Options supplémentaires](#additional-options)
1. [Table de mappage .NET Standard](#net-standard-mapping-table)
1. [Rubriques connexes](#related-topics)


## <a name="pre-requisites"></a>Conditions préalables

1. Visual Studio 2015. Installez l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; bien entendu, vous pouvez également utiliser les éditions Professional et Enterprise.
1. .NET Core : installez .NET Core, ainsi que des modèles et autres outils pour Visual Studio 2015 à partir de [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
1. Interface de ligne de commande NuGet. Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix. Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.

> [!Note]
> nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.



## <a name="create-the-class-library-project"></a>Créer le projet de bibliothèque de classes

1. Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez **Bibliothèque de classes (Portable)**, changez le nom en AppLogger et cliquez sur OK.

    ![Créer un projet de bibliothèque de classes](media/NetStandard-NewProject.png)

1. Dans la boîte de dialogue **Ajouter une bibliothèque de classes portable** qui s’affiche, sélectionnez les options `.NET Framework 4.6` et `ASP.NET Core 1.0`.
1. Cliquez avec le bouton droit sur `AppLogger (Portable)` dans l’Explorateur de solutions, sélectionnez **Propriétés**, sélectionnez l’onglet **Bibliothèque**, puis cliquez sur **Cibler .NET Platform Standard** dans la section **Ciblage**. Confirmez l’opération, puis sélectionnez `.NET Standard 1.4` dans la liste déroulante :

    ![Définition de la cible sur .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Cliquez sur l’onglet **Générer**, définissez **Configuration** sur `Release`, puis cochez la case **Fichier de documentation XML**.
1. Ajoutez votre code au composant, par exemple :

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. Générez le projet (avec la configuration Release) et vérifiez que les fichiers DLL et XML sont produits dans le dossier bin\Release.

## <a name="create-and-update-the-nuspec-file"></a>Créer et mettre à jour le fichier .nuspec

1. Ouvrez une invite de commandes, accédez au dossier contenant le dossier `AppLogg.csproj` (un niveau en dessous du fichier `.sln`) et exécutez la commande NuGet `spec` pour créer le fichier `AppLogger.nuspec` initial :

```
nuget spec
```

1. Ouvrez `AppLogger.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée. La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Ajoutez des assemblys de référence au fichier `.nuspec`, concrètement les fichiers DLL et XML IntelliSense de la bibliothèque :

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour générer tous les fichiers du package.


## <a name="package-the-component"></a>Empaqueter le composant

Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :

```
nuget pack AppLogger.nuspec
```

Cette opération génère `AppLogger.YOUR_NAME.1.0.0.nupkg`. Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :

![NuGet Package Explorer affichant le package AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Un fichier `.nupkg` est simplement un fichier zip avec une extension différente. Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.

Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).

Notez que `pack` requiert Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux. Sur un Mac, vous devez également convertir les chemins d’accès Windows dans le fichier `.nuspec` en chemins d’accès de style Unix.

## <a name="additional-options"></a>Options supplémentaires

Les sections suivantes présentent des options supplémentaires pour la création de packages NuGet :

- [Déclaration de dépendances](#declaring-dependencies)
- [Prise en charge de plusieurs frameworks cibles](#supporting-multiple-target-frameworks)
- [Ajout de cibles et de propriétés pour MSBuild](#adding-targets-and-props-for-msbuild)
- [Création de packages localisés](#creating-localized-packages)
- [Ajout d’un fichier readme](#adding-a-readme)

### <a name="declaring-dependencies"></a>Déclaration de dépendances

Si vous avez des dépendances sur d’autres packages NuGet, répertoriez-les dans l’élément `<dependencies>` avec des éléments `<group>`. Par exemple, pour déclarer une dépendance sur NewtonSoft.Json version 8.0.3 ou supérieure, ajoutez le code suivant :

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

La syntaxe de l’attribut *version* indique ici que la version 8.0.3 ou supérieure est acceptable. Pour spécifier des plages de versions différentes, consultez [Gestion de version des packages](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Prise en charge de plusieurs frameworks cibles

Supposons que vous souhaitez tirer parti d’une API dans .NET Framework 4.6.2 qui n’est pas disponible dans .NET Standard 1.4. Pour ce faire, vous devez d’abord vérifier que la bibliothèque se compile pour .NET 4.6.2 à l’aide d’une compilation conditionnelle ou de projets partagés. (Dans Visual Studio, vous pouvez créer un projet NetCore, ajouter le framework de votre choix à la section à frameworks multiples, puis effectuer une génération.) Ensuite, vous créez le package à l’aide de la technique simple de répertoire de travail basé sur une convention comme suit :

1. Dans le dossier racine du projet qui contient votre fichier `.nuspec`, créez un dossier nommé `lib`.
1. Dans `lib`, créez des dossiers pour chaque plateforme que vous souhaitez prendre en charge :

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. Dans le fichier `.nuspec`, ajoutez un nœud `files` sous le nœud `package` et faites référence aux fichiers dans `lib` à l’aide de caractères génériques. **Remarque :** Les remplacements de jeton n’étant pas pris en charge avec l’approche de répertoire de travail basé sur une convention, remplacez-les par des valeurs littérales :

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Créez le package à l’aide de `nuget pack AppLogger.spec`.

Pour plus d’informations sur l’utilisation de cette technique, consultez [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

### <a name="adding-targets-and-props-for-msbuild"></a>Ajout de cibles et de propriétés pour MSBuild

Vous pouvez être amené à ajouter des cibles ou propriétés de build personnalisées dans les projets qui utilisent votre package, comme dans le cas de l’exécution d’un processus ou outil personnalisé pendant la génération. À cette fin, vous ajoutez des fichiers à un dossier `\build`, comme décrit dans les étapes ci-dessous. Quand NuGet installe un package avec des fichiers \build, il ajoute un élément MSBuild au fichier projet pointant vers les fichiers .targets et .props.

> [!Note]
> Quand vous utilisez `project.json`, les cibles ne sont pas ajoutées au projet, mais sont accessibles via `project.lock.json`.


1. Dans le dossier du projet qui contient le fichier `.nuspec`, créez un dossier nommé `build`.
1. Dans `build`, créez des dossiers pour chaque langage pris en charge, puis dans ces derniers, placez vos fichiers `.targets` et `.props` :

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. Dans le fichier `.nuspec`, ajoutez un nœud `files` sous le nœud `package` et faites référence aux fichiers dans `build` à l’aide de caractères génériques.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Créez le package à l’aide de `nuget pack AppLogger.nuspec`.

Pour plus d’informations, reportez-vous à [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).


### <a name="creating-localized-packages"></a>Création de packages localisés

Pour créer des versions localisées de votre bibliothèque, vous pouvez créer des packages distincts pour différents paramètres régionaux, ou inclure des assemblys de ressources localisées dans un package unique. Voici comment effectuer cette dernière approche pour l’allemand et l’italien :

1. Dans chaque dossier de framework cible sous `lib`, créez des dossiers pour chaque langue prise en charge autre que l’anglais (langue par défaut). Dans ces dossiers, vous pouvez placer des assemblys de ressources et des fichiers XML IntelliSense localisés. Exemple :

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. Dans le fichier `.nuspec`, référencez ces fichiers dans le nœud `<files>` :

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Créez le package à l’aide de `nuget pack AppLogger.nuspec`.


### <a name="adding-a-readme"></a>Ajout d’un fichier readme

Quand vous incluez un fichier `readme.txt` dans la racine du package, Visual Studio l’affiche si le package est installé directement.

> [!Note]
> Les fichiers readme ne s’affichent pas pour les packages qui sont installés en tant que dépendance, ou pour les projets .NET Core.


Pour effectuer cette opération, créez votre fichier `readme.txt`, placez-le dans le dossier racine du projet, puis faites-y référence dans le fichier `.nuspec` :

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a>Table de mappage .NET Standard

|Nom de la plateforme |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1,5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Plateformes Mono/Xamarin| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|Plateforme Windows universelle| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>Rubriques connexes

- [Informations de référence sur le fichier nuspec](../schema/nuspec.md)
- [Packages de symboles](../create-packages/symbol-packages.md)
- [Gestion de version des packages](../reference/package-versioning.md)
- [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
- [Documentation de la bibliothèque .NET Standard](/dotnet/articles/standard/library)
- [Portage vers .NET Core à partir du .NET Framework](/dotnet/articles/core/porting/index)
