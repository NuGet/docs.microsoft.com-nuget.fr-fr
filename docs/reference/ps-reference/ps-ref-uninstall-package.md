---
title: Informations de référence sur PowerShell Uninstall-Package de NuGet
description: Référence pour Uninstall-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 961a9d68e5cba09030401fc871a93bf1145b23a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777397"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (console du gestionnaire de package dans Visual Studio)

*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Uninstall-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Supprime un package d’un projet, en supprimant éventuellement ses dépendances. Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si les autres packages dépendent de ce package, la commande va échouer, sauf si l’option –Force est spécifiée.

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | Souhaitée Identificateur du package à désinstaller. Le commutateur-ID lui-même est facultatif. |
| Version | Version du package à désinstaller, avec la version actuellement installée par défaut. |
| RemoveDependencies | Désinstallez le package et ses dépendances inutilisées. Autrement dit, si une dépendance possède un autre package qui en dépend, elle est ignorée. |
| ProjectName | Projet à partir duquel désinstaller le package, par défaut au projet par défaut. |
| Force | Force la désinstallation d’un package, même si d’autres packages en dépendent. |
| WhatIf | Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la désinstallation. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Uninstall-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```