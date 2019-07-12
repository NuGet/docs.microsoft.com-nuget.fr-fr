---
title: Référence PowerShell de synchronisation-Package NuGet
description: Référence de commande PowerShell de synchronisation-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842248"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="24ec2-103">Sync-Package (Console du gestionnaire de packages dans Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="24ec2-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="24ec2-104">*Version 3.0 et versions ultérieures ; disponible uniquement dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows.*</span><span class="sxs-lookup"><span data-stu-id="24ec2-104">*Version 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="24ec2-105">Obtient la version du package installé à partir de spécifié (ou par défaut) de projet et synchronise la version pour le reste des projets de la solution.</span><span class="sxs-lookup"><span data-stu-id="24ec2-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="24ec2-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="24ec2-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="24ec2-107">Paramètres</span><span class="sxs-lookup"><span data-stu-id="24ec2-107">Parameters</span></span>

| <span data-ttu-id="24ec2-108">Paramètre</span><span class="sxs-lookup"><span data-stu-id="24ec2-108">Parameter</span></span> | <span data-ttu-id="24ec2-109">Description</span><span class="sxs-lookup"><span data-stu-id="24ec2-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24ec2-110">Id</span><span class="sxs-lookup"><span data-stu-id="24ec2-110">Id</span></span> | <span data-ttu-id="24ec2-111">(Obligatoire) L’identificateur du package à synchroniser. -Id commutateur proprement dit est facultatif.</span><span class="sxs-lookup"><span data-stu-id="24ec2-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="24ec2-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="24ec2-112">IgnoreDependencies</span></span> | <span data-ttu-id="24ec2-113">Installer uniquement ce package et pas ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="24ec2-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="24ec2-114">Nom_projet</span><span class="sxs-lookup"><span data-stu-id="24ec2-114">ProjectName</span></span> | <span data-ttu-id="24ec2-115">Projet à synchroniser le package à partir, par défaut pour le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="24ec2-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="24ec2-116">Version</span><span class="sxs-lookup"><span data-stu-id="24ec2-116">Version</span></span> | <span data-ttu-id="24ec2-117">La version du package à se synchroniser, par défaut à la version actuellement installée.</span><span class="sxs-lookup"><span data-stu-id="24ec2-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="24ec2-118">source</span><span class="sxs-lookup"><span data-stu-id="24ec2-118">Source</span></span> | <span data-ttu-id="24ec2-119">Le chemin d’accès URL ou un dossier pour la source du package à rechercher.</span><span class="sxs-lookup"><span data-stu-id="24ec2-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="24ec2-120">Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif.</span><span class="sxs-lookup"><span data-stu-id="24ec2-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="24ec2-121">Si omis, `Sync-Package` recherche la source du package actuellement sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="24ec2-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="24ec2-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="24ec2-122">IncludePrerelease</span></span> | <span data-ttu-id="24ec2-123">Inclut les packages de version préliminaire dans la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="24ec2-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="24ec2-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="24ec2-124">FileConflictAction</span></span> | <span data-ttu-id="24ec2-125">L’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet.</span><span class="sxs-lookup"><span data-stu-id="24ec2-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="24ec2-126">Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="24ec2-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="24ec2-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="24ec2-127">DependencyVersion</span></span> | <span data-ttu-id="24ec2-128">La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="24ec2-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="24ec2-129">*La plus basse* (valeur par défaut) : la version la plus basse</span><span class="sxs-lookup"><span data-stu-id="24ec2-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="24ec2-130">*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</span><span class="sxs-lookup"><span data-stu-id="24ec2-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="24ec2-131">*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</span><span class="sxs-lookup"><span data-stu-id="24ec2-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="24ec2-132">*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="24ec2-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="24ec2-133">Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier.</span><span class="sxs-lookup"><span data-stu-id="24ec2-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="24ec2-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="24ec2-134">WhatIf</span></span> | <span data-ttu-id="24ec2-135">Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="24ec2-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="24ec2-136">Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.</span><span class="sxs-lookup"><span data-stu-id="24ec2-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="24ec2-137">Paramètres communs</span><span class="sxs-lookup"><span data-stu-id="24ec2-137">Common Parameters</span></span>

<span data-ttu-id="24ec2-138">`Sync-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24ec2-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="24ec2-139">Exemples</span><span class="sxs-lookup"><span data-stu-id="24ec2-139">Examples</span></span>

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
