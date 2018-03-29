---
title: Référence de PowerShell NuGet Open-PackagePage | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de commande PowerShell de PackagePage de l’ouverture de la Console du Gestionnaire de Package NuGet dans Visual Studio.
keywords: NuGet package manager console, commandes Powershell de NuGet, NuGet Powershell référence, ouvrez-PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="f8039-104">Ouvrir-PackagePage (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f8039-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f8039-105">*Déconseillé dans 3.0 + ; disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="f8039-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f8039-106">Lance le navigateur par défaut avec le projet, les licences ou les URL d’abus de rapport pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="f8039-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="f8039-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f8039-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f8039-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f8039-108">Parameters</span></span>

| <span data-ttu-id="f8039-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f8039-109">Parameter</span></span> | <span data-ttu-id="f8039-110">Description</span><span class="sxs-lookup"><span data-stu-id="f8039-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8039-111">Id</span><span class="sxs-lookup"><span data-stu-id="f8039-111">Id</span></span> | <span data-ttu-id="f8039-112">L’ID de package du package souhaité.</span><span class="sxs-lookup"><span data-stu-id="f8039-112">The package ID of the desired package.</span></span> <span data-ttu-id="f8039-113">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="f8039-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f8039-114">Version</span><span class="sxs-lookup"><span data-stu-id="f8039-114">Version</span></span> | <span data-ttu-id="f8039-115">La version du package, par défaut pour la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="f8039-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f8039-116">Source</span><span class="sxs-lookup"><span data-stu-id="f8039-116">Source</span></span> | <span data-ttu-id="f8039-117">La source du package, par défaut pour la source sélectionnée dans la liste déroulante de la source.</span><span class="sxs-lookup"><span data-stu-id="f8039-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="f8039-118">Licence</span><span class="sxs-lookup"><span data-stu-id="f8039-118">License</span></span> | <span data-ttu-id="f8039-119">Ouvre le navigateur vers une URL de licence du package.</span><span class="sxs-lookup"><span data-stu-id="f8039-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="f8039-120">Si - licence ni - ReportAbuse est spécifié, le navigateur s’ouvre projet URL du package.</span><span class="sxs-lookup"><span data-stu-id="f8039-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f8039-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="f8039-121">ReportAbuse</span></span> | <span data-ttu-id="f8039-122">Ouvre le navigateur vers une URL d’abus de rapport du package.</span><span class="sxs-lookup"><span data-stu-id="f8039-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="f8039-123">Si - licence ni - ReportAbuse est spécifié, le navigateur s’ouvre projet URL du package.</span><span class="sxs-lookup"><span data-stu-id="f8039-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f8039-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="f8039-124">PassThru</span></span> | <span data-ttu-id="f8039-125">Affiche l’URL ; Utilisez avec - WhatIf pour supprimer d’ouvrir le navigateur.</span><span class="sxs-lookup"><span data-stu-id="f8039-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="f8039-126">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="f8039-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f8039-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="f8039-127">Common Parameters</span></span>

<span data-ttu-id="f8039-128">`Open-PackagePage` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f8039-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f8039-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="f8039-129">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```