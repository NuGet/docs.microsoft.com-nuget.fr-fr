---
title: Référence de PowerShell Get-projet NuGet
description: Référence de commande GetProject PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="909c4-103">Get-projet (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="909c4-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="909c4-104">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="909c4-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="909c4-105">Affiche des informations sur la valeur par défaut ou le projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="909c4-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="909c4-106">`Get-Project` spécifiquement, retourne une référence à l’objet DTE (environnement d’outils de développement) de Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="909c4-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="909c4-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="909c4-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="909c4-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="909c4-108">Parameters</span></span>

| <span data-ttu-id="909c4-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="909c4-109">Parameter</span></span> | <span data-ttu-id="909c4-110">Description</span><span class="sxs-lookup"><span data-stu-id="909c4-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="909c4-111">Name</span><span class="sxs-lookup"><span data-stu-id="909c4-111">Name</span></span> | <span data-ttu-id="909c4-112">Spécifie le projet à afficher, par défaut pour le projet par défaut sélectionné dans la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="909c4-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="909c4-113">-Nom de commutateur est facultatif.</span><span class="sxs-lookup"><span data-stu-id="909c4-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="909c4-114">Tous</span><span class="sxs-lookup"><span data-stu-id="909c4-114">All</span></span> | <span data-ttu-id="909c4-115">Affiche des informations pour chaque projet dans la solution ; l’ordre des projets n’est pas déterministe.</span><span class="sxs-lookup"><span data-stu-id="909c4-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="909c4-116">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="909c4-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="909c4-117">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="909c4-117">Common Parameters</span></span>

<span data-ttu-id="909c4-118">`Get-Project` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="909c4-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="909c4-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="909c4-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```