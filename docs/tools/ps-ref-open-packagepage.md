---
title: Référence de PowerShell NuGet Open-PackagePage
description: Référence de commande PowerShell de Open-PackagePage dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842262"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="b479e-103">Open-PackagePage (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b479e-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b479e-104">*Déconseillé dans 3.0 + ; disponible uniquement dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="b479e-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b479e-105">Lance le navigateur par défaut avec le projet, une licence ou une URL d’abus de rapport pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="b479e-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="b479e-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b479e-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b479e-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b479e-107">Parameters</span></span>

| <span data-ttu-id="b479e-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="b479e-108">Parameter</span></span> | <span data-ttu-id="b479e-109">Description</span><span class="sxs-lookup"><span data-stu-id="b479e-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b479e-110">Id</span><span class="sxs-lookup"><span data-stu-id="b479e-110">Id</span></span> | <span data-ttu-id="b479e-111">L’ID de package du package souhaité.</span><span class="sxs-lookup"><span data-stu-id="b479e-111">The package ID of the desired package.</span></span> <span data-ttu-id="b479e-112">-Id commutateur proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="b479e-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b479e-113">Version</span><span class="sxs-lookup"><span data-stu-id="b479e-113">Version</span></span> | <span data-ttu-id="b479e-114">La version du package, par défaut vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="b479e-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="b479e-115">source</span><span class="sxs-lookup"><span data-stu-id="b479e-115">Source</span></span> | <span data-ttu-id="b479e-116">La source du package, par défaut pour la source sélectionnée dans la liste déroulante de la source.</span><span class="sxs-lookup"><span data-stu-id="b479e-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="b479e-117">Licence</span><span class="sxs-lookup"><span data-stu-id="b479e-117">License</span></span> | <span data-ttu-id="b479e-118">Ouvre le navigateur vers une URL de licence du package.</span><span class="sxs-lookup"><span data-stu-id="b479e-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="b479e-119">Si - licence ni - ReportAbuse est spécifié, le navigateur ouvre URL du projet du package.</span><span class="sxs-lookup"><span data-stu-id="b479e-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="b479e-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="b479e-120">ReportAbuse</span></span> | <span data-ttu-id="b479e-121">Ouvre le navigateur vers l’URL un abus de rapport du package.</span><span class="sxs-lookup"><span data-stu-id="b479e-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="b479e-122">Si - licence ni - ReportAbuse est spécifié, le navigateur ouvre URL du projet du package.</span><span class="sxs-lookup"><span data-stu-id="b479e-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="b479e-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="b479e-123">PassThru</span></span> | <span data-ttu-id="b479e-124">Affiche l’URL ; Utilisez avec - WhatIf pour supprimer l’ouverture du navigateur.</span><span class="sxs-lookup"><span data-stu-id="b479e-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="b479e-125">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="b479e-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b479e-126">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="b479e-126">Common Parameters</span></span>

<span data-ttu-id="b479e-127">`Open-PackagePage` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b479e-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b479e-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="b479e-128">Examples</span></span>

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