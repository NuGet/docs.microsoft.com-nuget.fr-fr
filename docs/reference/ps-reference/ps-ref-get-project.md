---
title: Informations de référence sur PowerShell pour le projet NuGet
description: Référence pour la commande PowerShell GetProject dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384618"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Console du gestionnaire de packages dans Visual Studio)

*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Affiche des informations sur le projet par défaut ou spécifié. `Get-Project` retourne spécifiquement un référent à l’objet Visual Studio DTE (Development Tools Environment) pour le projet.

## <a name="syntax"></a>Syntaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Paramètre | Description |
| --- | --- |
| Name | Spécifie le projet à afficher, en définissant par défaut le projet par défaut sélectionné dans la console du gestionnaire de package. Le commutateur-Name est lui-même facultatif. |
| Toutes les | Affiche des informations pour chaque projet de la solution ; l’ordre des projets n’est pas déterministe. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Get-Project` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```