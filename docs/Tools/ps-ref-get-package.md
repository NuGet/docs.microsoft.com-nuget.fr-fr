---
title: "Référence de PowerShell Get-Package NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "Référence de commande PowerShell de Get-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3f93ab82e9fb769ee20070aa39ba8e3e05953839
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7241e-104">Get-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7241e-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7241e-105">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Get-Package générique, consultez la [PowerShell PackageManagement référence](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="7241e-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7241e-106">Récupère la liste des packages installés dans le référentiel local, répertorie les packages disponibles à partir d’une source de package lorsqu’il est utilisé avec le commutateur - ListAvailable ou listes de mises à jour disponibles lorsqu’il est utilisé avec le commutateur - mise à jour.</span><span class="sxs-lookup"><span data-stu-id="7241e-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="7241e-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="7241e-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="7241e-108">Sans paramètres, `Get-Package` affiche la liste des packages installés dans le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="7241e-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="7241e-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7241e-109">Parameters</span></span>

| <span data-ttu-id="7241e-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7241e-110">Parameter</span></span> | <span data-ttu-id="7241e-111">Description</span><span class="sxs-lookup"><span data-stu-id="7241e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7241e-112">Source</span><span class="sxs-lookup"><span data-stu-id="7241e-112">Source</span></span> | <span data-ttu-id="7241e-113">Le chemin d’accès URL ou un dossier pour le package.</span><span class="sxs-lookup"><span data-stu-id="7241e-113">The URL or folder path for the package .</span></span> <span data-ttu-id="7241e-114">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="7241e-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7241e-115">Si omis, `Get-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="7241e-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="7241e-116">Lorsqu’il est utilisé avec - ListAvailable, par défaut nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7241e-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="7241e-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="7241e-117">ListAvailable</span></span> | <span data-ttu-id="7241e-118">Répertorie les packages disponibles à partir d’une source de package, par défaut nuget.org. Indique une valeur par défaut de 50 packages sauf si - PageSize et/ou - premier est spécifié.</span><span class="sxs-lookup"><span data-stu-id="7241e-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="7241e-119">Mises à jour</span><span class="sxs-lookup"><span data-stu-id="7241e-119">Updates</span></span> | <span data-ttu-id="7241e-120">Répertorie les packages qui ont une mise à jour est disponible à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="7241e-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="7241e-121">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="7241e-121">ProjectName</span></span> | <span data-ttu-id="7241e-122">Le projet à partir de laquelle obtenir les packages installés.</span><span class="sxs-lookup"><span data-stu-id="7241e-122">The project from which to get installed packages.</span></span> <span data-ttu-id="7241e-123">Si omis, retourne installées des projets pour la solution entière.</span><span class="sxs-lookup"><span data-stu-id="7241e-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="7241e-124">Filtre</span><span class="sxs-lookup"><span data-stu-id="7241e-124">Filter</span></span> | <span data-ttu-id="7241e-125">Une chaîne de filtrage utilisée pour limiter la liste des packages en utilisant l’ID de package, la description et les balises.</span><span class="sxs-lookup"><span data-stu-id="7241e-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="7241e-126">First</span><span class="sxs-lookup"><span data-stu-id="7241e-126">First</span></span> | <span data-ttu-id="7241e-127">Le nombre de packages à retourner à partir du début de la liste.</span><span class="sxs-lookup"><span data-stu-id="7241e-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="7241e-128">Si non spécifié, par défaut est 50.</span><span class="sxs-lookup"><span data-stu-id="7241e-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="7241e-129">Ignorer</span><span class="sxs-lookup"><span data-stu-id="7241e-129">Skip</span></span> | <span data-ttu-id="7241e-130">Omet le premier &lt;int&gt; packages à partir de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="7241e-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="7241e-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="7241e-131">AllVersions</span></span> | <span data-ttu-id="7241e-132">Affiche toutes les versions disponibles de chaque package à la place uniquement la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="7241e-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="7241e-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="7241e-133">IncludePrerelease</span></span> | <span data-ttu-id="7241e-134">Inclut les versions préliminaires des packages dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="7241e-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="7241e-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="7241e-135">PageSize</span></span> | <span data-ttu-id="7241e-136">*(3.0 +)*  Lorsqu’il est utilisé avec - ListAvailable (obligatoire), le nombre de packages à la liste avant de donner une invite pour continuer.</span><span class="sxs-lookup"><span data-stu-id="7241e-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="7241e-137">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="7241e-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7241e-138">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="7241e-138">Common Parameters</span></span>

<span data-ttu-id="7241e-139">`Get-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7241e-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7241e-140">Exemples</span><span class="sxs-lookup"><span data-stu-id="7241e-140">Examples</span></span>

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

