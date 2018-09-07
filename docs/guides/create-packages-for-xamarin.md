---
title: Créer des packages NuGet pour Xamarin (pour iOS, Android et Windows) avec Visual Studio 2015
description: Procédure pas à pas de bout en bout montrant comment créer des packages NuGet pour Xamarin qui utilisent des API natives sur iOS, Android et Windows.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: c43f4e80d456214ca354e136db6419a95fc797a0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551906"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="c5457-103">Créer des packages pour Xamarin avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c5457-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="c5457-104">Un package pour Xamarin contient du code qui utilise des API natives sur iOS, Android et Windows, suivant le système d’exploitation du runtime.</span><span class="sxs-lookup"><span data-stu-id="c5457-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="c5457-105">Bien que cela soit simple à faire, il est préférable de permettre aux développeurs d’utiliser le package à partir d’une bibliothèque de classes portable ou de bibliothèques .NET Standard par le biais d’une surface d’exposition d’API communes.</span><span class="sxs-lookup"><span data-stu-id="c5457-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="c5457-106">Dans cette procédure pas à pas, vous allez utiliser Visual Studio 2015 pour créer un package NuGet multiplateforme utilisable dans des projets mobiles sous iOS, sous Android et sous Windows.</span><span class="sxs-lookup"><span data-stu-id="c5457-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="c5457-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c5457-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="c5457-108">Créer la structure du projet et le code d’abstraction</span><span class="sxs-lookup"><span data-stu-id="c5457-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="c5457-109">Écrire du code spécifique de la plateforme</span><span class="sxs-lookup"><span data-stu-id="c5457-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="c5457-110">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="c5457-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="c5457-111">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="c5457-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="c5457-112">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="c5457-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="c5457-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c5457-113">Prerequisites</span></span>

1. <span data-ttu-id="c5457-114">Visual Studio 2015 avec la plateforme Windows universelle (UWP) et Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c5457-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="c5457-115">Installez l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; bien entendu, vous pouvez également utiliser les éditions Professional et Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c5457-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="c5457-116">Pour inclure les outils Xamarin et UWP, sélectionnez une installation personnalisée et cochez les options appropriées.</span><span class="sxs-lookup"><span data-stu-id="c5457-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="c5457-117">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5457-117">NuGet CLI.</span></span> <span data-ttu-id="c5457-118">Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="c5457-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="c5457-119">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="c5457-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="c5457-120">nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="c5457-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="c5457-121">Créer la structure du projet et le code d’abstraction</span><span class="sxs-lookup"><span data-stu-id="c5457-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="c5457-122">Téléchargez et exécutez le [plug-in de l’extension des modèles Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5457-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="c5457-123">Ces modèles facilitent la création de la structure de projet nécessaire pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="c5457-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="c5457-124">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, recherchez `Plugin`, sélectionnez le modèle **Plug-in pour Xamarin**, changez le nom en LoggingLibrary et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="c5457-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nouveau projet Application vide (Xamarin.Forms Portable) dans Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="c5457-126">La solution résultante contient deux projets de bibliothèque de classes portable, ainsi que divers projets propres à la plateforme :</span><span class="sxs-lookup"><span data-stu-id="c5457-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="c5457-127">La bibliothèque de classes portable nommée `Plugin.LoggingLibrary.Abstractions (Portable)` définit l’interface publique (surface d’exposition des API) du composant, en l’occurrence l’interface `ILoggingLibrary` contenue dans le fichier ILoggingLibrary.cs.</span><span class="sxs-lookup"><span data-stu-id="c5457-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="c5457-128">C’est là que vous définissez l’interface de votre bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="c5457-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="c5457-129">L’autre bibliothèque de classes portable, `Plugin.LoggingLibrary (Portable)`, contient le code dans CrossLoggingLibrary.cs qui recherche une implémentation propre à la plateforme de l’interface abstraite au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="c5457-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="c5457-130">En général, vous n’avez pas besoin de modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="c5457-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="c5457-131">Les projets propres à la plateforme, tels que `Plugin.LoggingLibrary.Android`, contiennent chacun une implémentation native de l’interface dans leurs fichiers LoggingLibraryImplementation.cs respectifs.</span><span class="sxs-lookup"><span data-stu-id="c5457-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="c5457-132">C’est là que vous générez le code de votre bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="c5457-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="c5457-133">Par défaut, le fichier ILoggingLibrary.cs du projet Abstractions contient une définition d’interface, mais aucune méthode.</span><span class="sxs-lookup"><span data-stu-id="c5457-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="c5457-134">Dans le cadre de cette procédure pas à pas, vous devez ajouter une méthode `Log` comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5457-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="c5457-135">Écrire du code spécifique de la plateforme</span><span class="sxs-lookup"><span data-stu-id="c5457-135">Write your platform-specific code</span></span>

<span data-ttu-id="c5457-136">Pour implémenter une implémentation spécifique de la plateforme de l’interface `ILoggingLibrary` et ses méthodes, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c5457-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="c5457-137">Ouvrez le fichier `LoggingLibraryImplementation.cs` de chaque projet de plateforme et ajoutez le code nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c5457-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="c5457-138">Par exemple (utilisation du projet `Plugin.LoggingLibrary.Android`) :</span><span class="sxs-lookup"><span data-stu-id="c5457-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="c5457-139">Répétez cette implémentation dans les projets pour chaque plateforme que vous souhaitez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="c5457-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="c5457-140">Cliquez avec le bouton droit sur le projet iOS, sélectionnez **Propriétés**, cliquez sur l’onglet **Générer** et supprimez « \iPhone » des paramètres **Chemin de sortie** et **Fichier de documentation XML**.</span><span class="sxs-lookup"><span data-stu-id="c5457-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="c5457-141">Vous pourrez ainsi poursuivre cette procédure pas à pas dans de meilleures conditions.</span><span class="sxs-lookup"><span data-stu-id="c5457-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="c5457-142">Enregistrez le fichier quand vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="c5457-142">Save the file when done.</span></span>
1. <span data-ttu-id="c5457-143">Cliquez avec le bouton droit sur la solution, sélectionnez **Gestionnaire de configurations...** et cochez les cases **Build** pour les bibliothèques de classes portables et chaque plateforme que vous prenez en charge.</span><span class="sxs-lookup"><span data-stu-id="c5457-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="c5457-144">Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour vérifier votre travail et générer les artefacts que vous allez ensuite empaqueter.</span><span class="sxs-lookup"><span data-stu-id="c5457-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="c5457-145">Si vous obtenez des erreurs liées à des références manquantes, cliquez avec le bouton droit sur la solution, sélectionnez **Restaurer des packages NuGet** pour installer des dépendances, puis regénérez la solution.</span><span class="sxs-lookup"><span data-stu-id="c5457-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="c5457-146">Pour effectuer une génération dans le cadre d’iOS, vous avez besoin d’un Mac en réseau connecté à Visual Studio, comme décrit dans [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) (Présentation de Xamarin.iOS pour Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="c5457-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="c5457-147">Si vous ne disposez pas d’un Mac, désactivez le projet iOS dans le gestionnaire de configuration (étape 3 ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="c5457-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="c5457-148">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="c5457-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="c5457-149">Ouvrez une invite de commandes, accédez au dossier `LoggingLibrary` qui se trouve un niveau en dessous du fichier `.sln` et exécutez la commande NuGet `spec` pour créer le fichier `Package.nuspec` initial :</span><span class="sxs-lookup"><span data-stu-id="c5457-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="c5457-150">Renommez ce fichier `LoggingLibrary.nuspec` et ouvrez-le dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="c5457-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="c5457-151">Mettez à jour le fichier afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="c5457-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="c5457-152">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="c5457-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="c5457-153">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="c5457-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="c5457-154">Vous pouvez apposer à la version de votre package le suffixe `-alpha`, `-beta` ou `-rc` pour marquer votre package en tant que préversion ; consultez [Préversions](../create-packages/prerelease-packages.md) pour plus d’informations sur les préversions.</span><span class="sxs-lookup"><span data-stu-id="c5457-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="c5457-155">Ajouter des assemblys de référence</span><span class="sxs-lookup"><span data-stu-id="c5457-155">Add reference assemblies</span></span>

<span data-ttu-id="c5457-156">Pour inclure des assemblys de référence propres à la plateforme, ajoutez le code suivant à l’élément `<files>` de `LoggingLibrary.nuspec` en fonction de vos plateformes prises en charge :</span><span class="sxs-lookup"><span data-stu-id="c5457-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="c5457-157">Pour raccourcir les noms des fichiers DLL et XML, cliquez avec le bouton droit sur un projet donné, sélectionnez l’onglet **Bibliothèque** et changez les noms d’assembly.</span><span class="sxs-lookup"><span data-stu-id="c5457-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="c5457-158">Ajouter des dépendances</span><span class="sxs-lookup"><span data-stu-id="c5457-158">Add dependencies</span></span>

<span data-ttu-id="c5457-159">Si vous avez des dépendances spécifiques pour des implémentations natives, utilisez l’élément `<dependencies>` avec des éléments `<group>` pour les spécifier, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c5457-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="c5457-160">Par exemple, le code suivant définit iTextSharp en tant que dépendance pour la cible UAP :</span><span class="sxs-lookup"><span data-stu-id="c5457-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="c5457-161">Fichier .nuspec final</span><span class="sxs-lookup"><span data-stu-id="c5457-161">Final .nuspec</span></span>

<span data-ttu-id="c5457-162">Votre fichier `.nuspec` final doit maintenant ressembler au code ci-après, où vous devez là aussi remplacer YOUR_NAME par une valeur appropriée :</span><span class="sxs-lookup"><span data-stu-id="c5457-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="c5457-163">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="c5457-163">Package the component</span></span>

<span data-ttu-id="c5457-164">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="c5457-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="c5457-165">Cette opération génère `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="c5457-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="c5457-166">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="c5457-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer affichant le package LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="c5457-168">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="c5457-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="c5457-169">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c5457-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="c5457-170">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c5457-170">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="c5457-171">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="c5457-171">Related topics</span></span>

- [<span data-ttu-id="c5457-172">Informations de référence sur le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="c5457-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="c5457-173">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="c5457-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="c5457-174">Gestion de version des packages</span><span class="sxs-lookup"><span data-stu-id="c5457-174">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c5457-175">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c5457-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c5457-176">Inclusion de cibles et de propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="c5457-176">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="c5457-177">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="c5457-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)