---
title: Référence de PowerShell NuGet Uninstall-Package
description: Référence de commande Uninstall-Package PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842470"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)

*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*

Supprime un package à partir d’un projet, éventuellement de supprimer ses dépendances. Si d’autres packages dépendent de ce package, la commande échoue, sauf si – Force l’option est spécifiée.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si d’autres packages dépendent de ce package, la commande échoue, sauf si – Force l’option est spécifiée.

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | (Obligatoire) L’identificateur du package à désinstaller. -Id commutateur proprement dit est facultatif. |
| Version | La version du package à désinstaller, par défaut à la version actuellement installée. |
| RemoveDependencies | Désinstallez le package et ses dépendances inutilisées. Autrement dit, si une dépendance a un autre package qui en dépend, elle est ignorée. |
| Nom_projet | Le projet à partir de laquelle la désinstallation du package, par défaut pour le projet par défaut. |
| Force | Force un package à désinstaller, même si d’autres packages qui en dépendent. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la désinstallation. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Uninstall-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
