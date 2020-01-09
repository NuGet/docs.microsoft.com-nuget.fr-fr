---
title: Désinstaller NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Uninstall-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384413"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4f347-103">Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4f347-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4f347-104">*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour la commande générique de désinstallation de PowerShell, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="4f347-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4f347-105">Supprime un package d’un projet, en supprimant éventuellement ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="4f347-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="4f347-106">Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4f347-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="4f347-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4f347-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4f347-108">Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4f347-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="4f347-109">Parameters</span><span class="sxs-lookup"><span data-stu-id="4f347-109">Parameters</span></span>

| <span data-ttu-id="4f347-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="4f347-110">Parameter</span></span> | <span data-ttu-id="4f347-111">Description</span><span class="sxs-lookup"><span data-stu-id="4f347-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f347-112">ID</span><span class="sxs-lookup"><span data-stu-id="4f347-112">Id</span></span> | <span data-ttu-id="4f347-113">Souhaitée Identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="4f347-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="4f347-114">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="4f347-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4f347-115">Version</span><span class="sxs-lookup"><span data-stu-id="4f347-115">Version</span></span> | <span data-ttu-id="4f347-116">Version du package à désinstaller, avec la version actuellement installée par défaut.</span><span class="sxs-lookup"><span data-stu-id="4f347-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="4f347-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="4f347-117">RemoveDependencies</span></span> | <span data-ttu-id="4f347-118">Désinstallez le package et ses dépendances inutilisées.</span><span class="sxs-lookup"><span data-stu-id="4f347-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="4f347-119">Autrement dit, si une dépendance possède un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="4f347-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="4f347-120">NomProjet</span><span class="sxs-lookup"><span data-stu-id="4f347-120">ProjectName</span></span> | <span data-ttu-id="4f347-121">Projet à partir duquel désinstaller le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="4f347-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="4f347-122">Force</span><span class="sxs-lookup"><span data-stu-id="4f347-122">Force</span></span> | <span data-ttu-id="4f347-123">Force la désinstallation d’un package, même si d’autres packages en dépendent.</span><span class="sxs-lookup"><span data-stu-id="4f347-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="4f347-124">Whatif</span><span class="sxs-lookup"><span data-stu-id="4f347-124">WhatIf</span></span> | <span data-ttu-id="4f347-125">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="4f347-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="4f347-126">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="4f347-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4f347-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="4f347-127">Common Parameters</span></span>

<span data-ttu-id="4f347-128">`Uninstall-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4f347-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4f347-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="4f347-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
