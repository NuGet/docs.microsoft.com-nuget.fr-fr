---
title: Informations de référence sur PowerShell Find-package de NuGet
description: Référence de la commande PowerShell Find-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384631"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c58aa-103">Find-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c58aa-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c58aa-104">*Version 3.0 +; Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande PowerShell Find-package générique, consultez les informations de référence sur le fichier [PackageManagement](/powershell/module/packagemanagement/?view=powershell-6)de la page.*</span><span class="sxs-lookup"><span data-stu-id="c58aa-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="c58aa-105">Obtient le jeu de packages distants avec l’ID ou les mots clés spécifiés à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="c58aa-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="c58aa-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c58aa-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c58aa-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="c58aa-107">Parameters</span></span>

| <span data-ttu-id="c58aa-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c58aa-108">Parameter</span></span> | <span data-ttu-id="c58aa-109">Description</span><span class="sxs-lookup"><span data-stu-id="c58aa-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c58aa-110">Mots clés d’ID &lt;&gt;</span><span class="sxs-lookup"><span data-stu-id="c58aa-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="c58aa-111">Souhaitée Mots clés à utiliser lors de la recherche de la source du package.</span><span class="sxs-lookup"><span data-stu-id="c58aa-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="c58aa-112">Utilisez-ExactMatch pour retourner uniquement les packages dont l’ID de package correspond aux mots clés.</span><span class="sxs-lookup"><span data-stu-id="c58aa-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="c58aa-113">Si aucun mot clé n’est donné, `Find-Package` retourne la liste des 20 premiers packages par téléchargement, ou le nombre spécifié par-First.</span><span class="sxs-lookup"><span data-stu-id="c58aa-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="c58aa-114">Notez que-ID est facultatif et qu’il n’y a pas d’opération.</span><span class="sxs-lookup"><span data-stu-id="c58aa-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="c58aa-115">Source</span><span class="sxs-lookup"><span data-stu-id="c58aa-115">Source</span></span> | <span data-ttu-id="c58aa-116">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="c58aa-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c58aa-117">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="c58aa-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c58aa-118">En cas d’omission, `Find-Package` recherche la source de package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c58aa-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c58aa-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="c58aa-119">AllVersions</span></span> | <span data-ttu-id="c58aa-120">Affiche toutes les versions disponibles de chaque package, et non uniquement la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c58aa-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="c58aa-121">First</span><span class="sxs-lookup"><span data-stu-id="c58aa-121">First</span></span> | <span data-ttu-id="c58aa-122">Nombre de packages à retourner à partir du début de la liste ; la valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="c58aa-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="c58aa-123">Skip</span><span class="sxs-lookup"><span data-stu-id="c58aa-123">Skip</span></span> | <span data-ttu-id="c58aa-124">Omet les premiers packages de&gt; &lt;int de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="c58aa-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="c58aa-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c58aa-125">IncludePrerelease</span></span> | <span data-ttu-id="c58aa-126">Contient des packages de version préliminaire dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="c58aa-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="c58aa-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="c58aa-127">ExactMatch</span></span> | <span data-ttu-id="c58aa-128">Spécifié pour utiliser &lt;Mots clés&gt; en tant qu’ID de package qui respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="c58aa-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="c58aa-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="c58aa-129">StartWith</span></span> | <span data-ttu-id="c58aa-130">Retourne les packages dont l’ID de package commence par &lt;Mots clés&gt;.</span><span class="sxs-lookup"><span data-stu-id="c58aa-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="c58aa-131">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="c58aa-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c58aa-132">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="c58aa-132">Common Parameters</span></span>

<span data-ttu-id="c58aa-133">`Find-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c58aa-133">`Find-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c58aa-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="c58aa-134">Examples</span></span>

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
