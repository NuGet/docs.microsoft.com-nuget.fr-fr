---
title: Informations de référence sur PowerShell Get-Project de NuGet
description: Référence pour la commande PowerShell GetProject dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777466"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (console du gestionnaire de package dans Visual Studio)

*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Affiche des informations sur le projet par défaut ou spécifié. `Get-Project` retourne spécifiquement un référent à l’objet Visual Studio DTE (Development Tools Environment) pour le projet.

## <a name="syntax"></a>Syntaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Nom | Spécifie le projet à afficher, en définissant par défaut le projet par défaut sélectionné dans la console du gestionnaire de package. Le commutateur-Name est lui-même facultatif. |
| Tous | Affiche des informations pour chaque projet de la solution ; l’ordre des projets n’est pas déterministe. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Get-Project` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```