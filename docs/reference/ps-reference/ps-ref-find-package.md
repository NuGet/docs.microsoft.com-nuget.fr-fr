---
title: Informations de référence sur PowerShell Find-package de NuGet
description: Référence de la commande PowerShell Find-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327386"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0aea0-103">Find-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0aea0-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0aea0-104">*Version 3.0 +; Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande PowerShell Find-package générique, consultez les informations de référence sur le fichier [PackageManagement](/powershell/module/packagemanagement/?view=powershell-6)de la page.*</span><span class="sxs-lookup"><span data-stu-id="0aea0-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="0aea0-105">Obtient le jeu de packages distants avec l’ID ou les mots clés spécifiés à partir de la source du package.</span><span class="sxs-lookup"><span data-stu-id="0aea0-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="0aea0-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0aea0-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0aea0-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0aea0-107">Parameters</span></span>

| <span data-ttu-id="0aea0-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0aea0-108">Parameter</span></span> | <span data-ttu-id="0aea0-109">Description</span><span class="sxs-lookup"><span data-stu-id="0aea0-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0aea0-110">Mots &lt;clés d’ID&gt;</span><span class="sxs-lookup"><span data-stu-id="0aea0-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="0aea0-111">Souhaitée Mots clés à utiliser lors de la recherche de la source du package.</span><span class="sxs-lookup"><span data-stu-id="0aea0-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="0aea0-112">Utilisez-ExactMatch pour retourner uniquement les packages dont l’ID de package correspond aux mots clés.</span><span class="sxs-lookup"><span data-stu-id="0aea0-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="0aea0-113">Si aucun mot clé n’est `Find-Package` donné, retourne la liste des 20 premiers packages par téléchargement ou le nombre spécifié par-First.</span><span class="sxs-lookup"><span data-stu-id="0aea0-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="0aea0-114">Notez que-ID est facultatif et qu’il n’y a pas d’opération.</span><span class="sxs-lookup"><span data-stu-id="0aea0-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="0aea0-115">source</span><span class="sxs-lookup"><span data-stu-id="0aea0-115">Source</span></span> | <span data-ttu-id="0aea0-116">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="0aea0-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="0aea0-117">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="0aea0-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="0aea0-118">En cas d’omission `Find-Package` , effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="0aea0-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="0aea0-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="0aea0-119">AllVersions</span></span> | <span data-ttu-id="0aea0-120">Affiche toutes les versions disponibles de chaque package, et non uniquement la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="0aea0-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="0aea0-121">Première</span><span class="sxs-lookup"><span data-stu-id="0aea0-121">First</span></span> | <span data-ttu-id="0aea0-122">Nombre de packages à retourner à partir du début de la liste; la valeur par défaut est 20.</span><span class="sxs-lookup"><span data-stu-id="0aea0-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="0aea0-123">Ignorer</span><span class="sxs-lookup"><span data-stu-id="0aea0-123">Skip</span></span> | <span data-ttu-id="0aea0-124">Omet les premiers &lt;packages int&gt; de la liste affichée.</span><span class="sxs-lookup"><span data-stu-id="0aea0-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="0aea0-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="0aea0-125">IncludePrerelease</span></span> | <span data-ttu-id="0aea0-126">Contient des packages de version préliminaire dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="0aea0-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="0aea0-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="0aea0-127">ExactMatch</span></span> | <span data-ttu-id="0aea0-128">Spécifié pour utiliser &lt;des&gt; Mots clés en tant qu’ID de package qui respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="0aea0-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="0aea0-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="0aea0-129">StartWith</span></span> | <span data-ttu-id="0aea0-130">Retourne les packages dont l’ID de &lt;package&gt;commence par des mots clés.</span><span class="sxs-lookup"><span data-stu-id="0aea0-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="0aea0-131">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="0aea0-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0aea0-132">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="0aea0-132">Common Parameters</span></span>

<span data-ttu-id="0aea0-133">`Find-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0aea0-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0aea0-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="0aea0-134">Examples</span></span>

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
