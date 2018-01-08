---
title: "Référence de PowerShell Install-Package NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Référence de commande PowerShell de Package d’installation de la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Install-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4d7645297d2cd48f39a8e2ec168040710f6fc7a3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c26ff-104">Install-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c26ff-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c26ff-105">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Install-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="c26ff-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="c26ff-106">Installe un package et ses dépendances dans un projet.</span><span class="sxs-lookup"><span data-stu-id="c26ff-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="c26ff-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c26ff-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="c26ff-108">Dans NuGet 2.8 + `Install-Package` peut passer un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="c26ff-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="c26ff-109">Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :</span><span class="sxs-lookup"><span data-stu-id="c26ff-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="c26ff-110">NuGet 2.7 et versions antérieur génère une erreur indiquant qu’une version plus récente est déjà installée.</span><span class="sxs-lookup"><span data-stu-id="c26ff-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>
  
## <a name="parameters"></a><span data-ttu-id="c26ff-111">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c26ff-111">Parameters</span></span>

| <span data-ttu-id="c26ff-112">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c26ff-112">Parameter</span></span> | <span data-ttu-id="c26ff-113">Description</span><span class="sxs-lookup"><span data-stu-id="c26ff-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c26ff-114">Id</span><span class="sxs-lookup"><span data-stu-id="c26ff-114">Id</span></span> | <span data-ttu-id="c26ff-115">(Obligatoire) L’identificateur du package à installer.</span><span class="sxs-lookup"><span data-stu-id="c26ff-115">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="c26ff-116">(*3.0 +*) l’identificateur peut être un chemin d’accès ou l’URL d’un `packages.config` fichier ou un `.nupkg` fichier.</span><span class="sxs-lookup"><span data-stu-id="c26ff-116">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="c26ff-117">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="c26ff-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c26ff-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="c26ff-118">IgnoreDependencies</span></span> | <span data-ttu-id="c26ff-119">Installer ce package uniquement, sans ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="c26ff-119">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="c26ff-120">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="c26ff-120">ProjectName</span></span> | <span data-ttu-id="c26ff-121">Le projet dans lequel installer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="c26ff-121">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="c26ff-122">Source</span><span class="sxs-lookup"><span data-stu-id="c26ff-122">Source</span></span> | <span data-ttu-id="c26ff-123">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="c26ff-123">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c26ff-124">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="c26ff-124">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c26ff-125">Si omis, `Install-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c26ff-125">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c26ff-126">Version</span><span class="sxs-lookup"><span data-stu-id="c26ff-126">Version</span></span> | <span data-ttu-id="c26ff-127">La version du package à installer, par défaut pour la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c26ff-127">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="c26ff-128">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c26ff-128">IncludePrerelease</span></span> | <span data-ttu-id="c26ff-129">Prend en compte les versions préliminaires des packages pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="c26ff-129">Considers prerelease packages for the install.</span></span> <span data-ttu-id="c26ff-130">Si omis, seuls les packages stables sont pris en compte.</span><span class="sxs-lookup"><span data-stu-id="c26ff-130">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="c26ff-131">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c26ff-131">FileConflictAction</span></span> | <span data-ttu-id="c26ff-132">Action à prendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="c26ff-132">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c26ff-133">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="c26ff-133">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="c26ff-134">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c26ff-134">DependencyVersion</span></span> | <span data-ttu-id="c26ff-135">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c26ff-135">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c26ff-136">*La plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="c26ff-136">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c26ff-137">*HighestPatch*: la version avec le correctif logiciel le plus bas majeure, mineure la plus basse, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="c26ff-137">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c26ff-138">*HighestMinor*: la version avec le plus bas principales, le correctif plus élevé de secondaire, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="c26ff-138">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c26ff-139">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="c26ff-139">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="c26ff-140">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="c26ff-140">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="c26ff-141">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c26ff-141">WhatIf</span></span> | <span data-ttu-id="c26ff-142">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer l’installation.</span><span class="sxs-lookup"><span data-stu-id="c26ff-142">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="c26ff-143">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="c26ff-143">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c26ff-144">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="c26ff-144">Common Parameters</span></span>

<span data-ttu-id="c26ff-145">`Install-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c26ff-145">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c26ff-146">Exemples</span><span class="sxs-lookup"><span data-stu-id="c26ff-146">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project.
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages.
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
