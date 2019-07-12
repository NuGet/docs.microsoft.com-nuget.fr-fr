---
title: Référence de PowerShell NuGet Find-Package
description: Référence de commande PowerShell de Find-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842520"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3e316-103">Find-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3e316-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3e316-104">*Version 3.0 et versions ultérieures ; Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Find-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3e316-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3e316-105">Obtient l’ensemble des packages à distance avec l’ID spécifié ou des mots clés à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="3e316-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="3e316-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="3e316-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3e316-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3e316-107">Parameters</span></span>

| <span data-ttu-id="3e316-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3e316-108">Parameter</span></span> | <span data-ttu-id="3e316-109">Description</span><span class="sxs-lookup"><span data-stu-id="3e316-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e316-110">ID &lt;mots clés&gt;</span><span class="sxs-lookup"><span data-stu-id="3e316-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="3e316-111">(Obligatoire) Mots clés à utiliser pour rechercher la source du package.</span><span class="sxs-lookup"><span data-stu-id="3e316-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="3e316-112">Utilisez - ExactMatch pour retourner uniquement les packages dont l’ID de package correspond aux mots clés.</span><span class="sxs-lookup"><span data-stu-id="3e316-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="3e316-113">Si aucun mot clé n’est fournies, `Find-Package` retourne une liste des packages top 20 par téléchargements ou le nombre spécifiée par - tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="3e316-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="3e316-114">Notez que - Id est facultatif et une absence d’opération.</span><span class="sxs-lookup"><span data-stu-id="3e316-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="3e316-115">source</span><span class="sxs-lookup"><span data-stu-id="3e316-115">Source</span></span> | <span data-ttu-id="3e316-116">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="3e316-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3e316-117">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="3e316-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3e316-118">Si omis, `Find-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="3e316-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3e316-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3e316-119">AllVersions</span></span> | <span data-ttu-id="3e316-120">Affiche toutes les versions disponibles de chaque package plutôt que seule la dernière version.</span><span class="sxs-lookup"><span data-stu-id="3e316-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="3e316-121">Première</span><span class="sxs-lookup"><span data-stu-id="3e316-121">First</span></span> | <span data-ttu-id="3e316-122">Le nombre de packages à retourner à partir du début de la liste. la valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="3e316-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="3e316-123">Ignorer</span><span class="sxs-lookup"><span data-stu-id="3e316-123">Skip</span></span> | <span data-ttu-id="3e316-124">Omet le premier &lt;int&gt; packages à partir de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="3e316-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="3e316-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3e316-125">IncludePrerelease</span></span> | <span data-ttu-id="3e316-126">Inclut les packages de version préliminaire dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="3e316-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="3e316-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="3e316-127">ExactMatch</span></span> | <span data-ttu-id="3e316-128">Spécifié à utiliser &lt;mots clés&gt; qu’un ID de package respectant la casse.</span><span class="sxs-lookup"><span data-stu-id="3e316-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="3e316-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="3e316-129">StartWith</span></span> | <span data-ttu-id="3e316-130">Retourne les packages dont package ID commence par &lt;mots clés&gt;.</span><span class="sxs-lookup"><span data-stu-id="3e316-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="3e316-131">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="3e316-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3e316-132">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="3e316-132">Common Parameters</span></span>

<span data-ttu-id="3e316-133">`Find-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3e316-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3e316-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="3e316-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
