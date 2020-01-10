---
title: Mise à jour NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Update-Package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384854"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5fe27-103">Update-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5fe27-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5fe27-104">*Disponible uniquement dans la [console du gestionnaire de package NuGet](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="5fe27-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5fe27-105">Met à jour un package et ses dépendances, ou tous les packages d’un projet, vers une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="5fe27-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="5fe27-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5fe27-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="5fe27-107">Dans NuGet 2.8 +, `Update-Package` peut être utilisé pour rétrograder un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="5fe27-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="5fe27-108">Par exemple, si vous avez installé Microsoft. AspNet. MVC 5.1.0-RC1, la commande suivante le rétrograde à 5.0.0 :</span><span class="sxs-lookup"><span data-stu-id="5fe27-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="5fe27-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="5fe27-109">Parameters</span></span>

|  <span data-ttu-id="5fe27-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="5fe27-110">Parameter</span></span> | <span data-ttu-id="5fe27-111">Description</span><span class="sxs-lookup"><span data-stu-id="5fe27-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5fe27-112">ID</span><span class="sxs-lookup"><span data-stu-id="5fe27-112">Id</span></span> | <span data-ttu-id="5fe27-113">Identificateur du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="5fe27-113">The identifier of the package to update.</span></span> <span data-ttu-id="5fe27-114">En cas d’omission, met à jour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="5fe27-114">If omitted, updates all packages.</span></span> <span data-ttu-id="5fe27-115">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="5fe27-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5fe27-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5fe27-116">IgnoreDependencies</span></span> | <span data-ttu-id="5fe27-117">Ignore la mise à jour des dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="5fe27-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="5fe27-118">NomProjet</span><span class="sxs-lookup"><span data-stu-id="5fe27-118">ProjectName</span></span> | <span data-ttu-id="5fe27-119">Nom du projet contenant les packages à mettre à jour, par défaut pour tous les projets.</span><span class="sxs-lookup"><span data-stu-id="5fe27-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="5fe27-120">cible</span><span class="sxs-lookup"><span data-stu-id="5fe27-120">Version</span></span> | <span data-ttu-id="5fe27-121">Version à utiliser pour la mise à niveau, avec la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="5fe27-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="5fe27-122">Dans NuGet 3.0 +, la valeur de version doit être l’une des valeurs les *plus basses, les plus élevées, les HighestMinor*ou les *HighestPatch* (équivalent à-Safe).</span><span class="sxs-lookup"><span data-stu-id="5fe27-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="5fe27-123">Safe</span><span class="sxs-lookup"><span data-stu-id="5fe27-123">Safe</span></span> | <span data-ttu-id="5fe27-124">Limite les mises à niveau vers des versions avec la même version principale et la version mineure que le package actuellement installé.</span><span class="sxs-lookup"><span data-stu-id="5fe27-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="5fe27-125">Source</span><span class="sxs-lookup"><span data-stu-id="5fe27-125">Source</span></span> | <span data-ttu-id="5fe27-126">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="5fe27-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5fe27-127">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="5fe27-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5fe27-128">En cas d’omission, `Update-Package` recherche la source de package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5fe27-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5fe27-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5fe27-129">IncludePrerelease</span></span> | <span data-ttu-id="5fe27-130">Contient des packages de version préliminaire pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="5fe27-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="5fe27-131">Réinstallation</span><span class="sxs-lookup"><span data-stu-id="5fe27-131">Reinstall</span></span> | <span data-ttu-id="5fe27-132">Resintalls les packages en utilisant les versions actuellement installées.</span><span class="sxs-lookup"><span data-stu-id="5fe27-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="5fe27-133">Consultez [Réinstallation et mise à jour des packages](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5fe27-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="5fe27-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5fe27-134">FileConflictAction</span></span> | <span data-ttu-id="5fe27-135">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="5fe27-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5fe27-136">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="5fe27-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="5fe27-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5fe27-137">DependencyVersion</span></span> | <span data-ttu-id="5fe27-138">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :</span><span class="sxs-lookup"><span data-stu-id="5fe27-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5fe27-139">La *plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="5fe27-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5fe27-140">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="5fe27-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5fe27-141">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="5fe27-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5fe27-142">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres) : la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="5fe27-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5fe27-143">Vous pouvez définir la valeur par défaut à l’aide du paramètre [`dependencyVersion`](../nuget-config-file.md#config-section) dans le fichier `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="5fe27-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5fe27-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="5fe27-144">ToHighestPatch</span></span> | <span data-ttu-id="5fe27-145">équivalent à-Safe.</span><span class="sxs-lookup"><span data-stu-id="5fe27-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="5fe27-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="5fe27-146">ToHighestMinor</span></span> | <span data-ttu-id="5fe27-147">Limite les mises à niveau à des versions avec la même version principale que le package actuellement installé.</span><span class="sxs-lookup"><span data-stu-id="5fe27-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="5fe27-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5fe27-148">WhatIf</span></span> | <span data-ttu-id="5fe27-149">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="5fe27-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="5fe27-150">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="5fe27-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="5fe27-151">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="5fe27-151">Common Parameters</span></span>

<span data-ttu-id="5fe27-152">`Update-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5fe27-152">`Update-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="5fe27-153">Exemples</span><span class="sxs-lookup"><span data-stu-id="5fe27-153">Examples</span></span>

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
