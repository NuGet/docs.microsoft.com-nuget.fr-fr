---
title: Référence de PowerShell NuGet Uninstall-Package
description: Référence de commande PowerShell de Package de désinstallation de la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ed690-103">Uninstall-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ed690-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ed690-104">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="ed690-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ed690-105">Supprime un package à partir d’un projet, et éventuellement de supprimer ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="ed690-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="ed690-106">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="ed690-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="ed690-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ed690-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ed690-108">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="ed690-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="ed690-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="ed690-109">Parameters</span></span>

| <span data-ttu-id="ed690-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ed690-110">Parameter</span></span> | <span data-ttu-id="ed690-111">Description</span><span class="sxs-lookup"><span data-stu-id="ed690-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed690-112">Id</span><span class="sxs-lookup"><span data-stu-id="ed690-112">Id</span></span> | <span data-ttu-id="ed690-113">(Obligatoire) L’identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="ed690-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="ed690-114">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="ed690-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ed690-115">Version</span><span class="sxs-lookup"><span data-stu-id="ed690-115">Version</span></span> | <span data-ttu-id="ed690-116">La version du package à désinstaller, par défaut pour la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="ed690-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="ed690-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="ed690-117">RemoveDependencies</span></span> | <span data-ttu-id="ed690-118">Désinstaller le package et ses dépendances non utilisées.</span><span class="sxs-lookup"><span data-stu-id="ed690-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="ed690-119">Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="ed690-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="ed690-120">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="ed690-120">ProjectName</span></span> | <span data-ttu-id="ed690-121">Le projet à partir de laquelle supprimer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="ed690-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="ed690-122">Force</span><span class="sxs-lookup"><span data-stu-id="ed690-122">Force</span></span> | <span data-ttu-id="ed690-123">Force un package à désinstaller, même si d’autres packages dépendent d’elle.</span><span class="sxs-lookup"><span data-stu-id="ed690-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="ed690-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ed690-124">WhatIf</span></span> | <span data-ttu-id="ed690-125">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="ed690-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="ed690-126">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="ed690-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ed690-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="ed690-127">Common Parameters</span></span>

<span data-ttu-id="ed690-128">`Uninstall-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ed690-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ed690-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="ed690-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
