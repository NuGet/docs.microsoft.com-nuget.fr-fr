---
title: Informations de référence sur PowerShell pour le projet NuGet
description: Référence pour la commande PowerShell GetProject dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384618"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="60831-103">Get-Project (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="60831-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="60831-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="60831-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="60831-105">Affiche des informations sur le projet par défaut ou spécifié.</span><span class="sxs-lookup"><span data-stu-id="60831-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="60831-106">`Get-Project` retourne spécifiquement un référent à l’objet Visual Studio DTE (Development Tools Environment) pour le projet.</span><span class="sxs-lookup"><span data-stu-id="60831-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="60831-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="60831-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="60831-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="60831-108">Parameters</span></span>

| <span data-ttu-id="60831-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="60831-109">Parameter</span></span> | <span data-ttu-id="60831-110">Description</span><span class="sxs-lookup"><span data-stu-id="60831-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60831-111">Name</span><span class="sxs-lookup"><span data-stu-id="60831-111">Name</span></span> | <span data-ttu-id="60831-112">Spécifie le projet à afficher, en définissant par défaut le projet par défaut sélectionné dans la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="60831-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="60831-113">Le commutateur-Name est lui-même facultatif.</span><span class="sxs-lookup"><span data-stu-id="60831-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="60831-114">Toutes les</span><span class="sxs-lookup"><span data-stu-id="60831-114">All</span></span> | <span data-ttu-id="60831-115">Affiche des informations pour chaque projet de la solution ; l’ordre des projets n’est pas déterministe.</span><span class="sxs-lookup"><span data-stu-id="60831-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="60831-116">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="60831-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="60831-117">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="60831-117">Common Parameters</span></span>

<span data-ttu-id="60831-118">`Get-Project` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="60831-118">`Get-Project` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="60831-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="60831-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```