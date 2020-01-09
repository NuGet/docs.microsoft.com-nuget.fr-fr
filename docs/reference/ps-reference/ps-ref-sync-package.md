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
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Console du gestionnaire de packages dans Visual Studio)

*Version 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Obtient la version du package installé à partir du projet spécifié (ou par défaut) et synchronise la version avec les autres projets de la solution.

## <a name="syntax"></a>Syntaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Paramètre | Description |
| --- | --- |
| ID | Souhaitée Identificateur du package à synchroniser. Le commutateur-ID lui-même est facultatif. |
| IgnoreDependencies | Installez uniquement ce package et non ses dépendances. |
| NomProjet | Projet à partir duquel synchroniser le package, par défaut au projet par défaut. |
| Version | Version du package à synchroniser, avec la version actuellement installée par défaut. |
| Source | URL ou chemin d’accès de dossier de la source du package à rechercher. Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif. En cas d’omission, `Sync-Package` recherche la source de package actuellement sélectionnée. |
| IncludePrerelease | Comprend des packages de version préliminaire dans la synchronisation. |
| FileConflictAction | Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :<br/><ul><li>La *plus basse* (par défaut) : la version la plus basse</li><li>*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</li><li>*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</li><li>La *plus élevée* (valeur par défaut pour Update-Package sans paramètres) : la version la plus élevée</li></ul>Vous pouvez définir la valeur par défaut à l’aide du paramètre [`dependencyVersion`](../nuget-config-file.md#config-section) dans le fichier `Nuget.Config`. |
| Whatif | Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la synchronisation. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Sync-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

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
