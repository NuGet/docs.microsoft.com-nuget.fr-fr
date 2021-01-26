---
title: Informations de référence sur PowerShell Open-PackagePage de NuGet
description: Référence pour Open-PackagePage commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780408"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="855f3-103">Open-PackagePage (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="855f3-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="855f3-104">*Déconseillé dans 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="855f3-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="855f3-105">Lance le navigateur par défaut avec l’URL du projet, de la licence ou du rapport d’abus pour le package spécifié.</span><span class="sxs-lookup"><span data-stu-id="855f3-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="855f3-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="855f3-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="855f3-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="855f3-107">Parameters</span></span>

| <span data-ttu-id="855f3-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="855f3-108">Parameter</span></span> | <span data-ttu-id="855f3-109">Description</span><span class="sxs-lookup"><span data-stu-id="855f3-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="855f3-110">Id</span><span class="sxs-lookup"><span data-stu-id="855f3-110">Id</span></span> | <span data-ttu-id="855f3-111">ID de package du package souhaité.</span><span class="sxs-lookup"><span data-stu-id="855f3-111">The package ID of the desired package.</span></span> <span data-ttu-id="855f3-112">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="855f3-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="855f3-113">Version</span><span class="sxs-lookup"><span data-stu-id="855f3-113">Version</span></span> | <span data-ttu-id="855f3-114">Version du package, avec la version la plus récente par défaut.</span><span class="sxs-lookup"><span data-stu-id="855f3-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="855f3-115">Source</span><span class="sxs-lookup"><span data-stu-id="855f3-115">Source</span></span> | <span data-ttu-id="855f3-116">Source du package, par défaut à la source sélectionnée dans la liste déroulante source.</span><span class="sxs-lookup"><span data-stu-id="855f3-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="855f3-117">Licence</span><span class="sxs-lookup"><span data-stu-id="855f3-117">License</span></span> | <span data-ttu-id="855f3-118">Ouvre le navigateur à l’URL de licence du package.</span><span class="sxs-lookup"><span data-stu-id="855f3-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="855f3-119">Si ni-License ni-ReportAbuse n’est spécifié, le navigateur ouvre l’URL du projet du package.</span><span class="sxs-lookup"><span data-stu-id="855f3-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="855f3-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="855f3-120">ReportAbuse</span></span> | <span data-ttu-id="855f3-121">Ouvre le navigateur sur l’URL d’abus de rapport du package.</span><span class="sxs-lookup"><span data-stu-id="855f3-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="855f3-122">Si ni-License ni-ReportAbuse n’est spécifié, le navigateur ouvre l’URL du projet du package.</span><span class="sxs-lookup"><span data-stu-id="855f3-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="855f3-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="855f3-123">PassThru</span></span> | <span data-ttu-id="855f3-124">Affiche l’URL ; Utilisez avec-WhatIf pour supprimer l’ouverture du navigateur.</span><span class="sxs-lookup"><span data-stu-id="855f3-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="855f3-125">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="855f3-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="855f3-126">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="855f3-126">Common Parameters</span></span>

<span data-ttu-id="855f3-127">`Open-PackagePage` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="855f3-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="855f3-128">Exemples</span><span class="sxs-lookup"><span data-stu-id="855f3-128">Examples</span></span>

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