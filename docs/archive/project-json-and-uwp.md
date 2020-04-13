---
title: Fichier project.json NuGet avec les projets UWP
description: Description de la façon dont le fichier project.json est utilisé pour suivre les dépendances NuGet dans les projets de plateforme Windows universelle (UWP).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494368"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="02800-103">project.json et UWP</span><span class="sxs-lookup"><span data-stu-id="02800-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="02800-104">Ce contenu est déconseillé.</span><span class="sxs-lookup"><span data-stu-id="02800-104">This content is deprecated.</span></span> <span data-ttu-id="02800-105">Les projets doivent utiliser soit le format `packages.config`, soit le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="02800-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="02800-106">Ce document décrit la structure du package qui utilise les fonctionnalités de NuGet 3+ (Visual Studio 2015 et versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="02800-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="02800-107">La propriété `minClientVersion` de votre `.nuspec` peut être utilisée pour indiquer que vous avez besoin des fonctionnalités décrites ici en lui affectant la valeur 3.1.</span><span class="sxs-lookup"><span data-stu-id="02800-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="02800-108">Ajout de la prise en charge de la plateforme Windows universelle à un package existant</span><span class="sxs-lookup"><span data-stu-id="02800-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="02800-109">Si vous disposez d’un package existant et que vous souhaitez ajouter la prise en charge des applications de la plateforme Windows universelle (UWP), alors vous n’avez pas besoin d’adopter le format d’empaquetage décrit ici.</span><span class="sxs-lookup"><span data-stu-id="02800-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="02800-110">Vous devez uniquement adopter ce format si vous avez besoin des fonctionnalités qu’il décrit et que vous voulez travailler uniquement avec les clients qui ont effectué une mise à jour vers la version 3+ du client NuGet.</span><span class="sxs-lookup"><span data-stu-id="02800-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="02800-111">Je cible déjà netcore45</span><span class="sxs-lookup"><span data-stu-id="02800-111">I already target netcore45</span></span>

<span data-ttu-id="02800-112">Si vous ciblez déjà `netcore45` et que vous n’avez pas besoin des fonctionnalités décrites ici, aucune action n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="02800-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="02800-113">Les packages `netcore45` peuvent être consommés par les applications UWP.</span><span class="sxs-lookup"><span data-stu-id="02800-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="02800-114">Je veux exploiter les API spécifiques de Windows 10</span><span class="sxs-lookup"><span data-stu-id="02800-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="02800-115">Dans ce cas, vous devez ajouter le moniker de la version cible de .Net Framework `uap10.0` (TFM ou TxM) à votre package.</span><span class="sxs-lookup"><span data-stu-id="02800-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="02800-116">Créez un dossier dans votre package et ajoutez l’assembly qui a été compilé pour utiliser Windows 10 dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="02800-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="02800-117">Je n’ai pas besoin des API spécifiques de Windows 10, mais je veux utiliser les nouvelles fonctionnalités .NET ou je n’ai pas encore netcore45</span><span class="sxs-lookup"><span data-stu-id="02800-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="02800-118">Dans ce cas, ajoutez le TxM `dotnet` à votre package.</span><span class="sxs-lookup"><span data-stu-id="02800-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="02800-119">Contrairement aux autres TxM, `dotnet` n’implique pas de surface d’exposition ni de plateforme.</span><span class="sxs-lookup"><span data-stu-id="02800-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="02800-120">Il indique que votre package fonctionne sur n’importe quelle plateforme sur laquelle vos dépendances fonctionnent.</span><span class="sxs-lookup"><span data-stu-id="02800-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="02800-121">Lors de la `dotnet` construction d’un paquet avec le TxM, vous êtes `.nuspec`susceptible d’avoir beaucoup plus de dépendances `System.Text`TxM spécifiques dans votre , que vous devez définir les paquets BCL dont vous dépendez, tels, , `System.Xml`, etc. Les emplacements sur lesquelles ces dépendances fonctionnent définissent l’endroit où votre colis fonctionne.</span><span class="sxs-lookup"><span data-stu-id="02800-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="02800-122">Comment trouver mes dépendances</span><span class="sxs-lookup"><span data-stu-id="02800-122">How do I find out my dependencies</span></span>

<span data-ttu-id="02800-123">Il existe deux façons de déterminer les dépendances à répertorier :</span><span class="sxs-lookup"><span data-stu-id="02800-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="02800-124">Utilisez l’outil [Générateur de dépendances NuSpec](https://github.com/onovotny/ReferenceGenerator) **tiers**.</span><span class="sxs-lookup"><span data-stu-id="02800-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="02800-125">Cet outil automatise le processus et met à jour votre fichier `.nuspec` avec les packages dépendants pendant la génération.</span><span class="sxs-lookup"><span data-stu-id="02800-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="02800-126">Il est disponible par le biais d’un package NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="02800-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="02800-127">(Méthode plus difficile) Utilisez `ILDasm` pour examiner votre `.dll` pour voir quels assemblys sont en fait nécessaires au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="02800-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="02800-128">Déterminez ensuite de quel package NuGet ils proviennent.</span><span class="sxs-lookup"><span data-stu-id="02800-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="02800-129">Consultez [`project.json`](project-json.md) le sujet pour plus de détails sur les `dotnet` fonctionnalités qui aident à la création d’un paquet qui prend en charge le TxM.</span><span class="sxs-lookup"><span data-stu-id="02800-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="02800-130">Si votre package est prévu pour fonctionner avec des projets de la bibliothèque de classes portables, nous vous recommandons fortement de créer un dossier `dotnet`, pour éviter les avertissements et les éventuels problèmes de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="02800-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="02800-131">Structure de répertoires</span><span class="sxs-lookup"><span data-stu-id="02800-131">Directory structure</span></span>

<span data-ttu-id="02800-132">Les packages NuGet qui utilisent ce format ont le dossier et les comportements connus suivants :</span><span class="sxs-lookup"><span data-stu-id="02800-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="02800-133">Dossier</span><span class="sxs-lookup"><span data-stu-id="02800-133">Folder</span></span> | <span data-ttu-id="02800-134">Comportements</span><span class="sxs-lookup"><span data-stu-id="02800-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="02800-135">Build</span><span class="sxs-lookup"><span data-stu-id="02800-135">Build</span></span> | <span data-ttu-id="02800-136">Contient des fichiers de cibles et de propriétés MSBuild dans ce dossier qui sont intégrées différemment au projet, mais à part cela, il n’y a aucun changement.</span><span class="sxs-lookup"><span data-stu-id="02800-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="02800-137">Outils</span><span class="sxs-lookup"><span data-stu-id="02800-137">Tools</span></span> | <span data-ttu-id="02800-138">`install.ps1` et `uninstall.ps1` ne sont pas exécutés.</span><span class="sxs-lookup"><span data-stu-id="02800-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="02800-139">`init.ps1` fonctionne comme il l’a toujours fait.</span><span class="sxs-lookup"><span data-stu-id="02800-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="02800-140">Contenu</span><span class="sxs-lookup"><span data-stu-id="02800-140">Content</span></span> | <span data-ttu-id="02800-141">Le contenu n’est pas copié automatiquement dans le projet de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="02800-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="02800-142">Une prise en charge de l’inclusion de contenu dans le projet est prévue dans une prochaine version.</span><span class="sxs-lookup"><span data-stu-id="02800-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="02800-143">Lib</span><span class="sxs-lookup"><span data-stu-id="02800-143">Lib</span></span> | <span data-ttu-id="02800-144">Pour de nombreux packages, le dossier `lib` fonctionne de la même manière que dans NuGet 2.x, mais avec des options étendues pour les noms utilisables et une meilleure logique pour récupérer le sous-dossier approprié lors de la consommation de packages.</span><span class="sxs-lookup"><span data-stu-id="02800-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="02800-145">Toutefois, lorsqu’il est utilisé conjointement avec `ref`, le dossier `lib` contient les assemblys qui implémentent la surface d’exposition définie par les assemblys inclus dans le dossier `ref`.</span><span class="sxs-lookup"><span data-stu-id="02800-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="02800-146">Ref</span><span class="sxs-lookup"><span data-stu-id="02800-146">Ref</span></span> | <span data-ttu-id="02800-147">`ref` est un dossier facultatif qui contient des assemblys .NET définissant la surface publique (types et méthodes publics) sur laquelle se compile une application.</span><span class="sxs-lookup"><span data-stu-id="02800-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="02800-148">Les assemblys inclus dans ce dossier n’ont peut-être aucune implémentation, ils sont purement utilisés pour définir la surface d’exposition du compilateur.</span><span class="sxs-lookup"><span data-stu-id="02800-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="02800-149">Si le package n’a pas de dossier `ref`, alors le dossier `lib` est à la fois l’assembly de référence et l’assembly d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="02800-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="02800-150">Runtimes</span><span class="sxs-lookup"><span data-stu-id="02800-150">Runtimes</span></span> | <span data-ttu-id="02800-151">Le dossier `runtimes` est un dossier facultatif qui contient du code spécifique du système d’exploitation, comme l’architecture du processeur et d’autres fichiers binaires dépendant de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="02800-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="02800-152">Fichiers de cibles et de propriétés MSBuild dans des packages</span><span class="sxs-lookup"><span data-stu-id="02800-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="02800-153">Les packages NuGet peuvent contenir des fichiers `.targets` et `.props` importés dans un projet MSBuild dans lequel le package est installé.</span><span class="sxs-lookup"><span data-stu-id="02800-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="02800-154">Dans NuGet 2.x, il fallait injecter des instructions `<Import>` dans le fichier `.csproj` pour cela. Dans NuGet 3.0, il n’y a pas d’action d’« installation dans le projet » spécifique.</span><span class="sxs-lookup"><span data-stu-id="02800-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="02800-155">Le processus de restauration du package écrit plutôt deux fichiers `[projectname].nuget.props` et `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="02800-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="02800-156">MSBuild sait rechercher ces deux fichiers et les importe automatiquement au début et à la fin du processus de génération du projet.</span><span class="sxs-lookup"><span data-stu-id="02800-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="02800-157">Ce comportement est très similaire à celui de NuGet 2.x, avec une différence majeure : *l’ordre des fichiers de cibles/propriétés n’est pas garanti dans ce cas*.</span><span class="sxs-lookup"><span data-stu-id="02800-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="02800-158">Toutefois, MSBuild offre des moyens de définir l’ordre des cibles par le biais des attributs `BeforeTargets` et `AfterTargets` de la définition `<Target>` (consultez [Target, élément (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="02800-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="02800-159">Lib et Ref</span><span class="sxs-lookup"><span data-stu-id="02800-159">Lib and Ref</span></span>

<span data-ttu-id="02800-160">Le comportement du dossier `lib` n’a pas changé de manière significative dans NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="02800-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="02800-161">En revanche, tous les assemblys doivent se trouver dans des sous-dossiers nommés comme un TxM. Ils ne peuvent plus être placés directement sous le dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="02800-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="02800-162">Un TxM est le nom d’une plateforme pour laquelle une ressource donnée dans un package est supposée travailler.</span><span class="sxs-lookup"><span data-stu-id="02800-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="02800-163">Logiquement, il s’agit d’une extension de TFM (moniker de la version cible de .Net Framework). Notamment, `net45`, `net46`, `netcore50` et `dnxcore50` sont tous des exemples de TxM (consultez [Versions cibles de .Net Framework](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="02800-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="02800-164">TxM peut faire référence à un framework (TFM) ainsi qu’à d’autres surfaces d’exposition propre à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="02800-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="02800-165">Par exemple, le TxM UWP (`uap10.0`) représente la surface d’exposition .NET, ainsi que la surface d’exposition Windows des applications UWP.</span><span class="sxs-lookup"><span data-stu-id="02800-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="02800-166">Un exemple de structure lib :</span><span class="sxs-lookup"><span data-stu-id="02800-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="02800-167">Le dossier `lib` contient les assemblys utilisés au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="02800-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="02800-168">Pour la plupart des packages, un dossier sous `lib` pour chacun de TxM cibles est le seul élément requis.</span><span class="sxs-lookup"><span data-stu-id="02800-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="02800-169">Ref</span><span class="sxs-lookup"><span data-stu-id="02800-169">Ref</span></span>

<span data-ttu-id="02800-170">Il existe parfois des cas où un autre assembly doit être utilisé lors de la compilation (c’est le cas des assemblys de référence .NET aujourd’hui).</span><span class="sxs-lookup"><span data-stu-id="02800-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="02800-171">Dans ces cas, utilisez un dossier de niveau supérieur appelé `ref` (comprenez « assemblys de référence »).</span><span class="sxs-lookup"><span data-stu-id="02800-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="02800-172">La plupart des auteurs de package n’ont pas besoin du dossier `ref`.</span><span class="sxs-lookup"><span data-stu-id="02800-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="02800-173">Il s’avère utile pour les packages qui doivent fournir une surface d’exposition cohérente pour la compilation et IntelliSense, mais qui ont une implémentation différente pour différents TxM.</span><span class="sxs-lookup"><span data-stu-id="02800-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="02800-174">Les principaux cas d’usage impliquent les packages `System.*` produits dans le cadre de la fourniture de .NET Core sur NuGet.</span><span class="sxs-lookup"><span data-stu-id="02800-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="02800-175">Ces packages ont des implémentations différentes unifiées par un ensemble cohérent d’assemblys de référence.</span><span class="sxs-lookup"><span data-stu-id="02800-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="02800-176">Mécaniquement, les assemblys inclus dans le dossier `ref` sont les assemblys de référence passés au compilateur.</span><span class="sxs-lookup"><span data-stu-id="02800-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="02800-177">Pour ceux qui ont utilisé csc.exe, il s’agit des assemblys que nous passons au commutateur de [l’option C# /reference](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="02800-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="02800-178">La structure du dossier `ref` est la même que `lib`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="02800-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="02800-179">Dans cet exemple, les assemblys inclus dans les répertoires `ref` sont tous identiques.</span><span class="sxs-lookup"><span data-stu-id="02800-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="02800-180">Runtimes</span><span class="sxs-lookup"><span data-stu-id="02800-180">Runtimes</span></span>

<span data-ttu-id="02800-181">Le dossier des runtimes contient des assemblys et des bibliothèques natives devant s’exécuter sur des « runtimes » spécifiques, qui sont généralement définis par le système d’exploitation et l’architecture du processeur.</span><span class="sxs-lookup"><span data-stu-id="02800-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="02800-182">Ces temps d’exécution sont identifiés à l’aide `win` [d’identifiants Runtime (RIDs)](/dotnet/core/rid-catalog) tels que , `win-x86`, `win7-x86`, `win8-64`etc.</span><span class="sxs-lookup"><span data-stu-id="02800-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="02800-183">Programmes d’assistance natifs pour utiliser les API spécifiques à la plateforme</span><span class="sxs-lookup"><span data-stu-id="02800-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="02800-184">L’exemple suivant montre un package qui a une implémentation purement managée pour plusieurs plateformes, mais qui utilise des assistances natives sur Windows 8, où il peut appeler des API natives propres à Windows 8.</span><span class="sxs-lookup"><span data-stu-id="02800-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="02800-185">Avec le package ci-dessus, les événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="02800-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="02800-186">En dehors de Windows 8, l’assembly `lib/net40/MyLibrary.dll` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="02800-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="02800-187">Sur Windows 8, `runtimes/win8-<architecture>/lib/MyLibrary.dll` est utilisé et `native/MyNativeHelper.dll` est copié dans la sortie de votre génération.</span><span class="sxs-lookup"><span data-stu-id="02800-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="02800-188">Dans l’exemple ci-dessus, l’assembly `lib/net40` est purement du code managé, tandis que les assemblys du dossier des runtimes utilisent p/invoke dans l’assembly d’assistance native pour appeler les API propres à Windows 8.</span><span class="sxs-lookup"><span data-stu-id="02800-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="02800-189">Un seul dossier `lib` est sélectionné, donc s’il existe un dossier propre au runtime, il est préféré à un `lib` non propre au runtime.</span><span class="sxs-lookup"><span data-stu-id="02800-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="02800-190">Le dossier natif est additif ; s’il existe, il est copié dans la sortie de la génération.</span><span class="sxs-lookup"><span data-stu-id="02800-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="02800-191">Wrapper managé</span><span class="sxs-lookup"><span data-stu-id="02800-191">Managed wrapper</span></span>

<span data-ttu-id="02800-192">Une autre façon d’utiliser les runtimes consiste à fournir un package qui est purement un wrapper managé sur un assembly natif.</span><span class="sxs-lookup"><span data-stu-id="02800-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="02800-193">Dans ce scénario, vous créez un package comme le suivant :</span><span class="sxs-lookup"><span data-stu-id="02800-193">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="02800-194">Dans ce cas, il n’y a pas de dossier `lib` de niveau supérieur puisque qu’il n’y a pas d’implémentation de ce package qui ne repose pas sur l’assembly natif correspondant.</span><span class="sxs-lookup"><span data-stu-id="02800-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="02800-195">Si l’assembly managé, `MyLibrary.dll`, était exactement le même dans les deux cas, alors nous pouvons le placer dans un dossier `lib` de niveau supérieur, mais étant donné que l’absence d’un assembly natif n’entraîne pas l’échec de l’installation du package s’il a été installé sur une plateforme autre que win-x86 ou win-x64, alors le dossier lib de niveau supérieur est utilisé sans qu’aucun assembly natif ne soit copié.</span><span class="sxs-lookup"><span data-stu-id="02800-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="02800-196">Création de packages pour NuGet 2 et NuGet 3</span><span class="sxs-lookup"><span data-stu-id="02800-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="02800-197">Si vous souhaitez créer un package consommable par des projets à l’aide de `packages.config` ainsi que des packages à l’aide de `project.json`, alors les conditions suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="02800-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="02800-198">Les dossiers ref et runtimes fonctionnent uniquement sur NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="02800-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="02800-199">Ils sont tous les deux ignorés par NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="02800-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="02800-200">Vous ne pouvez pas compter sur le fonctionnement de `install.ps1` ou `uninstall.ps1`.</span><span class="sxs-lookup"><span data-stu-id="02800-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="02800-201">Ces fichiers s’exécutent lorsque vous utilisez `packages.config`, mais ils sont ignorés avec `project.json`.</span><span class="sxs-lookup"><span data-stu-id="02800-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="02800-202">Par conséquent, votre package doit être utilisable sans qu’ils s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="02800-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="02800-203">`init.ps1` s’exécute toujours sur NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="02800-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="02800-204">L’installation des cibles et des propriétés est différente, alors vérifiez que votre package fonctionne comme prévu sur les deux clients.</span><span class="sxs-lookup"><span data-stu-id="02800-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="02800-205">Les sous-répertoires de lib doivent être un TxM dans NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="02800-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="02800-206">Vous ne pouvez pas placer des bibliothèques à la racine du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="02800-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="02800-207">Le contenu n’est pas copié automatiquement avec NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="02800-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="02800-208">Les consommateurs de votre package peuvent copier les fichiers eux-mêmes ou utiliser un outil comme un exécuteur de tâches pour automatiser la copie des fichiers.</span><span class="sxs-lookup"><span data-stu-id="02800-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="02800-209">Les transformations de fichiers sources et de configuration ne sont pas exécutées par NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="02800-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="02800-210">Si vous prenez en charge NuGet 2 et 3, alors votre `minClientVersion` doit être la version la plus basse du client NuGet 2 sur laquelle fonctionne votre package.</span><span class="sxs-lookup"><span data-stu-id="02800-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="02800-211">Dans le cas d’un package existant, aucune modification n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="02800-211">In the case of an existing package it shouldn't need to change.</span></span>
