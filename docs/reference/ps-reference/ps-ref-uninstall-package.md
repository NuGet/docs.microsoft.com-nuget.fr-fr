---
title: Désinstaller NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Uninstall-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327276"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4483e-103">Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4483e-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4483e-104">*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour la commande générique de désinstallation de PowerShell, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="4483e-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4483e-105">Supprime un package d’un projet, en supprimant éventuellement ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="4483e-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="4483e-106">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – force est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4483e-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="4483e-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4483e-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4483e-108">Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – force est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4483e-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="4483e-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="4483e-109">Parameters</span></span>

| <span data-ttu-id="4483e-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="4483e-110">Parameter</span></span> | <span data-ttu-id="4483e-111">Description</span><span class="sxs-lookup"><span data-stu-id="4483e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4483e-112">Id</span><span class="sxs-lookup"><span data-stu-id="4483e-112">Id</span></span> | <span data-ttu-id="4483e-113">Souhaitée Identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="4483e-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="4483e-114">Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="4483e-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4483e-115">Version</span><span class="sxs-lookup"><span data-stu-id="4483e-115">Version</span></span> | <span data-ttu-id="4483e-116">Version du package à désinstaller, avec la version actuellement installée par défaut.</span><span class="sxs-lookup"><span data-stu-id="4483e-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="4483e-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="4483e-117">RemoveDependencies</span></span> | <span data-ttu-id="4483e-118">Désinstallez le package et ses dépendances inutilisées.</span><span class="sxs-lookup"><span data-stu-id="4483e-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="4483e-119">Autrement dit, si une dépendance possède un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="4483e-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="4483e-120">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="4483e-120">ProjectName</span></span> | <span data-ttu-id="4483e-121">Projet à partir duquel désinstaller le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="4483e-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="4483e-122">Appliqués</span><span class="sxs-lookup"><span data-stu-id="4483e-122">Force</span></span> | <span data-ttu-id="4483e-123">Force la désinstallation d’un package, même si d’autres packages en dépendent.</span><span class="sxs-lookup"><span data-stu-id="4483e-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="4483e-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4483e-124">WhatIf</span></span> | <span data-ttu-id="4483e-125">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="4483e-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="4483e-126">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="4483e-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4483e-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="4483e-127">Common Parameters</span></span>

<span data-ttu-id="4483e-128">`Uninstall-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4483e-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4483e-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="4483e-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
