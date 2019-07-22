---
title: Désinstaller NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Uninstall-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327276"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Console du gestionnaire de packages dans Visual Studio)

*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour la commande générique de désinstallation de PowerShell, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Supprime un package d’un projet, en supprimant éventuellement ses dépendances. Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – force est spécifiée.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Si d’autres packages dépendent de ce package, la commande échoue, sauf si l’option – force est spécifiée.

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | Souhaitée Identificateur du package à désinstaller. Le commutateur-ID lui-même est facultatif. |
| Version | Version du package à désinstaller, avec la version actuellement installée par défaut. |
| RemoveDependencies | Désinstallez le package et ses dépendances inutilisées. Autrement dit, si une dépendance possède un autre package qui en dépend, elle est ignorée. |
| Nom_projet | Projet à partir duquel désinstaller le package, par défaut au projet par défaut. |
| Appliqués | Force la désinstallation d’un package, même si d’autres packages en dépendent. |
| WhatIf | Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la désinstallation. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Uninstall-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
