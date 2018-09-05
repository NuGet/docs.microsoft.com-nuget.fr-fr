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
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Console du gestionnaire de packages dans Visual Studio)

*Version 3.0 et versions ultérieures ; disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*

Obtient la version du package installé à partir de spécifié (ou par défaut) de projet et synchronise la version pour le reste des projets de la solution.

## <a name="syntax"></a>Syntaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | (Obligatoire) L’identificateur du package à synchroniser. -Id commutateur proprement dit est facultatif. |
| IgnoreDependencies | Installer uniquement ce package et pas ses dépendances. |
| Nom_projet | Projet à synchroniser le package à partir, par défaut pour le projet par défaut. |
| Version | La version du package à se synchroniser, par défaut à la version actuellement installée. |
| Source | Le chemin d’accès URL ou un dossier pour la source du package à rechercher. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Sync-Package` recherche la source du package actuellement sélectionnée. |
| IncludePrerelease | Inclut les packages de version préliminaire dans la synchronisation. |
| FileConflictAction | L’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :<br/><ul><li>*La plus basse* (valeur par défaut) : la version la plus basse</li><li>*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</li><li>*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</li><li>*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</li></ul>Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la synchronisation. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Sync-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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
