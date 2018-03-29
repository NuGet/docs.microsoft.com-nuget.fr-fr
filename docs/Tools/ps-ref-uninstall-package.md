---
title: Référence de PowerShell NuGet Uninstall-Package | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Référence de commande PowerShell de Package de désinstallation de la Console du Gestionnaire de Package NuGet dans Visual Studio.
keywords: NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Package de désinstallation
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b53a36a6456522aa0d9d0d7cdf412de464ba9e08
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="171d3-104">Uninstall-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="171d3-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="171d3-105">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="171d3-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="171d3-106">Supprime un package à partir d’un projet, et éventuellement de supprimer ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="171d3-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="171d3-107">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="171d3-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="171d3-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="171d3-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="171d3-109">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="171d3-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="171d3-110">Paramètres</span><span class="sxs-lookup"><span data-stu-id="171d3-110">Parameters</span></span>

| <span data-ttu-id="171d3-111">Paramètre</span><span class="sxs-lookup"><span data-stu-id="171d3-111">Parameter</span></span> | <span data-ttu-id="171d3-112">Description</span><span class="sxs-lookup"><span data-stu-id="171d3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="171d3-113">Id</span><span class="sxs-lookup"><span data-stu-id="171d3-113">Id</span></span> | <span data-ttu-id="171d3-114">(Obligatoire) L’identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="171d3-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="171d3-115">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="171d3-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="171d3-116">Version</span><span class="sxs-lookup"><span data-stu-id="171d3-116">Version</span></span> | <span data-ttu-id="171d3-117">La version du package à désinstaller, par défaut pour la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="171d3-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="171d3-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="171d3-118">RemoveDependencies</span></span> | <span data-ttu-id="171d3-119">Désinstaller le package et ses dépendances non utilisées.</span><span class="sxs-lookup"><span data-stu-id="171d3-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="171d3-120">Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="171d3-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="171d3-121">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="171d3-121">ProjectName</span></span> | <span data-ttu-id="171d3-122">Le projet à partir de laquelle supprimer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="171d3-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="171d3-123">Force</span><span class="sxs-lookup"><span data-stu-id="171d3-123">Force</span></span> | <span data-ttu-id="171d3-124">Force un package à désinstaller, même si d’autres packages dépendent d’elle.</span><span class="sxs-lookup"><span data-stu-id="171d3-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="171d3-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="171d3-125">WhatIf</span></span> | <span data-ttu-id="171d3-126">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="171d3-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="171d3-127">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="171d3-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="171d3-128">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="171d3-128">Common Parameters</span></span>

<span data-ttu-id="171d3-129">`Uninstall-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="171d3-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="171d3-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="171d3-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
