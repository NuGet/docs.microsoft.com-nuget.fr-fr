---
title: "Référence de synchronisation-Package NuGet PowerShell | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "Référence de commande PowerShell de synchronisation-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, synchronisation-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f69db-104">Synchronisation-Package (Package Manager Console dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f69db-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f69db-105">*Version 3.0 + ; disponible uniquement dans les [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows.*</span><span class="sxs-lookup"><span data-stu-id="f69db-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f69db-106">Obtient la version du package installé à partir de spécifié (ou par défaut) du projet et synchronise la version pour les autres projets dans la solution.</span><span class="sxs-lookup"><span data-stu-id="f69db-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="f69db-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f69db-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f69db-108">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f69db-108">Parameters</span></span>

| <span data-ttu-id="f69db-109">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f69db-109">Parameter</span></span> | <span data-ttu-id="f69db-110">Description</span><span class="sxs-lookup"><span data-stu-id="f69db-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f69db-111">Id</span><span class="sxs-lookup"><span data-stu-id="f69db-111">Id</span></span> | <span data-ttu-id="f69db-112">(Obligatoire) L’identificateur du package à synchroniser. -Id commutateur lui-même est facultative.</span><span class="sxs-lookup"><span data-stu-id="f69db-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f69db-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f69db-113">IgnoreDependencies</span></span> | <span data-ttu-id="f69db-114">Installer ce package uniquement, sans ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="f69db-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f69db-115">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="f69db-115">ProjectName</span></span> | <span data-ttu-id="f69db-116">Le projet pour synchroniser le package à partir, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="f69db-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="f69db-117">Version</span><span class="sxs-lookup"><span data-stu-id="f69db-117">Version</span></span> | <span data-ttu-id="f69db-118">La version du package pour la synchronisation, par défaut pour la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="f69db-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f69db-119">Source</span><span class="sxs-lookup"><span data-stu-id="f69db-119">Source</span></span> | <span data-ttu-id="f69db-120">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="f69db-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f69db-121">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="f69db-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f69db-122">Si omis, `Sync-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="f69db-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f69db-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f69db-123">IncludePrerelease</span></span> | <span data-ttu-id="f69db-124">Inclut les versions préliminaires des packages dans la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="f69db-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="f69db-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f69db-125">FileConflictAction</span></span> | <span data-ttu-id="f69db-126">Action à prendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="f69db-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f69db-127">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="f69db-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f69db-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f69db-128">DependencyVersion</span></span> | <span data-ttu-id="f69db-129">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f69db-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f69db-130">*La plus basse* (par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="f69db-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f69db-131">*HighestPatch*: la version avec le correctif logiciel le plus bas majeure, mineure la plus basse, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="f69db-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f69db-132">*HighestMinor*: la version avec le plus bas principales, le correctif plus élevé de secondaire, la plus élevée</span><span class="sxs-lookup"><span data-stu-id="f69db-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f69db-133">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="f69db-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f69db-134">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="f69db-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f69db-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f69db-135">WhatIf</span></span> | <span data-ttu-id="f69db-136">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="f69db-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="f69db-137">Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="f69db-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f69db-138">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="f69db-138">Common Parameters</span></span>

<span data-ttu-id="f69db-139">`Sync-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f69db-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f69db-140">Exemples</span><span class="sxs-lookup"><span data-stu-id="f69db-140">Examples</span></span>

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
