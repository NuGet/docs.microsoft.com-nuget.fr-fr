---
title: Désinstaller NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Uninstall-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384413"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)

*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour la commande générique de désinstallation de PowerShell, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Supprime un package d’un projet, en supprimant éventuellement ses dépendances. Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.

## <a name="parameters"></a>Parameters

| Paramètre | Description |
| --- | --- |
| ID | Souhaitée Identificateur du package à désinstaller. Le commutateur-ID lui-même est facultatif. |
| Version | Version du package à désinstaller, avec la version actuellement installée par défaut. |
| RemoveDependencies | Désinstallez le package et ses dépendances inutilisées. Autrement dit, si une dépendance possède un autre package qui en dépend, elle est ignorée. |
| NomProjet | Projet à partir duquel désinstaller le package, par défaut au projet par défaut. |
| Force | Force la désinstallation d’un package, même si d’autres packages en dépendent. |
| Whatif | Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la désinstallation. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Uninstall-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
