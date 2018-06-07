---
title: Référence de PowerShell Get-Package NuGet
description: Référence de commande PowerShell de Get-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f4b71fc44e44dcbd5d123a0e2fed63adb79964b5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818501"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="2277e-103">Get-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2277e-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2277e-104">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Get-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="2277e-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="2277e-105">Récupère la liste des packages installés dans le référentiel local, répertorie les packages disponibles à partir d’une source de package lorsqu’il est utilisé avec le commutateur - ListAvailable ou listes de mises à jour disponibles lorsqu’il est utilisé avec le commutateur - mise à jour.</span><span class="sxs-lookup"><span data-stu-id="2277e-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="2277e-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2277e-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="2277e-107">Sans paramètres, `Get-Package` affiche la liste des packages installés dans le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="2277e-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="2277e-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2277e-108">Parameters</span></span>

| <span data-ttu-id="2277e-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2277e-109">Parameter</span></span> | <span data-ttu-id="2277e-110">Description</span><span class="sxs-lookup"><span data-stu-id="2277e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2277e-111">Source</span><span class="sxs-lookup"><span data-stu-id="2277e-111">Source</span></span> | <span data-ttu-id="2277e-112">Le chemin d’accès URL ou un dossier pour le package.</span><span class="sxs-lookup"><span data-stu-id="2277e-112">The URL or folder path for the package .</span></span> <span data-ttu-id="2277e-113">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="2277e-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="2277e-114">Si omis, `Get-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="2277e-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="2277e-115">Lorsqu’il est utilisé avec - ListAvailable, par défaut nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2277e-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="2277e-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="2277e-116">ListAvailable</span></span> | <span data-ttu-id="2277e-117">Répertorie les packages disponibles à partir d’une source de package, par défaut nuget.org. Indique une valeur par défaut de 50 packages sauf si - PageSize et/ou - premier est spécifié.</span><span class="sxs-lookup"><span data-stu-id="2277e-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="2277e-118">Mises à jour</span><span class="sxs-lookup"><span data-stu-id="2277e-118">Updates</span></span> | <span data-ttu-id="2277e-119">Répertorie les packages qui ont une mise à jour est disponible à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="2277e-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="2277e-120">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="2277e-120">ProjectName</span></span> | <span data-ttu-id="2277e-121">Le projet à partir de laquelle obtenir les packages installés.</span><span class="sxs-lookup"><span data-stu-id="2277e-121">The project from which to get installed packages.</span></span> <span data-ttu-id="2277e-122">Si omis, retourne installées des projets pour la solution entière.</span><span class="sxs-lookup"><span data-stu-id="2277e-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="2277e-123">Filtre</span><span class="sxs-lookup"><span data-stu-id="2277e-123">Filter</span></span> | <span data-ttu-id="2277e-124">Une chaîne de filtrage utilisée pour limiter la liste des packages en utilisant l’ID de package, la description et les balises.</span><span class="sxs-lookup"><span data-stu-id="2277e-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="2277e-125">First</span><span class="sxs-lookup"><span data-stu-id="2277e-125">First</span></span> | <span data-ttu-id="2277e-126">Le nombre de packages à retourner à partir du début de la liste.</span><span class="sxs-lookup"><span data-stu-id="2277e-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="2277e-127">Si non spécifié, par défaut est 50.</span><span class="sxs-lookup"><span data-stu-id="2277e-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="2277e-128">Ignorer</span><span class="sxs-lookup"><span data-stu-id="2277e-128">Skip</span></span> | <span data-ttu-id="2277e-129">Omet le premier &lt;int&gt; packages à partir de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="2277e-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="2277e-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="2277e-130">AllVersions</span></span> | <span data-ttu-id="2277e-131">Affiche toutes les versions disponibles de chaque package à la place uniquement la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="2277e-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="2277e-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="2277e-132">IncludePrerelease</span></span> | <span data-ttu-id="2277e-133">Inclut les versions préliminaires des packages dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="2277e-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="2277e-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="2277e-134">PageSize</span></span> | <span data-ttu-id="2277e-135">*(3.0 +)*  Lorsqu’il est utilisé avec - ListAvailable (obligatoire), le nombre de packages à la liste avant de donner une invite pour continuer.</span><span class="sxs-lookup"><span data-stu-id="2277e-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="2277e-136">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="2277e-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2277e-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="2277e-137">Common Parameters</span></span>

<span data-ttu-id="2277e-138">`Get-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2277e-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2277e-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="2277e-139">Examples</span></span>

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
