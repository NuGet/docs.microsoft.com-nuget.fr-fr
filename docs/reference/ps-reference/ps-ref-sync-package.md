---
title: Synchronisation NuGet-référence PowerShell du package
description: Référence de la commande PowerShell de synchronisation du package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384901"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="cf037-103">Sync-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cf037-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="cf037-104">*Version 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="cf037-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="cf037-105">Obtient la version du package installé à partir du projet spécifié (ou par défaut) et synchronise la version avec les autres projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="cf037-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="cf037-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="cf037-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="cf037-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="cf037-107">Parameters</span></span>

| <span data-ttu-id="cf037-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="cf037-108">Parameter</span></span> | <span data-ttu-id="cf037-109">Description</span><span class="sxs-lookup"><span data-stu-id="cf037-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf037-110">ID</span><span class="sxs-lookup"><span data-stu-id="cf037-110">Id</span></span> | <span data-ttu-id="cf037-111">Souhaitée Identificateur du package à synchroniser. Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="cf037-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="cf037-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="cf037-112">IgnoreDependencies</span></span> | <span data-ttu-id="cf037-113">Installez uniquement ce package et non ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="cf037-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="cf037-114">NomProjet</span><span class="sxs-lookup"><span data-stu-id="cf037-114">ProjectName</span></span> | <span data-ttu-id="cf037-115">Projet à partir duquel synchroniser le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="cf037-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="cf037-116">Version</span><span class="sxs-lookup"><span data-stu-id="cf037-116">Version</span></span> | <span data-ttu-id="cf037-117">Version du package à synchroniser, avec la version actuellement installée par défaut.</span><span class="sxs-lookup"><span data-stu-id="cf037-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="cf037-118">Source</span><span class="sxs-lookup"><span data-stu-id="cf037-118">Source</span></span> | <span data-ttu-id="cf037-119">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="cf037-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="cf037-120">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="cf037-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="cf037-121">En cas d’omission, `Sync-Package` recherche la source de package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="cf037-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="cf037-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="cf037-122">IncludePrerelease</span></span> | <span data-ttu-id="cf037-123">Comprend des packages de version préliminaire dans la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="cf037-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="cf037-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="cf037-124">FileConflictAction</span></span> | <span data-ttu-id="cf037-125">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="cf037-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="cf037-126">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="cf037-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="cf037-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="cf037-127">DependencyVersion</span></span> | <span data-ttu-id="cf037-128">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf037-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="cf037-129">La *plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="cf037-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="cf037-130">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="cf037-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="cf037-131">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="cf037-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="cf037-132">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres) : la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="cf037-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="cf037-133">Vous pouvez définir la valeur par défaut à l’aide du paramètre [`dependencyVersion`](../nuget-config-file.md#config-section) dans le fichier `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="cf037-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="cf037-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="cf037-134">WhatIf</span></span> | <span data-ttu-id="cf037-135">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="cf037-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="cf037-136">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="cf037-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="cf037-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="cf037-137">Common Parameters</span></span>

<span data-ttu-id="cf037-138">`Sync-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cf037-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="cf037-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="cf037-139">Examples</span></span>

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
