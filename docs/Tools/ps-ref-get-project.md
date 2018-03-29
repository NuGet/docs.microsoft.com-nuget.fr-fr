---
title: Référence de PowerShell Get-projet NuGet | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de commande GetProject PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
keywords: NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Get-projet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="d82ac-104">Get-projet (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d82ac-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d82ac-105">*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="d82ac-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d82ac-106">Affiche des informations sur la valeur par défaut ou le projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="d82ac-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="d82ac-107">`Get-Project` spécifiquement, retourne une référence à l’objet DTE (environnement d’outils de développement) de Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="d82ac-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="d82ac-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d82ac-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d82ac-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d82ac-109">Parameters</span></span>

| <span data-ttu-id="d82ac-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d82ac-110">Parameter</span></span> | <span data-ttu-id="d82ac-111">Description</span><span class="sxs-lookup"><span data-stu-id="d82ac-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d82ac-112">Name</span><span class="sxs-lookup"><span data-stu-id="d82ac-112">Name</span></span> | <span data-ttu-id="d82ac-113">Spécifie le projet à afficher, par défaut pour le projet par défaut sélectionné dans la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="d82ac-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="d82ac-114">-Nom de commutateur est facultatif.</span><span class="sxs-lookup"><span data-stu-id="d82ac-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="d82ac-115">Tous</span><span class="sxs-lookup"><span data-stu-id="d82ac-115">All</span></span> | <span data-ttu-id="d82ac-116">Affiche des informations pour chaque projet dans la solution ; l’ordre des projets n’est pas déterministe.</span><span class="sxs-lookup"><span data-stu-id="d82ac-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="d82ac-117">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="d82ac-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d82ac-118">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="d82ac-118">Common Parameters</span></span>

<span data-ttu-id="d82ac-119">`Get-Project` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d82ac-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d82ac-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="d82ac-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```