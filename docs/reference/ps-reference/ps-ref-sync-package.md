---
title: Synchronisation NuGet-référence PowerShell du package
description: Référence de la commande PowerShell de synchronisation du package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327306"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="587f9-103">Sync-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="587f9-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="587f9-104">*Version 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="587f9-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="587f9-105">Obtient la version du package installé à partir du projet spécifié (ou par défaut) et synchronise la version avec les autres projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="587f9-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="587f9-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="587f9-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="587f9-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="587f9-107">Parameters</span></span>

| <span data-ttu-id="587f9-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="587f9-108">Parameter</span></span> | <span data-ttu-id="587f9-109">Description</span><span class="sxs-lookup"><span data-stu-id="587f9-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="587f9-110">Id</span><span class="sxs-lookup"><span data-stu-id="587f9-110">Id</span></span> | <span data-ttu-id="587f9-111">Souhaitée Identificateur du package à synchroniser. Le commutateur-ID lui-même est facultatif.</span><span class="sxs-lookup"><span data-stu-id="587f9-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="587f9-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="587f9-112">IgnoreDependencies</span></span> | <span data-ttu-id="587f9-113">Installez uniquement ce package et non ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="587f9-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="587f9-114">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="587f9-114">ProjectName</span></span> | <span data-ttu-id="587f9-115">Projet à partir duquel synchroniser le package, par défaut au projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="587f9-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="587f9-116">Version</span><span class="sxs-lookup"><span data-stu-id="587f9-116">Version</span></span> | <span data-ttu-id="587f9-117">Version du package à synchroniser, avec la version actuellement installée par défaut.</span><span class="sxs-lookup"><span data-stu-id="587f9-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="587f9-118">source</span><span class="sxs-lookup"><span data-stu-id="587f9-118">Source</span></span> | <span data-ttu-id="587f9-119">URL ou chemin d’accès de dossier de la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="587f9-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="587f9-120">Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif.</span><span class="sxs-lookup"><span data-stu-id="587f9-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="587f9-121">En cas d’omission `Sync-Package` , effectue une recherche dans la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="587f9-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="587f9-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="587f9-122">IncludePrerelease</span></span> | <span data-ttu-id="587f9-123">Comprend des packages de version préliminaire dans la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="587f9-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="587f9-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="587f9-124">FileConflictAction</span></span> | <span data-ttu-id="587f9-125">Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="587f9-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="587f9-126">Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="587f9-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="587f9-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="587f9-127">DependencyVersion</span></span> | <span data-ttu-id="587f9-128">Version des packages de dépendance à utiliser, qui peut être l’une des suivantes:</span><span class="sxs-lookup"><span data-stu-id="587f9-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="587f9-129">La *plus basse* (par défaut): la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="587f9-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="587f9-130">*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="587f9-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="587f9-131">*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="587f9-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="587f9-132">La *plus élevée* (valeur par défaut pour Update-Package sans paramètres): la version la plus élevée</span><span class="sxs-lookup"><span data-stu-id="587f9-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="587f9-133">Vous pouvez définir la valeur par défaut à [`dependencyVersion`](../nuget-config-file.md#config-section) l’aide du `Nuget.Config` paramètre dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="587f9-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="587f9-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="587f9-134">WhatIf</span></span> | <span data-ttu-id="587f9-135">Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="587f9-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="587f9-136">Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="587f9-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="587f9-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="587f9-137">Common Parameters</span></span>

<span data-ttu-id="587f9-138">`Sync-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="587f9-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="587f9-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="587f9-139">Examples</span></span>

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
