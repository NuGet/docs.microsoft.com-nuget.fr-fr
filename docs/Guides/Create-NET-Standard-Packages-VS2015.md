---
title: "Créer des packages NuGet .NET Standard avec Visual Studio 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Procédure pas à pas de bout en bout pour créer des packages NuGet .NET Standard à l’aide de NuGet 3.x et Visual Studio 2015."
keywords: "créer un package, packages .NET Standard, table de mappage .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="bbe42-104">Créer des packages .NET Standard avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bbe42-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="bbe42-105">*S’applique à NuGet 3.x. Consultez [Créer des packages .NET Standard avec Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) si vous envisagez d’utiliser NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="bbe42-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="bbe42-106">La [bibliothèque .NET Standard](/dotnet/articles/standard/library) est une spécification formelle des API .NET destinées à être disponibles sur tous les runtimes .NET, renforçant ainsi l’uniformité de l’écosystème .NET.</span><span class="sxs-lookup"><span data-stu-id="bbe42-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="bbe42-107">La bibliothèque .NET Standard définit un ensemble uniforme d’API de bibliothèque de classes de base pour toutes les plateformes .NET à implémenter, indépendamment de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="bbe42-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="bbe42-108">Elle permet aux développeurs de produire des bibliothèques de classes portables qui sont utilisables à travers tous les runtimes .NET, et réduit, si ce n’est élimine, les directives de compilation conditionnelle spécifiques à la plateforme dans le code partagé.</span><span class="sxs-lookup"><span data-stu-id="bbe42-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="bbe42-109">Ce guide vous explique comment créer un package nuget ciblant .NET Standard Library 1.4.</span><span class="sxs-lookup"><span data-stu-id="bbe42-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="bbe42-110">Cette opération fonctionne sur .NET Framework 4.6.1, la plateforme Windows universelle 10, .NET Core et Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bbe42-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="bbe42-111">Pour plus d’informations, consultez la [table de mappage .NET Standard](#net-standard-mapping-table) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="bbe42-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="bbe42-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="bbe42-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="bbe42-113">Créer le projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="bbe42-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="bbe42-114">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="bbe42-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="bbe42-115">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="bbe42-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="bbe42-116">Options supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bbe42-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="bbe42-117">Table de mappage .NET Standard</span><span class="sxs-lookup"><span data-stu-id="bbe42-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="bbe42-118">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="bbe42-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="bbe42-119">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="bbe42-119">Pre-requisites</span></span>

1. <span data-ttu-id="bbe42-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="bbe42-120">Visual Studio 2015.</span></span> <span data-ttu-id="bbe42-121">Installez l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/) ; bien entendu, vous pouvez également utiliser les éditions Professional et Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bbe42-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="bbe42-122">.NET Core : installez .NET Core, ainsi que des modèles et autres outils pour Visual Studio 2015 à partir de [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="bbe42-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="bbe42-123">Interface de ligne de commande NuGet.</span><span class="sxs-lookup"><span data-stu-id="bbe42-123">NuGet CLI.</span></span> <span data-ttu-id="bbe42-124">Téléchargez la dernière version de nuget.exe à partir de [nuget.org/downloads](https://nuget.org/downloads), puis enregistrez-la dans un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="bbe42-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="bbe42-125">Ajoutez ensuite cet emplacement à votre variable d’environnement PATH, si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="bbe42-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="bbe42-126">nuget.exe étant l’outil CLI proprement dit, pas un programme d’installation, veillez à enregistrer le fichier téléchargé à partir de votre navigateur au lieu de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="bbe42-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="bbe42-127">Créer le projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="bbe42-127">Create the class library project</span></span>

1. <span data-ttu-id="bbe42-128">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez **Bibliothèque de classes (Portable)**, changez le nom en AppLogger et cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="bbe42-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Créer un projet de bibliothèque de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="bbe42-130">Dans la boîte de dialogue **Ajouter une bibliothèque de classes portable** qui s’affiche, sélectionnez les options `.NET Framework 4.6` et `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="bbe42-131">Cliquez avec le bouton droit sur `AppLogger (Portable)` dans l’Explorateur de solutions, sélectionnez **Propriétés**, sélectionnez l’onglet **Bibliothèque**, puis cliquez sur **Cibler .NET Platform Standard** dans la section **Ciblage**.</span><span class="sxs-lookup"><span data-stu-id="bbe42-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="bbe42-132">Confirmez l’opération, puis sélectionnez `.NET Standard 1.4` dans la liste déroulante :</span><span class="sxs-lookup"><span data-stu-id="bbe42-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Définition de la cible sur .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="bbe42-134">Cliquez sur l’onglet **Générer**, définissez **Configuration** sur `Release`, puis cochez la case **Fichier de documentation XML**.</span><span class="sxs-lookup"><span data-stu-id="bbe42-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="bbe42-135">Ajoutez votre code au composant, par exemple :</span><span class="sxs-lookup"><span data-stu-id="bbe42-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="bbe42-136">Générez le projet (avec la configuration Release) et vérifiez que les fichiers DLL et XML sont produits dans le dossier bin\Release.</span><span class="sxs-lookup"><span data-stu-id="bbe42-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="bbe42-137">Créer et mettre à jour le fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="bbe42-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="bbe42-138">Ouvrez une invite de commandes, accédez au dossier contenant le dossier `AppLogg.csproj` (un niveau en dessous du fichier `.sln`) et exécutez la commande NuGet `spec` pour créer le fichier `AppLogger.nuspec` initial :</span><span class="sxs-lookup"><span data-stu-id="bbe42-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="bbe42-139">Ouvrez `AppLogger.nuspec` dans un éditeur et mettez-le à jour afin qu’il corresponde au code ci-après, en remplaçant YOUR_NAME par une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="bbe42-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="bbe42-140">La valeur `<id>`, en particulier, doit être unique dans nuget.org (consultez les conventions de nommage décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="bbe42-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="bbe42-141">De plus, vous devez également mettre à jour les balises authors et description afin de ne pas obtenir d’erreur durant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="bbe42-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="bbe42-142">Ajoutez des assemblys de référence au fichier `.nuspec`, concrètement les fichiers DLL et XML IntelliSense de la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="bbe42-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="bbe42-143">Cliquez avec le bouton droit sur la solution et sélectionnez **Générer la solution** pour générer tous les fichiers du package.</span><span class="sxs-lookup"><span data-stu-id="bbe42-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="bbe42-144">Empaqueter le composant</span><span class="sxs-lookup"><span data-stu-id="bbe42-144">Package the component</span></span>

<span data-ttu-id="bbe42-145">Une fois que le fichier `.nuspec` est finalisé et qu’il référence tous les fichiers à inclure dans le package, vous pouvez exécuter la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="bbe42-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="bbe42-146">Cette opération génère `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="bbe42-147">Si vous ouvrez ce fichier dans un outil tel que [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) et développez tous les nœuds, le contenu suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="bbe42-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet Package Explorer affichant le package AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="bbe42-149">Un fichier `.nupkg` est simplement un fichier zip avec une extension différente.</span><span class="sxs-lookup"><span data-stu-id="bbe42-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="bbe42-150">Vous pouvez alors également examiner le contenu de package en définissant `.nupkg` sur `.zip`, mais n’oubliez pas de restaurer l’extension avant de charger un package sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bbe42-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="bbe42-151">Pour mettre votre package à la disposition des autres développeurs, suivez les instructions indiquées dans [Publier un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bbe42-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="bbe42-152">Notez que `pack` requiert Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="bbe42-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="bbe42-153">Sur un Mac, vous devez également convertir les chemins d’accès Windows dans le fichier `.nuspec` en chemins d’accès de style Unix.</span><span class="sxs-lookup"><span data-stu-id="bbe42-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="bbe42-154">Options supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bbe42-154">Additional options</span></span>

<span data-ttu-id="bbe42-155">Les sections suivantes présentent des options supplémentaires pour la création de packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="bbe42-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="bbe42-156">Déclaration de dépendances</span><span class="sxs-lookup"><span data-stu-id="bbe42-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="bbe42-157">Prise en charge de plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="bbe42-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="bbe42-158">Ajout de cibles et de propriétés pour MSBuild</span><span class="sxs-lookup"><span data-stu-id="bbe42-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="bbe42-159">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="bbe42-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="bbe42-160">Ajout d’un fichier readme</span><span class="sxs-lookup"><span data-stu-id="bbe42-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="bbe42-161">Déclaration de dépendances</span><span class="sxs-lookup"><span data-stu-id="bbe42-161">Declaring dependencies</span></span>

<span data-ttu-id="bbe42-162">Si vous avez des dépendances sur d’autres packages NuGet, répertoriez-les dans l’élément `<dependencies>` avec des éléments `<group>`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="bbe42-163">Par exemple, pour déclarer une dépendance sur NewtonSoft.Json version 8.0.3 ou supérieure, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="bbe42-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="bbe42-164">La syntaxe de l’attribut *version* indique ici que la version 8.0.3 ou supérieure est acceptable.</span><span class="sxs-lookup"><span data-stu-id="bbe42-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="bbe42-165">Pour spécifier des plages de versions différentes, consultez [Gestion de version des packages](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bbe42-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="bbe42-166">Prise en charge de plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="bbe42-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="bbe42-167">Supposons que vous souhaitez tirer parti d’une API dans .NET Framework 4.6.2 qui n’est pas disponible dans .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="bbe42-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="bbe42-168">Pour ce faire, vous devez d’abord vérifier que la bibliothèque se compile pour .NET 4.6.2 à l’aide d’une compilation conditionnelle ou de projets partagés.</span><span class="sxs-lookup"><span data-stu-id="bbe42-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="bbe42-169">(Dans Visual Studio, vous pouvez créer un projet NetCore, ajouter le framework de votre choix à la section à frameworks multiples, puis effectuer une génération.) Ensuite, vous créez le package à l’aide de la technique simple de répertoire de travail basé sur une convention comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbe42-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="bbe42-170">Dans le dossier racine du projet qui contient votre fichier `.nuspec`, créez un dossier nommé `lib`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="bbe42-171">Dans `lib`, créez des dossiers pour chaque plateforme que vous souhaitez prendre en charge :</span><span class="sxs-lookup"><span data-stu-id="bbe42-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="bbe42-172">Dans le fichier `.nuspec`, ajoutez un nœud `files` sous le nœud `package` et faites référence aux fichiers dans `lib` à l’aide de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="bbe42-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="bbe42-173">**Remarque :** Les remplacements de jeton n’étant pas pris en charge avec l’approche de répertoire de travail basé sur une convention, remplacez-les par des valeurs littérales :</span><span class="sxs-lookup"><span data-stu-id="bbe42-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="bbe42-174">Créez le package à l’aide de `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="bbe42-175">Pour plus d’informations sur l’utilisation de cette technique, consultez [Prise en charge de plusieurs versions du .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="bbe42-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="bbe42-176">Ajout de cibles et de propriétés pour MSBuild</span><span class="sxs-lookup"><span data-stu-id="bbe42-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="bbe42-177">Vous pouvez être amené à ajouter des cibles ou propriétés de build personnalisées dans les projets qui utilisent votre package, comme dans le cas de l’exécution d’un processus ou outil personnalisé pendant la génération.</span><span class="sxs-lookup"><span data-stu-id="bbe42-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="bbe42-178">À cette fin, vous ajoutez des fichiers à un dossier `\build`, comme décrit dans les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bbe42-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="bbe42-179">Quand NuGet installe un package avec des fichiers \build, il ajoute un élément MSBuild au fichier projet pointant vers les fichiers .targets et .props.</span><span class="sxs-lookup"><span data-stu-id="bbe42-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="bbe42-180">Quand vous utilisez `project.json`, les cibles ne sont pas ajoutées au projet, mais sont accessibles via `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="bbe42-181">Dans le dossier du projet qui contient le fichier `.nuspec`, créez un dossier nommé `build`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="bbe42-182">Dans `build`, créez des dossiers pour chaque langage pris en charge, puis dans ces derniers, placez vos fichiers `.targets` et `.props` :</span><span class="sxs-lookup"><span data-stu-id="bbe42-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="bbe42-183">Dans le fichier `.nuspec`, ajoutez un nœud `files` sous le nœud `package` et faites référence aux fichiers dans `build` à l’aide de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="bbe42-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="bbe42-184">Créez le package à l’aide de `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="bbe42-185">Pour plus d’informations, reportez-vous à [Inclure des cibles et des propriétés MSBuild dans un package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="bbe42-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="bbe42-186">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="bbe42-186">Creating localized packages</span></span>

<span data-ttu-id="bbe42-187">Pour créer des versions localisées de votre bibliothèque, vous pouvez créer des packages distincts pour différents paramètres régionaux, ou inclure des assemblys de ressources localisées dans un package unique.</span><span class="sxs-lookup"><span data-stu-id="bbe42-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="bbe42-188">Voici comment effectuer cette dernière approche pour l’allemand et l’italien :</span><span class="sxs-lookup"><span data-stu-id="bbe42-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="bbe42-189">Dans chaque dossier de framework cible sous `lib`, créez des dossiers pour chaque langue prise en charge autre que l’anglais (langue par défaut).</span><span class="sxs-lookup"><span data-stu-id="bbe42-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="bbe42-190">Dans ces dossiers, vous pouvez placer des assemblys de ressources et des fichiers XML IntelliSense localisés.</span><span class="sxs-lookup"><span data-stu-id="bbe42-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="bbe42-191">Exemple :</span><span class="sxs-lookup"><span data-stu-id="bbe42-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="bbe42-192">Dans le fichier `.nuspec`, référencez ces fichiers dans le nœud `<files>` :</span><span class="sxs-lookup"><span data-stu-id="bbe42-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="bbe42-193">Créez le package à l’aide de `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbe42-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="bbe42-194">Ajout d’un fichier readme</span><span class="sxs-lookup"><span data-stu-id="bbe42-194">Adding a readme</span></span>

<span data-ttu-id="bbe42-195">Quand vous incluez un fichier `readme.txt` dans la racine du package, Visual Studio l’affiche si le package est installé directement.</span><span class="sxs-lookup"><span data-stu-id="bbe42-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="bbe42-196">Les fichiers readme ne s’affichent pas pour les packages qui sont installés en tant que dépendance, ou pour les projets .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bbe42-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="bbe42-197">Pour effectuer cette opération, créez votre fichier `readme.txt`, placez-le dans le dossier racine du projet, puis faites-y référence dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="bbe42-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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


## <a name="net-standard-mapping-table"></a><span data-ttu-id="bbe42-198">Table de mappage .NET Standard</span><span class="sxs-lookup"><span data-stu-id="bbe42-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="bbe42-199">Nom de la plateforme</span><span class="sxs-lookup"><span data-stu-id="bbe42-199">Platform Name</span></span> |<span data-ttu-id="bbe42-200">Alias</span><span class="sxs-lookup"><span data-stu-id="bbe42-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="bbe42-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="bbe42-201">.NET Standard</span></span> | <span data-ttu-id="bbe42-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="bbe42-202">netstandard</span></span>| <span data-ttu-id="bbe42-203">1.0</span><span class="sxs-lookup"><span data-stu-id="bbe42-203">1.0</span></span>| <span data-ttu-id="bbe42-204">1.1</span><span class="sxs-lookup"><span data-stu-id="bbe42-204">1.1</span></span>| <span data-ttu-id="bbe42-205">1.2</span><span class="sxs-lookup"><span data-stu-id="bbe42-205">1.2</span></span>| <span data-ttu-id="bbe42-206">1.3</span><span class="sxs-lookup"><span data-stu-id="bbe42-206">1.3</span></span>| <span data-ttu-id="bbe42-207">1.4</span><span class="sxs-lookup"><span data-stu-id="bbe42-207">1.4</span></span>| <span data-ttu-id="bbe42-208">1,5</span><span class="sxs-lookup"><span data-stu-id="bbe42-208">1.5</span></span>| <span data-ttu-id="bbe42-209">1.6</span><span class="sxs-lookup"><span data-stu-id="bbe42-209">1.6</span></span>|
|<span data-ttu-id="bbe42-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="bbe42-210">.NET Core</span></span> | <span data-ttu-id="bbe42-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="bbe42-211">netcoreapp</span></span>| <span data-ttu-id="bbe42-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-212">&#x2192;</span></span>| <span data-ttu-id="bbe42-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-213">&#x2192;</span></span>| <span data-ttu-id="bbe42-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-214">&#x2192;</span></span>| <span data-ttu-id="bbe42-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-215">&#x2192;</span></span>| <span data-ttu-id="bbe42-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-216">&#x2192;</span></span>| <span data-ttu-id="bbe42-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-217">&#x2192;</span></span>| <span data-ttu-id="bbe42-218">1.0</span><span class="sxs-lookup"><span data-stu-id="bbe42-218">1.0</span></span>|
|<span data-ttu-id="bbe42-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="bbe42-219">.NET Framework</span></span>| <span data-ttu-id="bbe42-220">net</span><span class="sxs-lookup"><span data-stu-id="bbe42-220">net</span></span>| <span data-ttu-id="bbe42-221">4.5</span><span class="sxs-lookup"><span data-stu-id="bbe42-221">4.5</span></span>| <span data-ttu-id="bbe42-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="bbe42-222">4.5.1</span></span>| <span data-ttu-id="bbe42-223">4.6</span><span class="sxs-lookup"><span data-stu-id="bbe42-223">4.6</span></span>| <span data-ttu-id="bbe42-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="bbe42-224">4.6.1</span></span>| <span data-ttu-id="bbe42-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="bbe42-225">4.6.2</span></span>| <span data-ttu-id="bbe42-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="bbe42-226">4.6.3</span></span>|
|<span data-ttu-id="bbe42-227">Plateformes Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="bbe42-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="bbe42-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-228">&#x2192;</span></span>| <span data-ttu-id="bbe42-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-229">&#x2192;</span></span>| <span data-ttu-id="bbe42-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-230">&#x2192;</span></span>| <span data-ttu-id="bbe42-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-231">&#x2192;</span></span>| <span data-ttu-id="bbe42-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-232">&#x2192;</span></span>| <span data-ttu-id="bbe42-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-233">&#x2192;</span></span>|
|<span data-ttu-id="bbe42-234">Plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="bbe42-234">Universal Windows Platform</span></span>| <span data-ttu-id="bbe42-235">uap</span><span class="sxs-lookup"><span data-stu-id="bbe42-235">uap</span></span>| <span data-ttu-id="bbe42-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-236">&#x2192;</span></span>| <span data-ttu-id="bbe42-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-237">&#x2192;</span></span>| <span data-ttu-id="bbe42-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-238">&#x2192;</span></span>| <span data-ttu-id="bbe42-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-239">&#x2192;</span></span>|<span data-ttu-id="bbe42-240">10.0</span><span class="sxs-lookup"><span data-stu-id="bbe42-240">10.0</span></span>|
|<span data-ttu-id="bbe42-241">Windows</span><span class="sxs-lookup"><span data-stu-id="bbe42-241">Windows</span></span>| <span data-ttu-id="bbe42-242">win</span><span class="sxs-lookup"><span data-stu-id="bbe42-242">win</span></span>| <span data-ttu-id="bbe42-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-243">&#x2192;</span></span>| <span data-ttu-id="bbe42-244">8.0</span><span class="sxs-lookup"><span data-stu-id="bbe42-244">8.0</span></span>| <span data-ttu-id="bbe42-245">8.1</span><span class="sxs-lookup"><span data-stu-id="bbe42-245">8.1</span></span>|
|<span data-ttu-id="bbe42-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="bbe42-246">Windows Phone</span></span>| <span data-ttu-id="bbe42-247">wpa</span><span class="sxs-lookup"><span data-stu-id="bbe42-247">wpa</span></span>| <span data-ttu-id="bbe42-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-248">&#x2192;</span></span>| <span data-ttu-id="bbe42-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="bbe42-249">&#x2192;</span></span>|<span data-ttu-id="bbe42-250">8.1</span><span class="sxs-lookup"><span data-stu-id="bbe42-250">8.1</span></span>|
|<span data-ttu-id="bbe42-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="bbe42-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="bbe42-252">wp</span><span class="sxs-lookup"><span data-stu-id="bbe42-252">wp</span></span>| <span data-ttu-id="bbe42-253">8.0</span><span class="sxs-lookup"><span data-stu-id="bbe42-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="bbe42-254">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="bbe42-254">Related topics</span></span>

- [<span data-ttu-id="bbe42-255">Informations de référence sur le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="bbe42-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="bbe42-256">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="bbe42-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="bbe42-257">Gestion de version des packages</span><span class="sxs-lookup"><span data-stu-id="bbe42-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="bbe42-258">Prise en charge de plusieurs versions du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="bbe42-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="bbe42-259">Inclure des cibles et des propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="bbe42-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="bbe42-260">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="bbe42-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="bbe42-261">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="bbe42-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="bbe42-262">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="bbe42-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
