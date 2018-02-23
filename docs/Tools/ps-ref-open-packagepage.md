---
title: "Référence de PowerShell NuGet Open-PackagePage | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande PowerShell de PackagePage de l’ouverture de la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, NuGet Powershell référence, ouvrez-PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cc645d9a2779fd6b1b329e9aac4777d50f75d16
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Ouvrir-PackagePage (Console du Gestionnaire de Package dans Visual Studio)

*Déconseillé dans 3.0 + ; disponible uniquement dans les [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows.*

Lance le navigateur par défaut avec le projet, les licences ou les URL d’abus de rapport pour le package spécifié.

## <a name="syntax"></a>Syntaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | L’ID de package du package souhaité. -Id commutateur lui-même est facultative. |
| Version | La version du package, par défaut pour la version la plus récente. |
| Source | La source du package, par défaut pour la source sélectionnée dans la liste déroulante de la source. |
| Licence | Ouvre le navigateur vers une URL de licence du package. Si - licence ni - ReportAbuse est spécifié, le navigateur s’ouvre projet URL du package. |
| ReportAbuse | Ouvre le navigateur vers une URL d’abus de rapport du package. Si - licence ni - ReportAbuse est spécifié, le navigateur s’ouvre projet URL du package. |
| PassThru | Affiche l’URL ; Utilisez avec - WhatIf pour supprimer d’ouvrir le navigateur. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Open-PackagePage` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```