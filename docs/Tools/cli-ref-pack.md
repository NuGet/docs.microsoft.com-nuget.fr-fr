---
title: Commande pack de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande pack de nuget.exe"
keywords: "référence de pack de NuGet, commande pack"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9ee5dc87ea33b4419bcd9a09751c41b53ae2f70e
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="52b43-104">commande de Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="52b43-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="52b43-105">**S’applique à :** la création de package &bullet; **versions prises en charge :** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="52b43-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="52b43-106">Crée un package NuGet selon le `.nuspec` ou le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="52b43-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="52b43-107">Le `dotnet pack` commande (consultez [dotnet commandes](dotnet-Commands.md)) et `msbuild /t:pack` (consultez [cibles de MSBuild](../reference/msbuild-targets.md)) peut être utilisé en tant que variantes.</span><span class="sxs-lookup"><span data-stu-id="52b43-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="52b43-108">Création d’un package à partir d’un fichier de projet sous Mono, n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="52b43-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="52b43-109">Vous devez également ajuster les chemins d’accès non locale dans le `.nuspec` chemins d’accès de style Unix, le fichier comme nuget.exe ne convertit pas les chemins d’accès Windows lui-même.</span><span class="sxs-lookup"><span data-stu-id="52b43-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="52b43-110">Utilisation</span><span class="sxs-lookup"><span data-stu-id="52b43-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="52b43-111">où `<nuspecPath>` et `<projectPath>` spécifier le `.nuspec` ou le fichier de projet respectivement.</span><span class="sxs-lookup"><span data-stu-id="52b43-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="52b43-112">Options</span><span class="sxs-lookup"><span data-stu-id="52b43-112">Options</span></span>

| <span data-ttu-id="52b43-113">Option</span><span class="sxs-lookup"><span data-stu-id="52b43-113">Option</span></span> | <span data-ttu-id="52b43-114">Description</span><span class="sxs-lookup"><span data-stu-id="52b43-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52b43-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="52b43-115">BasePath</span></span> | <span data-ttu-id="52b43-116">Définit le chemin d’accès de base des fichiers définis dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="52b43-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="52b43-117">Générer</span><span class="sxs-lookup"><span data-stu-id="52b43-117">Build</span></span> | <span data-ttu-id="52b43-118">Spécifie que le projet doit être créé avant de générer le package.</span><span class="sxs-lookup"><span data-stu-id="52b43-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="52b43-119">Exclure</span><span class="sxs-lookup"><span data-stu-id="52b43-119">Exclude</span></span> | <span data-ttu-id="52b43-120">Spécifie un ou plusieurs modèles de caractère générique à exclure lors de la création d’un package.</span><span class="sxs-lookup"><span data-stu-id="52b43-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="52b43-121">Pour spécifier plusieurs modèles, répétez l’indicateur d’exclusion.</span><span class="sxs-lookup"><span data-stu-id="52b43-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="52b43-122">Consultez l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="52b43-122">See example below.</span></span> |
| <span data-ttu-id="52b43-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="52b43-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="52b43-124">Empêche l’inclusion de répertoires vides lors de la création du package.</span><span class="sxs-lookup"><span data-stu-id="52b43-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="52b43-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="52b43-125">ForceEnglishOutput</span></span> | <span data-ttu-id="52b43-126">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="52b43-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="52b43-127">Help</span><span class="sxs-lookup"><span data-stu-id="52b43-127">Help</span></span> | <span data-ttu-id="52b43-128">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="52b43-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="52b43-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="52b43-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="52b43-130">Indique que le package généré doit inclure les projets référencés en tant que dépendances ou en tant que partie du package.</span><span class="sxs-lookup"><span data-stu-id="52b43-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="52b43-131">Si un projet référencé est associée à une `.nuspec` fichier ayant le même nom que le projet, puis ce projet référencé est ajouté en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="52b43-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="52b43-132">Sinon, le projet référencé est ajouté en tant que partie du package.</span><span class="sxs-lookup"><span data-stu-id="52b43-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="52b43-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="52b43-133">MinClientVersion</span></span> | <span data-ttu-id="52b43-134">Définir le *minClientVersion* attribut du package.</span><span class="sxs-lookup"><span data-stu-id="52b43-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="52b43-135">Cette valeur remplace la valeur existants *minClientVersion* d’attribut (le cas échéant) dans le `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="52b43-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="52b43-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="52b43-136">MSBuildPath</span></span> | <span data-ttu-id="52b43-137">*(4.0 +)*  Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="52b43-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="52b43-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="52b43-138">MSBuildVersion</span></span> | <span data-ttu-id="52b43-139">*(3.2 +)*  Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="52b43-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="52b43-140">Valeurs prises en charge sont 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="52b43-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="52b43-141">Par défaut que le MSBuild dans votre chemin d’accès est sélectionné, sinon la valeur par défaut pour la version installée la plus élevée de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="52b43-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="52b43-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="52b43-142">NoDefaultExcludes</span></span> | <span data-ttu-id="52b43-143">Empêche l’exclusion par défaut de NuGet package des fichiers et dossiers commençant par un point, tel que `.svn` et `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="52b43-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="52b43-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="52b43-144">NoPackageAnalysis</span></span> | <span data-ttu-id="52b43-145">Spécifie que le pack ne doit pas exécuter d’analyse du package après sa génération.</span><span class="sxs-lookup"><span data-stu-id="52b43-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="52b43-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="52b43-146">OutputDirectory</span></span> | <span data-ttu-id="52b43-147">Spécifie le dossier dans lequel est stocké le package créé.</span><span class="sxs-lookup"><span data-stu-id="52b43-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="52b43-148">Si aucun dossier n’est spécifié, le dossier actif est utilisé.</span><span class="sxs-lookup"><span data-stu-id="52b43-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="52b43-149">Propriétés</span><span class="sxs-lookup"><span data-stu-id="52b43-149">Properties</span></span> | <span data-ttu-id="52b43-150">Spécifie une liste de propriétés qui remplacent les valeurs dans le fichier projet ; consultez [propriétés communes des projets MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) des noms de propriétés.</span><span class="sxs-lookup"><span data-stu-id="52b43-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="52b43-151">L’argument des propriétés est une liste de jeton de paires = valeur, séparés par des points-virgules, où chaque occurrence de `$token$` dans le `.nuspec` fichier est remplacé par la valeur donnée.</span><span class="sxs-lookup"><span data-stu-id="52b43-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="52b43-152">Les valeurs peuvent être des chaînes entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="52b43-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="52b43-153">Notez que la propriété « Configuration », la valeur par défaut est « Debug ».</span><span class="sxs-lookup"><span data-stu-id="52b43-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="52b43-154">Pour attribuer une configuration Release, utilisez `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="52b43-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="52b43-155">Suffixe</span><span class="sxs-lookup"><span data-stu-id="52b43-155">Suffix</span></span> | <span data-ttu-id="52b43-156">*(3.4.4+)*  Ajoute un suffixe au numéro de version généré en interne, généralement utilisé pour l’ajout de la build ou autres identificateurs de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="52b43-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="52b43-157">Par exemple, à l’aide de `-suffix nightly` va créer un package avec un type de numéro de version `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="52b43-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="52b43-158">Suffixes doivent commencer par une lettre pour éviter les avertissements, les erreurs et identifier les éventuelles incompatibilités avec différentes versions de NuGet et le Gestionnaire de Package NuGet.</span><span class="sxs-lookup"><span data-stu-id="52b43-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="52b43-159">Symboles</span><span class="sxs-lookup"><span data-stu-id="52b43-159">Symbols</span></span> | <span data-ttu-id="52b43-160">Spécifie que le package contient des sources et des symboles.</span><span class="sxs-lookup"><span data-stu-id="52b43-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="52b43-161">Lorsqu’il est utilisé avec un `.nuspec` fichier, cette opération crée un fichier de package NuGet normal et le package de symboles correspondants.</span><span class="sxs-lookup"><span data-stu-id="52b43-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="52b43-162">Outil</span><span class="sxs-lookup"><span data-stu-id="52b43-162">Tool</span></span> | <span data-ttu-id="52b43-163">Spécifie que les fichiers de sortie du projet doivent être placés dans le `tool` dossier.</span><span class="sxs-lookup"><span data-stu-id="52b43-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="52b43-164">Commentaires</span><span class="sxs-lookup"><span data-stu-id="52b43-164">Verbosity</span></span> | <span data-ttu-id="52b43-165">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="52b43-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="52b43-166">Version</span><span class="sxs-lookup"><span data-stu-id="52b43-166">Version</span></span> | <span data-ttu-id="52b43-167">Remplace le numéro de version à partir de la `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="52b43-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="52b43-168">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="52b43-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="52b43-169">À l’exclusion des dépendances de développement</span><span class="sxs-lookup"><span data-stu-id="52b43-169">Excluding development dependencies</span></span>

<span data-ttu-id="52b43-170">Certains packages NuGet sont utiles en tant que dépendances de développement, ce qui vous aident à créer votre propre bibliothèque, mais ne sont pas forcément nécessaires en tant que dépendances de package réel.</span><span class="sxs-lookup"><span data-stu-id="52b43-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="52b43-171">Le `pack` commande ignorera `package` entrées dans `packages.config` qui ont le `developmentDependency` attribut la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="52b43-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="52b43-172">Ces entrées n’inclura pas comme un dépendances dans le package créé.</span><span class="sxs-lookup"><span data-stu-id="52b43-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="52b43-173">Par exemple, considérez les éléments suivants `packages.config` fichier dans le projet source :</span><span class="sxs-lookup"><span data-stu-id="52b43-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="52b43-174">Pour ce projet, le package créé par `nuget pack` a une dépendance sur `jQuery` et `microsoft-web-helpers` mais pas `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="52b43-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="52b43-175">Exemples</span><span class="sxs-lookup"><span data-stu-id="52b43-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
