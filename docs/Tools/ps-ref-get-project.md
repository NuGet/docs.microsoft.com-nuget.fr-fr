---
title: "Référence de PowerShell Get-projet NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande GetProject PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Get-projet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-projet (Console du Gestionnaire de Package dans Visual Studio)

*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*

Affiche des informations sur la valeur par défaut ou le projet spécifié. `Get-Project` spécifiquement, retourne une référence à l’objet DTE (environnement d’outils de développement) de Visual Studio pour le projet.

## <a name="syntax"></a>Syntaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Name | Spécifie le projet à afficher, par défaut pour le projet par défaut sélectionné dans la Console du Gestionnaire de Package. -Nom de commutateur est facultatif. |
| Tous | Affiche des informations pour chaque projet dans la solution ; l’ordre des projets n’est pas déterministe. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Get-Project` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```