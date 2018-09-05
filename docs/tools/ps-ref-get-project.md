---
title: Référence de PowerShell Get-projet NuGet
description: Référence de commande GetProject PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550435"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="0c94d-103">Get-Project (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0c94d-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0c94d-104">*Disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="0c94d-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0c94d-105">Affiche des informations sur la valeur par défaut ou le projet spécifié.</span><span class="sxs-lookup"><span data-stu-id="0c94d-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="0c94d-106">`Get-Project` en particulier, retourne un référent à l’objet DTE (Development Tools Environment) de Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="0c94d-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="0c94d-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0c94d-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0c94d-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0c94d-108">Parameters</span></span>

| <span data-ttu-id="0c94d-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0c94d-109">Parameter</span></span> | <span data-ttu-id="0c94d-110">Description</span><span class="sxs-lookup"><span data-stu-id="0c94d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c94d-111">Name</span><span class="sxs-lookup"><span data-stu-id="0c94d-111">Name</span></span> | <span data-ttu-id="0c94d-112">Spécifie le projet à afficher, par défaut pour le projet par défaut sélectionné dans la Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="0c94d-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="0c94d-113">-Nom du commutateur est lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="0c94d-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="0c94d-114">Tous</span><span class="sxs-lookup"><span data-stu-id="0c94d-114">All</span></span> | <span data-ttu-id="0c94d-115">Affiche des informations pour chaque projet dans la solution. l’ordre des projets n’est pas déterministe.</span><span class="sxs-lookup"><span data-stu-id="0c94d-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="0c94d-116">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="0c94d-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0c94d-117">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="0c94d-117">Common Parameters</span></span>

<span data-ttu-id="0c94d-118">`Get-Project` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0c94d-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0c94d-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="0c94d-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```