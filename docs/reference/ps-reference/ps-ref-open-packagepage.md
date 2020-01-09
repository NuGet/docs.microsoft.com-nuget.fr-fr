---
title: Informations de référence sur PowerShell Open-PackagePage de NuGet
description: Référence pour la commande PowerShell Open-PackagePage dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384426"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="e696b-103">Open-PackagePage (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e696b-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e696b-104">*Déconseillé dans 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="e696b-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e696b-105">Lance le navigateur par défaut avec l’URL du projet, de la licence ou du rapport d’abus pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="e696b-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="e696b-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e696b-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e696b-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="e696b-107">Parameters</span></span>

| <span data-ttu-id="e696b-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e696b-108">Parameter</span></span> | <span data-ttu-id="e696b-109">Description</span><span class="sxs-lookup"><span data-stu-id="e696b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e696b-110">ID</span><span class="sxs-lookup"><span data-stu-id="e696b-110">Id</span></span> | <span data-ttu-id="e696b-111">ID de package du package souhaité.</span><span class="sxs-lookup"><span data-stu-id="e696b-111">The package ID of the desired package.</span></span> <span data-ttu-id="e696b-112">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="e696b-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e696b-113">Version</span><span class="sxs-lookup"><span data-stu-id="e696b-113">Version</span></span> | <span data-ttu-id="e696b-114">Version du package, avec la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="e696b-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="e696b-115">Source</span><span class="sxs-lookup"><span data-stu-id="e696b-115">Source</span></span> | <span data-ttu-id="e696b-116">Source du package, par défaut à la source sélectionnée dans la liste déroulante source.</span><span class="sxs-lookup"><span data-stu-id="e696b-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="e696b-117">Licence</span><span class="sxs-lookup"><span data-stu-id="e696b-117">License</span></span> | <span data-ttu-id="e696b-118">Ouvre le navigateur à l’URL de licence du package.</span><span class="sxs-lookup"><span data-stu-id="e696b-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="e696b-119">Si ni-License ni-ReportAbuse n’est spécifié, le navigateur ouvre l’URL du projet du package.</span><span class="sxs-lookup"><span data-stu-id="e696b-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="e696b-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="e696b-120">ReportAbuse</span></span> | <span data-ttu-id="e696b-121">Ouvre le navigateur sur l’URL d’abus de rapport du package.</span><span class="sxs-lookup"><span data-stu-id="e696b-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="e696b-122">Si ni-License ni-ReportAbuse n’est spécifié, le navigateur ouvre l’URL du projet du package.</span><span class="sxs-lookup"><span data-stu-id="e696b-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="e696b-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="e696b-123">PassThru</span></span> | <span data-ttu-id="e696b-124">Affiche l’URL ; Utilisez avec-WhatIf pour supprimer l’ouverture du navigateur.</span><span class="sxs-lookup"><span data-stu-id="e696b-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="e696b-125">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="e696b-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e696b-126">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="e696b-126">Common Parameters</span></span>

<span data-ttu-id="e696b-127">`Open-PackagePage` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e696b-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e696b-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="e696b-128">Examples</span></span>

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