---
title: Informations de référence sur PowerShell Sync-Package de NuGet
description: Référence pour Sync-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238047"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c73f7-103">Sync-Package (console du gestionnaire de package dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c73f7-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c73f7-104">*Version 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="c73f7-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c73f7-105">Obtient la version du package installé à partir du projet spécifié (ou par défaut) et synchronise la version avec les autres projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="c73f7-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="c73f7-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c73f7-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c73f7-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="c73f7-107">Parameters</span></span>

| <span data-ttu-id="c73f7-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c73f7-108">Parameter</span></span> | <span data-ttu-id="c73f7-109">Description</span><span class="sxs-lookup"><span data-stu-id="c73f7-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c73f7-110">Id</span><span class="sxs-lookup"><span data-stu-id="c73f7-110">Id</span></span> | <span data-ttu-id="c73f7-111">Souhaitée Identificateur du package à synchroniser. Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="c73f7-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c73f7-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="c73f7-112">IgnoreDependencies</span></span> | <span data-ttu-id="c73f7-113">Installez uniquement ce package et non ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="c73f7-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="c73f7-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c73f7-114">ProjectName</span></span> | <span data-ttu-id="c73f7-115">Projet à partir duquel synchroniser le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="c73f7-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="c73f7-116">Version</span><span class="sxs-lookup"><span data-stu-id="c73f7-116">Version</span></span> | <span data-ttu-id="c73f7-117">Version du package à synchroniser, avec la version actuellement installée par défaut.</span><span class="sxs-lookup"><span data-stu-id="c73f7-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="c73f7-118">Source</span><span class="sxs-lookup"><span data-stu-id="c73f7-118">Source</span></span> | <span data-ttu-id="c73f7-119">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="c73f7-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c73f7-120">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="c73f7-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c73f7-121">En cas d’omission, `Sync-Package` effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="c73f7-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c73f7-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c73f7-122">IncludePrerelease</span></span> | <span data-ttu-id="c73f7-123">Comprend des packages de version préliminaire dans la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="c73f7-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="c73f7-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c73f7-124">FileConflictAction</span></span> | <span data-ttu-id="c73f7-125">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="c73f7-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c73f7-126">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll* et *(3.0 +)* *IgnoreAll* .</span><span class="sxs-lookup"><span data-stu-id="c73f7-126">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll* .</span></span> |
| <span data-ttu-id="c73f7-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c73f7-127">DependencyVersion</span></span> | <span data-ttu-id="c73f7-128">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :</span><span class="sxs-lookup"><span data-stu-id="c73f7-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c73f7-129">La *plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="c73f7-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c73f7-130">*HighestPatch* : version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="c73f7-130">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c73f7-131">*HighestMinor* : version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="c73f7-131">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c73f7-132">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres) : la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="c73f7-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="c73f7-133">Vous pouvez définir la valeur par défaut à l’aide du [`dependencyVersion`](../nuget-config-file.md#config-section) paramètre dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="c73f7-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="c73f7-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c73f7-134">WhatIf</span></span> | <span data-ttu-id="c73f7-135">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="c73f7-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="c73f7-136">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="c73f7-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c73f7-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="c73f7-137">Common Parameters</span></span>

<span data-ttu-id="c73f7-138">`Sync-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c73f7-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c73f7-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="c73f7-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```