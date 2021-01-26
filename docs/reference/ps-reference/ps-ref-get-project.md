---
title: Informations de référence sur PowerShell Get-Project de NuGet
description: Référence pour la commande PowerShell GetProject dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777466"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="ed1dd-103">Get-Project (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ed1dd-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ed1dd-104">*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="ed1dd-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ed1dd-105">Affiche des informations sur le projet par défaut ou spécifié.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="ed1dd-106">`Get-Project` retourne spécifiquement un référent à l’objet Visual Studio DTE (Development Tools Environment) pour le projet.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="ed1dd-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ed1dd-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ed1dd-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="ed1dd-108">Parameters</span></span>

| <span data-ttu-id="ed1dd-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ed1dd-109">Parameter</span></span> | <span data-ttu-id="ed1dd-110">Description</span><span class="sxs-lookup"><span data-stu-id="ed1dd-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed1dd-111">Nom</span><span class="sxs-lookup"><span data-stu-id="ed1dd-111">Name</span></span> | <span data-ttu-id="ed1dd-112">Spécifie le projet à afficher, en définissant par défaut le projet par défaut sélectionné dans la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="ed1dd-113">Le commutateur-Name est lui-même facultatif.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="ed1dd-114">Tous</span><span class="sxs-lookup"><span data-stu-id="ed1dd-114">All</span></span> | <span data-ttu-id="ed1dd-115">Affiche des informations pour chaque projet de la solution ; l’ordre des projets n’est pas déterministe.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="ed1dd-116">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ed1dd-117">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="ed1dd-117">Common Parameters</span></span>

<span data-ttu-id="ed1dd-118">`Get-Project` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ed1dd-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ed1dd-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="ed1dd-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```