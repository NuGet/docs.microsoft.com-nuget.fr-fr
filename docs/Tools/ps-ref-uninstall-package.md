---
title: Référence de PowerShell NuGet Uninstall-Package
description: Référence de commande PowerShell de Package de désinstallation de la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Package Manager Console dans Visual Studio)

*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*

Supprime un package à partir d’un projet, et éventuellement de supprimer ses dépendances. Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – Force option est spécifiée.

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | (Obligatoire) L’identificateur du package à désinstaller. -Id commutateur lui-même est facultative. |
| Version | La version du package à désinstaller, par défaut pour la version actuellement installée. |
| RemoveDependencies | Désinstaller le package et ses dépendances non utilisées. Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée. |
| Nom_projet | Le projet à partir de laquelle supprimer le package, par défaut pour le projet par défaut. |
| Force | Force un package à désinstaller, même si d’autres packages dépendent d’elle. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Uninstall-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
