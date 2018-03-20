---
title: "Créer des packages NuGet .NET Standard avec Visual Studio 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard à l’aide de NuGet 3.x et Visual Studio 2015."
keywords: "créer un package, packages .NET Standard, table de mappage .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="beac4-104">Créer des packages .NET Standard avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="beac4-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="beac4-105">*S’applique à NuGet 3.x. Consultez [Créer et publier un package avec Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) si vous envisagez d’utiliser NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="beac4-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="beac4-106">La [bibliothèque .NET Standard](/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET.</span><span class="sxs-lookup"><span data-stu-id="beac4-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="beac4-107">La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="beac4-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="beac4-108">Elle permet aux développeurs de produire du code qui est utilisable sur tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.</span><span class="sxs-lookup"><span data-stu-id="beac4-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="beac4-109">Ce guide vous explique comment créer un package NuGet ciblant .NET Standard Library 1.4.</span><span class="sxs-lookup"><span data-stu-id="beac4-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="beac4-110">Cette bibliothèque fonctionne sur le .NET Framework 4.6.1, la plateforme Windows universelle 10, .NET Core et Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="beac4-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="beac4-111">Pour plus d’informations, consultez la [table de mappage .NET Standard](#net-standard-mapping-table) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="beac4-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="beac4-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="beac4-112">Prerequisites</span></span>

1. <span data-ttu-id="beac4-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="beac4-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="beac4-114">SDK .NET Core</span><span class="sxs-lookup"><span data-stu-id="beac4-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="beac4-115">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="beac4-115">NuGet CLI.</span></span> <span data-ttu-id="beac4-116">Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="beac4-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="beac4-117">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="beac4-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="beac4-118">nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="beac4-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="beac4-119">Créer le projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="beac4-119">Create the class library project</span></span>

1. <span data-ttu-id="beac4-120">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez **Bibliothèque de classes (Portable)**, changez le nom en AppLogger et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="beac4-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Créer un projet de bibliothèque de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="beac4-122">Dans la boîte de dialogue **Ajouter une bibliothèque de classes portable** qui s’affiche, sélectionnez les options `.NET Framework 4.6` et `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="beac4-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="beac4-123">Cliquez avec le bouton droit sur `AppLogger (Portable)` dans l’Explorateur de solutions, sélectionnez **Propriétés**, sélectionnez l’onglet **Bibliothèque**, puis cliquez sur **Cibler .NET Platform Standard** dans la section **Ciblage**.</span><span class="sxs-lookup"><span data-stu-id="beac4-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="beac4-124">Confirmez l’opération, puis sélectionnez `.NET Standard 1.4` dans la liste déroulante :</span><span class="sxs-lookup"><span data-stu-id="beac4-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Définition de la cible sur .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="beac4-126">Cliquez sur l’onglet **Générer**, définissez **Configuration** sur `Release`, puis cochez la case **Fichier de documentation XML**.</span><span class="sxs-lookup"><span data-stu-id="beac4-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="beac4-127">Ajoutez votre code au composant, par exemple :</span><span class="sxs-lookup"><span data-stu-id="beac4-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="beac4-128">Définissez la configuration Release, générez le projet et vérifiez que les fichiers DLL et XML sont produits dans le dossier `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="beac4-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="beac4-129">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="beac4-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="beac4-130">Ouvrez une invite de commandes, accédez au dossier contenant le dossier `AppLogger.csproj` (un niveau en dessous du fichier `.sln`) et exécutez la commande NuGet `spec` pour créer le fichier `AppLogger.nuspec` initial :</span><span class="sxs-lookup"><span data-stu-id="beac4-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="beac4-131">Ouvrez `AppLogger.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="beac4-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="beac4-132">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="beac4-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="beac4-133">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="beac4-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="beac4-134">Ajoutez des assemblys de référence au fichier `.nuspec`, concrètement les fichiers DLL et XML IntelliSense de la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="beac4-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="beac4-135">Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour générer tous les fichiers du package.</span><span class="sxs-lookup"><span data-stu-id="beac4-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="beac4-136">Déclaration de dépendances</span><span class="sxs-lookup"><span data-stu-id="beac4-136">Declaring dependencies</span></span>

<span data-ttu-id="beac4-137">Si vous avez des dépendances sur d’autres packages NuGet, répertoriez-les dans l’élément `<dependencies>` du manifeste avec des éléments `<group>`.</span><span class="sxs-lookup"><span data-stu-id="beac4-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="beac4-138">Par exemple, pour déclarer une dépendance sur NewtonSoft.Json version 8.0.3 ou supérieure, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="beac4-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="beac4-139">La syntaxe de l’attribut *version* indique ici que la version 8.0.3 ou supérieure est acceptable.</span><span class="sxs-lookup"><span data-stu-id="beac4-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="beac4-140">Pour spécifier des plages de versions différentes, consultez [Gestion de version des packages](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="beac4-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="beac4-141">Ajout d’un fichier readme</span><span class="sxs-lookup"><span data-stu-id="beac4-141">Adding a readme</span></span>

<span data-ttu-id="beac4-142">Créez votre fichier `readme.txt`, placez-le dans le dossier racine du projet, puis faites-y référence dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="beac4-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="beac4-143">Visual Studio affiche `readme.txt` quand le package est installé dans un projet.</span><span class="sxs-lookup"><span data-stu-id="beac4-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="beac4-144">Les fichiers n’est pas affiché quand il est installé dans des projets .NET Core ou pour des packages qui sont installés en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="beac4-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="beac4-145">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="beac4-145">Package the component</span></span>

<span data-ttu-id="beac4-146">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="beac4-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="beac4-147">Cette opération génère `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="beac4-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="beac4-148">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="beac4-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer affichant le package AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="beac4-150">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="beac4-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="beac4-151">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="beac4-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="beac4-152">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="beac4-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="beac4-153">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="beac4-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="beac4-154">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="beac4-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="beac4-155">Table de mappage .NET Standard</span><span class="sxs-lookup"><span data-stu-id="beac4-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="beac4-156">Nom de la plateforme</span><span class="sxs-lookup"><span data-stu-id="beac4-156">Platform Name</span></span> | <span data-ttu-id="beac4-157">Alias</span><span class="sxs-lookup"><span data-stu-id="beac4-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="beac4-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="beac4-158">.NET Standard</span></span> | <span data-ttu-id="beac4-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="beac4-159">netstandard</span></span> | <span data-ttu-id="beac4-160">1.0</span><span class="sxs-lookup"><span data-stu-id="beac4-160">1.0</span></span> | <span data-ttu-id="beac4-161">1.1</span><span class="sxs-lookup"><span data-stu-id="beac4-161">1.1</span></span> | <span data-ttu-id="beac4-162">1.2</span><span class="sxs-lookup"><span data-stu-id="beac4-162">1.2</span></span> | <span data-ttu-id="beac4-163">1.3</span><span class="sxs-lookup"><span data-stu-id="beac4-163">1.3</span></span> | <span data-ttu-id="beac4-164">1.4</span><span class="sxs-lookup"><span data-stu-id="beac4-164">1.4</span></span> | <span data-ttu-id="beac4-165">1,5</span><span class="sxs-lookup"><span data-stu-id="beac4-165">1.5</span></span> | <span data-ttu-id="beac4-166">1.6</span><span class="sxs-lookup"><span data-stu-id="beac4-166">1.6</span></span> |
| <span data-ttu-id="beac4-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="beac4-167">.NET Core</span></span> | <span data-ttu-id="beac4-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="beac4-168">netcoreapp</span></span> | <span data-ttu-id="beac4-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-169">&#x2192;</span></span> | <span data-ttu-id="beac4-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-170">&#x2192;</span></span> | <span data-ttu-id="beac4-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-171">&#x2192;</span></span> | <span data-ttu-id="beac4-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-172">&#x2192;</span></span> | <span data-ttu-id="beac4-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-173">&#x2192;</span></span> | <span data-ttu-id="beac4-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-174">&#x2192;</span></span> | <span data-ttu-id="beac4-175">1.0</span><span class="sxs-lookup"><span data-stu-id="beac4-175">1.0</span></span> |
| <span data-ttu-id="beac4-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="beac4-176">.NET Framework</span></span> | <span data-ttu-id="beac4-177">net</span><span class="sxs-lookup"><span data-stu-id="beac4-177">net</span></span> | <span data-ttu-id="beac4-178">4.5</span><span class="sxs-lookup"><span data-stu-id="beac4-178">4.5</span></span> | <span data-ttu-id="beac4-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="beac4-179">4.5.1</span></span> | <span data-ttu-id="beac4-180">4.6</span><span class="sxs-lookup"><span data-stu-id="beac4-180">4.6</span></span> | <span data-ttu-id="beac4-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="beac4-181">4.6.1</span></span> | <span data-ttu-id="beac4-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="beac4-182">4.6.2</span></span> | <span data-ttu-id="beac4-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="beac4-183">4.6.3</span></span> |
| <span data-ttu-id="beac4-184">Plateformes Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="beac4-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="beac4-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-185">&#x2192;</span></span> | <span data-ttu-id="beac4-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-186">&#x2192;</span></span> | <span data-ttu-id="beac4-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-187">&#x2192;</span></span> | <span data-ttu-id="beac4-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-188">&#x2192;</span></span> | <span data-ttu-id="beac4-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-189">&#x2192;</span></span> | <span data-ttu-id="beac4-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-190">&#x2192;</span></span> |
| <span data-ttu-id="beac4-191">Plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="beac4-191">Universal Windows Platform</span></span> | <span data-ttu-id="beac4-192">uap</span><span class="sxs-lookup"><span data-stu-id="beac4-192">uap</span></span> | <span data-ttu-id="beac4-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-193">&#x2192;</span></span> | <span data-ttu-id="beac4-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-194">&#x2192;</span></span> | <span data-ttu-id="beac4-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-195">&#x2192;</span></span> | <span data-ttu-id="beac4-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-196">&#x2192;</span></span> |<span data-ttu-id="beac4-197">10.0</span><span class="sxs-lookup"><span data-stu-id="beac4-197">10.0</span></span> |
| <span data-ttu-id="beac4-198">Windows</span><span class="sxs-lookup"><span data-stu-id="beac4-198">Windows</span></span> | <span data-ttu-id="beac4-199">win</span><span class="sxs-lookup"><span data-stu-id="beac4-199">win</span></span>| <span data-ttu-id="beac4-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-200">&#x2192;</span></span> | <span data-ttu-id="beac4-201">8.0</span><span class="sxs-lookup"><span data-stu-id="beac4-201">8.0</span></span> | <span data-ttu-id="beac4-202">8.1</span><span class="sxs-lookup"><span data-stu-id="beac4-202">8.1</span></span> |
| <span data-ttu-id="beac4-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="beac4-203">Windows Phone</span></span> | <span data-ttu-id="beac4-204">wpa</span><span class="sxs-lookup"><span data-stu-id="beac4-204">wpa</span></span>| <span data-ttu-id="beac4-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-205">&#x2192;</span></span>| <span data-ttu-id="beac4-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="beac4-206">&#x2192;</span></span> | <span data-ttu-id="beac4-207">8.1</span><span class="sxs-lookup"><span data-stu-id="beac4-207">8.1</span></span> |
| <span data-ttu-id="beac4-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="beac4-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="beac4-209">wp</span><span class="sxs-lookup"><span data-stu-id="beac4-209">wp</span></span> | <span data-ttu-id="beac4-210">8.0</span><span class="sxs-lookup"><span data-stu-id="beac4-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="beac4-211">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="beac4-211">Related topics</span></span>

- [<span data-ttu-id="beac4-212">Informations de référence sur le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="beac4-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="beac4-213">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="beac4-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="beac4-214">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="beac4-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="beac4-215">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="beac4-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="beac4-216">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="beac4-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="beac4-217">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="beac4-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="beac4-218">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="beac4-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="beac4-219">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="beac4-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
