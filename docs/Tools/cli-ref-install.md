---
title: "Commande d’installation de NuGet CLI | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande d’installation de nuget.exe"
keywords: "NuGet installer référence, la commande de package d’installation"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d5f53c833fb42c9fe37d0629eab33e8f0bc70d7
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="ad64b-104">installation de commande (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="ad64b-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="ad64b-105">**S’applique à :** package consommation &bullet; **versions prises en charge :** toutes les</span><span class="sxs-lookup"><span data-stu-id="ad64b-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ad64b-106">Télécharge et installe un package dans un projet, par défaut dans le dossier actif, l’utilisation de sources de package spécifié.</span><span class="sxs-lookup"><span data-stu-id="ad64b-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="ad64b-107">Pour télécharger un package directement à l’extérieur du contexte d’un projet, visitez la page de du package sur [nuget.org](https://www.nuget.org) et sélectionnez le **télécharger** lien.</span><span class="sxs-lookup"><span data-stu-id="ad64b-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="ad64b-108">Si aucune source n’est spécifiées, ceux répertoriés dans le fichier de configuration globale, `%APPDATA%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Linux/Mac), sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="ad64b-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="ad64b-109">Consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ad64b-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="ad64b-110">Si aucun des packages spécifiques ne sont spécifiés, `install` installe tous les packages répertoriés dans le fichier `packages.config` fichier semblable à [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ad64b-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="ad64b-111">Le `install` commande ne modifie pas un fichier projet ou `packages.config`; de cette façon, il est similaire à `restore` dans la mesure où il uniquement ajoute des packages sur le disque, mais ne modifie pas les dépendances d’un projet.</span><span class="sxs-lookup"><span data-stu-id="ad64b-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="ad64b-112">Pour ajouter une dépendance, ajoutez un projet via l’interface utilisateur du Gestionnaire de Package ou de la Console dans Visual Studio, ou modifier `packages.config` , puis exécutez soit `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="ad64b-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="ad64b-113">Utilisation</span><span class="sxs-lookup"><span data-stu-id="ad64b-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="ad64b-114">où `<packageID>` le package à installer (à l’aide de la version la plus récente), les noms ou `<configFilePath>` identifie les `packages.config` fichier qui répertorie les packages à installer.</span><span class="sxs-lookup"><span data-stu-id="ad64b-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="ad64b-115">Vous pouvez indiquer une version spécifique avec la `-Version` option.</span><span class="sxs-lookup"><span data-stu-id="ad64b-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="ad64b-116">Options</span><span class="sxs-lookup"><span data-stu-id="ad64b-116">Options</span></span>

| <span data-ttu-id="ad64b-117">Option</span><span class="sxs-lookup"><span data-stu-id="ad64b-117">Option</span></span> | <span data-ttu-id="ad64b-118">Description</span><span class="sxs-lookup"><span data-stu-id="ad64b-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad64b-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ad64b-119">ConfigFile</span></span> | <span data-ttu-id="ad64b-120">Le fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="ad64b-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ad64b-121">Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ad64b-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ad64b-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ad64b-122">DependencyVersion</span></span> | <span data-ttu-id="ad64b-123">*(4.4 +)*  Spécifie une version spécifique, la substitution du comportement de résolution de dépendance par défaut.</span><span class="sxs-lookup"><span data-stu-id="ad64b-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="ad64b-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="ad64b-124">DisableParallelProcessing</span></span> | <span data-ttu-id="ad64b-125">Désactive l’installation de plusieurs packages en parallèle.</span><span class="sxs-lookup"><span data-stu-id="ad64b-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="ad64b-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="ad64b-126">ExcludeVersion</span></span> | <span data-ttu-id="ad64b-127">Installe le package dans un dossier nommé avec uniquement le nom du package et pas le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="ad64b-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="ad64b-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="ad64b-128">FallbackSource</span></span> | <span data-ttu-id="ad64b-129">*(3.2 +)*  Une liste des sources de package à utiliser comme secours au cas où le package n’est pas trouvé dans le serveur principal ou source par défaut.</span><span class="sxs-lookup"><span data-stu-id="ad64b-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="ad64b-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ad64b-130">ForceEnglishOutput</span></span> | <span data-ttu-id="ad64b-131">*(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais.</span><span class="sxs-lookup"><span data-stu-id="ad64b-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ad64b-132">Framework</span><span class="sxs-lookup"><span data-stu-id="ad64b-132">Framework</span></span> | <span data-ttu-id="ad64b-133">*(4.4 +)*  Framework cible utilisé pour la sélection des dépendances.</span><span class="sxs-lookup"><span data-stu-id="ad64b-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="ad64b-134">Par défaut, 'Any' Si non spécifié.</span><span class="sxs-lookup"><span data-stu-id="ad64b-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="ad64b-135">Help</span><span class="sxs-lookup"><span data-stu-id="ad64b-135">Help</span></span> | <span data-ttu-id="ad64b-136">Affiche l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="ad64b-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="ad64b-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="ad64b-137">NoCache</span></span> | <span data-ttu-id="ad64b-138">NuGet empêche l’utilisation de packages de caches de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ad64b-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="ad64b-139">Non interactif</span><span class="sxs-lookup"><span data-stu-id="ad64b-139">NonInteractive</span></span> | <span data-ttu-id="ad64b-140">Supprime les invites de saisie utilisateur ou les confirmations.</span><span class="sxs-lookup"><span data-stu-id="ad64b-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ad64b-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="ad64b-141">OutputDirectory</span></span> | <span data-ttu-id="ad64b-142">Spécifie le dossier dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="ad64b-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ad64b-143">Si aucun dossier n’est spécifié, le dossier actif est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ad64b-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="ad64b-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="ad64b-144">PackageSaveMode</span></span> | <span data-ttu-id="ad64b-145">Spécifie les types de fichiers à enregistrer après l’installation du package : un des `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ad64b-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="ad64b-146">Version préliminaire</span><span class="sxs-lookup"><span data-stu-id="ad64b-146">PreRelease</span></span> | <span data-ttu-id="ad64b-147">Permet de versions préliminaires des packages à installer.</span><span class="sxs-lookup"><span data-stu-id="ad64b-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="ad64b-148">Cet indicateur n’est pas requis lors de la restauration des packages avec `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="ad64b-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="ad64b-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="ad64b-149">RequireConsent</span></span> | <span data-ttu-id="ad64b-150">Vérifie que la restauration des packages est activé avant de télécharger et installer les packages.</span><span class="sxs-lookup"><span data-stu-id="ad64b-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ad64b-151">Pour plus d’informations, consultez [restauration des packages](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ad64b-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="ad64b-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="ad64b-152">SolutionDirectory</span></span> | <span data-ttu-id="ad64b-153">Spécifie le dossier racine de la solution pour lequel restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="ad64b-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="ad64b-154">Source</span><span class="sxs-lookup"><span data-stu-id="ad64b-154">Source</span></span> | <span data-ttu-id="ad64b-155">Spécifie la liste des sources de package (en tant qu’URL) pour utiliser.</span><span class="sxs-lookup"><span data-stu-id="ad64b-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="ad64b-156">Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ad64b-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="ad64b-157">Commentaires</span><span class="sxs-lookup"><span data-stu-id="ad64b-157">Verbosity</span></span> | <span data-ttu-id="ad64b-158">Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*.</span><span class="sxs-lookup"><span data-stu-id="ad64b-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="ad64b-159">Version</span><span class="sxs-lookup"><span data-stu-id="ad64b-159">Version</span></span> | <span data-ttu-id="ad64b-160">Spécifie la version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="ad64b-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="ad64b-161">Consultez également [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ad64b-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ad64b-162">Exemples</span><span class="sxs-lookup"><span data-stu-id="ad64b-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
