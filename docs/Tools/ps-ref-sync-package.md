---
title: "Référence de synchronisation-Package NuGet PowerShell | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande PowerShell de synchronisation-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, synchronisation-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Synchronisation-Package (Package Manager Console dans Visual Studio)

*Version 3.0 + ; disponible uniquement dans les [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows.*

Obtient la version du package installé à partir de spécifié (ou par défaut) du projet et synchronise la version pour les autres projets dans la solution.

## <a name="syntax"></a>Syntaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | (Obligatoire) L’identificateur du package à synchroniser. -Id commutateur lui-même est facultative. |
| IgnoreDependencies | Installer ce package uniquement, sans ses dépendances. |
| Nom_projet | Le projet pour synchroniser le package à partir, par défaut pour le projet par défaut. |
| Version | La version du package pour la synchronisation, par défaut pour la version actuellement installée. |
| Source | Le chemin d’accès URL ou un dossier pour la source du package à rechercher. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Sync-Package` recherche la source du package actuellement sélectionnée. |
| IncludePrerelease | Inclut les versions préliminaires des packages dans la synchronisation. |
| FileConflictAction | Action à prendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :<br/><ul><li>*La plus basse* (par défaut) : la version la plus basse</li><li>*HighestPatch*: la version avec le correctif logiciel le plus bas majeure, mineure la plus basse, la plus élevée</li><li>*HighestMinor*: la version avec le plus bas principales, le correctif plus élevé de secondaire, la plus élevée</li><li>*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</li></ul>Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la synchronisation. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Sync-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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
