---
title: Créer des packages NuGet .NET Standard et .NET Framework avec Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard et .NET Framework avec NuGet 3.x et Visual Studio 2015.
keywords: créer un package, packages .NET Standard, packages .NET Framework
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbe0a0788b5fc9ba37f7db601bd51c3e4f78f5b8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="9c260-104">Créer des packages .NET Standard et .NET Framework avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="9c260-104">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="9c260-105">**Remarque :** Visual Studio 2017 est recommandé pour développer des bibliothèques .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="9c260-105">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="9c260-106">Visual Studio 2015 peut fonctionner, mais les outils .NET Core n’étaient qu’en préversion.</span><span class="sxs-lookup"><span data-stu-id="9c260-106">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="9c260-107">Consultez la page [Créer et publier un package avec Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pour utiliser NuGet 4.x+ et Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9c260-107">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="9c260-108">La [bibliothèque .NET Standard](/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET.</span><span class="sxs-lookup"><span data-stu-id="9c260-108">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="9c260-109">La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="9c260-109">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="9c260-110">Elle permet aux développeurs de produire du code qui est utilisable sur tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.</span><span class="sxs-lookup"><span data-stu-id="9c260-110">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="9c260-111">Ce guide vous explique comment créer un package NuGet ciblant une bibliothèque .NET Standard 1.4 ou .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="9c260-111">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="9c260-112">Une bibliothèque .NET Standard 1.4 fonctionne sur .NET Framework 4.6.1, la plateforme Windows universelle 10, .NET Core et Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9c260-112">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="9c260-113">Pour plus d’informations, consultez la [table de mappage .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentation .NET).</span><span class="sxs-lookup"><span data-stu-id="9c260-113">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="9c260-114">Vous pouvez choisir une autre version de la bibliothèque .NET Standard si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9c260-114">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c260-115">Prérequis</span><span class="sxs-lookup"><span data-stu-id="9c260-115">Prerequisites</span></span>

1. <span data-ttu-id="9c260-116">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="9c260-116">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="9c260-117">(.NET Standard uniquement) [Kit SDK .NET Core](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="9c260-117">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="9c260-118">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c260-118">NuGet CLI.</span></span> <span data-ttu-id="9c260-119">Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="9c260-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="9c260-120">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="9c260-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="9c260-121">nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="9c260-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="9c260-122">Créer le projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="9c260-122">Create the class library project</span></span>

1. <span data-ttu-id="9c260-123">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez **Bibliothèque de classes (portable)**, remplacez le nom par AppLogger et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c260-123">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Créer un projet de bibliothèque de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="9c260-125">Dans la boîte de dialogue **Ajouter une bibliothèque de classes portable** qui s’affiche, sélectionnez les options de `.NET Framework 4.6` et de `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="9c260-125">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="9c260-126">(Si vous ciblez .NET Framework, vous pouvez sélectionner n’importe quelle option correspondante.)</span><span class="sxs-lookup"><span data-stu-id="9c260-126">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="9c260-127">Si vous ciblez .NET Standard, cliquez avec le bouton droit sur `AppLogger (Portable)` dans l’Explorateur de solutions, sélectionnez **Propriétés**, l’onglet **Bibliothèque**, puis **Cibler .NET Platform Standard** dans la section **Ciblage**.</span><span class="sxs-lookup"><span data-stu-id="9c260-127">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="9c260-128">Cette action demande une confirmation, après quoi vous pourrez sélectionner `.NET Standard 1.4` (ou une autre version disponible) dans la liste déroulante :</span><span class="sxs-lookup"><span data-stu-id="9c260-128">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Définition de la cible sur .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="9c260-130">Cliquez sur l’onglet **Générer**, définissez **Configuration** sur `Release`, puis cochez la case **Fichier de documentation XML**.</span><span class="sxs-lookup"><span data-stu-id="9c260-130">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="9c260-131">Ajoutez votre code au composant, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9c260-131">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="9c260-132">Définissez la configuration Release, générez le projet et vérifiez que les fichiers DLL et XML sont produits dans le dossier `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="9c260-132">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9c260-133">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="9c260-133">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="9c260-134">Ouvrez une invite de commandes, accédez au dossier contenant le dossier `AppLogger.csproj` (un niveau en dessous du fichier `.sln`) et exécutez la commande NuGet `spec` pour créer le fichier `AppLogger.nuspec` initial :</span><span class="sxs-lookup"><span data-stu-id="9c260-134">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="9c260-135">Ouvrez `AppLogger.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="9c260-135">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9c260-136">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="9c260-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="9c260-137">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="9c260-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="9c260-138">Ajoutez des assemblys de référence au fichier `.nuspec`, concrètement les fichiers DLL et XML IntelliSense de la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="9c260-138">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="9c260-139">Si vous ciblez .NET Standard, les entrées se présentent ainsi :</span><span class="sxs-lookup"><span data-stu-id="9c260-139">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="9c260-140">Si vous ciblez .NET Framework, les entrées se présentent ainsi :</span><span class="sxs-lookup"><span data-stu-id="9c260-140">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="9c260-141">Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour générer tous les fichiers du package.</span><span class="sxs-lookup"><span data-stu-id="9c260-141">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="9c260-142">Déclaration de dépendances</span><span class="sxs-lookup"><span data-stu-id="9c260-142">Declaring dependencies</span></span>

<span data-ttu-id="9c260-143">Si vous avez des dépendances sur d’autres packages NuGet, répertoriez-les dans l’élément `<dependencies>` du manifeste avec des éléments `<group>`.</span><span class="sxs-lookup"><span data-stu-id="9c260-143">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="9c260-144">Par exemple, pour déclarer une dépendance sur NewtonSoft.Json version 8.0.3 ou supérieure, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="9c260-144">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="9c260-145">La syntaxe de l’attribut *version* indique ici que la version 8.0.3 ou supérieure est acceptable.</span><span class="sxs-lookup"><span data-stu-id="9c260-145">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="9c260-146">Pour spécifier des plages de versions différentes, consultez [Gestion de version des packages](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9c260-146">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="9c260-147">Ajout d’un fichier readme</span><span class="sxs-lookup"><span data-stu-id="9c260-147">Adding a readme</span></span>

<span data-ttu-id="9c260-148">Créez votre fichier `readme.txt`, placez-le dans le dossier racine du projet, puis faites-y référence dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="9c260-148">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="9c260-149">Visual Studio affiche `readme.txt` quand le package est installé dans un projet.</span><span class="sxs-lookup"><span data-stu-id="9c260-149">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="9c260-150">Les fichiers n’est pas affiché quand il est installé dans des projets .NET Core ou pour des packages qui sont installés en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="9c260-150">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="9c260-151">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="9c260-151">Package the component</span></span>

<span data-ttu-id="9c260-152">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="9c260-152">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="9c260-153">Cette opération génère `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9c260-153">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9c260-154">Si vous ouvrez ce fichier dans un outil comme [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et que vous développez tous les nœuds, le contenu suivant (indiqué pour .NET Standard) apparaît :</span><span class="sxs-lookup"><span data-stu-id="9c260-154">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet Package Explorer affichant le package AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9c260-156">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="9c260-156">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9c260-157">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9c260-157">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9c260-158">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9c260-158">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="9c260-159">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="9c260-159">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9c260-160">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="9c260-160">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="9c260-161">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="9c260-161">Related topics</span></span>

- [<span data-ttu-id="9c260-162">Informations de référence sur le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="9c260-162">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9c260-163">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9c260-163">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9c260-164">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="9c260-164">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9c260-165">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="9c260-165">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9c260-166">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="9c260-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="9c260-167">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="9c260-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9c260-168">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="9c260-168">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9c260-169">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9c260-169">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
