---
title: Multiciblage pour les packages NuGet
description: Description des différentes méthodes pour cibler plusieurs versions de .NET Framework à partir d’un seul package NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: d1a64c61954381b7ab3a7ecc8aa5a812cfa14e8b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="12de3-103">Prise en charge de plusieurs versions de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="12de3-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="12de3-104">*Pour les projets .NET Core qui utilisent NuGet 4.0 +, consultez [Commandes NuGet pack et restore en tant que cibles MSBuild](../reference/msbuild-targets.md) pour plus d’informations sur le ciblage croisé.*</span><span class="sxs-lookup"><span data-stu-id="12de3-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="12de3-105">De nombreuses bibliothèques ciblent une version spécifique de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="12de3-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="12de3-106">Par exemple, vous pouvez avoir une première version de votre bibliothèque propre à la plateforme Windows universelle (UWP) et une autre version qui exploite les fonctionnalités de .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="12de3-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="12de3-107">Pour en tenir compte, NuGet prend en charge le placement de plusieurs versions de la même bibliothèque dans un même package dans le cadre de l’utilisation de la méthode de répertoire de travail basée sur une convention décrite dans [Création d’un package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="12de3-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="12de3-108">Structure de dossiers de la version du framework</span><span class="sxs-lookup"><span data-stu-id="12de3-108">Framework version folder structure</span></span>

<span data-ttu-id="12de3-109">Lorsque vous créez un package qui contient uniquement une version d’une bibliothèque ou qui cible plusieurs frameworks, vous créez systématiquement des sous-dossiers dans le dossier `lib` en utilisant des noms de framework différents qui respectent la casse selon la convention suivante :</span><span class="sxs-lookup"><span data-stu-id="12de3-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="12de3-110">Pour obtenir la liste complète des noms pris en charge, consultez les [informations de référence sur les versions cibles de .Net Framework](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="12de3-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="12de3-111">Vous ne devez jamais avoir une version de la bibliothèque qui n’est pas propre à un framework et placée directement dans le dossier `lib` racine.</span><span class="sxs-lookup"><span data-stu-id="12de3-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="12de3-112">(Cette fonctionnalité était prise en charge uniquement avec `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="12de3-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="12de3-113">En effet, la bibliothèque serait alors compatible avec n’importe quelle version cible de .Net Framework et pourrait être installée n’importe où, entraînant des erreurs inattendues du runtime.</span><span class="sxs-lookup"><span data-stu-id="12de3-113">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="12de3-114">L’ajout d’assemblys dans le dossier racine (comme `lib\abc.dll`) ou des sous-dossiers (comme `lib\abc\abc.dll`) est déprécié et ignoré lorsque vous utilisez le format PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="12de3-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="12de3-115">Par exemple, la structure de dossiers suivante prend en charge quatre versions d’un assembly propres à un framework :</span><span class="sxs-lookup"><span data-stu-id="12de3-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="12de3-116">Pour inclure facilement tous ces fichiers lors de la génération du package, utilisez un caractère générique `**` récursif dans la section `<files>` de votre `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="12de3-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="12de3-117">Dossiers propres à l’architecture</span><span class="sxs-lookup"><span data-stu-id="12de3-117">Architecture-specific folders</span></span>

<span data-ttu-id="12de3-118">Si vous avez des assemblys propres à une architecture, autrement dit, des assemblys distincts qui ciblent ARM, x86 et x64, vous devez les placer dans un dossier nommé `runtimes` au sein de sous-dossiers nommés `{platform}-{architecture}\lib\{framework}` ou `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="12de3-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="12de3-119">Par exemple, la structure de dossiers suivante s’adapte à la fois aux DLL natives et managées ciblant Windows 10 et le framework `uap10.0` :</span><span class="sxs-lookup"><span data-stu-id="12de3-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="12de3-120">Consultez [Créer des packages UWP](../guides/create-uwp-packages.md) pour obtenir un exemple de référencement de ces fichiers dans le manifeste `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="12de3-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="12de3-121">Correspondance entre les versions d’assembly et la version cible de .Net Framework dans un projet</span><span class="sxs-lookup"><span data-stu-id="12de3-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="12de3-122">Lorsque NuGet installe un package qui a plusieurs versions d’assembly, il essaie de faire correspondre le nom du framework de l’assembly à la version cible de .Net Framework du projet.</span><span class="sxs-lookup"><span data-stu-id="12de3-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="12de3-123">Si aucune correspondance n’est trouvée, NuGet copie l’assembly de la version la plus élevée inférieure ou égale à la version cible de .Net Framework du projet, si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="12de3-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="12de3-124">Si aucun assembly compatible n’est trouvé, NuGet renvoie un message d’erreur approprié.</span><span class="sxs-lookup"><span data-stu-id="12de3-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="12de3-125">Par exemple, considérez la structure de dossiers suivante dans un package :</span><span class="sxs-lookup"><span data-stu-id="12de3-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="12de3-126">Quand vous installez ce package dans un projet qui cible .NET Framework 4.6, NuGet installe l’assembly dans le dossier `net45`, car il s’agit de la version disponible la plus élevée inférieure ou égale à 4.6.</span><span class="sxs-lookup"><span data-stu-id="12de3-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="12de3-127">D’autre part, si le projet cible .NET Framework 4.6.1, NuGet installe l’assembly dans le dossier `net461`.</span><span class="sxs-lookup"><span data-stu-id="12de3-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="12de3-128">Si le projet cible .NET framework 4.0 et des versions antérieures, NuGet envoie un message d’erreur approprié indiquant que l’assembly compatible est introuvable.</span><span class="sxs-lookup"><span data-stu-id="12de3-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="12de3-129">Regroupement d’assemblys par version du framework</span><span class="sxs-lookup"><span data-stu-id="12de3-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="12de3-130">NuGet copie des assemblys à partir d’un seul dossier de bibliothèque dans le package.</span><span class="sxs-lookup"><span data-stu-id="12de3-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="12de3-131">Par exemple, supposons qu’un package présente la structure de dossiers suivante :</span><span class="sxs-lookup"><span data-stu-id="12de3-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="12de3-132">Lorsque le package est installé dans un projet qui cible .NET Framework 4.5, `MyAssembly.dll` (v2.0) est le seul assembly installé.</span><span class="sxs-lookup"><span data-stu-id="12de3-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="12de3-133">`MyAssembly.Core.dll` (v1.0) n’est pas installé, car il n’est pas répertorié dans le dossier `net45`.</span><span class="sxs-lookup"><span data-stu-id="12de3-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="12de3-134">NuGet se comporte ainsi car `MyAssembly.Core.dll` a peut-être été fusionné dans la version 2.0 de `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="12de3-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="12de3-135">Si vous voulez que `MyAssembly.Core.dll` soit installé pour .NET Framework 4.5, placez une copie dans le dossier `net45`.</span><span class="sxs-lookup"><span data-stu-id="12de3-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="12de3-136">Regroupement d’assemblys par profil du framework</span><span class="sxs-lookup"><span data-stu-id="12de3-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="12de3-137">NuGet prend également en charge le ciblage d’un profil de framework spécifique en ajoutant un tiret et le nom du profil à la fin du dossier.</span><span class="sxs-lookup"><span data-stu-id="12de3-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="12de3-138">Les profils pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="12de3-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="12de3-139">`client` : Client Profile</span><span class="sxs-lookup"><span data-stu-id="12de3-139">`client`: Client Profile</span></span>
- <span data-ttu-id="12de3-140">`full` : Full Profile</span><span class="sxs-lookup"><span data-stu-id="12de3-140">`full`: Full Profile</span></span>
- <span data-ttu-id="12de3-141">`wp` : Windows Phone</span><span class="sxs-lookup"><span data-stu-id="12de3-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="12de3-142">`cf` : Compact Framework</span><span class="sxs-lookup"><span data-stu-id="12de3-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="12de3-143">Détermination de la cible NuGet à utiliser</span><span class="sxs-lookup"><span data-stu-id="12de3-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="12de3-144">Lorsque vous empaquetez des bibliothèques ciblant la bibliothèque de classes portable, il peut être difficile de déterminer quelle cible NuGet vous devez utiliser dans vos noms de dossier et votre fichier `.nuspec`, en particulier si vous ciblez uniquement un sous-ensemble de la bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="12de3-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="12de3-145">Les ressources externes suivantes peuvent vous aider à la déterminer :</span><span class="sxs-lookup"><span data-stu-id="12de3-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="12de3-146">[Profils de framework dans .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="12de3-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="12de3-147">[Profils de la bibliothèque de classes portable](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co) : tableau qui énumère les profils de la bibliothèque de classes portable et leurs cibles NuGet équivalentes</span><span class="sxs-lookup"><span data-stu-id="12de3-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="12de3-148">[Outil des profils de la bibliothèque de classes portable](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com) : outil en ligne de commande permettant de déterminer les profils de la bibliothèque de classes portable disponibles sur votre système</span><span class="sxs-lookup"><span data-stu-id="12de3-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="12de3-149">Fichiers de contenu et scripts PowerShell</span><span class="sxs-lookup"><span data-stu-id="12de3-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="12de3-150">Des fichiers de contenu mutables et une exécution des scripts sont disponibles au format `packages.config` uniquement ; ils sont dépréciés avec tous les autres des formats et ne doivent pas être utilisés pour de nouveaux packages.</span><span class="sxs-lookup"><span data-stu-id="12de3-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="12de3-151">Avec `packages.config`, il est possible de regrouper les fichiers de contenu et les scripts PowerShell par version cible de .Net Framework en utilisant la même convention de dossier à l’intérieur des dossiers `content` et `tools`.</span><span class="sxs-lookup"><span data-stu-id="12de3-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="12de3-152">Exemple :</span><span class="sxs-lookup"><span data-stu-id="12de3-152">For example:</span></span>

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

<span data-ttu-id="12de3-153">Si un dossier de framework est vide, NuGet n’y ajoute pas de références d’assembly ni de fichiers de contenu ou n’exécute pas les scripts PowerShell pour ce framework.</span><span class="sxs-lookup"><span data-stu-id="12de3-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="12de3-154">Étant donné que `init.ps1` s’exécute au niveau de la solution et ne dépend pas du projet, il doit être placé directement sous le dossier `tools`.</span><span class="sxs-lookup"><span data-stu-id="12de3-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="12de3-155">Ce fichier est ignoré s’il est placé sous un dossier de framework.</span><span class="sxs-lookup"><span data-stu-id="12de3-155">It's ignored if placed under a framework folder.</span></span>
