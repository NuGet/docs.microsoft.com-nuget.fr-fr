---
title: Créer des packages NuGet pour la plateforme Windows universelle
description: Une procédure pas à pas de bout en bout de la création de paquets NuGet à l’aide d’un composant Windows Runtime pour la plate-forme Windows universelle en C.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231804"
---
# <a name="create-uwp-packages-c"></a>Créer des forfaits UWP (C)

La [plateforme Windows universelle (UWP)](/windows/uwp) fournit une plateforme d’application commune pour chaque appareil qui exécute Windows 10. Dans ce modèle, les applications UWP peuvent appeler à la fois les API WinRT communes à tous les appareils et les API (notamment Win32 et .NET) propres à la famille d’appareils sur laquelle les applications s’exécutent.

Dans ce cadre pas à pas, vous créez un package NuGet avec un composant C’UWP (y compris un contrôle XAML) qui peut être utilisé dans des projets gérés et autochtones.

## <a name="prerequisites"></a>Prérequis

1. Visual Studio 2019. Installer l’édition communautaire 2019 gratuitement de [visualstudio.com](https://www.visualstudio.com/); vous pouvez également utiliser les éditions Professionnels et Entreprises.

1. Interface de ligne de commande NuGet. Téléchargez la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix (le téléchargement est directement le `.exe`). Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait. [Plus de détails](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Créer un composant Windows Runtime UWP

1. Dans Visual Studio, choisissez **File > New > Project**, recherchez le modèle «uwp cô », sélectionnez le modèle de composant Windows **Runtime (Windows universel),** cliquez ensuite, changez le nom en ImageEnhancer et cliquez sur Créer. À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.

    ![Création d’un projet de composant Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. Cliquez à droite sur le projet dans Solution Explorer, **sélectionnez Ajouter > nouvel élément**, sélectionnez **Templated Control**, changez le nom pour AwesomeImageControl.cs et cliquez sur **Ajouter**:

    ![Ajout d’un nouvel élément Contrôle basé sur un modèle XAML au projet](media/UWP-NewXAMLControl-CS.png)

1. Cliquez à droite sur le projet dans Solution Explorer et sélectionnez **propriétés.** Dans la page Propriétés, choisissez **l’onglet Construire** et activez **le fichier de documentation XML**:

    ![Définition de Génération de fichiers de documentation XML sur Oui](media/UWP-GenerateXMLDocFiles-CS.png)

1. Cliquez à droite sur la *solution* maintenant, sélectionnez **Batch Build**, vérifiez les cinq cases de construction dans le dialogue comme indiqué ci-dessous. Ainsi, quand vous effectuez une génération, vous générez un jeu complet d’artefacts pour chacun des systèmes cibles que Windows prend en charge.

    ![Générer en tâche de fond](media/UWP-BatchBuild-CS.png)

1. Dans la boîte de dialogue Générer en tâche de fond, cliquez sur **Générer** pour vérifier le projet et créer les fichiers de sortie dont vous avez besoin pour le package NuGet.

> [!Note]
> Dans cette procédure pas à pas, vous utilisez les artefacts de débogage pour le package. Pour un package sans débogage, cochez plutôt les options Release dans la boîte de dialogue Générer en tâche de fond et consultez les dossiers Release résultants dans les étapes qui suivent.

## <a name="create-and-update-the-nuspec-file"></a>Créer et mettre à jour le fichier .nuspec

Pour créer le fichier `.nuspec` initial, effectuez les trois étapes ci-dessous. Les sections qui suivent vous guident tout au long des autres mises à jour nécessaires.

1. Ouvrez une invite de commandes et accédez au dossier contenant `ImageEnhancer.csproj` (il s’agit d’un sous-dossier situé en dessous du fichier solution).
1. Exécuter [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) la commande `ImageEnhancer.nuspec` pour générer (le nom du fichier `.csroj` est pris à partir du nom du fichier):

    ```cli
    nuget spec
    ```

1. Ouvrez `ImageEnhancer.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée. Ne laissez aucune des valeurs $propertyName$. La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.

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

Dans votre composant, la logique de base du type ImageEnhancer est `ImageEnhancer.winmd` en code natif, qui est contenu dans les différents assemblages qui sont générés pour chaque temps d’exécution cible (ARM, ARM64, x86, et x64). Pour inclure ces assemblys dans le package, référencez-les dans la section `<files>`, ainsi que leurs fichiers de ressources .pri associés :

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

Avec le `.nuspec` référencement terminé de tous les fichiers que vous devez [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) inclure dans le paquet, vous êtes prêt à exécuter la commande :

```cli
nuget pack ImageEnhancer.nuspec
```

Cette opération génère `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et que vous développez tous les nœuds, le contenu suivant apparaît :

![NuGet Package Explorer affichant le package ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un fichier `.nupkg` est simplement un fichier zip avec une extension différente. Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.

Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Rubriques connexes

- [.nuspec Référence](../reference/nuspec.md)
- [Packages de symboles](../create-packages/symbol-packages-snupkg.md)
- [Contrôle de version des packages](../concepts/package-versioning.md)
- [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Création de forfaits localisés](../create-packages/creating-localized-packages.md)
