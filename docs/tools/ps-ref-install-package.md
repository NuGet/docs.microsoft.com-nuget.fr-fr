---
title: Référence de PowerShell Install-Package NuGet
description: Référence de commande Install-Package PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546024"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d0963-103">Install-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d0963-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d0963-104">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Install-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d0963-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d0963-105">Installe un package et ses dépendances dans un projet.</span><span class="sxs-lookup"><span data-stu-id="d0963-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="d0963-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d0963-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d0963-107">Dans NuGet 2.8 + `Install-Package` peuvent passer un package existant dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="d0963-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="d0963-108">Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :</span><span class="sxs-lookup"><span data-stu-id="d0963-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="d0963-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d0963-109">Parameters</span></span>

| <span data-ttu-id="d0963-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d0963-110">Parameter</span></span> | <span data-ttu-id="d0963-111">Description</span><span class="sxs-lookup"><span data-stu-id="d0963-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0963-112">Id</span><span class="sxs-lookup"><span data-stu-id="d0963-112">Id</span></span> | <span data-ttu-id="d0963-113">(Obligatoire) L’identificateur du package à installer.</span><span class="sxs-lookup"><span data-stu-id="d0963-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="d0963-114">(*3.0 +*) l’identificateur peut être un chemin d’accès ou l’URL d’un `packages.config` fichier ou un `.nupkg` fichier.</span><span class="sxs-lookup"><span data-stu-id="d0963-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="d0963-115">-Id commutateur proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="d0963-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d0963-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="d0963-116">IgnoreDependencies</span></span> | <span data-ttu-id="d0963-117">Installer uniquement ce package et pas ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="d0963-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="d0963-118">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="d0963-118">ProjectName</span></span> | <span data-ttu-id="d0963-119">Le projet dans lequel installer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="d0963-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d0963-120">Source</span><span class="sxs-lookup"><span data-stu-id="d0963-120">Source</span></span> | <span data-ttu-id="d0963-121">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="d0963-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d0963-122">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="d0963-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d0963-123">Si omis, `Install-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d0963-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d0963-124">Version</span><span class="sxs-lookup"><span data-stu-id="d0963-124">Version</span></span> | <span data-ttu-id="d0963-125">La version du package à installer, par défaut vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="d0963-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d0963-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d0963-126">IncludePrerelease</span></span> | <span data-ttu-id="d0963-127">Prend en compte pour l’installation des packages de version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="d0963-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="d0963-128">Si omis, seuls les packages stables sont considérés comme.</span><span class="sxs-lookup"><span data-stu-id="d0963-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="d0963-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d0963-129">FileConflictAction</span></span> | <span data-ttu-id="d0963-130">L’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="d0963-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d0963-131">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="d0963-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="d0963-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="d0963-132">DependencyVersion</span></span> | <span data-ttu-id="d0963-133">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0963-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d0963-134">*La plus basse* (valeur par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="d0963-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d0963-135">*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="d0963-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d0963-136">*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</span><span class="sxs-lookup"><span data-stu-id="d0963-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d0963-137">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="d0963-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="d0963-138">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="d0963-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="d0963-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d0963-139">WhatIf</span></span> | <span data-ttu-id="d0963-140">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer l’installation.</span><span class="sxs-lookup"><span data-stu-id="d0963-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="d0963-141">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="d0963-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d0963-142">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="d0963-142">Common Parameters</span></span>

<span data-ttu-id="d0963-143">`Install-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d0963-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d0963-144">Exemples</span><span class="sxs-lookup"><span data-stu-id="d0963-144">Examples</span></span>

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
