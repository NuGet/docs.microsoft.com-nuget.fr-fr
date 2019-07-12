---
title: Référence de PowerShell Get-projet NuGet
description: Référence de commande GetProject PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842282"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Console du gestionnaire de packages dans Visual Studio)

*Disponible uniquement dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows.*

Affiche des informations sur la valeur par défaut ou le projet spécifié. `Get-Project` en particulier, retourne un référent à l’objet DTE (Development Tools Environment) de Visual Studio pour le projet.

## <a name="syntax"></a>Syntaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Nom | Spécifie le projet à afficher, par défaut pour le projet par défaut sélectionné dans la Console du Gestionnaire de Package. -Nom du commutateur est lui-même est facultatif. |
| Tous | Affiche des informations pour chaque projet dans la solution. l’ordre des projets n’est pas déterministe. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Get-Project` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```