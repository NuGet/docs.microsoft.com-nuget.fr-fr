---
title: Commande du Pack de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Pack
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780043"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="b747e-103">commande Pack (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="b747e-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="b747e-104">**S’applique à :** &bullet; **versions prises en charge** pour la création de package : 2.7 +</span><span class="sxs-lookup"><span data-stu-id="b747e-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="b747e-105">Crée un package NuGet basé sur le fichier [. NuSpec](../nuspec.md) ou le fichier projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="b747e-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="b747e-106">La `dotnet pack` commande (consultez les [commandes dotnet](../dotnet-Commands.md)) et `msbuild -t:pack` (voir [cibles MSBuild](../msbuild-targets.md)) peut être utilisée comme variantes.</span><span class="sxs-lookup"><span data-stu-id="b747e-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="b747e-107">Utilisez [`dotnet pack`](../dotnet-Commands.md) ou [`msbuild -t:pack`](../msbuild-targets.md) pour les projets basés sur [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="b747e-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="b747e-108">Sous mono, la création d’un package à partir d’un fichier projet n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b747e-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="b747e-109">Vous devez également ajuster les chemins non locaux dans le `.nuspec` fichier aux chemins de style UNIX, car nuget.exe ne convertit pas les chemins Windows eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="b747e-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="b747e-110">Utilisation</span><span class="sxs-lookup"><span data-stu-id="b747e-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="b747e-111">où `<nuspecPath>` et `<projectPath>` spécifient `.nuspec` respectivement le fichier projet ou.</span><span class="sxs-lookup"><span data-stu-id="b747e-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="b747e-112">Options</span><span class="sxs-lookup"><span data-stu-id="b747e-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="b747e-113">Définit le chemin d’accès de base des fichiers définis dans le fichier [. NuSpec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="b747e-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="b747e-114">Spécifie que le projet doit être généré avant de générer le package.</span><span class="sxs-lookup"><span data-stu-id="b747e-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b747e-115">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="b747e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b747e-116">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b747e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="b747e-117">Spécifie un ou plusieurs modèles de caractères génériques à exclure lors de la création d’un package.</span><span class="sxs-lookup"><span data-stu-id="b747e-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="b747e-118">Pour spécifier plusieurs modèles, répétez l’indicateur-Exclude.</span><span class="sxs-lookup"><span data-stu-id="b747e-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="b747e-119">Voir l'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b747e-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="b747e-120">Empêche l’inclusion de répertoires vides lors de la génération du package.</span><span class="sxs-lookup"><span data-stu-id="b747e-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b747e-121">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="b747e-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b747e-122">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="b747e-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="b747e-123">Indique que le package généré doit inclure des projets référencés en tant que dépendances ou dans le cadre du package.</span><span class="sxs-lookup"><span data-stu-id="b747e-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="b747e-124">Si un projet référencé a un fichier correspondant `.nuspec` portant le même nom que le projet, ce projet référencé est ajouté en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="b747e-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="b747e-125">Dans le cas contraire, le projet référencé est ajouté dans le cadre du package.</span><span class="sxs-lookup"><span data-stu-id="b747e-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="b747e-126">Spécifiez si la commande doit préparer le répertoire de sortie du package pour prendre en charge le partage en tant que flux.</span><span class="sxs-lookup"><span data-stu-id="b747e-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="b747e-127">Définissez l’attribut *minClientVersion* pour le package créé.</span><span class="sxs-lookup"><span data-stu-id="b747e-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="b747e-128">Cette valeur remplace la valeur de l’attribut *minClientVersion* existant (le cas échéant) dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="b747e-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="b747e-129">*(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande, prioritaire sur `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="b747e-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="b747e-130">*(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="b747e-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b747e-131">Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="b747e-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="b747e-132">Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b747e-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="b747e-133">Empêche l’exclusion par défaut des fichiers de package NuGet et des fichiers et dossiers commençant par un point, comme `.svn` et `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="b747e-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b747e-134">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b747e-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="b747e-135">Spécifie que le pack ne doit pas exécuter d’analyse du package après sa génération.</span><span class="sxs-lookup"><span data-stu-id="b747e-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="b747e-136">Spécifie le dossier dans lequel le package créé est stocké.</span><span class="sxs-lookup"><span data-stu-id="b747e-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="b747e-137">Si aucun dossier n’est spécifié, le dossier actif est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b747e-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="b747e-138">Spécifiez si la commande doit préparer le nom de la sortie du package sans la version.</span><span class="sxs-lookup"><span data-stu-id="b747e-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="b747e-139">Spécifie le dossier Packages.</span><span class="sxs-lookup"><span data-stu-id="b747e-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="b747e-140">Doit apparaître en dernier sur la ligne de commande après d’autres options.</span><span class="sxs-lookup"><span data-stu-id="b747e-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="b747e-141">Spécifie une liste de propriétés qui remplacent les valeurs du fichier projet ; consultez les [Propriétés communes des projets MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) pour les noms de propriété.</span><span class="sxs-lookup"><span data-stu-id="b747e-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="b747e-142">L’argument Properties ici est une liste de paires jeton = valeur, séparées par des points-virgules, où chaque occurrence de `$token$` dans le `.nuspec` fichier sera remplacée par la valeur donnée.</span><span class="sxs-lookup"><span data-stu-id="b747e-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="b747e-143">Les valeurs peuvent être des chaînes entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="b747e-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="b747e-144">Notez que, pour la propriété « configuration », la valeur par défaut est « Debug ».</span><span class="sxs-lookup"><span data-stu-id="b747e-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="b747e-145">Pour passer à une configuration Release, utilisez `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="b747e-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="b747e-146">**En général**, les propriétés doivent être identiques à celles utilisées lors de la génération du projet correspondant, afin d’éviter un comportement potentiellement étrange.</span><span class="sxs-lookup"><span data-stu-id="b747e-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="b747e-147">Spécifie le répertoire de la solution.</span><span class="sxs-lookup"><span data-stu-id="b747e-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="b747e-148">*(3.4.4 +)* Ajoute un suffixe au numéro de version généré en interne, généralement utilisé pour ajouter la build ou d’autres identificateurs de préversion.</span><span class="sxs-lookup"><span data-stu-id="b747e-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="b747e-149">Par exemple, l’utilisation de `-suffix nightly` crée un package avec un numéro de version comme `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="b747e-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="b747e-150">Les suffixes doivent commencer par une lettre pour éviter les avertissements, les erreurs et les incompatibilités potentielles avec les différentes versions de NuGet et du gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="b747e-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="b747e-151">Lorsque vous créez un package de symboles, permet de choisir entre le `snupkg` `symbols.nupkg` format et.</span><span class="sxs-lookup"><span data-stu-id="b747e-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="b747e-152">Spécifie que le package contient des sources et des symboles.</span><span class="sxs-lookup"><span data-stu-id="b747e-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="b747e-153">Lorsqu’il est utilisé avec un `.nuspec` fichier, cela crée un fichier de package NuGet standard et le package de symboles correspondant.</span><span class="sxs-lookup"><span data-stu-id="b747e-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="b747e-154">Par défaut, il crée un [package de symboles hérité](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="b747e-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="b747e-155">Le nouveau format recommandé pour les packages de symboles est .snupkg.</span><span class="sxs-lookup"><span data-stu-id="b747e-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="b747e-156">Consultez [Création de packages de symboles (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="b747e-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="b747e-157">Spécifie que les fichiers de sortie du projet doivent être placés dans le `tool` dossier.</span><span class="sxs-lookup"><span data-stu-id="b747e-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b747e-158">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="b747e-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="b747e-159">Remplace le numéro de version du `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="b747e-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="b747e-160">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b747e-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="b747e-161">Exclusion des dépendances de développement</span><span class="sxs-lookup"><span data-stu-id="b747e-161">Excluding development dependencies</span></span>

<span data-ttu-id="b747e-162">Certains packages NuGet sont utiles en tant que dépendances de développement, qui vous aident à créer votre propre bibliothèque, mais qui ne sont pas nécessairement nécessaires en tant que dépendances de package réelles.</span><span class="sxs-lookup"><span data-stu-id="b747e-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="b747e-163">La `pack` commande ignore les `package` entrées dans `packages.config` dont l' `developmentDependency` attribut a la valeur `true` .</span><span class="sxs-lookup"><span data-stu-id="b747e-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="b747e-164">Ces entrées ne sont pas incluses en tant que dépendances dans le package créé.</span><span class="sxs-lookup"><span data-stu-id="b747e-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="b747e-165">Par exemple, considérez le `packages.config` fichier suivant dans le projet source :</span><span class="sxs-lookup"><span data-stu-id="b747e-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="b747e-166">Pour ce projet, le package créé par `nuget pack` aura une dépendance sur `jQuery` et, `microsoft-web-helpers` mais pas sur `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="b747e-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="b747e-167">Suppression des avertissements de Pack</span><span class="sxs-lookup"><span data-stu-id="b747e-167">Suppressing pack warnings</span></span>

<span data-ttu-id="b747e-168">Bien qu’il soit recommandé de résoudre tous les avertissements NuGet au cours de vos opérations de Pack, il est justifié, dans certains cas, de les supprimer.</span><span class="sxs-lookup"><span data-stu-id="b747e-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="b747e-169">Vous pouvez obtenir cela de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="b747e-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="b747e-170">Package nuget.exe Pack. NuSpec-Properties nowarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="b747e-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="b747e-171">Exemples</span><span class="sxs-lookup"><span data-stu-id="b747e-171">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
