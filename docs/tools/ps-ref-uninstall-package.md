---
title: Référence de PowerShell NuGet Uninstall-Package
description: Référence de commande PowerShell de Package de désinstallation de la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818865"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f3846-103">Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f3846-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f3846-104">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f3846-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f3846-105">Supprime un package à partir d’un projet, et éventuellement de supprimer ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="f3846-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="f3846-106">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f3846-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="f3846-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f3846-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f3846-108">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f3846-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="f3846-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f3846-109">Parameters</span></span>

| <span data-ttu-id="f3846-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f3846-110">Parameter</span></span> | <span data-ttu-id="f3846-111">Description</span><span class="sxs-lookup"><span data-stu-id="f3846-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3846-112">Id</span><span class="sxs-lookup"><span data-stu-id="f3846-112">Id</span></span> | <span data-ttu-id="f3846-113">(Obligatoire) L’identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="f3846-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="f3846-114">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="f3846-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f3846-115">Version</span><span class="sxs-lookup"><span data-stu-id="f3846-115">Version</span></span> | <span data-ttu-id="f3846-116">La version du package à désinstaller, par défaut pour la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="f3846-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f3846-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="f3846-117">RemoveDependencies</span></span> | <span data-ttu-id="f3846-118">Désinstaller le package et ses dépendances non utilisées.</span><span class="sxs-lookup"><span data-stu-id="f3846-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="f3846-119">Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="f3846-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="f3846-120">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="f3846-120">ProjectName</span></span> | <span data-ttu-id="f3846-121">Le projet à partir de laquelle supprimer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="f3846-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f3846-122">Force</span><span class="sxs-lookup"><span data-stu-id="f3846-122">Force</span></span> | <span data-ttu-id="f3846-123">Force un package à désinstaller, même si d’autres packages dépendent d’elle.</span><span class="sxs-lookup"><span data-stu-id="f3846-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="f3846-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f3846-124">WhatIf</span></span> | <span data-ttu-id="f3846-125">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="f3846-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="f3846-126">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="f3846-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f3846-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="f3846-127">Common Parameters</span></span>

<span data-ttu-id="f3846-128">`Uninstall-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f3846-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f3846-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="f3846-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
