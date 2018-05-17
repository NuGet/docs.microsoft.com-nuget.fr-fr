---
title: Créer des packages .NET Standard et des packages NuGet .NET Framework avec Visual Studio 2015
description: Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard et .NET Framework avec NuGet 3.x et Visual Studio 2015.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: a77d977b2abc4cfd8be48e97e4c811e68e09bd61
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="293b4-103">Créer des packages .NET Standard et .NET Framework avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="293b4-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="293b4-104">**Remarque :** Visual Studio 2017 est recommandé pour développer des bibliothèques .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="293b4-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="293b4-105">Visual Studio 2015 peut fonctionner, mais les outils .NET Core n’étaient qu’en préversion.</span><span class="sxs-lookup"><span data-stu-id="293b4-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="293b4-106">Consultez la page [Créer et publier un package avec Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pour utiliser NuGet 4.x+ et Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="293b4-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="293b4-107">La [bibliothèque .NET Standard](/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET.</span><span class="sxs-lookup"><span data-stu-id="293b4-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="293b4-108">La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="293b4-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="293b4-109">Elle permet aux développeurs de produire du code qui est utilisable sur tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.</span><span class="sxs-lookup"><span data-stu-id="293b4-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="293b4-110">Ce guide vous explique comment créer un package NuGet ciblant une bibliothèque .NET Standard 1.4 ou .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="293b4-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="293b4-111">Une bibliothèque .NET Standard 1.4 fonctionne sur .NET Framework 4.6.1, la plateforme Windows universelle 10, .NET Core et Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="293b4-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="293b4-112">Pour plus d’informations, consultez la [table de mappage .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentation .NET).</span><span class="sxs-lookup"><span data-stu-id="293b4-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="293b4-113">Vous pouvez choisir une autre version de la bibliothèque .NET Standard si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="293b4-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="293b4-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="293b4-114">Prerequisites</span></span>

1. <span data-ttu-id="293b4-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="293b4-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="293b4-116">(.NET Standard uniquement) [Kit SDK .NET Core](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="293b4-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="293b4-117">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="293b4-117">NuGet CLI.</span></span> <span data-ttu-id="293b4-118">Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="293b4-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="293b4-119">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="293b4-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="293b4-120">nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="293b4-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="293b4-121">Créer le projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="293b4-121">Create the class library project</span></span>

1. <span data-ttu-id="293b4-122">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez **Bibliothèque de classes (portable)**, remplacez le nom par AppLogger et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="293b4-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Créer un projet de bibliothèque de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="293b4-124">Dans la boîte de dialogue **Ajouter une bibliothèque de classes portable** qui s’affiche, sélectionnez les options de `.NET Framework 4.6` et de `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="293b4-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="293b4-125">(Si vous ciblez .NET Framework, vous pouvez sélectionner n’importe quelle option correspondante.)</span><span class="sxs-lookup"><span data-stu-id="293b4-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="293b4-126">Si vous ciblez .NET Standard, cliquez avec le bouton droit sur `AppLogger (Portable)` dans l’Explorateur de solutions, sélectionnez **Propriétés**, l’onglet **Bibliothèque**, puis **Cibler .NET Platform Standard** dans la section **Ciblage**.</span><span class="sxs-lookup"><span data-stu-id="293b4-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="293b4-127">Cette action demande une confirmation, après quoi vous pourrez sélectionner `.NET Standard 1.4` (ou une autre version disponible) dans la liste déroulante :</span><span class="sxs-lookup"><span data-stu-id="293b4-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Définition de la cible sur .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="293b4-129">Cliquez sur l’onglet **Générer**, définissez **Configuration** sur `Release`, puis cochez la case **Fichier de documentation XML**.</span><span class="sxs-lookup"><span data-stu-id="293b4-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="293b4-130">Ajoutez votre code au composant, par exemple :</span><span class="sxs-lookup"><span data-stu-id="293b4-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="293b4-131">Définissez la configuration Release, générez le projet et vérifiez que les fichiers DLL et XML sont produits dans le dossier `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="293b4-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="293b4-132">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="293b4-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="293b4-133">Ouvrez une invite de commandes, accédez au dossier contenant le dossier `AppLogger.csproj` (un niveau en dessous du fichier `.sln`) et exécutez la commande NuGet `spec` pour créer le fichier `AppLogger.nuspec` initial :</span><span class="sxs-lookup"><span data-stu-id="293b4-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="293b4-134">Ouvrez `AppLogger.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="293b4-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="293b4-135">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="293b4-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="293b4-136">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="293b4-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="293b4-137">Ajoutez des assemblys de référence au fichier `.nuspec`, concrètement les fichiers DLL et XML IntelliSense de la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="293b4-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="293b4-138">Si vous ciblez .NET Standard, les entrées se présentent ainsi :</span><span class="sxs-lookup"><span data-stu-id="293b4-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="293b4-139">Si vous ciblez .NET Framework, les entrées se présentent ainsi :</span><span class="sxs-lookup"><span data-stu-id="293b4-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="293b4-140">Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour générer tous les fichiers du package.</span><span class="sxs-lookup"><span data-stu-id="293b4-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="293b4-141">Déclaration de dépendances</span><span class="sxs-lookup"><span data-stu-id="293b4-141">Declaring dependencies</span></span>

<span data-ttu-id="293b4-142">Si vous avez des dépendances sur d’autres packages NuGet, répertoriez-les dans l’élément `<dependencies>` du manifeste avec des éléments `<group>`.</span><span class="sxs-lookup"><span data-stu-id="293b4-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="293b4-143">Par exemple, pour déclarer une dépendance sur NewtonSoft.Json version 8.0.3 ou supérieure, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="293b4-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="293b4-144">La syntaxe de l’attribut *version* indique ici que la version 8.0.3 ou supérieure est acceptable.</span><span class="sxs-lookup"><span data-stu-id="293b4-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="293b4-145">Pour spécifier des plages de versions différentes, consultez [Gestion de version des packages](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="293b4-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="293b4-146">Ajout d’un fichier readme</span><span class="sxs-lookup"><span data-stu-id="293b4-146">Adding a readme</span></span>

<span data-ttu-id="293b4-147">Créez votre fichier `readme.txt`, placez-le dans le dossier racine du projet, puis faites-y référence dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="293b4-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="293b4-148">Visual Studio affiche `readme.txt` quand le package est installé dans un projet.</span><span class="sxs-lookup"><span data-stu-id="293b4-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="293b4-149">Les fichiers n’est pas affiché quand il est installé dans des projets .NET Core ou pour des packages qui sont installés en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="293b4-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="293b4-150">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="293b4-150">Package the component</span></span>

<span data-ttu-id="293b4-151">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="293b4-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="293b4-152">Cette opération génère `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="293b4-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="293b4-153">Si vous ouvrez ce fichier dans un outil comme [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et que vous développez tous les nœuds, le contenu suivant (indiqué pour .NET Standard) apparaît :</span><span class="sxs-lookup"><span data-stu-id="293b4-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet Package Explorer affichant le package AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="293b4-155">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="293b4-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="293b4-156">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="293b4-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="293b4-157">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="293b4-157">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="293b4-158">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="293b4-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="293b4-159">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="293b4-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="293b4-160">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="293b4-160">Related topics</span></span>

- [<span data-ttu-id="293b4-161">Informations de référence sur le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="293b4-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="293b4-162">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="293b4-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="293b4-163">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="293b4-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="293b4-164">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="293b4-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="293b4-165">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="293b4-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="293b4-166">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="293b4-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="293b4-167">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="293b4-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="293b4-168">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="293b4-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
