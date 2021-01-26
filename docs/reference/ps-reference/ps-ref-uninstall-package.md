---
title: Informations de référence sur PowerShell Uninstall-Package de NuGet
description: Référence pour Uninstall-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 961a9d68e5cba09030401fc871a93bf1145b23a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777397"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d18b8-103">Uninstall-Package (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d18b8-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d18b8-104">*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Uninstall-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d18b8-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d18b8-105">Supprime un package d’un projet, en supprimant éventuellement ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="d18b8-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="d18b8-106">Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d18b8-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="d18b8-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d18b8-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d18b8-108">Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d18b8-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="d18b8-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d18b8-109">Parameters</span></span>

| <span data-ttu-id="d18b8-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d18b8-110">Parameter</span></span> | <span data-ttu-id="d18b8-111">Description</span><span class="sxs-lookup"><span data-stu-id="d18b8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d18b8-112">Id</span><span class="sxs-lookup"><span data-stu-id="d18b8-112">Id</span></span> | <span data-ttu-id="d18b8-113">Souhaitée Identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="d18b8-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="d18b8-114">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="d18b8-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d18b8-115">Version</span><span class="sxs-lookup"><span data-stu-id="d18b8-115">Version</span></span> | <span data-ttu-id="d18b8-116">Version du package à désinstaller, avec la version actuellement installée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d18b8-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="d18b8-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="d18b8-117">RemoveDependencies</span></span> | <span data-ttu-id="d18b8-118">Désinstallez le package et ses dépendances inutilisées.</span><span class="sxs-lookup"><span data-stu-id="d18b8-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="d18b8-119">Autrement dit, si une dépendance possède un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="d18b8-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="d18b8-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d18b8-120">ProjectName</span></span> | <span data-ttu-id="d18b8-121">Projet à partir duquel désinstaller le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="d18b8-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d18b8-122">Force</span><span class="sxs-lookup"><span data-stu-id="d18b8-122">Force</span></span> | <span data-ttu-id="d18b8-123">Force la désinstallation d’un package, même si d’autres packages en dépendent.</span><span class="sxs-lookup"><span data-stu-id="d18b8-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="d18b8-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d18b8-124">WhatIf</span></span> | <span data-ttu-id="d18b8-125">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="d18b8-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="d18b8-126">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="d18b8-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d18b8-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="d18b8-127">Common Parameters</span></span>

<span data-ttu-id="d18b8-128">`Uninstall-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d18b8-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d18b8-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="d18b8-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```