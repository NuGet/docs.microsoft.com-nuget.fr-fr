---
title: Créer des packages NuGet pour la plateforme Windows universelle
description: Procédure pas à pas de bout en bout de la création de packages NuGet à l’aide d’un C#composant Windows Runtime pour le plateforme Windows universelle dans.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231804"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="d34ca-103">Créer des packages UWPC#()</span><span class="sxs-lookup"><span data-stu-id="d34ca-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="d34ca-104">La [plateforme Windows universelle (UWP)](/windows/uwp) fournit une plateforme d’application commune pour chaque appareil qui exécute Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d34ca-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="d34ca-105">Dans ce modèle, les applications UWP peuvent appeler à la fois les API WinRT communes à tous les appareils et les API (notamment Win32 et .NET) propres à la famille d’appareils sur laquelle les applications s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="d34ca-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="d34ca-106">Dans cette procédure pas à pas, vous allez créer C# un package NuGet avec un composant UWP (y compris un contrôle XAML) qui peut être utilisé dans les projets managés et natifs.</span><span class="sxs-lookup"><span data-stu-id="d34ca-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d34ca-107">Conditions préalables requises</span><span class="sxs-lookup"><span data-stu-id="d34ca-107">Prerequisites</span></span>

1. <span data-ttu-id="d34ca-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="d34ca-108">Visual Studio 2019.</span></span> <span data-ttu-id="d34ca-109">Installez gratuitement l’édition Community de 2019 à partir de [VisualStudio.com](https://www.visualstudio.com/). vous pouvez également utiliser les éditions Professional et Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d34ca-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="d34ca-110">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="d34ca-110">NuGet CLI.</span></span> <span data-ttu-id="d34ca-111">Téléchargez la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix (le téléchargement est directement le `.exe`).</span><span class="sxs-lookup"><span data-stu-id="d34ca-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="d34ca-112">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="d34ca-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="d34ca-113">[Détails supplémentaires](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="d34ca-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="d34ca-114">Créer un composant Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="d34ca-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="d34ca-115">Dans Visual Studio, choisissez **fichier > nouveau projet de >**, recherchez « UWP c# », sélectionnez le modèle **Windows Runtime composant (Windows universel)** , cliquez sur suivant, changez le nom en ImageEnhancer, puis cliquez sur créer.</span><span class="sxs-lookup"><span data-stu-id="d34ca-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="d34ca-116">À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.</span><span class="sxs-lookup"><span data-stu-id="d34ca-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Création d’un projet de composant Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="d34ca-118">Cliquez avec le bouton droit sur le projet dans Explorateur de solutions, sélectionnez **ajouter > nouvel élément**, sélectionnez **contrôle basé**sur un modèle, changez le nom en AwesomeImageControl.cs, puis cliquez sur **Ajouter**:</span><span class="sxs-lookup"><span data-stu-id="d34ca-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Ajout d’un nouvel élément Contrôle basé sur un modèle XAML au projet](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="d34ca-120">Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez {3}Propriétés{4}.</span><span class="sxs-lookup"><span data-stu-id="d34ca-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="d34ca-121">Dans la page Propriétés, choisissez l’onglet **générer** et activez **fichier de documentation XML**:</span><span class="sxs-lookup"><span data-stu-id="d34ca-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Définition de Génération de fichiers de documentation XML sur Oui](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="d34ca-123">Cliquez avec le bouton droit sur la *solution* maintenant, sélectionnez **génération de lot**, cochez les cinq zones Build dans la boîte de dialogue, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d34ca-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="d34ca-124">Ainsi, quand vous effectuez une génération, vous générez un jeu complet d’artefacts pour chacun des systèmes cibles que Windows prend en charge.</span><span class="sxs-lookup"><span data-stu-id="d34ca-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Générer en tâche de fond](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="d34ca-126">Dans la boîte de dialogue Générer en tâche de fond, cliquez sur **Générer** pour vérifier le projet et créer les fichiers de sortie dont vous avez besoin pour le package NuGet.</span><span class="sxs-lookup"><span data-stu-id="d34ca-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="d34ca-127">Dans cette procédure pas à pas, vous utilisez les artefacts de débogage pour le package.</span><span class="sxs-lookup"><span data-stu-id="d34ca-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="d34ca-128">Pour un package sans débogage, cochez plutôt les options Release dans la boîte de dialogue Générer en tâche de fond et consultez les dossiers Release résultants dans les étapes qui suivent.</span><span class="sxs-lookup"><span data-stu-id="d34ca-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="d34ca-129">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="d34ca-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="d34ca-130">Pour créer le fichier `.nuspec` initial, effectuez les trois étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d34ca-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="d34ca-131">Les sections qui suivent vous guident tout au long des autres mises à jour nécessaires.</span><span class="sxs-lookup"><span data-stu-id="d34ca-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="d34ca-132">Ouvrez une invite de commandes et accédez au dossier contenant `ImageEnhancer.csproj` (il s’agit d’un sous-dossier situé en dessous du fichier solution).</span><span class="sxs-lookup"><span data-stu-id="d34ca-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="d34ca-133">Exécutez la commande [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) pour générer `ImageEnhancer.nuspec` (le nom du fichier est extrait du nom du fichier `.csroj`) :</span><span class="sxs-lookup"><span data-stu-id="d34ca-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="d34ca-134">Ouvrez `ImageEnhancer.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="d34ca-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="d34ca-135">Ne laissez aucune des valeurs de $propertyName $.</span><span class="sxs-lookup"><span data-stu-id="d34ca-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="d34ca-136">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="d34ca-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="d34ca-137">Veillez également à mettre à jour les balises authors et description afin de ne pas recevoir de message d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="d34ca-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="d34ca-138">Pour les packages générés en vue d’une consommation publique, faites particulièrement attention à l’élément `<tags>`, car ces balises aident l’utilisateur à trouver votre package et à comprendre ce qu’il fait.</span><span class="sxs-lookup"><span data-stu-id="d34ca-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="d34ca-139">Ajout de métadonnées Windows au package</span><span class="sxs-lookup"><span data-stu-id="d34ca-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="d34ca-140">Un composant Windows Runtime nécessite des métadonnées qui décrivent tous ses types disponibles publiquement ; ainsi, les autres applications et bibliothèques peuvent le consommer.</span><span class="sxs-lookup"><span data-stu-id="d34ca-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="d34ca-141">Ces métadonnées sont contenues dans un fichier .winmd, qui est créé quand vous compilez le projet et doit être inclus dans le package NuGet.</span><span class="sxs-lookup"><span data-stu-id="d34ca-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="d34ca-142">Un fichier XML avec des données IntelliSense est également généré en même temps et doit aussi être inclus.</span><span class="sxs-lookup"><span data-stu-id="d34ca-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="d34ca-143">Ajoutez le nœud `<files>` suivant au fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="d34ca-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="d34ca-144">Ajout de contenu XAML</span><span class="sxs-lookup"><span data-stu-id="d34ca-144">Adding XAML content</span></span>

<span data-ttu-id="d34ca-145">Pour inclure un contrôle XAML dans votre composant, vous devez ajouter le fichier XAML qui possède le modèle par défaut pour le contrôle (tel que généré par le modèle de projet).</span><span class="sxs-lookup"><span data-stu-id="d34ca-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="d34ca-146">Vous devez insérer la référence à ce fichier dans la section `<files>` :</span><span class="sxs-lookup"><span data-stu-id="d34ca-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="d34ca-147">Ajout des bibliothèques d’implémentation native</span><span class="sxs-lookup"><span data-stu-id="d34ca-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="d34ca-148">Au sein de votre composant, la logique principale du type ImageEnhancer est en code natif, qui est contenue dans les différents assemblys `ImageEnhancer.winmd` générés pour chaque Runtime cible (ARM, ARM64, x86 et x64).</span><span class="sxs-lookup"><span data-stu-id="d34ca-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="d34ca-149">Pour inclure ces assemblys dans le package, référencez-les dans la section `<files>`, ainsi que leurs fichiers de ressources .pri associés :</span><span class="sxs-lookup"><span data-stu-id="d34ca-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="d34ca-150">Fichier .nuspec final</span><span class="sxs-lookup"><span data-stu-id="d34ca-150">Final .nuspec</span></span>

<span data-ttu-id="d34ca-151">Votre fichier `.nuspec` final doit maintenant ressembler au code ci-après, où vous devez là aussi remplacer YOUR_NAME par une valeur appropriée :</span><span class="sxs-lookup"><span data-stu-id="d34ca-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="d34ca-152">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="d34ca-152">Package the component</span></span>

<span data-ttu-id="d34ca-153">Une fois l' `.nuspec` terminée référençant tous les fichiers que vous devez inclure dans le package, vous êtes prêt à exécuter la commande [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) :</span><span class="sxs-lookup"><span data-stu-id="d34ca-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="d34ca-154">Cette opération génère `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d34ca-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="d34ca-155">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="d34ca-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer affichant le package ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d34ca-157">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="d34ca-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d34ca-158">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d34ca-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="d34ca-159">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d34ca-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="d34ca-160">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="d34ca-160">Related topics</span></span>

- [<span data-ttu-id="d34ca-161">Informations de référence sur le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="d34ca-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="d34ca-162">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="d34ca-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="d34ca-163">Gestion de version des packages</span><span class="sxs-lookup"><span data-stu-id="d34ca-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="d34ca-164">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d34ca-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d34ca-165">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="d34ca-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="d34ca-166">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="d34ca-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
