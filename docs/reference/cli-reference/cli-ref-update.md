---
title: Commande de mise à jour de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236787"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="db325-103">Update, commande (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="db325-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="db325-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : toutes</span><span class="sxs-lookup"><span data-stu-id="db325-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="db325-105">Mettez à jour tous les packages dans un projet (en utilisant `packages.config`) avec leurs dernières versions disponibles.</span><span class="sxs-lookup"><span data-stu-id="db325-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="db325-106">Il est recommandé d’exécuter [« Restore »](cli-ref-restore.md) avant d’exécuter le `update` .</span><span class="sxs-lookup"><span data-stu-id="db325-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="db325-107">(Pour mettre à jour un package individuel, utilisez [`nuget install`](cli-ref-install.md) sans spécifier de numéro de version, auquel cas NuGet installe la version la plus récente.)</span><span class="sxs-lookup"><span data-stu-id="db325-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="db325-108">Remarque : `update` ne fonctionne pas avec l’interface CLI s’exécutant sous mono (Mac OSX ou Linux) ou lors de l’utilisation du format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="db325-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="db325-109">La `update` commande met également à jour les références d’assembly dans le fichier projet, à condition que ces références existent déjà.</span><span class="sxs-lookup"><span data-stu-id="db325-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="db325-110">Si un package mis à jour a un assembly ajouté, une nouvelle référence n’est *pas* ajoutée.</span><span class="sxs-lookup"><span data-stu-id="db325-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="db325-111">Les références d’assembly des nouvelles dépendances de package ne sont pas non plus ajoutées.</span><span class="sxs-lookup"><span data-stu-id="db325-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="db325-112">Pour inclure ces opérations dans le cadre d’une mise à jour, mettez à jour le package dans Visual Studio à l’aide de l’interface utilisateur du gestionnaire de package ou de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="db325-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="db325-113">Cette commande peut également être utilisée pour mettre à jour nuget.exe elle-même à l’aide de l’indicateur *-Self* .</span><span class="sxs-lookup"><span data-stu-id="db325-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="db325-114">Utilisation</span><span class="sxs-lookup"><span data-stu-id="db325-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="db325-115">où `<configPath>` identifie un `packages.config` fichier solution ou qui répertorie les dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="db325-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="db325-116">Options</span><span class="sxs-lookup"><span data-stu-id="db325-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="db325-117">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="db325-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="db325-118">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="db325-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="db325-119">Spécifie la version des packages de dépendance à utiliser, qui peut être l’une des suivantes :</span><span class="sxs-lookup"><span data-stu-id="db325-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="db325-120">La *plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="db325-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="db325-121">*HighestPatch* : version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="db325-121">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="db325-122">*HighestMinor* : version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="db325-122">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="db325-123">La *plus élevée* : la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="db325-123">*Highest* : the highest version</span></span></li><li><span data-ttu-id="db325-124">*Ignorer* : aucun package de dépendances ne sera utilisé</span><span class="sxs-lookup"><span data-stu-id="db325-124">*Ignore* : No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="db325-125">Spécifie l’action par défaut lorsqu’un fichier d’un package existe déjà dans le projet cible.</span><span class="sxs-lookup"><span data-stu-id="db325-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="db325-126">Affectez la valeur `Overwrite` pour toujours remplacer les fichiers.</span><span class="sxs-lookup"><span data-stu-id="db325-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="db325-127">Affectez la valeur `Ignore` pour ignorer les fichiers.</span><span class="sxs-lookup"><span data-stu-id="db325-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="db325-128">L' `PromptUser` action, la valeur par défaut, demande à chaque fichier en conflit `OverwriteAll` , sauf si ou `IgnoreAll` est fourni, qui s’applique à tous les fichiers restants.</span><span class="sxs-lookup"><span data-stu-id="db325-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="db325-129">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="db325-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="db325-130">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="db325-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="db325-131">Spécifie une liste d’ID de package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="db325-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="db325-132">*(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande, prioritaire sur `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="db325-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="db325-133">*(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="db325-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="db325-134">Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="db325-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="db325-135">Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="db325-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="db325-136">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db325-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="db325-137">Autorise la mise à jour vers les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="db325-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="db325-138">Cet indicateur n’est pas nécessaire lors de la mise à jour des packages de version préliminaire déjà installés.</span><span class="sxs-lookup"><span data-stu-id="db325-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="db325-139">Spécifie le dossier local dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="db325-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="db325-140">Spécifie que seules les mises à jour dont la version la plus récente est disponible dans la même version principale et la version mineure que le package installé seront installées.</span><span class="sxs-lookup"><span data-stu-id="db325-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="db325-141">Met à jour nuget.exe vers la dernière version ; tous les autres arguments sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="db325-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="db325-142">Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="db325-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="db325-143">En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="db325-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="db325-144">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="db325-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="db325-145">Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="db325-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="db325-146">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="db325-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="db325-147">Exemples</span><span class="sxs-lookup"><span data-stu-id="db325-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
