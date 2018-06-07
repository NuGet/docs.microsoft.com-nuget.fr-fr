---
title: Commande de mise à jour de NuGet CLI
description: Référence de la commande de mise à jour de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39e269b10a0cf144d5971d2af9f82a606e0b6904
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817705"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="23add-103">update (commande, NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="23add-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="23add-104">**S’applique à :** package consommation &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="23add-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="23add-105">Met à jour tous les packages dans un projet (à l’aide de `packages.config`) pour leurs dernières versions disponibles.</span><span class="sxs-lookup"><span data-stu-id="23add-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="23add-106">Il est recommandé d’exécuter ['restore'](cli-ref-restore.md) avant d’exécuter le `update`.</span><span class="sxs-lookup"><span data-stu-id="23add-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="23add-107">(Pour mettre à jour un package individuel, utilisez [ `nuget install` ](cli-ref-install.md) sans spécifier un numéro de version, dans lequel cas NuGet installe la dernière version.)</span><span class="sxs-lookup"><span data-stu-id="23add-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="23add-108">Remarque : `update` ne fonctionne pas avec l’interface CLI en cours d’exécution sous Mono (Mac OSX ou Linux) ou lorsque vous utilisez le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="23add-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="23add-109">Le `update` commande met également à jour les références d’assembly dans le fichier projet, condition celles référence déjà exister.</span><span class="sxs-lookup"><span data-stu-id="23add-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="23add-110">Si un package de mise à jour a un assembly ajouté, une nouvelle référence est *pas* ajouté.</span><span class="sxs-lookup"><span data-stu-id="23add-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="23add-111">Nouvelles dépendances de package est également inutile leurs références d’assembly ajoutées.</span><span class="sxs-lookup"><span data-stu-id="23add-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="23add-112">Pour inclure ces opérations dans le cadre d’une mise à jour, mettre à jour le package dans Visual Studio à l’aide du Gestionnaire de Package UI ou la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="23add-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="23add-113">Cette commande peut également servir à mettre à jour de nuget.exe lui-même à l’aide de la *-self* indicateur.</span><span class="sxs-lookup"><span data-stu-id="23add-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="23add-114">Utilisation</span><span class="sxs-lookup"><span data-stu-id="23add-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="23add-115">où `<configPath>` soit identifie un `packages.config` ou le fichier de solution qui répertorie les dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="23add-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="23add-116">Options</span><span class="sxs-lookup"><span data-stu-id="23add-116">Options</span></span>

| <span data-ttu-id="23add-117">Option</span><span class="sxs-lookup"><span data-stu-id="23add-117">Option</span></span> | <span data-ttu-id="23add-118">Description</span><span class="sxs-lookup"><span data-stu-id="23add-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="23add-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="23add-119">ConfigFile</span></span> | <span data-ttu-id="23add-120">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="23add-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="23add-121">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="23add-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="23add-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="23add-122">FileConflictAction</span></span> | <span data-ttu-id="23add-123">Spécifie l’action à entreprendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="23add-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="23add-124">Les valeurs sont *remplacer, ignorer, aucun*.</span><span class="sxs-lookup"><span data-stu-id="23add-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="23add-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="23add-125">ForceEnglishOutput</span></span> | <span data-ttu-id="23add-126">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="23add-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="23add-127">Help</span><span class="sxs-lookup"><span data-stu-id="23add-127">Help</span></span> | <span data-ttu-id="23add-128">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="23add-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="23add-129">Id</span><span class="sxs-lookup"><span data-stu-id="23add-129">Id</span></span> | <span data-ttu-id="23add-130">Spécifie une liste d’ID pour mettre à jour de package.</span><span class="sxs-lookup"><span data-stu-id="23add-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="23add-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="23add-131">MSBuildPath</span></span> | <span data-ttu-id="23add-132">*(4.0 +)*  Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="23add-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="23add-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="23add-133">MSBuildVersion</span></span> | <span data-ttu-id="23add-134">*(3.2 +)*  Spécifie la version de MSBuild à utiliser avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="23add-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="23add-135">Valeurs prises en charge sont 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="23add-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="23add-136">Par défaut que le MSBuild dans votre chemin d’accès est sélectionné, sinon la valeur par défaut pour la version installée la plus élevée de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="23add-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="23add-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="23add-137">NonInteractive</span></span> | <span data-ttu-id="23add-138">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="23add-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="23add-139">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="23add-139">PreRelease</span></span> | <span data-ttu-id="23add-140">Permet la mise à jour vers les versions préliminaires.</span><span class="sxs-lookup"><span data-stu-id="23add-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="23add-141">Cet indicateur n’est pas nécessaire lors de la mise à jour des versions préliminaires des packages qui sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="23add-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="23add-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="23add-142">RepositoryPath</span></span> | <span data-ttu-id="23add-143">Spécifie le dossier local dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="23add-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="23add-144">Safe</span><span class="sxs-lookup"><span data-stu-id="23add-144">Safe</span></span> | <span data-ttu-id="23add-145">Spécifie qui met à jour uniquement avec la version la plus récente disponible dans la même version majeure et mineure que le package installé sera installé.</span><span class="sxs-lookup"><span data-stu-id="23add-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="23add-146">Self</span><span class="sxs-lookup"><span data-stu-id="23add-146">Self</span></span> | <span data-ttu-id="23add-147">Nuget.exe mises à jour vers la dernière version ; tous les autres arguments sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="23add-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="23add-148">Source</span><span class="sxs-lookup"><span data-stu-id="23add-148">Source</span></span> | <span data-ttu-id="23add-149">Spécifie la liste des sources de package (en tant qu’URL) pour utiliser les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="23add-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="23add-150">Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="23add-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="23add-151">Commentaires</span><span class="sxs-lookup"><span data-stu-id="23add-151">Verbosity</span></span> | <span data-ttu-id="23add-152">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="23add-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="23add-153">Version</span><span class="sxs-lookup"><span data-stu-id="23add-153">Version</span></span> | <span data-ttu-id="23add-154">Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="23add-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="23add-155">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="23add-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="23add-156">Exemples</span><span class="sxs-lookup"><span data-stu-id="23add-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
