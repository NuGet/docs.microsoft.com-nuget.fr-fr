---
title: Créer des packages NuGet pour Xamarin (pour iOS, Android et Windows) avec Visual Studio 2017 ou 2019
description: Procédure pas à pas de bout en bout montrant comment créer des packages NuGet pour Xamarin qui utilisent des API natives sur iOS, Android et Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385675"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="d468c-103">Créer des packages pour Xamarin avec Visual Studio 2017 ou 2019</span><span class="sxs-lookup"><span data-stu-id="d468c-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="d468c-104">Un package pour Xamarin contient du code qui utilise des API natives sur iOS, Android et Windows, suivant le système d’exploitation du runtime.</span><span class="sxs-lookup"><span data-stu-id="d468c-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="d468c-105">Bien que cela soit simple à faire, il est préférable de permettre aux développeurs d’utiliser le package à partir d’une bibliothèque de classes portable ou de bibliothèques .NET Standard par le biais d’une surface d’exposition d’API communes.</span><span class="sxs-lookup"><span data-stu-id="d468c-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="d468c-106">Dans cette procédure pas à pas, vous utilisez Visual Studio 2017 ou 2019 pour créer un package NuGet multiplateforme qui peut être utilisé dans des projets mobiles sur iOS, Android et Windows.</span><span class="sxs-lookup"><span data-stu-id="d468c-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="d468c-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d468c-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="d468c-108">Créer la structure du projet et le code d’abstraction</span><span class="sxs-lookup"><span data-stu-id="d468c-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="d468c-109">Écrire du code spécifique de la plateforme</span><span class="sxs-lookup"><span data-stu-id="d468c-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="d468c-110">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="d468c-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="d468c-111">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="d468c-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="d468c-112">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="d468c-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="d468c-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="d468c-113">Prerequisites</span></span>

1. <span data-ttu-id="d468c-114">Visual Studio 2017 ou 2019 avec plateforme Windows universelle (UWP) et Xamarin.</span><span class="sxs-lookup"><span data-stu-id="d468c-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="d468c-115">Installez l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; bien entendu, vous pouvez également utiliser les éditions Professional et Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d468c-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="d468c-116">Pour inclure les outils Xamarin et UWP, sélectionnez une installation personnalisée et cochez les options appropriées.</span><span class="sxs-lookup"><span data-stu-id="d468c-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="d468c-117">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="d468c-117">NuGet CLI.</span></span> <span data-ttu-id="d468c-118">Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d468c-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="d468c-119">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="d468c-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="d468c-120">nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="d468c-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="d468c-121">Créer la structure du projet et le code d’abstraction</span><span class="sxs-lookup"><span data-stu-id="d468c-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="d468c-122">Téléchargez et exécutez l' [extension de modèles de plug-in .NET standard multiplateforme](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d468c-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="d468c-123">Ces modèles facilitent la création de la structure de projet nécessaire pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d468c-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="d468c-124">Dans Visual Studio 2017, **fichier > nouveau projet de >** , recherchez `Plugin`, sélectionnez le modèle de **plug-in bibliothèque de .NET standard multiplateforme** , remplacez le nom par LoggingLibrary, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="d468c-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nouveau projet application vide (Xamarin. Forms portable) dans VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="d468c-126">Dans Visual Studio 2019, **fichier > nouveau projet de >** , recherchez `Plugin`, sélectionnez le modèle de **plug-in bibliothèque de .NET standard multiplateforme** , puis cliquez sur suivant.</span><span class="sxs-lookup"><span data-stu-id="d468c-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nouveau projet application vide (Xamarin. Forms portable) dans VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="d468c-128">Remplacez le nom par LoggingLibrary, puis cliquez sur créer.</span><span class="sxs-lookup"><span data-stu-id="d468c-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Configuration de la nouvelle application vide (Xamarin. Forms portable) dans VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="d468c-130">La solution obtenue contient deux projets partagés, ainsi qu’un large éventail de projets spécifiques à la plateforme :</span><span class="sxs-lookup"><span data-stu-id="d468c-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="d468c-131">Le projet `ILoggingLibrary`, qui est contenu dans le fichier `ILoggingLibrary.shared.cs`, définit l’interface publique (la surface d’exposition de l’API) du composant.</span><span class="sxs-lookup"><span data-stu-id="d468c-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="d468c-132">C’est là que vous définissez l’interface de votre bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="d468c-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="d468c-133">L’autre projet partagé contient du code dans `CrossLoggingLibrary.shared.cs` qui localise une implémentation spécifique à la plateforme de l’interface abstraite au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d468c-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="d468c-134">En général, vous n’avez pas besoin de modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="d468c-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="d468c-135">Les projets spécifiques à la plateforme, tels que les `LoggingLibrary.android.cs`, contiennent chacun une implémentation native de l’interface dans leurs fichiers `LoggingLibraryImplementation.cs` (VS 2017) ou `LoggingLibrary.<PLATFORM>.cs` (VS 2019) respectifs.</span><span class="sxs-lookup"><span data-stu-id="d468c-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="d468c-136">C’est là que vous générez le code de votre bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="d468c-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="d468c-137">Par défaut, le fichier ILoggingLibrary.shared.cs du projet `ILoggingLibrary` contient une définition d’interface, mais aucune méthode.</span><span class="sxs-lookup"><span data-stu-id="d468c-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="d468c-138">Dans le cadre de cette procédure pas à pas, vous devez ajouter une méthode `Log` comme suit :</span><span class="sxs-lookup"><span data-stu-id="d468c-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="d468c-139">Écrire du code spécifique de la plateforme</span><span class="sxs-lookup"><span data-stu-id="d468c-139">Write your platform-specific code</span></span>

<span data-ttu-id="d468c-140">Pour implémenter une implémentation spécifique de la plateforme de l’interface `ILoggingLibrary` et ses méthodes, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d468c-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="d468c-141">Ouvrez le fichier `LoggingLibraryImplementation.cs` (VS 2017) ou `LoggingLibrary.<PLATFORM>.cs` (VS 2019) de chaque projet de plateforme, puis ajoutez le code nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d468c-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="d468c-142">Par exemple (à l’aide du projet `Android` Platform) :</span><span class="sxs-lookup"><span data-stu-id="d468c-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

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

1. <span data-ttu-id="d468c-143">Répétez cette implémentation dans les projets pour chaque plateforme que vous souhaitez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="d468c-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="d468c-144">Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour vérifier votre travail et générer les artefacts que vous allez ensuite empaqueter.</span><span class="sxs-lookup"><span data-stu-id="d468c-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="d468c-145">Si vous obtenez des erreurs liées à des références manquantes, cliquez avec le bouton droit sur la solution, sélectionnez **Restaurer des packages NuGet** pour installer des dépendances, puis regénérez la solution.</span><span class="sxs-lookup"><span data-stu-id="d468c-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="d468c-146">Si vous utilisez Visual Studio 2019, avant de sélectionner **restaurer les packages NuGet** et d’essayer de reconstruire, vous devez modifier la version de `MSBuild.Sdk.Extras` en `2.0.54` dans `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="d468c-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="d468c-147">Pour accéder à ce fichier, vous devez tout d’abord cliquer avec le bouton droit sur le projet (sous la solution) et sélectionner `Unload Project`, après quoi vous cliquez avec le bouton droit sur le projet déchargé et sélectionnez `Edit LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="d468c-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="d468c-148">Pour effectuer une génération dans le cadre d’iOS, vous avez besoin d’un Mac en réseau connecté à Visual Studio, comme décrit dans [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) (Présentation de Xamarin.iOS pour Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d468c-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="d468c-149">Si vous ne disposez pas d’un Mac, désactivez le projet iOS dans le gestionnaire de configuration (étape 3 ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="d468c-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="d468c-150">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="d468c-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="d468c-151">Ouvrez une invite de commandes, accédez au dossier `LoggingLibrary` qui se trouve un niveau en dessous du fichier `.sln` et exécutez la commande NuGet `spec` pour créer le fichier `Package.nuspec` initial :</span><span class="sxs-lookup"><span data-stu-id="d468c-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="d468c-152">Renommez ce fichier `LoggingLibrary.nuspec` et ouvrez-le dans un éditeur.</span><span class="sxs-lookup"><span data-stu-id="d468c-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="d468c-153">Mettez à jour le fichier afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="d468c-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="d468c-154">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="d468c-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="d468c-155">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="d468c-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="d468c-156">Vous pouvez apposer à la version de votre package le suffixe `-alpha`, `-beta` ou `-rc` pour marquer votre package en tant que préversion ; consultez [Préversions](../create-packages/prerelease-packages.md) pour plus d’informations sur les préversions.</span><span class="sxs-lookup"><span data-stu-id="d468c-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="d468c-157">Ajouter des assemblys de référence</span><span class="sxs-lookup"><span data-stu-id="d468c-157">Add reference assemblies</span></span>

<span data-ttu-id="d468c-158">Pour inclure des assemblys de référence propres à la plateforme, ajoutez le code suivant à l’élément `<files>` de `LoggingLibrary.nuspec` en fonction de vos plateformes prises en charge :</span><span class="sxs-lookup"><span data-stu-id="d468c-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="d468c-159">Pour raccourcir les noms des fichiers DLL et XML, cliquez avec le bouton droit sur un projet donné, sélectionnez l’onglet **Bibliothèque** et changez les noms d’assembly.</span><span class="sxs-lookup"><span data-stu-id="d468c-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="d468c-160">Ajouter des dépendances</span><span class="sxs-lookup"><span data-stu-id="d468c-160">Add dependencies</span></span>

<span data-ttu-id="d468c-161">Si vous avez des dépendances spécifiques pour des implémentations natives, utilisez l’élément `<dependencies>` avec des éléments `<group>` pour les spécifier, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d468c-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="d468c-162">Par exemple, le code suivant définit iTextSharp en tant que dépendance pour la cible UAP :</span><span class="sxs-lookup"><span data-stu-id="d468c-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="d468c-163">Fichier .nuspec final</span><span class="sxs-lookup"><span data-stu-id="d468c-163">Final .nuspec</span></span>

<span data-ttu-id="d468c-164">Votre fichier `.nuspec` final doit maintenant ressembler au code ci-après, où vous devez là aussi remplacer YOUR_NAME par une valeur appropriée :</span><span class="sxs-lookup"><span data-stu-id="d468c-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2018</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="d468c-165">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="d468c-165">Package the component</span></span>

<span data-ttu-id="d468c-166">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="d468c-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="d468c-167">Cette opération génère `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d468c-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="d468c-168">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et que vous développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="d468c-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer affichant le package LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d468c-170">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="d468c-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d468c-171">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d468c-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="d468c-172">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d468c-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="d468c-173">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="d468c-173">Related topics</span></span>

- [<span data-ttu-id="d468c-174">Informations de référence sur le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="d468c-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="d468c-175">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="d468c-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="d468c-176">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="d468c-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="d468c-177">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d468c-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d468c-178">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="d468c-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="d468c-179">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="d468c-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)