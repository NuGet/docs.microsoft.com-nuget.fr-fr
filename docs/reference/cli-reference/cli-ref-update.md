---
title: Commande de mise à jour de l’interface CLI NuGet
description: Référence pour la commande de mise à jour de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327506"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="e5c00-103">update (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e5c00-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="e5c00-104">**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: toutes</span><span class="sxs-lookup"><span data-stu-id="e5c00-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e5c00-105">Mettez à jour tous les packages dans un projet (en utilisant `packages.config`) avec leurs dernières versions disponibles.</span><span class="sxs-lookup"><span data-stu-id="e5c00-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="e5c00-106">Il est recommandé d’exécuter [«Restore»](cli-ref-restore.md) avant d' `update`exécuter le.</span><span class="sxs-lookup"><span data-stu-id="e5c00-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="e5c00-107">(Pour mettre à jour un package individuel [`nuget install`](cli-ref-install.md) , utilisez sans spécifier de numéro de version, auquel cas NuGet installe la version la plus récente.)</span><span class="sxs-lookup"><span data-stu-id="e5c00-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="e5c00-108">Remarque: `update` ne fonctionne pas avec l’interface CLI s’exécutant sous mono (Mac OSX ou Linux) ou lors de l’utilisation du format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e5c00-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="e5c00-109">La `update` commande met également à jour les références d’assembly dans le fichier projet, à condition que ces références existent déjà.</span><span class="sxs-lookup"><span data-stu-id="e5c00-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="e5c00-110">Si un package mis à jour a un assembly ajouté, une nouvelle référence n’est *pas* ajoutée.</span><span class="sxs-lookup"><span data-stu-id="e5c00-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="e5c00-111">Les références d’assembly des nouvelles dépendances de package ne sont pas non plus ajoutées.</span><span class="sxs-lookup"><span data-stu-id="e5c00-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="e5c00-112">Pour inclure ces opérations dans le cadre d’une mise à jour, mettez à jour le package dans Visual Studio à l’aide de l’interface utilisateur du gestionnaire de package ou de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="e5c00-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="e5c00-113">Cette commande peut également être utilisée pour mettre à jour NuGet. exe lui-même à l’aide de l’indicateur *-Self* .</span><span class="sxs-lookup"><span data-stu-id="e5c00-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="e5c00-114">Usage</span><span class="sxs-lookup"><span data-stu-id="e5c00-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="e5c00-115">où `<configPath>` identifie un `packages.config` fichier solution ou qui répertorie les dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="e5c00-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="e5c00-116">Options</span><span class="sxs-lookup"><span data-stu-id="e5c00-116">Options</span></span>

| <span data-ttu-id="e5c00-117">Option</span><span class="sxs-lookup"><span data-stu-id="e5c00-117">Option</span></span> | <span data-ttu-id="e5c00-118">Description</span><span class="sxs-lookup"><span data-stu-id="e5c00-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e5c00-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e5c00-119">ConfigFile</span></span> | <span data-ttu-id="e5c00-120">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="e5c00-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e5c00-121">S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e5c00-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e5c00-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e5c00-122">FileConflictAction</span></span> | <span data-ttu-id="e5c00-123">Spécifie l’action à entreprendre lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="e5c00-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e5c00-124">Les valeurs sont *overwrite, ignore, None*.</span><span class="sxs-lookup"><span data-stu-id="e5c00-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="e5c00-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e5c00-125">ForceEnglishOutput</span></span> | <span data-ttu-id="e5c00-126">*(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="e5c00-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e5c00-127">Help</span><span class="sxs-lookup"><span data-stu-id="e5c00-127">Help</span></span> | <span data-ttu-id="e5c00-128">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="e5c00-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="e5c00-129">Id</span><span class="sxs-lookup"><span data-stu-id="e5c00-129">Id</span></span> | <span data-ttu-id="e5c00-130">Spécifie une liste d’ID de package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="e5c00-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="e5c00-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="e5c00-131">MSBuildPath</span></span> | <span data-ttu-id="e5c00-132">*(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="e5c00-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="e5c00-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="e5c00-133">MSBuildVersion</span></span> | <span data-ttu-id="e5c00-134">*(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="e5c00-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e5c00-135">Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="e5c00-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="e5c00-136">Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e5c00-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="e5c00-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e5c00-137">NonInteractive</span></span> | <span data-ttu-id="e5c00-138">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e5c00-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e5c00-139">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="e5c00-139">PreRelease</span></span> | <span data-ttu-id="e5c00-140">Autorise la mise à jour vers les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="e5c00-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="e5c00-141">Cet indicateur n’est pas nécessaire lors de la mise à jour des packages de version préliminaire déjà installés.</span><span class="sxs-lookup"><span data-stu-id="e5c00-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="e5c00-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="e5c00-142">RepositoryPath</span></span> | <span data-ttu-id="e5c00-143">Spécifie le dossier local dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="e5c00-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="e5c00-144">Safe</span><span class="sxs-lookup"><span data-stu-id="e5c00-144">Safe</span></span> | <span data-ttu-id="e5c00-145">Spécifie que seules les mises à jour dont la version la plus récente est disponible dans la même version principale et la version mineure que le package installé seront installées.</span><span class="sxs-lookup"><span data-stu-id="e5c00-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="e5c00-146">Rythme</span><span class="sxs-lookup"><span data-stu-id="e5c00-146">Self</span></span> | <span data-ttu-id="e5c00-147">Met à jour NuGet. exe vers la dernière version; tous les autres arguments sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="e5c00-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="e5c00-148">source</span><span class="sxs-lookup"><span data-stu-id="e5c00-148">Source</span></span> | <span data-ttu-id="e5c00-149">Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="e5c00-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="e5c00-150">En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e5c00-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="e5c00-151">Commentaires</span><span class="sxs-lookup"><span data-stu-id="e5c00-151">Verbosity</span></span> | <span data-ttu-id="e5c00-152">Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="e5c00-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="e5c00-153">Version</span><span class="sxs-lookup"><span data-stu-id="e5c00-153">Version</span></span> | <span data-ttu-id="e5c00-154">Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="e5c00-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="e5c00-155">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e5c00-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e5c00-156">Exemples</span><span class="sxs-lookup"><span data-stu-id="e5c00-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
