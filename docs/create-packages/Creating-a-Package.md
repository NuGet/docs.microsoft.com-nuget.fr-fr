---
title: Guide pratique pour créer un package NuGet
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 1221631b22eed7d2d8e58bd08ff120d91231d49b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580392"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="c44c5-103">Création de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="c44c5-103">Creating NuGet packages</span></span>

<span data-ttu-id="c44c5-104">Quel que soit la fonction de votre package ou le code qu’il contient, vous utilisez `nuget.exe` pour empaqueter cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="c44c5-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="c44c5-105">Pour installer `nuget.exe`, consultez [Installer l’interface de ligne de commande NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="c44c5-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="c44c5-106">Notez que Visual Studio n’inclut pas automatiquement `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="c44c5-107">Techniquement parlant, un package NuGet n’est qu’un fichier ZIP renommé avec l’extension `.nupkg` et dont le contenu correspond à certaines conventions.</span><span class="sxs-lookup"><span data-stu-id="c44c5-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="c44c5-108">Cette rubrique décrit le processus détaillé de création d’un package qui répond à ces conventions.</span><span class="sxs-lookup"><span data-stu-id="c44c5-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="c44c5-109">Pour consulter une procédure pas à pas ciblée, reportez-vous à [Démarrage rapide : créer et publier un package](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="c44c5-110">L’empaquetage commence par le code compilé (assemblys), les symboles et/ou d’autres fichiers à remettre sous forme de package (consultez [Vue d’ensemble et flux de travail](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="c44c5-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="c44c5-111">Ce processus est indépendant de la compilation ou de la génération des fichiers destinés au package, même si vous pouvez tirer des informations contenues dans un fichier projet pour maintenir synchronisés les assemblys et packages compilés.</span><span class="sxs-lookup"><span data-stu-id="c44c5-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="c44c5-112">Cette rubrique s’applique aux types de projet autres que les projets .NET Core utilisant Visual Studio 2017 et NuGet 4.0+.</span><span class="sxs-lookup"><span data-stu-id="c44c5-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="c44c5-113">Dans ces projets .NET Core, NuGet utilise des informations contenues dans le fichier projet directement.</span><span class="sxs-lookup"><span data-stu-id="c44c5-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="c44c5-114">Pour plus d’informations, consultez [Créer des packages .NET standard avec Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) et [Commandes NuGet pack et restore en tant que cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="c44c5-115">Déterminer quels assemblys empaqueter</span><span class="sxs-lookup"><span data-stu-id="c44c5-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="c44c5-116">La plupart des packages à usage général contiennent un ou plusieurs assemblys que d’autres développeurs peuvent utiliser dans leurs propres projets.</span><span class="sxs-lookup"><span data-stu-id="c44c5-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="c44c5-117">En règle générale, il est préférable d’avoir un seul assembly par package NuGet, à condition que chaque assembly soit indépendamment utile.</span><span class="sxs-lookup"><span data-stu-id="c44c5-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="c44c5-118">Par exemple, si vous avez un `Utilities.dll` qui dépend de `Parser.dll`, et que `Parser.dll` est utile tout seul, créez un seul package pour chacun.</span><span class="sxs-lookup"><span data-stu-id="c44c5-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="c44c5-119">Ainsi, les développeurs peuvent utiliser `Parser.dll` indépendamment de `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="c44c5-120">Si votre bibliothèque se compose de plusieurs assemblys qui ne sont pas indépendamment utiles, alors il est possible de les combiner en un seul package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="c44c5-121">À l’aide de l’exemple précédent, si `Parser.dll` contient du code utilisé uniquement par `Utilities.dll`, alors il est possible de conserver `Parser.dll` dans le même package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="c44c5-122">De même, si `Utilities.dll` dépend de `Utilities.resources.dll`, et que ce dernier n’est pas utile tout seul, alors placez les deux dans le même package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="c44c5-123">En réalité, les ressources correspondent à un cas spécial.</span><span class="sxs-lookup"><span data-stu-id="c44c5-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="c44c5-124">Lorsqu’un package est installé dans un projet, NuGet ajoute automatiquement des références d’assembly aux DLL du package, *à l’exclusion* de celles nommées `.resources.dll`, car elles sont supposées être des assemblys satellites localisés (consultez [Création de packages localisés](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="c44c5-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="c44c5-125">C’est pourquoi vous devez éviter d’utiliser `.resources.dll` pour les fichiers qui contiennent du code de package essentiel.</span><span class="sxs-lookup"><span data-stu-id="c44c5-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="c44c5-126">Si votre bibliothèque contient des assemblys COM Interop, suivez les instructions supplémentaires données dans [Création de packages avec des assemblys COM Interop](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="c44c5-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="c44c5-127">Rôle et structure du fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="c44c5-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="c44c5-128">Une fois que vous savez quels fichiers vous voulez empaqueter, l’étape suivante consiste à créer un manifeste de package dans un fichier XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="c44c5-129">Le manifeste :</span><span class="sxs-lookup"><span data-stu-id="c44c5-129">The manifest:</span></span>

1. <span data-ttu-id="c44c5-130">Décrit le contenu du package et est lui-même inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="c44c5-131">Dirige la création du package et indique à NuGet comment installer le package dans un projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="c44c5-132">Par exemple, le manifeste identifie les autres dépendances de package pour que NuGet puisse également les installer lorsque le package principal est installé.</span><span class="sxs-lookup"><span data-stu-id="c44c5-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="c44c5-133">Contient des propriétés à la fois obligatoires et facultatives comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c44c5-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="c44c5-134">Pour plus de précision, notamment sur les autres propriétés non mentionnées ici, consultez les [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="c44c5-135">Propriétés obligatoires :</span><span class="sxs-lookup"><span data-stu-id="c44c5-135">Required properties:</span></span>

- <span data-ttu-id="c44c5-136">Identificateur du package, qui doit être unique dans toute la galerie qui héberge le package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="c44c5-137">Numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [préversions](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="c44c5-138">Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)</span><span class="sxs-lookup"><span data-stu-id="c44c5-138">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="c44c5-139">Informations sur l’auteur et le propriétaire.</span><span class="sxs-lookup"><span data-stu-id="c44c5-139">Author and owner information.</span></span>
- <span data-ttu-id="c44c5-140">Longue description du package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-140">A long description of the package.</span></span>

<span data-ttu-id="c44c5-141">Propriétés facultatives communes :</span><span class="sxs-lookup"><span data-stu-id="c44c5-141">Common optional properties:</span></span>

- <span data-ttu-id="c44c5-142">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="c44c5-142">Release notes</span></span>
- <span data-ttu-id="c44c5-143">Informations de copyright</span><span class="sxs-lookup"><span data-stu-id="c44c5-143">Copyright information</span></span>
- <span data-ttu-id="c44c5-144">Brève description de l’[interface utilisateur du gestionnaire de package dans Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="c44c5-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="c44c5-145">ID de paramètres régionaux</span><span class="sxs-lookup"><span data-stu-id="c44c5-145">A locale ID</span></span>
- <span data-ttu-id="c44c5-146">URL de la page d’accueil et de la licence</span><span class="sxs-lookup"><span data-stu-id="c44c5-146">Home page and license URLs</span></span>
- <span data-ttu-id="c44c5-147">URL de l’icône</span><span class="sxs-lookup"><span data-stu-id="c44c5-147">An icon URL</span></span>
- <span data-ttu-id="c44c5-148">Listes des dépendances et références</span><span class="sxs-lookup"><span data-stu-id="c44c5-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="c44c5-149">Balises facilitant les recherches dans la galerie</span><span class="sxs-lookup"><span data-stu-id="c44c5-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="c44c5-150">Voici un fichier `.nuspec` classique (mais fictif), avec des commentaires décrivant les propriétés :</span><span class="sxs-lookup"><span data-stu-id="c44c5-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="c44c5-151">Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Gestion des versions de package](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="c44c5-152">Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `include` et `exclude` sur l’élément `dependency`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="c44c5-153">Consultez [Informations de référence sur le fichier .nuspec - Dépendances](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="c44c5-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="c44c5-154">Étant donné que le manifeste est inclus dans le package à partir duquel il est créé, vous pouvez en trouver de nombreux autres exemples en examinant les packages existants.</span><span class="sxs-lookup"><span data-stu-id="c44c5-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="c44c5-155">Le dossier *global-packages*, sur votre ordinateur, représente une bonne source ; son emplacement est retourné par la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c44c5-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="c44c5-156">Accédez à un dossier *package\version* quelconque, copiez le fichier `.nupkg` dans un fichier `.zip`, puis ouvrez ce fichier `.zip` et examinez le fichier `.nuspec` qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="c44c5-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="c44c5-157">Lorsque vous créez un fichier `.nuspec` à partir d’un projet Visual Studio, le manifeste contient les jetons qui sont remplacés par des informations du projet lors de la génération du package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="c44c5-158">Consultez [Création du fichier .nuspec à partir d’un projet Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="c44c5-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="c44c5-159">Création du fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="c44c5-159">Creating the .nuspec file</span></span>

<span data-ttu-id="c44c5-160">La création d’un manifeste complet commence généralement par un fichier `.nuspec` de base généré par l’intermédiaire de l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c44c5-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="c44c5-161">Un répertoire de travail basé sur une convention</span><span class="sxs-lookup"><span data-stu-id="c44c5-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="c44c5-162">Une DLL d’assembly</span><span class="sxs-lookup"><span data-stu-id="c44c5-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="c44c5-163">Un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c44c5-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="c44c5-164">Un nouveau fichier avec des valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="c44c5-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="c44c5-165">Vous modifiez ensuite le fichier manuellement afin qu’il décrive le contenu exact que vous voulez dans le package final.</span><span class="sxs-lookup"><span data-stu-id="c44c5-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="c44c5-166">Les fichiers `.nuspec` générés contiennent des espaces réservés qui doivent être modifiés avant de créer le package avec la commande `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="c44c5-167">Cette commande échoue si le fichier `.nuspec` contient des espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="c44c5-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="c44c5-168">À partir d’un répertoire de travail basé sur une convention</span><span class="sxs-lookup"><span data-stu-id="c44c5-168">From a convention-based working directory</span></span>

<span data-ttu-id="c44c5-169">Dans la mesure où un package NuGet n’est qu’un fichier ZIP renommé avec l’extension `.nupkg`, il est souvent plus simple de créer la structure de dossiers souhaitée sur le système de fichiers local, puis de créer directement le fichier `.nuspec` à partir de cette structure.</span><span class="sxs-lookup"><span data-stu-id="c44c5-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="c44c5-170">La commande `nuget pack` ajoute alors automatiquement tous les fichiers dans cette structure de dossiers (à l’exclusion des dossiers qui commencent par `.`, ce qui vous permet de conserver les fichiers privés dans la même structure).</span><span class="sxs-lookup"><span data-stu-id="c44c5-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="c44c5-171">L’avantage de cette approche est que vous n’avez pas besoin de spécifier, dans le manifeste, les fichiers à inclure dans le package (comme expliqué plus loin dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="c44c5-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="c44c5-172">Vous pouvez simplement demander à votre processus de génération de produire la structure de dossiers exacte qui est placée dans le package et vous pouvez facilement inclure d’autres fichiers qui ne font peut-être pas partie d’un projet :</span><span class="sxs-lookup"><span data-stu-id="c44c5-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="c44c5-173">Contenu et code source à injecter dans le projet cible.</span><span class="sxs-lookup"><span data-stu-id="c44c5-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="c44c5-174">Scripts PowerShell (les packages utilisés dans NuGet 2.x peuvent aussi inclure des scripts d’installation, ce qui n’est pas pris en charge dans NuGet 3.x et les versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="c44c5-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="c44c5-175">Transformations des fichiers de configuration et de code source existants dans un projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="c44c5-176">Les conventions de dossier sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="c44c5-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="c44c5-177">Dossier</span><span class="sxs-lookup"><span data-stu-id="c44c5-177">Folder</span></span> | <span data-ttu-id="c44c5-178">Description</span><span class="sxs-lookup"><span data-stu-id="c44c5-178">Description</span></span> | <span data-ttu-id="c44c5-179">Action à l’installation du package</span><span class="sxs-lookup"><span data-stu-id="c44c5-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c44c5-180">(racine)</span><span class="sxs-lookup"><span data-stu-id="c44c5-180">(root)</span></span> | <span data-ttu-id="c44c5-181">Emplacement du fichier Lisez-moi.txt</span><span class="sxs-lookup"><span data-stu-id="c44c5-181">Location for readme.txt</span></span> | <span data-ttu-id="c44c5-182">Visual Studio affiche un fichier Lisez-moi.txt à la racine du package lorsque le package est installé.</span><span class="sxs-lookup"><span data-stu-id="c44c5-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="c44c5-183">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="c44c5-183">lib/{tfm}</span></span> | <span data-ttu-id="c44c5-184">Fichiers d’assembly (`.dll`), de documentation (`.xml`) et de symbole (`.pdb`) du TFM (moniker de la version cible de .NET Framework) donné</span><span class="sxs-lookup"><span data-stu-id="c44c5-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="c44c5-185">Les assemblys sont ajoutés comme références pour la compilation et l’exécution. `.xml` et `.pdb` sont copiés dans les dossiers du projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-185">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="c44c5-186">Consultez [Prise en charge de plusieurs frameworks cibles](supporting-multiple-target-frameworks.md) pour créer des sous-dossiers propres à la cible du framework.</span><span class="sxs-lookup"><span data-stu-id="c44c5-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="c44c5-187">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="c44c5-187">ref/{tfm}</span></span> | <span data-ttu-id="c44c5-188">Fichiers d’assembly (`.dll`) et de symbole (`.pdb`) du TFM (moniker de framework cible) donné</span><span class="sxs-lookup"><span data-stu-id="c44c5-188">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="c44c5-189">Les assemblys étant uniquement ajoutés comme références pour la compilation, rien n’est copié dans le dossier bin du projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-189">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="c44c5-190">runtimes</span><span class="sxs-lookup"><span data-stu-id="c44c5-190">runtimes</span></span> | <span data-ttu-id="c44c5-191">Fichiers d’assemblies propres à l’architecture (`.dll`), de symboles (`.pdb`) et de ressources natives (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="c44c5-191">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="c44c5-192">Les assemblys sont uniquement ajoutés comme références pour l’exécution. Les autres fichiers sont copiés dans les dossiers du projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-192">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="c44c5-193">Il doit toujours y avoir un assembly spécifique à `AnyCPU` (TFM) correspondant sous le dossier `/ref/{tfm}` pour fournir l’assembly correspondant au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="c44c5-193">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="c44c5-194">Consultez [Prise en charge de plusieurs frameworks cibles](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-194">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="c44c5-195">contenu</span><span class="sxs-lookup"><span data-stu-id="c44c5-195">content</span></span> | <span data-ttu-id="c44c5-196">Fichiers arbitraires</span><span class="sxs-lookup"><span data-stu-id="c44c5-196">Arbitrary files</span></span> | <span data-ttu-id="c44c5-197">Le contenu est copié à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-197">Contents are copied to the project root.</span></span> <span data-ttu-id="c44c5-198">Considérez que le dossier **content** est la racine de l’application cible qui consomme le package en définitive.</span><span class="sxs-lookup"><span data-stu-id="c44c5-198">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="c44c5-199">Pour que le package ajoute une image dans le dossier */images* de l’application, placez-le dans le dossier *content/images* du package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-199">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="c44c5-200">build</span><span class="sxs-lookup"><span data-stu-id="c44c5-200">build</span></span> | <span data-ttu-id="c44c5-201">Fichiers `.targets` et `.props` MSBuild</span><span class="sxs-lookup"><span data-stu-id="c44c5-201">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="c44c5-202">Automatiquement insérés dans le fichier projet ou `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="c44c5-202">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="c44c5-203">outils</span><span class="sxs-lookup"><span data-stu-id="c44c5-203">tools</span></span> | <span data-ttu-id="c44c5-204">Scripts PowerShell et programmes accessibles à partir de la console du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="c44c5-204">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="c44c5-205">Le dossier `tools` est ajouté à la variable d’environnement `PATH` de la console du gestionnaire de package uniquement (et *non* à `PATH` comme défini pour MSBuild lors de la génération du projet).</span><span class="sxs-lookup"><span data-stu-id="c44c5-205">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="c44c5-206">Dans la mesure où la structure de dossiers peut contenir n’importe quel nombre d’assemblys pour n’importe quel nombre de frameworks cibles, cette méthode est nécessaire pour créer des packages qui prennent en charge plusieurs frameworks.</span><span class="sxs-lookup"><span data-stu-id="c44c5-206">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="c44c5-207">Dans tous les cas, une fois que la structure de dossiers voulue est en place, exécutez la commande suivante dans ce dossier pour créer le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="c44c5-207">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="c44c5-208">Là encore, le fichier `.nuspec` généré ne contient aucune référence explicite aux fichiers inclus dans la structure de dossiers.</span><span class="sxs-lookup"><span data-stu-id="c44c5-208">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="c44c5-209">NuGet inclut automatiquement tous les fichiers lorsque le package est créé.</span><span class="sxs-lookup"><span data-stu-id="c44c5-209">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="c44c5-210">Vous devez quand même modifier les valeurs d’espace réservé dans d’autres parties du manifeste.</span><span class="sxs-lookup"><span data-stu-id="c44c5-210">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="c44c5-211">À partir d’une DLL d’assembly</span><span class="sxs-lookup"><span data-stu-id="c44c5-211">From an assembly DLL</span></span>

<span data-ttu-id="c44c5-212">Dans le cas simple d’une création de package à partir d’un assembly, vous pouvez générer un fichier `.nuspec` à partir des métadonnées incluses dans l’assembly à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c44c5-212">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="c44c5-213">L’utilisation de cette forme remplace quelques espaces réservés dans le manifeste par des valeurs spécifiques de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="c44c5-213">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="c44c5-214">Par exemple, la propriété `<id>` est définie sur le nom de l’assembly et `<version>` est définie sur la version de l’assembly.</span><span class="sxs-lookup"><span data-stu-id="c44c5-214">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="c44c5-215">Les autres propriétés dans le manifeste, en revanche, n’ont pas de valeurs correspondantes dans l’assembly et contiennent donc toujours des espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="c44c5-215">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="c44c5-216">À partir d’un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c44c5-216">From a Visual Studio project</span></span>

<span data-ttu-id="c44c5-217">La création d’un fichier `.nuspec` à partir d’un fichier `.csproj` ou `.vbproj` s’avère pratique, car les autres packages installés dans ces projets sont automatiquement référencés en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="c44c5-217">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="c44c5-218">Utilisez simplement la commande suivante dans le même dossier que le fichier projet :</span><span class="sxs-lookup"><span data-stu-id="c44c5-218">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="c44c5-219">Le fichier `<project-name>.nuspec` obtenu contient les *jetons* qui sont remplacés au moment de l’empaquetage par des valeurs du projet, notamment des références à tous les autres packages qui ont déjà été installés.</span><span class="sxs-lookup"><span data-stu-id="c44c5-219">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="c44c5-220">Un jeton est délimité par des symboles `$` des deux côtés de la propriété de projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-220">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="c44c5-221">Par exemple, la valeur `<id>` dans un manifeste généré de cette manière se présente généralement comme suit :</span><span class="sxs-lookup"><span data-stu-id="c44c5-221">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="c44c5-222">Ce jeton est remplacé par la valeur `AssemblyName` du fichier projet au moment de l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="c44c5-222">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="c44c5-223">Pour connaître le mappage exact des valeurs de projet sur les jetons `.nuspec`, consultez les [Informations de référence sur les jetons de remplacement](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="c44c5-223">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="c44c5-224">Les jetons vous évite d’avoir à mettre à jour des valeurs cruciales comme le numéro de version dans le fichier `.nuspec` quand vous mettez à jour le projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-224">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="c44c5-225">(Vous pouvez toujours remplacer les jetons par des valeurs littérales, si vous le souhaitez).</span><span class="sxs-lookup"><span data-stu-id="c44c5-225">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="c44c5-226">Notez qu’il existe plusieurs autres options d’empaquetage disponibles quand vous utilisez un projet Visual Studio, comme décrit plus loin dans [Exécution de nuget pack pour générer le fichier .nupkg](#running-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="c44c5-226">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="c44c5-227">Packages au niveau de la solution</span><span class="sxs-lookup"><span data-stu-id="c44c5-227">Solution-level packages</span></span>

<span data-ttu-id="c44c5-228">*NuGet 2.x uniquement. Non disponible dans NuGet 3.0+.*</span><span class="sxs-lookup"><span data-stu-id="c44c5-228">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="c44c5-229">NuGet 2.x prenait en charge la notion de package au niveau de la solution qui permettait d’installer des outils ou des commandes supplémentaires pour la console du gestionnaire de package (contenu du dossier `tools`), sans ajouter de références, de contenu, ni générer des personnalisations pour les projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="c44c5-229">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="c44c5-230">De tels packages ne contiennent aucun fichier dans leurs dossiers `lib`, `content` ou `build` directs et aucune de leurs dépendances n’ont des fichiers dans leurs dossiers `lib`, `content` ou `build` respectifs.</span><span class="sxs-lookup"><span data-stu-id="c44c5-230">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="c44c5-231">NuGet assure le suivi des packages installés au niveau de la solution dans un fichier `packages.config` du dossier `.nuget`, au lieu du fichier `packages.config` du projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-231">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="c44c5-232">Nouveau fichier avec des valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="c44c5-232">New file with default values</span></span>

<span data-ttu-id="c44c5-233">La commande suivante crée un manifeste par défaut avec des espaces réservés, ce qui vous permet d’être sûr de commencer avec la structure de fichiers appropriée :</span><span class="sxs-lookup"><span data-stu-id="c44c5-233">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="c44c5-234">Si vous omettez le \<nom_du_package\>, le fichier obtenu est `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-234">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="c44c5-235">Si vous fournissez un nom comme `Contoso.Utility.UsefulStuff`, le fichier est `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-235">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="c44c5-236">Le fichier `.nuspec` obtenu contient des espaces réservés pour des valeurs telles que `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-236">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="c44c5-237">Veillez à modifier le fichier avant de l’utiliser pour créer le fichier `.nupkg` final.</span><span class="sxs-lookup"><span data-stu-id="c44c5-237">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="c44c5-238">Choix d’un identificateur de package unique et définition du numéro de version</span><span class="sxs-lookup"><span data-stu-id="c44c5-238">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="c44c5-239">L’identificateur de package (élément `<id>`) et le numéro de version (élément `<version>`) sont les deux valeurs les plus importantes dans le manifeste, car ils identifient de façon unique le code exact contenu dans le package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-239">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="c44c5-240">**Bonnes pratiques en matière d’identificateur de package :**</span><span class="sxs-lookup"><span data-stu-id="c44c5-240">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="c44c5-241">**Unicité** : l’identificateur doit être unique sur nuget.org ou dans la galerie qui héberge le package, quelle qu’elle soit.</span><span class="sxs-lookup"><span data-stu-id="c44c5-241">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="c44c5-242">Avant de déterminer un identificateur, faites une recherche dans la galerie applicable pour vérifier si le nom est déjà en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="c44c5-242">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="c44c5-243">Pour éviter les conflits, utilisez le nom de votre société comme première partie de l’identificateur, par exemple `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-243">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="c44c5-244">**Noms comme les espaces de noms** : suivez un modèle similaire aux espaces de noms dans .NET, en utilisant la notation à points au lieu de traits d’union.</span><span class="sxs-lookup"><span data-stu-id="c44c5-244">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="c44c5-245">Par exemple, utilisez `Contoso.Utility.UsefulStuff` plutôt que `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-245">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="c44c5-246">Les consommateurs trouvent également pratique de faire correspondre l’identificateur du package aux espaces de noms utilisés dans le code.</span><span class="sxs-lookup"><span data-stu-id="c44c5-246">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="c44c5-247">**Exemples de package** : si vous produisez un package d’exemple de code qui montre comment utiliser un autre package, attachez `.Sample` comme suffixe à l’identificateur, comme dans `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-247">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="c44c5-248">(L’exemple de package dépend naturellement de l’autre package.) Lorsque vous créez un exemple de package, utilisez la méthode du répertoire de travail basé sur une convention décrite précédemment.</span><span class="sxs-lookup"><span data-stu-id="c44c5-248">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="c44c5-249">Dans le dossier `content`, réorganisez l’exemple de code dans un dossier appelé `\Samples\<identifier>` comme dans `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-249">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="c44c5-250">**Bonnes pratiques en matière de version de package :**</span><span class="sxs-lookup"><span data-stu-id="c44c5-250">**Best practices for the package version:**</span></span>

- <span data-ttu-id="c44c5-251">En général, définissez la version du package pour qu’elle corresponde à la bibliothèque, bien que cela ne soit pas strictement obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c44c5-251">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="c44c5-252">C’est très simple lorsque vous limitez un package à un seul assembly, comme décrit précédemment dans [Déterminer quels assemblys empaqueter](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="c44c5-252">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="c44c5-253">Globalement, n’oubliez pas que NuGet lui-même traire les versions de package lors de la résolution des dépendances, pas les versions d’assembly.</span><span class="sxs-lookup"><span data-stu-id="c44c5-253">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="c44c5-254">Lorsque vous utilisez un schéma de version non standard, veillez à prendre en compte les règles de gestion de versions NuGet, comme expliqué dans [Gestion des versions de package](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-254">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="c44c5-255">Les séries suivantes de courts billets de blog s’avèrent également utiles pour comprendre la gestion de versions :</span><span class="sxs-lookup"><span data-stu-id="c44c5-255">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="c44c5-256">Partie 1 : Affronter les difficultés liées aux DLL</span><span class="sxs-lookup"><span data-stu-id="c44c5-256">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="c44c5-257">Partie 2 : L’algorithme principal</span><span class="sxs-lookup"><span data-stu-id="c44c5-257">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="c44c5-258">Partie 3 : Unification par le biais de redirections de liaison</span><span class="sxs-lookup"><span data-stu-id="c44c5-258">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="c44c5-259">Définition d’un type de package</span><span class="sxs-lookup"><span data-stu-id="c44c5-259">Setting a package type</span></span>

<span data-ttu-id="c44c5-260">Avec NuGet 3.5+, les packages peuvent être marqués avec un *type de package* spécifique pour indiquer leur usage prévu.</span><span class="sxs-lookup"><span data-stu-id="c44c5-260">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="c44c5-261">Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.</span><span class="sxs-lookup"><span data-stu-id="c44c5-261">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="c44c5-262">Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).</span><span class="sxs-lookup"><span data-stu-id="c44c5-262">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="c44c5-263">Les packages de type `DotnetCliTool` sont des extensions de l’[interface de ligne de commande .NET](/dotnet/articles/core/tools/index) et ils sont appelés à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="c44c5-263">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="c44c5-264">De tels packages peuvent être installés uniquement dans des projets .NET Core et n’ont aucun effet sur les opérations de restauration.</span><span class="sxs-lookup"><span data-stu-id="c44c5-264">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="c44c5-265">Plus d’informations sur ces extensions par projet sont disponibles dans la documentation [Extensibilité de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="c44c5-265">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="c44c5-266">Les packages de type personnalisé utilisent un identificateur de type arbitraire qui respecte les mêmes règles de format que les ID de package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-266">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="c44c5-267">Tous les types autres que `Dependency` et `DotnetCliTool`, en revanche, ne sont pas reconnus par le gestionnaire de package NuGet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c44c5-267">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="c44c5-268">Les types de package sont définis dans le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-268">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="c44c5-269">Il est préférable pour la compatibilité descendante de ne *pas* définir explicitement le type `Dependency` et de plutôt compter sur le fait que NuGet supposera qu’il s’agit de ce type quand aucun type n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="c44c5-269">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="c44c5-270">`.nuspec` : indique le type de package dans un nœud `packageTypes\packageType` sous l’élément `<metadata>` :</span><span class="sxs-lookup"><span data-stu-id="c44c5-270">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="c44c5-271">Ajout d’un fichier Lisez-moi et d’autres fichiers</span><span class="sxs-lookup"><span data-stu-id="c44c5-271">Adding a readme and other files</span></span>

<span data-ttu-id="c44c5-272">Pour spécifier directement les fichiers à inclure dans le package, utilisez le nœud `<files>` dans le fichier `.nuspec`, ce qui *suit* la balise `<metadata>` :</span><span class="sxs-lookup"><span data-stu-id="c44c5-272">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="c44c5-273">Lorsque vous utilisez la méthode du répertoire de travail basé sur une convention, vous pouvez placer le fichier Lisez-moi.txt à la racine du package et le reste du contenu dans le dossier `content`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-273">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="c44c5-274">Aucun élément `<file>` n’est nécessaire dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="c44c5-274">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="c44c5-275">Lorsque vous incluez un fichier nommé `readme.txt` à la racine du package, Visual Studio affiche le contenu de ce fichier sous forme de texte brut immédiatement après avoir installé le package directement.</span><span class="sxs-lookup"><span data-stu-id="c44c5-275">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="c44c5-276">(Les fichiers Lisez-moi ne s’affichent pas pour les packages installés en tant que dépendances).</span><span class="sxs-lookup"><span data-stu-id="c44c5-276">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="c44c5-277">Par exemple, voici comment s’affiche le fichier Lisez-moi du package HtmlAgilityPack :</span><span class="sxs-lookup"><span data-stu-id="c44c5-277">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Affichage d’un fichier Lisez-moi pour un package NuGet lors de l’installation](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="c44c5-279">Si vous incluez un nœud `<files>` vide dans le fichier `.nuspec`, NuGet n’inclut aucun autre contenu dans le package autre que celui du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-279">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="c44c5-280">Inclusion de cibles et de propriétés MSBuild dans un package</span><span class="sxs-lookup"><span data-stu-id="c44c5-280">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="c44c5-281">Vous pouvez être amené à ajouter des cibles ou propriétés de build personnalisées dans les projets qui utilisent votre package, comme dans le cas de l’exécution d’un processus ou outil personnalisé pendant la génération.</span><span class="sxs-lookup"><span data-stu-id="c44c5-281">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="c44c5-282">Pour cela, vous placez les fichiers sous la forme de `<package_id>.targets` ou `<package_id>.props` (par exemple, `Contoso.Utility.UsefulStuff.targets`) dans le dossier `\build` du projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-282">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="c44c5-283">Les fichiers inclus dans le dossier `\build` racine sont considérés comme appropriés à toutes les versions cibles de .Net Framework.</span><span class="sxs-lookup"><span data-stu-id="c44c5-283">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="c44c5-284">Pour fournir des fichiers spécifiques au framework, commencez par les placer dans les sous-dossiers appropriés, notamment :</span><span class="sxs-lookup"><span data-stu-id="c44c5-284">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="c44c5-285">Ensuite, dans le fichier `.nuspec`, veillez à faire référence à ces fichiers dans le nœud `<files>` :</span><span class="sxs-lookup"><span data-stu-id="c44c5-285">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="c44c5-286">L’inclusion des propriétés et des cibles MSBuild dans un package a été [introduite avec NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). Il est donc recommandé d’ajouter l’attribut `minClientVersion="2.5"` à l’élément `metadata` pour indiquer la version minimale du client NuGet nécessaire pour utiliser le package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-286">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="c44c5-287">Quand NuGet installe un package avec des fichiers `\build`, il ajoute des éléments `<Import>` MSBuild au fichier projet pointant vers les fichiers `.targets` et `.props`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-287">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="c44c5-288">(`.props` est ajouté en haut du fichier projet. `.targets` est ajouté en bas.) Un élément `<Import>` MSBuild conditionnel distinct est ajouté pour chaque version cible de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c44c5-288">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="c44c5-289">Les fichiers `.props` et `.targets` MSBuild du ciblage multi-infrastructure peuvent être placés dans le dossier `\buildCrossTargeting`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-289">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="c44c5-290">Lors de l’installation de package, NuGet ajoute les éléments `<Import>` correspondants au fichier projet à la condition que la version cible de .NET Framework ne soit pas définie (la propriété MSBuild `$(TargetFramework)` doit être vide).</span><span class="sxs-lookup"><span data-stu-id="c44c5-290">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="c44c5-291">Avec NuGet 3.x, les cibles ne sont pas ajoutées au projet, mais accessibles via `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-291">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="c44c5-292">Création de packages avec des assemblys COM Interop</span><span class="sxs-lookup"><span data-stu-id="c44c5-292">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="c44c5-293">Les packages qui contiennent des assemblys COM Interop doivent inclure un [fichier de cibles](#including-msbuild-props-and-targets-in-a-package) approprié afin que les bonnes métadonnées `EmbedInteropTypes` soient ajoutées aux projets en utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c44c5-293">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="c44c5-294">Par défaut, les métadonnées `EmbedInteropTypes` sont toujours fausses pour tous les assemblys lorsque PackageReference est utilisé, si bien que le fichier de cibles ajoute ces métadonnées explicitement.</span><span class="sxs-lookup"><span data-stu-id="c44c5-294">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="c44c5-295">Pour éviter les conflits, le nom de la cible doit être unique ; dans l’idéal, utilisez une combinaison du nom de votre package et de l’assembly incorporé, en remplaçant `{InteropAssemblyName}` dans l’exemple ci-dessous par cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c44c5-295">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="c44c5-296">(Consultez également [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) pour obtenir un exemple.)</span><span class="sxs-lookup"><span data-stu-id="c44c5-296">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="c44c5-297">Notez que, si le format de gestion `packages.config` est utilisé, l’ajout de références aux assemblys à partir des packages amène NuGet et Visual Studio à rechercher des assemblys COM Interop et à affecter à `EmbedInteropTypes` la valeur true dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-297">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="c44c5-298">Dans ce cas, les cibles sont remplacées.</span><span class="sxs-lookup"><span data-stu-id="c44c5-298">In this case the targets are overriden.</span></span>

<span data-ttu-id="c44c5-299">De plus, [les ressources de build ne circulent pas de manière transitive](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) par défaut.</span><span class="sxs-lookup"><span data-stu-id="c44c5-299">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="c44c5-300">Les packages créés comme décrit ici fonctionnent différemment quand ils sont extraits en tant que dépendance transitive d’un projet vers une référence de projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-300">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="c44c5-301">Le consommateur du package peut les autoriser à circuler en modifiant la valeur par défaut PrivateAssets de sorte à ce qu’elle n’inclue pas de build.</span><span class="sxs-lookup"><span data-stu-id="c44c5-301">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="c44c5-302">Exécution de nuget pack pour générer le fichier .nupkg</span><span class="sxs-lookup"><span data-stu-id="c44c5-302">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="c44c5-303">Lorsque vous utilisez un assembly ou le répertoire de travail basé sur une convention, créez un package en exécutant `nuget pack` avec votre fichier `.nuspec`, en remplaçant `<project-name>` par votre nom de fichier spécifique :</span><span class="sxs-lookup"><span data-stu-id="c44c5-303">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="c44c5-304">Lorsque vous utilisez un projet Visual Studio, exécutez `nuget pack` avec votre fichier projet, ce qui charge automatiquement le fichier `.nuspec` du projet et remplace tous les jetons qu’il contient en utilisant les valeurs contenues dans le fichier projet :</span><span class="sxs-lookup"><span data-stu-id="c44c5-304">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="c44c5-305">Il est nécessaire d’utiliser le fichier projet directement pour le remplacement des jetons, car le projet est la source des valeurs de jeton.</span><span class="sxs-lookup"><span data-stu-id="c44c5-305">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="c44c5-306">Le remplacement des jetons ne se produit pas si vous utilisez `nuget pack` avec un fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-306">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="c44c5-307">Dans tous les cas, `nuget pack` exclut les dossiers qui commencent par un point, comme `.git` ou `.hg`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-307">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="c44c5-308">NuGet indique s’il existe des erreurs dans le fichier `.nuspec` à corriger, comme l’oubli de modifier des valeurs d’espace réservé dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="c44c5-308">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="c44c5-309">Une fois que `nuget pack` réussit, vous avez un fichier `.nupkg` que vous pouvez publier dans une galerie appropriée, comme décrit dans [Publication d’un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-309">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="c44c5-310">Une manière utile d’examiner un package après l’avoir créé consiste à l’ouvrir dans l’outil [Explorateur de package](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="c44c5-310">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="c44c5-311">Vous obtenez ainsi une vue graphique du contenu du package et de son manifeste.</span><span class="sxs-lookup"><span data-stu-id="c44c5-311">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="c44c5-312">Vous pouvez également renommer le fichier `.nupkg` obtenu en fichier `.zip` et explorer son contenu directement.</span><span class="sxs-lookup"><span data-stu-id="c44c5-312">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="c44c5-313">Options supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c44c5-313">Additional options</span></span>

<span data-ttu-id="c44c5-314">Vous pouvez utiliser divers commutateurs de ligne de commande avec `nuget pack` pour exclure des fichiers, remplacer le numéro de version dans le manifeste et modifier le dossier de sortie, entre autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="c44c5-314">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="c44c5-315">Pour en obtenir la liste complète, reportez-vous aux [informations de référence sur la commande pack](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-315">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="c44c5-316">Les options suivantes figurent parmi les quelques options communes aux projets Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="c44c5-316">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="c44c5-317">**Projets référencés** : si le projet fait référence à d’autres projets, vous pouvez ajouter les projets référencés dans le cadre du package, ou en tant que dépendances, à l’aide de l’option `-IncludeReferencedProjects` :</span><span class="sxs-lookup"><span data-stu-id="c44c5-317">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="c44c5-318">Ce processus d’inclusion est récursif, donc si `MyProject.csproj` fait référence aux projets B et C, et que ces projets font référence aux projets D, E et F, alors les fichiers de B, C, D, E et F sont inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="c44c5-318">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="c44c5-319">Si un projet référencé inclut un fichier `.nuspec` bien à lui, alors NuGet ajoute ce projet référencé plutôt en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="c44c5-319">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="c44c5-320">Vous devez empaqueter et publier ce projet séparément.</span><span class="sxs-lookup"><span data-stu-id="c44c5-320">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="c44c5-321">**Configuration de build** : par défaut, NuGet utilise la configuration de build par défaut définie dans le fichier projet, généralement *Debug*.</span><span class="sxs-lookup"><span data-stu-id="c44c5-321">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="c44c5-322">Pour compresser des fichiers d’une configuration de build différente, comme *Release*, utilisez l’option `-properties` avec la configuration :</span><span class="sxs-lookup"><span data-stu-id="c44c5-322">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="c44c5-323">**Symboles** : pour inclure les symboles qui permettent aux utilisateurs de parcourir votre code de package dans le débogueur, utilisez l’option `-Symbols` :</span><span class="sxs-lookup"><span data-stu-id="c44c5-323">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="c44c5-324">Test de l’installation du package</span><span class="sxs-lookup"><span data-stu-id="c44c5-324">Testing package installation</span></span>

<span data-ttu-id="c44c5-325">Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test.</span><span class="sxs-lookup"><span data-stu-id="c44c5-325">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="c44c5-326">Les tests permettent de s’assurer que les fichiers nécessaires se placent tous au bon endroit dans le projet.</span><span class="sxs-lookup"><span data-stu-id="c44c5-326">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="c44c5-327">Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-327">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="c44c5-328">Pour les tests automatisés, le processus de base est le suivant :</span><span class="sxs-lookup"><span data-stu-id="c44c5-328">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="c44c5-329">Copiez le fichier `.nupkg` dans un dossier local.</span><span class="sxs-lookup"><span data-stu-id="c44c5-329">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="c44c5-330">Ajoutez le dossier à vos sources de package à l’aide de la commande `nuget sources add -name <name> -source <path>` (consultez [Sources nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="c44c5-330">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="c44c5-331">Notez que vous ne devez définir cette source locale qu’une seule fois sur un ordinateur donné.</span><span class="sxs-lookup"><span data-stu-id="c44c5-331">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="c44c5-332">Installez le package à partir de cette source en utilisant `nuget install <packageID> -source <name>` où `<name>` correspond au nom de votre source tel qu’il est donné à `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="c44c5-332">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="c44c5-333">La spécification de la source permet de s’assurer que le package est installé à partir de cette source uniquement.</span><span class="sxs-lookup"><span data-stu-id="c44c5-333">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="c44c5-334">Examinez votre système de fichiers pour vérifier que les fichiers sont correctement installés.</span><span class="sxs-lookup"><span data-stu-id="c44c5-334">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c44c5-335">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c44c5-335">Next Steps</span></span>

<span data-ttu-id="c44c5-336">Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c44c5-336">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="c44c5-337">Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="c44c5-337">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="c44c5-338">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="c44c5-338">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c44c5-339">Prise en charge de plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="c44c5-339">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c44c5-340">Transformations de fichiers sources et de configuration</span><span class="sxs-lookup"><span data-stu-id="c44c5-340">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="c44c5-341">Localisation</span><span class="sxs-lookup"><span data-stu-id="c44c5-341">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="c44c5-342">Préversions</span><span class="sxs-lookup"><span data-stu-id="c44c5-342">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="c44c5-343">Enfin, il existe d’autres types de package à connaître :</span><span class="sxs-lookup"><span data-stu-id="c44c5-343">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="c44c5-344">Packages natifs</span><span class="sxs-lookup"><span data-stu-id="c44c5-344">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="c44c5-345">Packages de symboles</span><span class="sxs-lookup"><span data-stu-id="c44c5-345">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
