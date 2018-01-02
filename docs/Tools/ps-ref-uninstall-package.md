---
title: "Référence de PowerShell NuGet Uninstall-Package | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Référence de commande PowerShell de Package de désinstallation de la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Package de désinstallation"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e98ce-104">Uninstall-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e98ce-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e98ce-105">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e98ce-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e98ce-106">Supprime un package à partir d’un projet, et éventuellement de supprimer ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="e98ce-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="e98ce-107">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e98ce-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="e98ce-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e98ce-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e98ce-109">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e98ce-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="e98ce-110">Paramètres</span><span class="sxs-lookup"><span data-stu-id="e98ce-110">Parameters</span></span>

| <span data-ttu-id="e98ce-111">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e98ce-111">Parameter</span></span> | <span data-ttu-id="e98ce-112">Description</span><span class="sxs-lookup"><span data-stu-id="e98ce-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e98ce-113">Id</span><span class="sxs-lookup"><span data-stu-id="e98ce-113">Id</span></span> | <span data-ttu-id="e98ce-114">(Obligatoire) L’identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="e98ce-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="e98ce-115">-Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="e98ce-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e98ce-116">Version</span><span class="sxs-lookup"><span data-stu-id="e98ce-116">Version</span></span> | <span data-ttu-id="e98ce-117">La version du package à désinstaller, par défaut pour la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="e98ce-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e98ce-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="e98ce-118">RemoveDependencies</span></span> | <span data-ttu-id="e98ce-119">Désinstaller le package et ses dépendances non utilisées.</span><span class="sxs-lookup"><span data-stu-id="e98ce-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="e98ce-120">Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="e98ce-120">That is, if any dependency has another package that depends on it, it is skipped.</span></span> |
| <span data-ttu-id="e98ce-121">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="e98ce-121">ProjectName</span></span> | <span data-ttu-id="e98ce-122">Le projet à partir de laquelle supprimer le package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="e98ce-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e98ce-123">Force</span><span class="sxs-lookup"><span data-stu-id="e98ce-123">Force</span></span> | <span data-ttu-id="e98ce-124">Force un package à désinstaller, même si d’autres packages dépendent d’elle.</span><span class="sxs-lookup"><span data-stu-id="e98ce-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="e98ce-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e98ce-125">WhatIf</span></span> | <span data-ttu-id="e98ce-126">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="e98ce-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="e98ce-127">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="e98ce-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e98ce-128">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="e98ce-128">Common Parameters</span></span>

<span data-ttu-id="e98ce-129">`Uninstall-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e98ce-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e98ce-130">Exemples</span><span class="sxs-lookup"><span data-stu-id="e98ce-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
