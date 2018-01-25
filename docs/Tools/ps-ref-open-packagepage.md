---
title: "Référence de PowerShell NuGet Open-PackagePage | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande PowerShell de PackagePage de l’ouverture de la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, NuGet Powershell référence, ouvrez-PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="37669-104">Ouvrir-PackagePage (Console du Gestionnaire de Package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="37669-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="37669-105">*Déconseillé dans 3.0 + ; disponible uniquement dans les [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="37669-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="37669-106">Lance le navigateur par défaut avec le projet, les licences ou les URL d’abus de rapport pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="37669-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="37669-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="37669-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="37669-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="37669-108">Parameters</span></span>

| <span data-ttu-id="37669-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="37669-109">Parameter</span></span> | <span data-ttu-id="37669-110">Description</span><span class="sxs-lookup"><span data-stu-id="37669-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="37669-111">Id</span><span class="sxs-lookup"><span data-stu-id="37669-111">Id</span></span> | <span data-ttu-id="37669-112">L’ID de package du package souhaité.</span><span class="sxs-lookup"><span data-stu-id="37669-112">The package ID of the desired package.</span></span> <span data-ttu-id="37669-113">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="37669-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="37669-114">Version</span><span class="sxs-lookup"><span data-stu-id="37669-114">Version</span></span> | <span data-ttu-id="37669-115">La version du package, par défaut pour la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="37669-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="37669-116">Source</span><span class="sxs-lookup"><span data-stu-id="37669-116">Source</span></span> | <span data-ttu-id="37669-117">La source du package, par défaut pour la source sélectionnée dans la liste déroulante de la source.</span><span class="sxs-lookup"><span data-stu-id="37669-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="37669-118">Licence</span><span class="sxs-lookup"><span data-stu-id="37669-118">License</span></span> | <span data-ttu-id="37669-119">Ouvre le navigateur vers une URL de licence du package.</span><span class="sxs-lookup"><span data-stu-id="37669-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="37669-120">Si - licence ni - ReportAbuse est spécifié, le navigateur s’ouvre projet URL du package.</span><span class="sxs-lookup"><span data-stu-id="37669-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="37669-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="37669-121">ReportAbuse</span></span> | <span data-ttu-id="37669-122">Ouvre le navigateur vers une URL d’abus de rapport du package.</span><span class="sxs-lookup"><span data-stu-id="37669-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="37669-123">Si - licence ni - ReportAbuse est spécifié, le navigateur s’ouvre projet URL du package.</span><span class="sxs-lookup"><span data-stu-id="37669-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="37669-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="37669-124">PassThru</span></span> | <span data-ttu-id="37669-125">Affiche l’URL ; Utilisez avec - WhatIf pour supprimer d’ouvrir le navigateur.</span><span class="sxs-lookup"><span data-stu-id="37669-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="37669-126">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="37669-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="37669-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="37669-127">Common Parameters</span></span>

<span data-ttu-id="37669-128">`Open-PackagePage`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="37669-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="37669-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="37669-129">Examples</span></span>

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