---
title: "Référence de PowerShell NuGet Uninstall-Package | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Référence de commande PowerShell de Package de désinstallation de la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Package de désinstallation"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Package Manager Console dans Visual Studio)

*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Uninstall-Package générique, consultez la [PowerShell PackageManagement référence](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*

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

`Uninstall-Package`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
