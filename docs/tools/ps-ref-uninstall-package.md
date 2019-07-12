---
title: Référence de PowerShell NuGet Uninstall-Package
description: Référence de commande Uninstall-Package PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842470"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="563ac-103">Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="563ac-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="563ac-104">*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="563ac-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="563ac-105">Supprime un package à partir d’un projet, éventuellement de supprimer ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="563ac-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="563ac-106">Si d’autres packages dépendent de ce package, la commande échoue, sauf si – Force l’option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="563ac-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="563ac-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="563ac-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="563ac-108">Si d’autres packages dépendent de ce package, la commande échoue, sauf si – Force l’option est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="563ac-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="563ac-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="563ac-109">Parameters</span></span>

| <span data-ttu-id="563ac-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="563ac-110">Parameter</span></span> | <span data-ttu-id="563ac-111">Description</span><span class="sxs-lookup"><span data-stu-id="563ac-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="563ac-112">Id</span><span class="sxs-lookup"><span data-stu-id="563ac-112">Id</span></span> | <span data-ttu-id="563ac-113">(Obligatoire) L’identificateur du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="563ac-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="563ac-114">-Id commutateur proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="563ac-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="563ac-115">Version</span><span class="sxs-lookup"><span data-stu-id="563ac-115">Version</span></span> | <span data-ttu-id="563ac-116">La version du package à désinstaller, par défaut à la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="563ac-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="563ac-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="563ac-117">RemoveDependencies</span></span> | <span data-ttu-id="563ac-118">Désinstallez le package et ses dépendances inutilisées.</span><span class="sxs-lookup"><span data-stu-id="563ac-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="563ac-119">Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="563ac-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="563ac-120">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="563ac-120">ProjectName</span></span> | <span data-ttu-id="563ac-121">Le projet à partir de laquelle la désinstallation du package, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="563ac-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="563ac-122">Force</span><span class="sxs-lookup"><span data-stu-id="563ac-122">Force</span></span> | <span data-ttu-id="563ac-123">Force un package à désinstaller, même si d’autres packages qui en dépendent.</span><span class="sxs-lookup"><span data-stu-id="563ac-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="563ac-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="563ac-124">WhatIf</span></span> | <span data-ttu-id="563ac-125">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation.</span><span class="sxs-lookup"><span data-stu-id="563ac-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="563ac-126">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="563ac-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="563ac-127">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="563ac-127">Common Parameters</span></span>

<span data-ttu-id="563ac-128">`Uninstall-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="563ac-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="563ac-129">Exemples</span><span class="sxs-lookup"><span data-stu-id="563ac-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
