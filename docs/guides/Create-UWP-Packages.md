---
title: Créer des packages NuGet pour la plateforme Windows universelle
description: Procédure pas à pas de bout en bout pour créer des packages NuGet à l’aide d’un composant Windows Runtime pour la plateforme Windows universelle.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380765"
---
# <a name="create-uwp-packages"></a>Créer des packages UWP

La [plateforme Windows universelle (UWP)](https://developer.microsoft.com/windows) fournit une plateforme d’application commune pour chaque appareil qui exécute Windows 10. Dans ce modèle, les applications UWP peuvent appeler à la fois les API WinRT communes à tous les appareils et les API (notamment Win32 et .NET) propres à la famille d’appareils sur laquelle les applications s’exécutent.

Dans cette procédure pas à pas, vous créez un package NuGet avec un composant UWP natif (y compris un contrôle XAML) qui peut être utilisé dans les projets natifs et managés.

## <a name="prerequisites"></a>Prérequis

1. Visual Studio 2017 ou Visual Studio 2015. Installez l’édition Community 2017 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; vous pouvez également utiliser les éditions Professional et Enterprise.

1. Interface de ligne de commande NuGet. Téléchargez la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix (le téléchargement est directement le `.exe`). Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.

## <a name="create-a-uwp-windows-runtime-component"></a>Créer un composant Windows Runtime UWP

1. Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C++ > Windows > Universel**, sélectionnez le modèle **Composant Windows Runtime (Windows universel)** , changez le nom en ImageEnhancer, puis cliquez sur OK. À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.

    ![Création d’un projet de composant Windows Runtime UWP](media/UWP-NewProject.png)

1. Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, sélectionnez **Ajouter > Nouvel élément**, cliquez sur le nœud **Visual C++ > XAML**, sélectionnez **Contrôle basé sur un modèle**, changez le nom en AwesomeImageControl.cpp, puis cliquez sur **Ajouter** :

    ![Ajout d’un nouvel élément Contrôle basé sur un modèle XAML au projet](media/UWP-NewXAMLControl.png)

1. Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez Propriétés. Dans la page Propriétés, développez **Propriétés de configuration > C/C++** , puis cliquez sur **Fichiers de sortie**. Dans le volet droit, définissez **Génération de fichiers de documentation XML** sur Oui :

    ![Définition de Génération de fichiers de documentation XML sur Oui](media/UWP-GenerateXMLDocFiles.png)

1. À présent, cliquez avec le bouton droit sur la *solution*, sélectionnez **Générer en tâche de fond**, cochez les trois cases Debug dans la boîte de dialogue, comme illustré ci-dessous. Ainsi, quand vous effectuez une génération, vous générez un jeu complet d’artefacts pour chacun des systèmes cibles que Windows prend en charge.

    ![Générer en tâche de fond](media/UWP-BatchBuild.png)

1. Dans la boîte de dialogue Générer en tâche de fond, cliquez sur **Générer** pour vérifier le projet et créer les fichiers de sortie dont vous avez besoin pour le package NuGet.

> [!Note]
> Dans cette procédure pas à pas, vous utilisez les artefacts de débogage pour le package. Pour un package sans débogage, cochez plutôt les options Release dans la boîte de dialogue Générer en tâche de fond et consultez les dossiers Release résultants dans les étapes qui suivent.

## <a name="create-and-update-the-nuspec-file"></a>Créer et mettre à jour le fichier .nuspec

Pour créer le fichier `.nuspec` initial, effectuez les trois étapes ci-dessous. Les sections qui suivent vous guident tout au long des autres mises à jour nécessaires.

1. Ouvrez une invite de commandes et accédez au dossier contenant `ImageEnhancer.vcxproj` (il s’agit d’un sous-dossier situé en dessous du fichier solution).
1. Exécutez la commande NuGet `spec` pour générer `ImageEnhancer.nuspec` (le nom du fichier est tiré du nom du fichier `.vcxproj`) :

    ```cli
    nuget spec
    ```

1. Ouvrez `ImageEnhancer.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée. La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Pour les packages générés en vue d’une consommation publique, faites particulièrement attention à l’élément `<tags>`, car ces balises aident l’utilisateur à trouver votre package et à comprendre ce qu’il fait.

### <a name="adding-windows-metadata-to-the-package"></a>Ajout de métadonnées Windows au package

Un composant Windows Runtime nécessite des métadonnées qui décrivent tous ses types disponibles publiquement ; ainsi, les autres applications et bibliothèques peuvent le consommer. Ces métadonnées sont contenues dans un fichier .winmd, qui est créé quand vous compilez le projet et doit être inclus dans le package NuGet. Un fichier XML avec des données IntelliSense est également généré en même temps et doit aussi être inclus.

Ajoutez le nœud `<files>` suivant au fichier `.nuspec` :

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Ajout de contenu XAML

Pour inclure un contrôle XAML dans votre composant, vous devez ajouter le fichier XAML qui possède le modèle par défaut pour le contrôle (tel que généré par le modèle de projet). Vous devez insérer la référence à ce fichier dans la section `<files>` :

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Ajout des bibliothèques d’implémentation native

Au sein de votre composant, la logique principale du type ImageEnhancer est en code natif, qui est inclus dans les différents assemblys `ImageEnhancer.dll` générés pour chaque runtime cible (ARM, x86 et x64). Pour inclure ces assemblys dans le package, référencez-les dans la section `<files>`, ainsi que leurs fichiers de ressources .pri associés :

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Ajout d’un fichier .targets

Ensuite, les projets C++ et JavaScript susceptibles de consommer votre package NuGet ont besoin d’un fichier .targets pour identifier les fichiers winmd et d’assembly nécessaires. (Les projets C# et Visual Basic effectuent cette opération automatiquement.) Créez ce fichier en copiant le texte ci-dessous dans `ImageEnhancer.targets` et enregistrez-le dans le même dossier que le fichier `.nuspec`. _Remarque_ : Ce fichier `.targets` doit avoir le même nom que l’ID de package (par exemple, l’élément `<Id>` du fichier `.nupspec`) :

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Ensuite, faites référence à `ImageEnhancer.targets` dans votre fichier `.nuspec` :

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Fichier .nuspec final

Votre fichier `.nuspec` final doit maintenant ressembler au code ci-après, où vous devez là aussi remplacer YOUR_NAME par une valeur appropriée :

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Empaqueter le composant

Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :

```cli
nuget pack ImageEnhancer.nuspec
```

Cette opération génère `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :

![NuGet Package Explorer affichant le package ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un fichier `.nupkg` est simplement un fichier zip avec une extension différente. Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.

Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Rubriques connexes

- [Informations de référence sur le fichier nuspec](../reference/nuspec.md)
- [Packages de symboles](../create-packages/symbol-packages-snupkg.md)
- [Gestion de version des packages](../concepts/package-versioning.md)
- [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)
