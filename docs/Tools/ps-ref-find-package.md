---
title: "Référence de PowerShell Find-Package NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: "Référence de commande PowerShell de Find-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Find-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fb55cc71e0d4b8eee28b232e64d2cc42364fc153
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="19e27-104">Find-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="19e27-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="19e27-105">*Version 3.0 + ; Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Find-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="19e27-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="19e27-106">Obtient l’ensemble de packages distants avec l’ID spécifié ou des mots clés à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="19e27-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="19e27-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="19e27-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="19e27-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="19e27-108">Parameters</span></span>

| <span data-ttu-id="19e27-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="19e27-109">Parameter</span></span> | <span data-ttu-id="19e27-110">Description</span><span class="sxs-lookup"><span data-stu-id="19e27-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19e27-111">ID &lt;mots clés&gt;</span><span class="sxs-lookup"><span data-stu-id="19e27-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="19e27-112">(Obligatoire) Mots clés à utiliser pour rechercher la source du package.</span><span class="sxs-lookup"><span data-stu-id="19e27-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="19e27-113">ExactMatch - permet de retourner uniquement les packages dont l’ID de package correspond aux mots clés.</span><span class="sxs-lookup"><span data-stu-id="19e27-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="19e27-114">Si aucun mot clé n’est fournies, `Find-Package` retourne une liste des packages 20 premiers par les téléchargements ou le nombre spécifiée par - tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="19e27-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="19e27-115">Notez que - Id est facultatif et une absence d’opération.</span><span class="sxs-lookup"><span data-stu-id="19e27-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="19e27-116">Source</span><span class="sxs-lookup"><span data-stu-id="19e27-116">Source</span></span> | <span data-ttu-id="19e27-117">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="19e27-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="19e27-118">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="19e27-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="19e27-119">Si omis, `Find-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="19e27-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="19e27-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="19e27-120">AllVersions</span></span> | <span data-ttu-id="19e27-121">Affiche toutes les versions disponibles de chaque package à la place uniquement la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="19e27-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="19e27-122">First</span><span class="sxs-lookup"><span data-stu-id="19e27-122">First</span></span> | <span data-ttu-id="19e27-123">Le nombre de packages à retourner à partir du début de la liste. la valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="19e27-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="19e27-124">Ignorer</span><span class="sxs-lookup"><span data-stu-id="19e27-124">Skip</span></span> | <span data-ttu-id="19e27-125">Omet le premier &lt;int&gt; packages à partir de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="19e27-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="19e27-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="19e27-126">IncludePrerelease</span></span> | <span data-ttu-id="19e27-127">Inclut les versions préliminaires des packages dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="19e27-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="19e27-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="19e27-128">ExactMatch</span></span> | <span data-ttu-id="19e27-129">Spécifié à utiliser &lt;mots clés&gt; comme un ID de package qui respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="19e27-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="19e27-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="19e27-130">StartWith</span></span> | <span data-ttu-id="19e27-131">Retourne les packages dont package ID commence par &lt;mots clés&gt;.</span><span class="sxs-lookup"><span data-stu-id="19e27-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="19e27-132">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="19e27-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="19e27-133">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="19e27-133">Common Parameters</span></span>

<span data-ttu-id="19e27-134">`Find-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="19e27-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="19e27-135">Exemples</span><span class="sxs-lookup"><span data-stu-id="19e27-135">Examples</span></span>

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
