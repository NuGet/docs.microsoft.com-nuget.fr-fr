---
title: Référence PowerShell de synchronisation-Package NuGet
description: Référence de commande PowerShell de synchronisation-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547992"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e8e51-103">Sync-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e8e51-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e8e51-104">*Version 3.0 et versions ultérieures ; disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="e8e51-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e8e51-105">Obtient la version du package installé à partir de spécifié (ou par défaut) de projet et synchronise la version pour le reste des projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="e8e51-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="e8e51-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e8e51-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e8e51-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="e8e51-107">Parameters</span></span>

| <span data-ttu-id="e8e51-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e8e51-108">Parameter</span></span> | <span data-ttu-id="e8e51-109">Description</span><span class="sxs-lookup"><span data-stu-id="e8e51-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8e51-110">Id</span><span class="sxs-lookup"><span data-stu-id="e8e51-110">Id</span></span> | <span data-ttu-id="e8e51-111">(Obligatoire) L’identificateur du package à synchroniser. -Id commutateur proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="e8e51-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e8e51-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e8e51-112">IgnoreDependencies</span></span> | <span data-ttu-id="e8e51-113">Installer uniquement ce package et pas ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="e8e51-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="e8e51-114">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="e8e51-114">ProjectName</span></span> | <span data-ttu-id="e8e51-115">Projet à synchroniser le package à partir, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="e8e51-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="e8e51-116">Version</span><span class="sxs-lookup"><span data-stu-id="e8e51-116">Version</span></span> | <span data-ttu-id="e8e51-117">La version du package à se synchroniser, par défaut à la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="e8e51-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e8e51-118">Source</span><span class="sxs-lookup"><span data-stu-id="e8e51-118">Source</span></span> | <span data-ttu-id="e8e51-119">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="e8e51-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e8e51-120">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="e8e51-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e8e51-121">Si omis, `Sync-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="e8e51-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e8e51-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e8e51-122">IncludePrerelease</span></span> | <span data-ttu-id="e8e51-123">Inclut les packages de version préliminaire dans la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="e8e51-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="e8e51-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e8e51-124">FileConflictAction</span></span> | <span data-ttu-id="e8e51-125">L’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="e8e51-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e8e51-126">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="e8e51-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="e8e51-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e8e51-127">DependencyVersion</span></span> | <span data-ttu-id="e8e51-128">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8e51-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e8e51-129">*La plus basse* (valeur par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="e8e51-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e8e51-130">*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="e8e51-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e8e51-131">*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</span><span class="sxs-lookup"><span data-stu-id="e8e51-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e8e51-132">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="e8e51-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e8e51-133">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="e8e51-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e8e51-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e8e51-134">WhatIf</span></span> | <span data-ttu-id="e8e51-135">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="e8e51-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="e8e51-136">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="e8e51-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e8e51-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="e8e51-137">Common Parameters</span></span>

<span data-ttu-id="e8e51-138">`Sync-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e8e51-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e8e51-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="e8e51-139">Examples</span></span>

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
