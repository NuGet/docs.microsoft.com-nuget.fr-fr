---
title: Mise à jour NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Update-Package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327266"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9316b-103">Update-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9316b-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9316b-104">*Disponible uniquement dans la [console du gestionnaire de package NuGet](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="9316b-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9316b-105">Met à jour un package et ses dépendances, ou tous les packages d’un projet, vers une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="9316b-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="9316b-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9316b-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="9316b-107">Dans NuGet 2.8 +, `Update-Package` peut être utilisé pour rétrograder un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="9316b-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="9316b-108">Par exemple, si vous avez installé Microsoft. AspNet. MVC 5.1.0-RC1, la commande suivante le rétrograde à 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="9316b-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="9316b-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9316b-109">Parameters</span></span>

|  <span data-ttu-id="9316b-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9316b-110">Parameter</span></span> | <span data-ttu-id="9316b-111">Description</span><span class="sxs-lookup"><span data-stu-id="9316b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9316b-112">Id</span><span class="sxs-lookup"><span data-stu-id="9316b-112">Id</span></span> | <span data-ttu-id="9316b-113">Identificateur du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="9316b-113">The identifier of the package to update.</span></span> <span data-ttu-id="9316b-114">En cas d’omission, met à jour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="9316b-114">If omitted, updates all packages.</span></span> <span data-ttu-id="9316b-115">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="9316b-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9316b-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="9316b-116">IgnoreDependencies</span></span> | <span data-ttu-id="9316b-117">Ignore la mise à jour des dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="9316b-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="9316b-118">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="9316b-118">ProjectName</span></span> | <span data-ttu-id="9316b-119">Nom du projet contenant les packages à mettre à jour, par défaut pour tous les projets.</span><span class="sxs-lookup"><span data-stu-id="9316b-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="9316b-120">Version</span><span class="sxs-lookup"><span data-stu-id="9316b-120">Version</span></span> | <span data-ttu-id="9316b-121">Version à utiliser pour la mise à niveau, avec la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="9316b-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="9316b-122">Dans NuGet 3.0 +, la valeur de version doit être l’une des valeurs les *plus basses, les plus élevées, les HighestMinor*ou les *HighestPatch* (équivalent à-Safe).</span><span class="sxs-lookup"><span data-stu-id="9316b-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="9316b-123">Safe</span><span class="sxs-lookup"><span data-stu-id="9316b-123">Safe</span></span> | <span data-ttu-id="9316b-124">Limite les mises à niveau vers des versions avec la même version principale et la version mineure que le package actuellement installé.</span><span class="sxs-lookup"><span data-stu-id="9316b-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="9316b-125">source</span><span class="sxs-lookup"><span data-stu-id="9316b-125">Source</span></span> | <span data-ttu-id="9316b-126">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="9316b-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="9316b-127">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="9316b-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9316b-128">En cas d’omission `Update-Package` , effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="9316b-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="9316b-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="9316b-129">IncludePrerelease</span></span> | <span data-ttu-id="9316b-130">Contient des packages de version préliminaire pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="9316b-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="9316b-131">Réinstallation</span><span class="sxs-lookup"><span data-stu-id="9316b-131">Reinstall</span></span> | <span data-ttu-id="9316b-132">Resintalls les packages en utilisant les versions actuellement installées.</span><span class="sxs-lookup"><span data-stu-id="9316b-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="9316b-133">Consultez [Réinstallation et mise à jour des packages](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9316b-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="9316b-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="9316b-134">FileConflictAction</span></span> | <span data-ttu-id="9316b-135">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="9316b-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="9316b-136">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="9316b-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="9316b-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="9316b-137">DependencyVersion</span></span> | <span data-ttu-id="9316b-138">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes:</span><span class="sxs-lookup"><span data-stu-id="9316b-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="9316b-139">La *plus basse* (par défaut): la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="9316b-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="9316b-140">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="9316b-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="9316b-141">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="9316b-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="9316b-142">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres): la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="9316b-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="9316b-143">Vous pouvez définir la valeur par défaut à [`dependencyVersion`](../nuget-config-file.md#config-section) l’aide du `Nuget.Config` paramètre dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="9316b-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="9316b-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="9316b-144">ToHighestPatch</span></span> | <span data-ttu-id="9316b-145">équivalent à-Safe.</span><span class="sxs-lookup"><span data-stu-id="9316b-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="9316b-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="9316b-146">ToHighestMinor</span></span> | <span data-ttu-id="9316b-147">Limite les mises à niveau à des versions avec la même version principale que le package actuellement installé.</span><span class="sxs-lookup"><span data-stu-id="9316b-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="9316b-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="9316b-148">WhatIf</span></span> | <span data-ttu-id="9316b-149">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="9316b-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="9316b-150">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="9316b-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="9316b-151">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="9316b-151">Common Parameters</span></span>

<span data-ttu-id="9316b-152">`Update-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9316b-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="9316b-153">Exemples</span><span class="sxs-lookup"><span data-stu-id="9316b-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```