---
title: "Référence de Package de mise à jour de NuGet PowerShell | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande PowerShell de Package de mise à jour dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Package de mise à jour"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ae3a4-104">Package de mise à jour (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ae3a4-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ae3a4-105">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="ae3a4-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ae3a4-106">Met à jour un package et ses dépendances ou tous les packages dans un projet, une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="ae3a4-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ae3a4-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ae3a4-108">Dans NuGet 2.8 + `Update-Package` peut être utilisé pour passer d’un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="ae3a4-109">Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :</span><span class="sxs-lookup"><span data-stu-id="ae3a4-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="ae3a4-110">Paramètres</span><span class="sxs-lookup"><span data-stu-id="ae3a4-110">Parameters</span></span>

|  <span data-ttu-id="ae3a4-111">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ae3a4-111">Parameter</span></span> | <span data-ttu-id="ae3a4-112">Description</span><span class="sxs-lookup"><span data-stu-id="ae3a4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae3a4-113">Id</span><span class="sxs-lookup"><span data-stu-id="ae3a4-113">Id</span></span> | <span data-ttu-id="ae3a4-114">L’identificateur du package à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-114">The identifier of the package to update.</span></span> <span data-ttu-id="ae3a4-115">Si omis, met à jour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-115">If omitted, updates all packages.</span></span> <span data-ttu-id="ae3a4-116">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ae3a4-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="ae3a4-117">IgnoreDependencies</span></span> | <span data-ttu-id="ae3a4-118">Ignore la mise à jour des dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-118">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="ae3a4-119">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="ae3a4-119">ProjectName</span></span> | <span data-ttu-id="ae3a4-120">Le nom du projet contenant les packages à mettre à jour, par défaut à tous les projets.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-120">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="ae3a4-121">Version</span><span class="sxs-lookup"><span data-stu-id="ae3a4-121">Version</span></span> | <span data-ttu-id="ae3a4-122">La version à utiliser pour la mise à niveau, la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-122">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="ae3a4-123">Dans NuGet 3.0 +, la valeur de version doit être *la plus faible, plus élevé, HighestMinor*, ou *HighestPatch* (équivalent à - Safe).</span><span class="sxs-lookup"><span data-stu-id="ae3a4-123">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="ae3a4-124">Safe</span><span class="sxs-lookup"><span data-stu-id="ae3a4-124">Safe</span></span> | <span data-ttu-id="ae3a4-125">Contraint les mises à niveau vers des versions uniquement avec la même version majeure et mineure en tant que le package actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-125">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="ae3a4-126">Source</span><span class="sxs-lookup"><span data-stu-id="ae3a4-126">Source</span></span> | <span data-ttu-id="ae3a4-127">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-127">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ae3a4-128">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-128">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ae3a4-129">Si omis, `Uninstall-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-129">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ae3a4-130">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ae3a4-130">IncludePrerelease</span></span> | <span data-ttu-id="ae3a4-131">Inclut les versions préliminaires des packages de mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-131">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="ae3a4-132">Réinstallation</span><span class="sxs-lookup"><span data-stu-id="ae3a4-132">Reinstall</span></span> | <span data-ttu-id="ae3a4-133">Packages de Resintalls à l’aide de leur version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-133">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="ae3a4-134">Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ae3a4-134">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="ae3a4-135">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ae3a4-135">FileConflictAction</span></span> | <span data-ttu-id="ae3a4-136">Action à prendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-136">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ae3a4-137">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="ae3a4-137">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="ae3a4-138">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ae3a4-138">DependencyVersion</span></span> | <span data-ttu-id="ae3a4-139">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae3a4-139">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ae3a4-140">*La plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="ae3a4-140">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ae3a4-141">*HighestPatch*: la version avec le correctif logiciel le plus bas majeure, mineure la plus basse, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="ae3a4-141">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ae3a4-142">*HighestMinor*: la version avec le plus bas principales, le correctif plus élevé de secondaire, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="ae3a4-142">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ae3a4-143">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="ae3a4-143">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="ae3a4-144">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-144">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="ae3a4-145">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="ae3a4-145">ToHighestPatch</span></span> | <span data-ttu-id="ae3a4-146">Contraint les mises à niveau uniquement aux versions avec la version mineure de même que le package actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-146">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="ae3a4-147">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="ae3a4-147">ToHighestMinor</span></span> | <span data-ttu-id="ae3a4-148">Contraint les mises à niveau uniquement aux versions avec la même version principale que le package actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-148">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="ae3a4-149">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ae3a4-149">WhatIf</span></span> | <span data-ttu-id="ae3a4-150">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-150">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="ae3a4-151">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-151">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="ae3a4-152">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="ae3a4-152">Common Parameters</span></span>

<span data-ttu-id="ae3a4-153">`Update-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ae3a4-153">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="ae3a4-154">Exemples</span><span class="sxs-lookup"><span data-stu-id="ae3a4-154">Examples</span></span>

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