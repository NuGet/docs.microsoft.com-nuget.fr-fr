---
title: Multiciblage pour les packages NuGet
description: Description des différentes méthodes pour cibler plusieurs versions de .NET Framework à partir d’un seul package NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 4413779361dad3a650da36b3c69bbb55b62804ee
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380733"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="bf0dd-103">Prendre en charge plusieurs versions de .NET</span><span class="sxs-lookup"><span data-stu-id="bf0dd-103">Support multiple .NET versions</span></span>

<span data-ttu-id="bf0dd-104">De nombreuses bibliothèques ciblent une version spécifique de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="bf0dd-105">Par exemple, vous pouvez avoir une première version de votre bibliothèque propre à la plateforme Windows universelle (UWP) et une autre version qui exploite les fonctionnalités de .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="bf0dd-106">Pour ce faire, NuGet prend en charge le placement de plusieurs versions de la même bibliothèque dans un package unique.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="bf0dd-107">Cet article décrit la disposition d’un package NuGet, quelle que soit la façon dont le package ou les assemblys sont générés (c’est-à-dire que la disposition est la même, que vous utilisiez plusieurs fichiers *. csproj* non-SDK et un fichier *. NuSpec* personnalisé, ou un seul fichier multiciblé SDK-style *. csproj*).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="bf0dd-108">Pour un projet SDK-style, les [cibles de packs](../reference/msbuild-targets.md) NuGet savent comment le package doit être disposé, automatisent le placement des assemblys dans les dossiers de bibliothèque corrects et créent des groupes de dépendances pour chaque framework cible (TFM).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="bf0dd-109">Pour des instructions détaillées, consultez [Prendre en charge plusieurs versions de .NET Framework](multiple-target-frameworks-project-file.md) dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="bf0dd-110">Vous devez disposer manuellement le package comme décrit dans cet article lorsque vous utilisez la méthode de répertoire de travail basée sur une convention décrite dans [Création d’un package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="bf0dd-111">Pour un projet SDK-style, la méthode automatisée est recommandée, mais vous pouvez également choisir de disposer manuellement le package comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="bf0dd-112">Structure de dossiers de la version du framework</span><span class="sxs-lookup"><span data-stu-id="bf0dd-112">Framework version folder structure</span></span>

<span data-ttu-id="bf0dd-113">Lorsque vous créez un package qui contient uniquement une version d’une bibliothèque ou qui cible plusieurs frameworks, vous créez systématiquement des sous-dossiers dans le dossier `lib` en utilisant des noms de framework différents qui respectent la casse selon la convention suivante :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="bf0dd-114">Pour obtenir la liste complète des noms pris en charge, consultez les [informations de référence sur les versions cibles de .Net Framework](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="bf0dd-115">Vous ne devez jamais avoir une version de la bibliothèque qui n’est pas propre à un framework et placée directement dans le dossier `lib` racine.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="bf0dd-116">(Cette fonctionnalité était prise en charge uniquement avec `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="bf0dd-117">En effet, la bibliothèque serait alors compatible avec n’importe quelle version cible de .Net Framework et pourrait être installée n’importe où, entraînant des erreurs inattendues du runtime.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="bf0dd-118">L’ajout d’assemblys dans le dossier racine (comme `lib\abc.dll`) ou des sous-dossiers (comme `lib\abc\abc.dll`) est déprécié et ignoré lorsque vous utilisez le format PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="bf0dd-119">Par exemple, la structure de dossiers suivante prend en charge quatre versions d’un assembly propres à un framework :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="bf0dd-120">Pour inclure facilement tous ces fichiers lors de la génération du package, utilisez un caractère générique `**` récursif dans la section `<files>` de votre `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="bf0dd-121">Dossiers propres à l’architecture</span><span class="sxs-lookup"><span data-stu-id="bf0dd-121">Architecture-specific folders</span></span>

<span data-ttu-id="bf0dd-122">Si vous avez des assemblys propres à une architecture, autrement dit, des assemblys distincts qui ciblent ARM, x86 et x64, vous devez les placer dans un dossier nommé `runtimes` au sein de sous-dossiers nommés `{platform}-{architecture}\lib\{framework}` ou `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="bf0dd-123">Par exemple, la structure de dossiers suivante s’adapte à la fois aux DLL natives et managées ciblant Windows 10 et le framework `uap10.0` :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="bf0dd-124">Ces assemblys sont disponibles uniquement au moment de l’exécution. Si vous souhaitez fournir l’assembly correspondant au moment de la compilation, indiquez l’assembly `AnyCPU` dans le dossier `/ref/{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="bf0dd-125">Notez que NuGet choisit toujours ces ressources de compilation ou d’exécution dans un seul dossier. Si des ressources compatibles se trouvent dans `/ref`, `/lib` est donc ignoré lors de l’ajout d’assemblys au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="bf0dd-126">De même, s’il existe des éléments compatibles de `/runtime`, alors également `/lib` seront ignorés pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-126">Similarly, if there are some compatible assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="bf0dd-127">Consultez [Créer des packages UWP](../guides/create-uwp-packages.md) pour obtenir un exemple de référencement de ces fichiers dans le manifeste `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="bf0dd-128">Consultez également [Empaquetage d’un composant d’application Windows Store avec NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="bf0dd-129">Correspondance entre les versions d’assembly et la version cible de .Net Framework dans un projet</span><span class="sxs-lookup"><span data-stu-id="bf0dd-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="bf0dd-130">Lorsque NuGet installe un package qui a plusieurs versions d’assembly, il essaie de faire correspondre le nom du framework de l’assembly à la version cible de .Net Framework du projet.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="bf0dd-131">Si aucune correspondance n’est trouvée, NuGet copie l’assembly de la version la plus élevée inférieure ou égale à la version cible de .Net Framework du projet, si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="bf0dd-132">Si aucun assembly compatible n’est trouvé, NuGet renvoie un message d’erreur approprié.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="bf0dd-133">Par exemple, considérez la structure de dossiers suivante dans un package :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="bf0dd-134">Quand vous installez ce package dans un projet qui cible .NET Framework 4.6, NuGet installe l’assembly dans le dossier `net45`, car il s’agit de la version disponible la plus élevée inférieure ou égale à 4.6.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="bf0dd-135">D’autre part, si le projet cible .NET Framework 4.6.1, NuGet installe l’assembly dans le dossier `net461`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="bf0dd-136">Si le projet cible .NET framework 4.0 et des versions antérieures, NuGet envoie un message d’erreur approprié indiquant que l’assembly compatible est introuvable.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="bf0dd-137">Regroupement d’assemblys par version du framework</span><span class="sxs-lookup"><span data-stu-id="bf0dd-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="bf0dd-138">NuGet copie des assemblys à partir d’un seul dossier de bibliothèque dans le package.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="bf0dd-139">Par exemple, supposons qu’un package présente la structure de dossiers suivante :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="bf0dd-140">Lorsque le package est installé dans un projet qui cible .NET Framework 4.5, `MyAssembly.dll` (v2.0) est le seul assembly installé.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="bf0dd-141">`MyAssembly.Core.dll` (v1.0) n’est pas installé, car il n’est pas répertorié dans le dossier `net45`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="bf0dd-142">NuGet se comporte ainsi car `MyAssembly.Core.dll` a peut-être été fusionné dans la version 2.0 de `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="bf0dd-143">Si vous voulez que `MyAssembly.Core.dll` soit installé pour .NET Framework 4.5, placez une copie dans le dossier `net45`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="bf0dd-144">Regroupement d’assemblys par profil du framework</span><span class="sxs-lookup"><span data-stu-id="bf0dd-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="bf0dd-145">NuGet prend également en charge le ciblage d’un profil de framework spécifique en ajoutant un tiret et le nom du profil à la fin du dossier.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="bf0dd-146">Les profils pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="bf0dd-147">`client` : Client Profile</span><span class="sxs-lookup"><span data-stu-id="bf0dd-147">`client`: Client Profile</span></span>
- <span data-ttu-id="bf0dd-148">`full` : Full Profile</span><span class="sxs-lookup"><span data-stu-id="bf0dd-148">`full`: Full Profile</span></span>
- <span data-ttu-id="bf0dd-149">`wp` : Windows Phone</span><span class="sxs-lookup"><span data-stu-id="bf0dd-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="bf0dd-150">`cf` : Compact Framework</span><span class="sxs-lookup"><span data-stu-id="bf0dd-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="bf0dd-151">Déclaration de dépendances (avancée)</span><span class="sxs-lookup"><span data-stu-id="bf0dd-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="bf0dd-152">Lors de la compression d’un fichier projet, NuGet tente de générer automatiquement les dépendances à partir du projet.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="bf0dd-153">Les informations de cette section sur l’utilisation d’un fichier *.nuspec* pour déclarer des dépendances sont généralement nécessaires pour des scénarios avancés uniquement.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="bf0dd-154">*(Version 2.0 +)* Vous pouvez déclarer des dépendances de package dans le fichier *.nuspec* correspondant au à la version cible de .Net Framework à l’aide d’éléments `<group>` au sein de l’élément `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="bf0dd-155">Pour plus d'informations, consultez [Éléments de dépendances](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="bf0dd-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="bf0dd-156">Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="bf0dd-157">Ces dépendances sont installées ensemble quand la version cible de .Net Framework est compatible avec le profil de framework du projet.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="bf0dd-158">Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="bf0dd-159">Nous vous recommandons d’utiliser un groupe par moniker de framework cible (TFM) pour les fichiers dans les dossiers  *lib/* et *ref/* .</span><span class="sxs-lookup"><span data-stu-id="bf0dd-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="bf0dd-160">L’exemple suivant illustre différentes variantes de l’élément `<group>` :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="bf0dd-161">Détermination de la cible NuGet à utiliser</span><span class="sxs-lookup"><span data-stu-id="bf0dd-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="bf0dd-162">Lorsque vous empaquetez des bibliothèques ciblant la bibliothèque de classes portable, il peut être difficile de déterminer quelle cible NuGet vous devez utiliser dans vos noms de dossier et votre fichier `.nuspec`, en particulier si vous ciblez uniquement un sous-ensemble de la bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="bf0dd-163">Les ressources externes suivantes peuvent vous aider à la déterminer :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="bf0dd-164">[Profils de framework dans .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="bf0dd-164">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="bf0dd-165">[Profils de la bibliothèque de classes portable](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co) : tableau qui énumère les profils de la bibliothèque de classes portable et leurs cibles NuGet équivalentes</span><span class="sxs-lookup"><span data-stu-id="bf0dd-165">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="bf0dd-166">[Outil des profils de la bibliothèque de classes portable](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com) : outil en ligne de commande permettant de déterminer les profils de la bibliothèque de classes portable disponibles sur votre système</span><span class="sxs-lookup"><span data-stu-id="bf0dd-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="bf0dd-167">Fichiers de contenu et scripts PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf0dd-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="bf0dd-168">Des fichiers de contenu mutables et une exécution des scripts sont disponibles au format `packages.config` uniquement ; ils sont dépréciés avec tous les autres des formats et ne doivent pas être utilisés pour de nouveaux packages.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="bf0dd-169">Avec `packages.config`, il est possible de regrouper les fichiers de contenu et les scripts PowerShell par version cible de .Net Framework en utilisant la même convention de dossier à l’intérieur des dossiers `content` et `tools`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="bf0dd-170">Exemple :</span><span class="sxs-lookup"><span data-stu-id="bf0dd-170">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="bf0dd-171">Si un dossier de framework est vide, NuGet n’y ajoute pas de références d’assembly ni de fichiers de contenu ou n’exécute pas les scripts PowerShell pour ce framework.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="bf0dd-172">Étant donné que `init.ps1` s’exécute au niveau de la solution et ne dépend pas du projet, il doit être placé directement sous le dossier `tools`.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="bf0dd-173">Ce fichier est ignoré s’il est placé sous un dossier de framework.</span><span class="sxs-lookup"><span data-stu-id="bf0dd-173">It's ignored if placed under a framework folder.</span></span>
