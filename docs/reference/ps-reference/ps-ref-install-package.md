---
title: Informations de référence sur PowerShell Install-Package de NuGet
description: Référence pour Install-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901692"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5d0bd-103">Install-Package (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5d0bd-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5d0bd-104">*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Install-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="5d0bd-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="5d0bd-105">Installe un package et ses dépendances dans un projet.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="5d0bd-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="5d0bd-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="5d0bd-107">Dans NuGet 2.8 +, `Install-Package` peut rétrograder un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="5d0bd-108">Par exemple, si vous avez installé Microsoft. AspNet. MVC 5.1.0-RC1, la commande suivante le rétrograde à 5.0.0 :</span><span class="sxs-lookup"><span data-stu-id="5d0bd-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="5d0bd-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="5d0bd-109">Parameters</span></span>

| <span data-ttu-id="5d0bd-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="5d0bd-110">Parameter</span></span> | <span data-ttu-id="5d0bd-111">Description</span><span class="sxs-lookup"><span data-stu-id="5d0bd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d0bd-112">Id</span><span class="sxs-lookup"><span data-stu-id="5d0bd-112">Id</span></span> | <span data-ttu-id="5d0bd-113">Souhaitée Identificateur du package à installer.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="5d0bd-114">(*3.0 +*) L’identificateur peut être un chemin d’accès ou une URL d’un `packages.config` fichier ou d’un `.nupkg` fichier.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="5d0bd-115">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5d0bd-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5d0bd-116">IgnoreDependencies</span></span> | <span data-ttu-id="5d0bd-117">Installez uniquement ce package et non ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="5d0bd-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5d0bd-118">ProjectName</span></span> | <span data-ttu-id="5d0bd-119">Projet dans lequel installer le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="5d0bd-120">Source</span><span class="sxs-lookup"><span data-stu-id="5d0bd-120">Source</span></span> | <span data-ttu-id="5d0bd-121">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5d0bd-122">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5d0bd-123">En cas d’omission, `Install-Package` effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5d0bd-124">Version</span><span class="sxs-lookup"><span data-stu-id="5d0bd-124">Version</span></span> | <span data-ttu-id="5d0bd-125">Version du package à installer, avec la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="5d0bd-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5d0bd-126">IncludePrerelease</span></span> | <span data-ttu-id="5d0bd-127">Prend en compte les packages de version préliminaire pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="5d0bd-128">En l’absence d’indications, seuls les packages stables sont considérés.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="5d0bd-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5d0bd-129">FileConflictAction</span></span> | <span data-ttu-id="5d0bd-130">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5d0bd-131">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll* et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="5d0bd-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5d0bd-132">DependencyVersion</span></span> | <span data-ttu-id="5d0bd-133">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d0bd-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5d0bd-134">La *plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="5d0bd-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5d0bd-135">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5d0bd-136">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="5d0bd-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5d0bd-137">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres) : la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="5d0bd-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5d0bd-138">Vous pouvez définir la valeur par défaut à l’aide du [`dependencyVersion`](../nuget-config-file.md#config-section) paramètre dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5d0bd-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5d0bd-139">WhatIf</span></span> | <span data-ttu-id="5d0bd-140">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer l’installation.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="5d0bd-141">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5d0bd-142">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="5d0bd-142">Common Parameters</span></span>

<span data-ttu-id="5d0bd-143">`Install-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5d0bd-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5d0bd-144">Exemples</span><span class="sxs-lookup"><span data-stu-id="5d0bd-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```