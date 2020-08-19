---
title: Commande d’installation de l’interface CLI NuGet
description: Référence pour la commande nuget.exe install
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623095"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="d0c69-103">commande Install (interface CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="d0c69-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="d0c69-104">**S’applique à :** &bullet; **versions prises en charge par** la consommation des packages : toutes</span><span class="sxs-lookup"><span data-stu-id="d0c69-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d0c69-105">Télécharge et installe un package dans un projet, en utilisant par défaut le dossier actif, à l’aide des sources de package spécifiées.</span><span class="sxs-lookup"><span data-stu-id="d0c69-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="d0c69-106">Pour télécharger un package directement en dehors du contexte d’un projet, accédez à la page du package sur [NuGet.org](https://www.nuget.org) et sélectionnez le lien de **Téléchargement** .</span><span class="sxs-lookup"><span data-stu-id="d0c69-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="d0c69-107">Si aucune source n’est spécifiée, celles répertoriées dans le fichier de configuration global `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="d0c69-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="d0c69-108">Pour plus d’informations, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md) .</span><span class="sxs-lookup"><span data-stu-id="d0c69-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="d0c69-109">Si aucun package spécifique n’est spécifié, `install` installe tous les packages répertoriés dans le fichier du projet `packages.config` , en le rendant similaire à [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="d0c69-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="d0c69-110">La `install` commande ne modifie pas un fichier projet ou `packages.config` . de cette façon, elle est semblable à dans le sens `restore` où elle ajoute uniquement des packages sur le disque, mais ne modifie pas les dépendances d’un projet.</span><span class="sxs-lookup"><span data-stu-id="d0c69-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="d0c69-111">Pour ajouter une dépendance, ajoutez un package par le biais de l’interface utilisateur ou de la console du gestionnaire de package dans Visual Studio, ou modifiez, `packages.config` puis exécutez `install` ou `restore` .</span><span class="sxs-lookup"><span data-stu-id="d0c69-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="d0c69-112">Usage</span><span class="sxs-lookup"><span data-stu-id="d0c69-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="d0c69-113">où `<packageID>` nomme le package à installer (à l’aide de la version la plus récente) ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à installer.</span><span class="sxs-lookup"><span data-stu-id="d0c69-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="d0c69-114">Vous pouvez indiquer une version spécifique avec l' `-Version` option.</span><span class="sxs-lookup"><span data-stu-id="d0c69-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="d0c69-115">Options</span><span class="sxs-lookup"><span data-stu-id="d0c69-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d0c69-116">Fichier de configuration NuGet à appliquer.</span><span class="sxs-lookup"><span data-stu-id="d0c69-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d0c69-117">S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d0c69-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="d0c69-118">*(4.4 +)* Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0c69-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d0c69-119">La *plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="d0c69-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d0c69-120">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="d0c69-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d0c69-121">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="d0c69-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d0c69-122">La *plus élevée*: la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="d0c69-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="d0c69-123">*Ignorer*: aucun package de dépendances ne sera utilisé</span><span class="sxs-lookup"><span data-stu-id="d0c69-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="d0c69-124">Téléchargez directement sans remplir de caches avec des métadonnées ou des binaires.</span><span class="sxs-lookup"><span data-stu-id="d0c69-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="d0c69-125">Désactive l’installation de plusieurs packages en parallèle.</span><span class="sxs-lookup"><span data-stu-id="d0c69-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="d0c69-126">Installe le package dans un dossier nommé avec uniquement le nom du package et non le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="d0c69-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="d0c69-127">*(3.2 +)* Liste de sources de packages à utiliser comme secours si le package est introuvable dans la source principale ou par défaut.</span><span class="sxs-lookup"><span data-stu-id="d0c69-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d0c69-128">*(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.</span><span class="sxs-lookup"><span data-stu-id="d0c69-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="d0c69-129">*(4.4 +)* Framework cible utilisé pour la sélection des dépendances.</span><span class="sxs-lookup"><span data-stu-id="d0c69-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="d0c69-130">La valeur par défaut est « any » s’il n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="d0c69-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d0c69-131">Affiche des informations d’aide pour la commande.</span><span class="sxs-lookup"><span data-stu-id="d0c69-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="d0c69-132">Empêche NuGet d’utiliser les packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="d0c69-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="d0c69-133">Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d0c69-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d0c69-134">Supprime les invites de saisie ou de confirmation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d0c69-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="d0c69-135">Spécifie le dossier dans lequel les packages sont installés.</span><span class="sxs-lookup"><span data-stu-id="d0c69-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="d0c69-136">Si aucun dossier n’est spécifié, le dossier actif est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d0c69-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="d0c69-137">Spécifie les types de fichiers à enregistrer après l’installation du package : l’un des éléments `nuspec` , `nupkg` ou `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="d0c69-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="d0c69-138">Autorise l’installation des packages de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="d0c69-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="d0c69-139">Cet indicateur n’est pas requis lors de la restauration de packages avec `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="d0c69-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="d0c69-140">Vérifie que la restauration des packages est activée avant de télécharger et d’installer les packages.</span><span class="sxs-lookup"><span data-stu-id="d0c69-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="d0c69-141">Pour plus d’informations, consultez [restauration de packages](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d0c69-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="d0c69-142">Spécifie le dossier racine de la solution pour laquelle restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="d0c69-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="d0c69-143">Spécifie la liste des sources de packages (sous forme d’URL) à utiliser.</span><span class="sxs-lookup"><span data-stu-id="d0c69-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="d0c69-144">En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d0c69-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d0c69-145">Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d0c69-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="d0c69-146">Spécifie la version du package à installer.</span><span class="sxs-lookup"><span data-stu-id="d0c69-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="d0c69-147">Voir aussi [variables d’environnement](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d0c69-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d0c69-148">Exemples</span><span class="sxs-lookup"><span data-stu-id="d0c69-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
