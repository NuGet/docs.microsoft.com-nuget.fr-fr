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
# <a name="create-uwp-packages"></a><span data-ttu-id="c4578-103">Créer des packages UWP</span><span class="sxs-lookup"><span data-stu-id="c4578-103">Create UWP packages</span></span>

<span data-ttu-id="c4578-104">La [plateforme Windows universelle (UWP)](https://developer.microsoft.com/windows) fournit une plateforme d’application commune pour chaque appareil qui exécute Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c4578-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="c4578-105">Dans ce modèle, les applications UWP peuvent appeler à la fois les API WinRT communes à tous les appareils et les API (notamment Win32 et .NET) propres à la famille d’appareils sur laquelle les applications s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="c4578-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="c4578-106">Dans cette procédure pas à pas, vous créez un package NuGet avec un composant UWP natif (y compris un contrôle XAML) qui peut être utilisé dans les projets natifs et managés.</span><span class="sxs-lookup"><span data-stu-id="c4578-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4578-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c4578-107">Prerequisites</span></span>

1. <span data-ttu-id="c4578-108">Visual Studio 2017 ou Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c4578-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="c4578-109">Installez l’édition Community 2017 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; vous pouvez également utiliser les éditions Professional et Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c4578-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="c4578-110">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4578-110">NuGet CLI.</span></span> <span data-ttu-id="c4578-111">Téléchargez la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix (le téléchargement est directement le `.exe`).</span><span class="sxs-lookup"><span data-stu-id="c4578-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="c4578-112">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="c4578-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="c4578-113">Créer un composant Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="c4578-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="c4578-114">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C++ > Windows > Universel**, sélectionnez le modèle **Composant Windows Runtime (Windows universel)** , changez le nom en ImageEnhancer, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="c4578-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="c4578-115">À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.</span><span class="sxs-lookup"><span data-stu-id="c4578-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Création d’un projet de composant Windows Runtime UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="c4578-117">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, sélectionnez **Ajouter > Nouvel élément**, cliquez sur le nœud **Visual C++ > XAML**, sélectionnez **Contrôle basé sur un modèle**, changez le nom en AwesomeImageControl.cpp, puis cliquez sur **Ajouter** :</span><span class="sxs-lookup"><span data-stu-id="c4578-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Ajout d’un nouvel élément Contrôle basé sur un modèle XAML au projet](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="c4578-119">Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez Propriétés.</span><span class="sxs-lookup"><span data-stu-id="c4578-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="c4578-120">Dans la page Propriétés, développez **Propriétés de configuration > C/C++** , puis cliquez sur **Fichiers de sortie**.</span><span class="sxs-lookup"><span data-stu-id="c4578-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="c4578-121">Dans le volet droit, définissez **Génération de fichiers de documentation XML** sur Oui :</span><span class="sxs-lookup"><span data-stu-id="c4578-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Définition de Génération de fichiers de documentation XML sur Oui](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="c4578-123">À présent, cliquez avec le bouton droit sur la *solution*, sélectionnez **Générer en tâche de fond**, cochez les trois cases Debug dans la boîte de dialogue, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c4578-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="c4578-124">Ainsi, quand vous effectuez une génération, vous générez un jeu complet d’artefacts pour chacun des systèmes cibles que Windows prend en charge.</span><span class="sxs-lookup"><span data-stu-id="c4578-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Générer en tâche de fond](media/UWP-BatchBuild.png)

1. <span data-ttu-id="c4578-126">Dans la boîte de dialogue Générer en tâche de fond, cliquez sur **Générer** pour vérifier le projet et créer les fichiers de sortie dont vous avez besoin pour le package NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4578-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="c4578-127">Dans cette procédure pas à pas, vous utilisez les artefacts de débogage pour le package.</span><span class="sxs-lookup"><span data-stu-id="c4578-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="c4578-128">Pour un package sans débogage, cochez plutôt les options Release dans la boîte de dialogue Générer en tâche de fond et consultez les dossiers Release résultants dans les étapes qui suivent.</span><span class="sxs-lookup"><span data-stu-id="c4578-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="c4578-129">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="c4578-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="c4578-130">Pour créer le fichier `.nuspec` initial, effectuez les trois étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c4578-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="c4578-131">Les sections qui suivent vous guident tout au long des autres mises à jour nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c4578-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="c4578-132">Ouvrez une invite de commandes et accédez au dossier contenant `ImageEnhancer.vcxproj` (il s’agit d’un sous-dossier situé en dessous du fichier solution).</span><span class="sxs-lookup"><span data-stu-id="c4578-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="c4578-133">Exécutez la commande NuGet `spec` pour générer `ImageEnhancer.nuspec` (le nom du fichier est tiré du nom du fichier `.vcxproj`) :</span><span class="sxs-lookup"><span data-stu-id="c4578-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="c4578-134">Ouvrez `ImageEnhancer.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="c4578-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="c4578-135">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="c4578-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="c4578-136">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="c4578-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="c4578-137">Pour les packages générés en vue d’une consommation publique, faites particulièrement attention à l’élément `<tags>`, car ces balises aident l’utilisateur à trouver votre package et à comprendre ce qu’il fait.</span><span class="sxs-lookup"><span data-stu-id="c4578-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="c4578-138">Ajout de métadonnées Windows au package</span><span class="sxs-lookup"><span data-stu-id="c4578-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="c4578-139">Un composant Windows Runtime nécessite des métadonnées qui décrivent tous ses types disponibles publiquement ; ainsi, les autres applications et bibliothèques peuvent le consommer.</span><span class="sxs-lookup"><span data-stu-id="c4578-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="c4578-140">Ces métadonnées sont contenues dans un fichier .winmd, qui est créé quand vous compilez le projet et doit être inclus dans le package NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4578-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="c4578-141">Un fichier XML avec des données IntelliSense est également généré en même temps et doit aussi être inclus.</span><span class="sxs-lookup"><span data-stu-id="c4578-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="c4578-142">Ajoutez le nœud `<files>` suivant au fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="c4578-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="c4578-143">Ajout de contenu XAML</span><span class="sxs-lookup"><span data-stu-id="c4578-143">Adding XAML content</span></span>

<span data-ttu-id="c4578-144">Pour inclure un contrôle XAML dans votre composant, vous devez ajouter le fichier XAML qui possède le modèle par défaut pour le contrôle (tel que généré par le modèle de projet).</span><span class="sxs-lookup"><span data-stu-id="c4578-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="c4578-145">Vous devez insérer la référence à ce fichier dans la section `<files>` :</span><span class="sxs-lookup"><span data-stu-id="c4578-145">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="c4578-146">Ajout des bibliothèques d’implémentation native</span><span class="sxs-lookup"><span data-stu-id="c4578-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="c4578-147">Au sein de votre composant, la logique principale du type ImageEnhancer est en code natif, qui est inclus dans les différents assemblys `ImageEnhancer.dll` générés pour chaque runtime cible (ARM, x86 et x64).</span><span class="sxs-lookup"><span data-stu-id="c4578-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="c4578-148">Pour inclure ces assemblys dans le package, référencez-les dans la section `<files>`, ainsi que leurs fichiers de ressources .pri associés :</span><span class="sxs-lookup"><span data-stu-id="c4578-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="adding-targets"></a><span data-ttu-id="c4578-149">Ajout d’un fichier .targets</span><span class="sxs-lookup"><span data-stu-id="c4578-149">Adding .targets</span></span>

<span data-ttu-id="c4578-150">Ensuite, les projets C++ et JavaScript susceptibles de consommer votre package NuGet ont besoin d’un fichier .targets pour identifier les fichiers winmd et d’assembly nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c4578-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="c4578-151">(Les projets C# et Visual Basic effectuent cette opération automatiquement.) Créez ce fichier en copiant le texte ci-dessous dans `ImageEnhancer.targets` et enregistrez-le dans le même dossier que le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c4578-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="c4578-152">_Remarque_ : Ce fichier `.targets` doit avoir le même nom que l’ID de package (par exemple, l’élément `<Id>` du fichier `.nupspec`) :</span><span class="sxs-lookup"><span data-stu-id="c4578-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="c4578-153">Ensuite, faites référence à `ImageEnhancer.targets` dans votre fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="c4578-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="c4578-154">Fichier .nuspec final</span><span class="sxs-lookup"><span data-stu-id="c4578-154">Final .nuspec</span></span>

<span data-ttu-id="c4578-155">Votre fichier `.nuspec` final doit maintenant ressembler au code ci-après, où vous devez là aussi remplacer YOUR_NAME par une valeur appropriée :</span><span class="sxs-lookup"><span data-stu-id="c4578-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="c4578-156">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="c4578-156">Package the component</span></span>

<span data-ttu-id="c4578-157">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="c4578-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="c4578-158">Cette opération génère `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="c4578-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="c4578-159">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="c4578-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer affichant le package ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="c4578-161">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="c4578-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="c4578-162">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c4578-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="c4578-163">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c4578-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="c4578-164">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="c4578-164">Related topics</span></span>

- [<span data-ttu-id="c4578-165">Informations de référence sur le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="c4578-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="c4578-166">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="c4578-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="c4578-167">Gestion de version des packages</span><span class="sxs-lookup"><span data-stu-id="c4578-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="c4578-168">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c4578-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c4578-169">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="c4578-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="c4578-170">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="c4578-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
