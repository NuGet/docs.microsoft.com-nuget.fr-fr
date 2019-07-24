---
title: Installation NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Install-Package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327336"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="cea13-103">Install-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cea13-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="cea13-104">*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande PowerShell Install-Package générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="cea13-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="cea13-105">Installe un package et ses dépendances dans un projet.</span><span class="sxs-lookup"><span data-stu-id="cea13-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="cea13-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="cea13-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="cea13-107">Dans NuGet 2.8 +, `Install-Package` peut rétrograder un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="cea13-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="cea13-108">Par exemple, si vous avez installé Microsoft. AspNet. MVC 5.1.0-RC1, la commande suivante le rétrograde à 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="cea13-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="cea13-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="cea13-109">Parameters</span></span>

| <span data-ttu-id="cea13-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cea13-110">Parameter</span></span> | <span data-ttu-id="cea13-111">Description</span><span class="sxs-lookup"><span data-stu-id="cea13-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cea13-112">Id</span><span class="sxs-lookup"><span data-stu-id="cea13-112">Id</span></span> | <span data-ttu-id="cea13-113">Souhaitée Identificateur du package à installer.</span><span class="sxs-lookup"><span data-stu-id="cea13-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="cea13-114">(*3.0 +* ) L’identificateur peut être un chemin d’accès ou une URL `packages.config` d’un fichier `.nupkg` ou d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="cea13-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="cea13-115">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="cea13-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="cea13-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="cea13-116">IgnoreDependencies</span></span> | <span data-ttu-id="cea13-117">Installez uniquement ce package et non ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="cea13-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="cea13-118">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="cea13-118">ProjectName</span></span> | <span data-ttu-id="cea13-119">Projet dans lequel installer le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="cea13-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="cea13-120">source</span><span class="sxs-lookup"><span data-stu-id="cea13-120">Source</span></span> | <span data-ttu-id="cea13-121">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="cea13-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="cea13-122">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="cea13-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="cea13-123">En cas d’omission `Install-Package` , effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="cea13-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="cea13-124">Version</span><span class="sxs-lookup"><span data-stu-id="cea13-124">Version</span></span> | <span data-ttu-id="cea13-125">Version du package à installer, avec la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="cea13-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="cea13-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="cea13-126">IncludePrerelease</span></span> | <span data-ttu-id="cea13-127">Prend en compte les packages de version préliminaire pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="cea13-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="cea13-128">En cas d’omission, seuls les packages stables sont pris en compte.</span><span class="sxs-lookup"><span data-stu-id="cea13-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="cea13-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="cea13-129">FileConflictAction</span></span> | <span data-ttu-id="cea13-130">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="cea13-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="cea13-131">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="cea13-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="cea13-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="cea13-132">DependencyVersion</span></span> | <span data-ttu-id="cea13-133">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes:</span><span class="sxs-lookup"><span data-stu-id="cea13-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="cea13-134">La *plus basse* (par défaut): la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="cea13-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="cea13-135">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="cea13-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="cea13-136">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="cea13-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="cea13-137">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres): la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="cea13-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="cea13-138">Vous pouvez définir la valeur par défaut à [`dependencyVersion`](../nuget-config-file.md#config-section) l’aide du `Nuget.Config` paramètre dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="cea13-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="cea13-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="cea13-139">WhatIf</span></span> | <span data-ttu-id="cea13-140">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer l’installation.</span><span class="sxs-lookup"><span data-stu-id="cea13-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="cea13-141">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="cea13-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="cea13-142">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="cea13-142">Common Parameters</span></span>

<span data-ttu-id="cea13-143">`Install-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cea13-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="cea13-144">Exemples</span><span class="sxs-lookup"><span data-stu-id="cea13-144">Examples</span></span>

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