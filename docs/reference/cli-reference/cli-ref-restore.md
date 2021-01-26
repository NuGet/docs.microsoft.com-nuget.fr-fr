---
title: Commande de restauration de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780027"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="a8135-103">Restore, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="a8135-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="a8135-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : 2.7 +</span><span class="sxs-lookup"><span data-stu-id="a8135-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="a8135-105">Télécharge et installe tous les packages manquants dans le `packages` dossier.</span><span class="sxs-lookup"><span data-stu-id="a8135-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="a8135-106">Lorsqu’il est utilisé avec NuGet 4.0 + et le format PackageReference, génère un `<project>.nuget.props` fichier, si nécessaire, dans le `obj` dossier.</span><span class="sxs-lookup"><span data-stu-id="a8135-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="a8135-107">(Le fichier peut être omis dans le contrôle de code source.)</span><span class="sxs-lookup"><span data-stu-id="a8135-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="a8135-108">Sur Mac OSX et Linux avec l’interface CLI sur mono, la restauration des packages n’est pas prise en charge avec PackageReference.</span><span class="sxs-lookup"><span data-stu-id="a8135-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="a8135-109">Utilisation</span><span class="sxs-lookup"><span data-stu-id="a8135-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="a8135-110">où `<projectPath>` spécifie l’emplacement d’une solution ou d’un `packages.config` fichier.</span><span class="sxs-lookup"><span data-stu-id="a8135-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="a8135-111">Consultez les [Remarques](#remarks) ci-dessous pour obtenir des détails sur le comportement.</span><span class="sxs-lookup"><span data-stu-id="a8135-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="a8135-112">Options</span><span class="sxs-lookup"><span data-stu-id="a8135-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a8135-113">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="a8135-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a8135-114">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a8135-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="a8135-115">*(4.0 +)* Télécharge les packages directement sans remplir les caches avec des binaires ou des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="a8135-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="a8135-116">Désactive la restauration de plusieurs packages en parallèle.</span><span class="sxs-lookup"><span data-stu-id="a8135-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="a8135-117">*(3.2 +)* Liste de sources de packages à utiliser comme secours si le package est introuvable dans la source principale ou par défaut.</span><span class="sxs-lookup"><span data-stu-id="a8135-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="a8135-118">Utilisez un point-virgule pour séparer les entrées de liste.</span><span class="sxs-lookup"><span data-stu-id="a8135-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="a8135-119">Dans les projets basés sur PackageReference, force la résolution de toutes les dépendances même si la dernière restauration a réussi.</span><span class="sxs-lookup"><span data-stu-id="a8135-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="a8135-120">La spécification de cet indicateur est semblable à la suppression du `project.assets.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="a8135-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="a8135-121">Cela ne contourne pas le cache http.</span><span class="sxs-lookup"><span data-stu-id="a8135-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a8135-122">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="a8135-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="a8135-123">Force la restauration à réévaluer toutes les dépendances même si un fichier de verrouillage existe déjà.</span><span class="sxs-lookup"><span data-stu-id="a8135-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a8135-124">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="a8135-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="a8135-125">Emplacement de sortie où le fichier de verrouillage de projet est écrit.</span><span class="sxs-lookup"><span data-stu-id="a8135-125">Output location where project lock file is written.</span></span> <span data-ttu-id="a8135-126">Par défaut, cette valeur est `PROJECT_ROOT\packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="a8135-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="a8135-127">N’autorise pas la mise à jour du fichier de verrouillage de projet.</span><span class="sxs-lookup"><span data-stu-id="a8135-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="a8135-128">*(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande, prioritaire sur `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="a8135-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="a8135-129">*(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="a8135-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="a8135-130">Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="a8135-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="a8135-131">Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a8135-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="a8135-132">Empêche NuGet d’utiliser les packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="a8135-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="a8135-133">Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="a8135-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a8135-134">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a8135-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="a8135-135">Spécifie le dossier dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="a8135-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="a8135-136">Si aucun dossier n’est spécifié, le dossier actif est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a8135-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="a8135-137">Obligatoire lors de la restauration avec un `packages.config` fichier, sauf si `PackagesDirectory` ou `SolutionDirectory` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a8135-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="a8135-138">Spécifie les types de fichiers à enregistrer après l’installation du package : l’un des éléments `nuspec` , `nupkg` ou `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="a8135-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="a8135-139">Comme pour `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="a8135-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="a8135-140">Obligatoire lors de la restauration avec un `packages.config` fichier, sauf si `OutputDirectory` ou `SolutionDirectory` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a8135-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="a8135-141">Délai d’expiration en secondes pour la résolution des références entre projets.</span><span class="sxs-lookup"><span data-stu-id="a8135-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="a8135-142">*(4.0 +)* Restaure tous les projets de référence pour les projets UWP et .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a8135-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="a8135-143">Ne s’applique pas aux projets qui utilisent `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="a8135-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="a8135-144">Vérifie que la restauration des packages est activée avant de télécharger et d’installer les packages.</span><span class="sxs-lookup"><span data-stu-id="a8135-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="a8135-145">Pour plus d’informations, consultez [restauration de packages](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a8135-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="a8135-146">Spécifie le dossier de la solution.</span><span class="sxs-lookup"><span data-stu-id="a8135-146">Specifies the solution folder.</span></span> <span data-ttu-id="a8135-147">Non valide lors de la restauration de packages pour une solution.</span><span class="sxs-lookup"><span data-stu-id="a8135-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="a8135-148">Obligatoire lors de la restauration avec un `packages.config` fichier, sauf si `PackagesDirectory` ou `OutputDirectory` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a8135-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="a8135-149">Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="a8135-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="a8135-150">En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configuration du comportement de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a8135-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a8135-151">Utilisez un point-virgule pour séparer les entrées de liste.</span><span class="sxs-lookup"><span data-stu-id="a8135-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="a8135-152">Active la génération et l’utilisation du fichier de verrouillage de projet avec Restore.</span><span class="sxs-lookup"><span data-stu-id="a8135-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a8135-153">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a8135-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a8135-154">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a8135-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="a8135-155">Notes</span><span class="sxs-lookup"><span data-stu-id="a8135-155">Remarks</span></span>

<span data-ttu-id="a8135-156">La commande Restore effectue les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8135-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="a8135-157">Déterminez le mode d’opération de la commande Restore.</span><span class="sxs-lookup"><span data-stu-id="a8135-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="a8135-158">type de fichier projectPath</span><span class="sxs-lookup"><span data-stu-id="a8135-158">projectPath file type</span></span> | <span data-ttu-id="a8135-159">Comportement</span><span class="sxs-lookup"><span data-stu-id="a8135-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="a8135-160">Solution (dossier)</span><span class="sxs-lookup"><span data-stu-id="a8135-160">Solution (folder)</span></span> | <span data-ttu-id="a8135-161">NuGet recherche un `.sln` fichier et l’utilise s’il est trouvé ; sinon, génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="a8135-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="a8135-162">`(SolutionDir)\.nuget` est utilisé comme dossier de démarrage.</span><span class="sxs-lookup"><span data-stu-id="a8135-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="a8135-163">Fichier `.sln`</span><span class="sxs-lookup"><span data-stu-id="a8135-163">`.sln` file</span></span> | <span data-ttu-id="a8135-164">Restaurez les packages identifiés par la solution ; génère une erreur si `-SolutionDirectory` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a8135-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="a8135-165">`$(SolutionDir)\.nuget` est utilisé comme dossier de démarrage.</span><span class="sxs-lookup"><span data-stu-id="a8135-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="a8135-166">`packages.config` fichier projet ou</span><span class="sxs-lookup"><span data-stu-id="a8135-166">`packages.config` or project file</span></span> | <span data-ttu-id="a8135-167">Restaurez les packages listés dans le fichier, en résolvant et en installant les dépendances.</span><span class="sxs-lookup"><span data-stu-id="a8135-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="a8135-168">Autre type de fichier</span><span class="sxs-lookup"><span data-stu-id="a8135-168">Other file type</span></span> | <span data-ttu-id="a8135-169">Le fichier est supposé être un `.sln` fichier comme indiqué ci-dessus ; s’il ne s’agit pas d’une solution, NuGet génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="a8135-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="a8135-170">(projectPath non spécifié)</span><span class="sxs-lookup"><span data-stu-id="a8135-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="a8135-171">NuGet recherche les fichiers solution dans le dossier actif.</span><span class="sxs-lookup"><span data-stu-id="a8135-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="a8135-172">Si un seul fichier est trouvé, il est utilisé pour restaurer les packages. Si plusieurs solutions sont trouvées, NuGet génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="a8135-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="a8135-173">S’il n’existe aucun fichier solution, NuGet recherche un `packages.config` et l’utilise pour restaurer des packages.</span><span class="sxs-lookup"><span data-stu-id="a8135-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="a8135-174">Si aucune solution ou aucun `packages.config` fichier n’est trouvé, NuGet génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="a8135-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="a8135-175">Déterminer le dossier Packages en utilisant l’ordre de priorité suivant (NuGet génère une erreur si aucun de ces dossiers n’est trouvé) :</span><span class="sxs-lookup"><span data-stu-id="a8135-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="a8135-176">Dossier spécifié avec `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="a8135-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="a8135-177">La `repositoryPath` valeur dans `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="a8135-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="a8135-178">Le dossier spécifié avec `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="a8135-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="a8135-179">Lors de la restauration de packages pour une solution, NuGet effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8135-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="a8135-180">Charge le fichier solution.</span><span class="sxs-lookup"><span data-stu-id="a8135-180">Loads the solution file.</span></span>
    - <span data-ttu-id="a8135-181">Restaure les packages de niveau solution listés dans dans `$(SolutionDir)\.nuget\packages.config` le `packages` dossier.</span><span class="sxs-lookup"><span data-stu-id="a8135-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="a8135-182">Restaurez les packages listés dans dans `$(ProjectDir)\packages.config` le `packages` dossier.</span><span class="sxs-lookup"><span data-stu-id="a8135-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="a8135-183">Pour chaque package spécifié, restaurez le package en parallèle, sauf si `-DisableParallelProcessing` est spécifié.</span><span class="sxs-lookup"><span data-stu-id="a8135-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="a8135-184">Exemples</span><span class="sxs-lookup"><span data-stu-id="a8135-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
