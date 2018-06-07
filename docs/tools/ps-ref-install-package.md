---
title: Référence de PowerShell Install-Package NuGet
description: Référence de commande PowerShell de Package d’installation de la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 6b2326d7b1ada8a337ae50ffd09f9deea80545af
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817952"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="fe97a-103">Install-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fe97a-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fe97a-104">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Install-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="fe97a-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="fe97a-105">Installe un package et ses dépendances dans un projet.</span><span class="sxs-lookup"><span data-stu-id="fe97a-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="fe97a-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="fe97a-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="fe97a-107">Dans NuGet 2.8 + `Install-Package` peut passer un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="fe97a-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="fe97a-108">Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :</span><span class="sxs-lookup"><span data-stu-id="fe97a-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="fe97a-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="fe97a-109">Parameters</span></span>

| <span data-ttu-id="fe97a-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="fe97a-110">Parameter</span></span> | <span data-ttu-id="fe97a-111">Description</span><span class="sxs-lookup"><span data-stu-id="fe97a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe97a-112">Id</span><span class="sxs-lookup"><span data-stu-id="fe97a-112">Id</span></span> | <span data-ttu-id="fe97a-113">(Obligatoire) L’identificateur du package à installer.</span><span class="sxs-lookup"><span data-stu-id="fe97a-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="fe97a-114">(*3.0 +*) l’identificateur peut être un chemin d’accès ou l’URL d’un `packages.config` fichier ou un `.nupkg` fichier.</span><span class="sxs-lookup"><span data-stu-id="fe97a-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="fe97a-115">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="fe97a-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="fe97a-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="fe97a-116">IgnoreDependencies</span></span> | <span data-ttu-id="fe97a-117">Installer ce package uniquement, sans ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="fe97a-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="fe97a-118">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="fe97a-118">ProjectName</span></span> | <span data-ttu-id="fe97a-119">Le projet dans lequel installer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="fe97a-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="fe97a-120">Source</span><span class="sxs-lookup"><span data-stu-id="fe97a-120">Source</span></span> | <span data-ttu-id="fe97a-121">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="fe97a-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="fe97a-122">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="fe97a-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="fe97a-123">Si omis, `Install-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="fe97a-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="fe97a-124">Version</span><span class="sxs-lookup"><span data-stu-id="fe97a-124">Version</span></span> | <span data-ttu-id="fe97a-125">La version du package à installer, par défaut pour la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="fe97a-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="fe97a-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="fe97a-126">IncludePrerelease</span></span> | <span data-ttu-id="fe97a-127">Prend en compte les versions préliminaires des packages pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="fe97a-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="fe97a-128">Si omis, seuls les packages stables sont pris en compte.</span><span class="sxs-lookup"><span data-stu-id="fe97a-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="fe97a-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="fe97a-129">FileConflictAction</span></span> | <span data-ttu-id="fe97a-130">Action à prendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="fe97a-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="fe97a-131">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="fe97a-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="fe97a-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="fe97a-132">DependencyVersion</span></span> | <span data-ttu-id="fe97a-133">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe97a-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="fe97a-134">*La plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="fe97a-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="fe97a-135">*HighestPatch*: la version avec le correctif logiciel le plus bas majeure, mineure la plus basse, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="fe97a-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="fe97a-136">*HighestMinor*: la version avec le plus bas principales, le correctif plus élevé de secondaire, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="fe97a-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="fe97a-137">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="fe97a-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="fe97a-138">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="fe97a-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="fe97a-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="fe97a-139">WhatIf</span></span> | <span data-ttu-id="fe97a-140">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer l’installation.</span><span class="sxs-lookup"><span data-stu-id="fe97a-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="fe97a-141">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="fe97a-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fe97a-142">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="fe97a-142">Common Parameters</span></span>

<span data-ttu-id="fe97a-143">`Install-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fe97a-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fe97a-144">Exemples</span><span class="sxs-lookup"><span data-stu-id="fe97a-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
