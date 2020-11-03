---
title: Créer des packages NuGet pour la plateforme Windows universelle
description: Procédure pas à pas de bout en bout de la création de packages NuGet à l’aide d’un composant Windows Runtime pour le plateforme Windows universelle en C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 6f8037f439d627af158b6d5b7746a633b053e514
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238008"
---
# <a name="create-uwp-packages-c"></a>Créer des packages UWP (C#)

La [plateforme Windows universelle (UWP)](/windows/uwp) fournit une plateforme d’application commune pour chaque appareil qui exécute Windows 10. Dans ce modèle, les applications UWP peuvent appeler à la fois les API WinRT communes à tous les appareils et les API (notamment Win32 et .NET) propres à la famille d’appareils sur laquelle les applications s’exécutent.

Dans cette procédure pas à pas, vous créez un package NuGet avec un composant UWP C# (y compris un contrôle XAML) qui peut être utilisé dans les projets managés et natifs.

## <a name="prerequisites"></a>Prérequis

1. Visual Studio 2019. Installez gratuitement l’édition Community de 2019 à partir de [VisualStudio.com](https://www.visualstudio.com/). vous pouvez également utiliser les éditions Professional et Enterprise.

1. Interface de ligne de commande NuGet. Téléchargez la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix (le téléchargement est directement le `.exe`). Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait. [Plus de détails](../reference/nuget-exe-cli-reference.md#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Créer un composant Windows Runtime UWP

1. Dans Visual Studio, choisissez **fichier > nouveau projet de >** , recherchez « UWP c# », sélectionnez le modèle **Windows Runtime composant (Windows universel)** , cliquez sur suivant, changez le nom en ImageEnhancer, puis cliquez sur créer. À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.

    ![Création d’un projet de composant Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. Cliquez avec le bouton droit sur le projet dans Explorateur de solutions, sélectionnez **ajouter > nouvel élément** , sélectionnez **contrôle basé** sur un modèle, changez le nom en AwesomeImageControl.cs, puis cliquez sur **Ajouter** :

    ![Ajout d’un nouvel élément Contrôle basé sur un modèle XAML au projet](media/UWP-NewXAMLControl-CS.png)

1. Dans Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis sélectionnez **Propriétés.** Dans la page Propriétés, choisissez l’onglet **générer** et activez **fichier de documentation XML** :

    ![Définition de Génération de fichiers de documentation XML sur Oui](media/UWP-GenerateXMLDocFiles-CS.png)

1. Cliquez avec le bouton droit sur la *solution* maintenant, sélectionnez **génération de lot** , cochez les cinq zones Build dans la boîte de dialogue, comme indiqué ci-dessous. Ainsi, quand vous effectuez une génération, vous générez un jeu complet d’artefacts pour chacun des systèmes cibles que Windows prend en charge.

    ![Générer en tâche de fond](media/UWP-BatchBuild-CS.png)

1. Dans la boîte de dialogue Générer en tâche de fond, cliquez sur **Générer** pour vérifier le projet et créer les fichiers de sortie dont vous avez besoin pour le package NuGet.

> [!Note]
> Dans cette procédure pas à pas, vous utilisez les artefacts de débogage pour le package. Pour un package sans débogage, cochez plutôt les options Release dans la boîte de dialogue Générer en tâche de fond et consultez les dossiers Release résultants dans les étapes qui suivent.

## <a name="create-and-update-the-nuspec-file"></a>Créer et mettre à jour le fichier .nuspec

Pour créer le fichier `.nuspec` initial, effectuez les trois étapes ci-dessous. Les sections qui suivent vous guident tout au long des autres mises à jour nécessaires.

1. Ouvrez une invite de commandes et accédez au dossier contenant `ImageEnhancer.csproj` (il s’agit d’un sous-dossier situé en dessous du fichier solution).
1. Exécutez la [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) commande pour générer `ImageEnhancer.nuspec` (le nom du fichier est tiré du nom du `.csroj` fichier) :

    ```cli
    nuget spec
    ```

1. Ouvrez `ImageEnhancer.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée. Ne laissez aucune des valeurs de $propertyName $. La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.

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
        <copyright>Copyright 2020</copyright>
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
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
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

Au sein de votre composant, la logique principale du type ImageEnhancer est en code natif, qui est contenue dans les différents `ImageEnhancer.winmd` assemblys générés pour chaque Runtime cible (ARM, ARM64, x86 et x64). Pour inclure ces assemblys dans le package, référencez-les dans la section `<files>`, ainsi que leurs fichiers de ressources .pri associés :

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Empaqueter le composant

Une fois que vous avez fait `.nuspec` référence à tous les fichiers que vous devez inclure dans le package, vous êtes prêt à exécuter la [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) commande :

```cli
nuget pack ImageEnhancer.nuspec
```

Cette opération génère `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et que vous développez tous les nœuds, le contenu suivant apparaît :

![NuGet Package Explorer affichant le package ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un fichier `.nupkg` est simplement un fichier zip avec une extension différente. Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.

Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Rubriques connexes

- [Référence. NuSpec](../reference/nuspec.md)
- [Packages de symboles](../create-packages/symbol-packages-snupkg.md)
- [Gestion des versions de package](../concepts/package-versioning.md)
- [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Création de packages localisés](../create-packages/creating-localized-packages.md)