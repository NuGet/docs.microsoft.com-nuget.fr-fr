---
title: "Commande d’installation de NuGet CLI | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Référence de la commande d’installation de nuget.exe"
keywords: "NuGet installer référence, la commande de package d’installation"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="55451-104">installation de commande (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="55451-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="55451-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="55451-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="55451-106">Télécharge et installe un package dans un projet, par défaut dans le dossier actif, l’utilisation de sources de package spécifié.</span><span class="sxs-lookup"><span data-stu-id="55451-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="55451-107">Pour télécharger un package directement à l’extérieur du contexte d’un projet, visitez la page de du package sur [nuget.org](https://www.nuget.org) et sélectionnez le **télécharger** lien.</span><span class="sxs-lookup"><span data-stu-id="55451-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="55451-108">Si aucune source n’est spécifiées, ceux répertoriés dans le fichier de configuration globale, `%APPDATA%\NuGet\NuGet.Config`, sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="55451-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="55451-109">Consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="55451-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="55451-110">Si aucun des packages spécifiques ne sont spécifiés, `install` installe tous les packages répertoriés dans le fichier `packages.config` fichier semblable à [ `restore` ](#restore).</span><span class="sxs-lookup"><span data-stu-id="55451-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="55451-111">(Le `install` commande ne fonctionne pas avec `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="55451-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="55451-112">Le `install` commande ne modifie pas un fichier projet ou `packages.config`; de cette façon, il est similaire à `restore` dans la mesure où il uniquement ajoute des packages sur le disque, mais ne modifie pas les dépendances d’un projet.</span><span class="sxs-lookup"><span data-stu-id="55451-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="55451-113">Pour ajouter une dépendance, ajoutez un projet via l’interface utilisateur du Gestionnaire de Package ou de la Console dans Visual Studio, ou modifier `packages.config` , puis exécutez soit `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="55451-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="55451-114">Pour les projets à l’aide de `project.json`, vous pouvez modifier ce fichier, puis exécutez `restore`.</span><span class="sxs-lookup"><span data-stu-id="55451-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="55451-115">Utilisation</span><span class="sxs-lookup"><span data-stu-id="55451-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="55451-116">où `<packageID>` le package à installer (à l’aide de la version la plus récente), les noms ou `<configFilePath>` identifie les `packages.config` fichier qui répertorie les packages à installer.</span><span class="sxs-lookup"><span data-stu-id="55451-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="55451-117">Vous pouvez indiquer une version spécifique avec la `-Version` option.</span><span class="sxs-lookup"><span data-stu-id="55451-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="55451-118">Options</span><span class="sxs-lookup"><span data-stu-id="55451-118">Options</span></span>

| <span data-ttu-id="55451-119">Option</span><span class="sxs-lookup"><span data-stu-id="55451-119">Option</span></span> | <span data-ttu-id="55451-120">Description</span><span class="sxs-lookup"><span data-stu-id="55451-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55451-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="55451-121">ConfigFile</span></span> | <span data-ttu-id="55451-122">*(2.5 +)*  NuGet le fichier de configuration à appliquer.</span><span class="sxs-lookup"><span data-stu-id="55451-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="55451-123">Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.</span><span class="sxs-lookup"><span data-stu-id="55451-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="55451-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="55451-124">DisableParallelProcessing</span></span> | <span data-ttu-id="55451-125">Désactive l’installation de plusieurs packages en parallèle.</span><span class="sxs-lookup"><span data-stu-id="55451-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="55451-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="55451-126">ExcludeVersion</span></span> | <span data-ttu-id="55451-127">Installe le package dans un dossier nommé avec uniquement le nom du package et pas le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="55451-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="55451-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="55451-128">FallbackSource</span></span> | <span data-ttu-id="55451-129">*(3.2 +)*  Une liste des sources de package à utiliser comme secours au cas où le package n’est pas trouvé dans le serveur principal ou source par défaut.</span><span class="sxs-lookup"><span data-stu-id="55451-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="55451-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="55451-130">ForceEnglishOutput</span></span> | <span data-ttu-id="55451-131">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="55451-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="55451-132">Framework</span><span class="sxs-lookup"><span data-stu-id="55451-132">Framework</span></span> | <span data-ttu-id="55451-133">*(4.4 +)*  Framework cible utilisé pour la sélection des dépendances.</span><span class="sxs-lookup"><span data-stu-id="55451-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="55451-134">Par défaut, 'Any' Si non spécifié.</span><span class="sxs-lookup"><span data-stu-id="55451-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="55451-135">Help</span><span class="sxs-lookup"><span data-stu-id="55451-135">Help</span></span> | <span data-ttu-id="55451-136">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="55451-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="55451-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="55451-137">NoCache</span></span> | <span data-ttu-id="55451-138">NuGet empêche l’utilisation de packages de caches de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="55451-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="55451-139">Non interactif</span><span class="sxs-lookup"><span data-stu-id="55451-139">NonInteractive</span></span> | <span data-ttu-id="55451-140">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="55451-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="55451-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="55451-141">OutputDirectory</span></span> | <span data-ttu-id="55451-142">Spécifie le dossier dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="55451-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="55451-143">Si aucun dossier n’est spécifié, le dossier actif est utilisé.</span><span class="sxs-lookup"><span data-stu-id="55451-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="55451-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="55451-144">PackageSaveMode</span></span> | <span data-ttu-id="55451-145">Spécifie les types de fichiers à enregistrer après l’installation du package : un des `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="55451-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="55451-146">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="55451-146">PreRelease</span></span> | <span data-ttu-id="55451-147">Permet de versions préliminaires des packages à installer.</span><span class="sxs-lookup"><span data-stu-id="55451-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="55451-148">Cet indicateur n’est pas requis lors de la restauration des packages avec `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="55451-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="55451-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="55451-149">RequireConsent</span></span> | <span data-ttu-id="55451-150">Vérifie que la restauration des packages est activé avant de télécharger et installer les packages.</span><span class="sxs-lookup"><span data-stu-id="55451-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="55451-151">Pour plus d’informations, consultez [restauration des packages](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="55451-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="55451-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="55451-152">SolutionDirectory</span></span> | <span data-ttu-id="55451-153">Spécifie le dossier racine de la solution pour lequel restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="55451-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="55451-154">Source</span><span class="sxs-lookup"><span data-stu-id="55451-154">Source</span></span> | <span data-ttu-id="55451-155">Spécifie la liste des sources de package (en tant qu’URL) pour utiliser.</span><span class="sxs-lookup"><span data-stu-id="55451-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="55451-156">Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [NuGet de configuration de comportement](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="55451-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="55451-157">Commentaires</span><span class="sxs-lookup"><span data-stu-id="55451-157">Verbosity</span></span> | <span data-ttu-id="55451-158">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="55451-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="55451-159">Version</span><span class="sxs-lookup"><span data-stu-id="55451-159">Version</span></span> | <span data-ttu-id="55451-160">Spécifie la version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="55451-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="55451-161">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="55451-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="55451-162">Exemples</span><span class="sxs-lookup"><span data-stu-id="55451-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
