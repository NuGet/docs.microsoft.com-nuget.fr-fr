---
title: Informations de référence sur PowerShell Get-Package de NuGet
description: Référence pour Get-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901731"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c9380-103">Get-Package (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c9380-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c9380-104">*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Get-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="c9380-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="c9380-105">Récupère la liste des packages installés dans le référentiel local, répertorie les packages disponibles à partir d’une source de package lorsqu’ils sont utilisés avec le commutateur-ListAvailable, ou répertorie les mises à jour disponibles lorsqu’elles sont utilisées avec le commutateur-Update.</span><span class="sxs-lookup"><span data-stu-id="c9380-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="c9380-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="c9380-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="c9380-107">Sans paramètres, `Get-Package` affiche la liste des packages installés dans le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="c9380-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="c9380-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c9380-108">Parameters</span></span>

| <span data-ttu-id="c9380-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c9380-109">Parameter</span></span> | <span data-ttu-id="c9380-110">Description</span><span class="sxs-lookup"><span data-stu-id="c9380-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9380-111">Source</span><span class="sxs-lookup"><span data-stu-id="c9380-111">Source</span></span> | <span data-ttu-id="c9380-112">URL ou chemin d’accès du dossier pour le package.</span><span class="sxs-lookup"><span data-stu-id="c9380-112">The URL or folder path for the package .</span></span> <span data-ttu-id="c9380-113">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="c9380-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c9380-114">En cas d’omission, `Get-Package` effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c9380-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="c9380-115">En cas d’utilisation avec-ListAvailable, la valeur par défaut est nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c9380-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="c9380-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="c9380-116">ListAvailable</span></span> | <span data-ttu-id="c9380-117">Répertorie les packages disponibles à partir d’une source de package, par défaut nuget.org. Affiche la valeur par défaut de 50 packages, sauf si-PageSize et/ou-First sont spécifiés.</span><span class="sxs-lookup"><span data-stu-id="c9380-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="c9380-118">Mises à jour</span><span class="sxs-lookup"><span data-stu-id="c9380-118">Updates</span></span> | <span data-ttu-id="c9380-119">Répertorie les packages dont la mise à jour est disponible à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="c9380-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="c9380-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c9380-120">ProjectName</span></span> | <span data-ttu-id="c9380-121">Projet à partir duquel les packages installés doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="c9380-121">The project from which to get installed packages.</span></span> <span data-ttu-id="c9380-122">En cas d’omission, retourne les projets installés pour l’ensemble de la solution.</span><span class="sxs-lookup"><span data-stu-id="c9380-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="c9380-123">Filtrer</span><span class="sxs-lookup"><span data-stu-id="c9380-123">Filter</span></span> | <span data-ttu-id="c9380-124">Chaîne de filtrage utilisée pour limiter la liste des packages en l’appliquant à l’ID de package, à la description et aux balises.</span><span class="sxs-lookup"><span data-stu-id="c9380-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="c9380-125">Premier</span><span class="sxs-lookup"><span data-stu-id="c9380-125">First</span></span> | <span data-ttu-id="c9380-126">Nombre de packages à retourner à partir du début de la liste.</span><span class="sxs-lookup"><span data-stu-id="c9380-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="c9380-127">S’il n’est pas spécifié, la valeur par défaut est 50.</span><span class="sxs-lookup"><span data-stu-id="c9380-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="c9380-128">Ignorer</span><span class="sxs-lookup"><span data-stu-id="c9380-128">Skip</span></span> | <span data-ttu-id="c9380-129">Omet les premiers &lt; packages int &gt; de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="c9380-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="c9380-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="c9380-130">AllVersions</span></span> | <span data-ttu-id="c9380-131">Affiche toutes les versions disponibles de chaque package, et non uniquement la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c9380-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="c9380-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c9380-132">IncludePrerelease</span></span> | <span data-ttu-id="c9380-133">Contient des packages de version préliminaire dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="c9380-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="c9380-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="c9380-134">PageSize</span></span> | <span data-ttu-id="c9380-135">*(3.0 +)* En cas d’utilisation avec-ListAvailable (obligatoire), nombre de packages à répertorier avant de donner une invite pour continuer.</span><span class="sxs-lookup"><span data-stu-id="c9380-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="c9380-136">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="c9380-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c9380-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="c9380-137">Common Parameters</span></span>

<span data-ttu-id="c9380-138">`Get-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c9380-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c9380-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="c9380-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```