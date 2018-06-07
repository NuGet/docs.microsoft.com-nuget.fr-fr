---
title: Référence de PowerShell NuGet Open-PackagePage
description: Référence de commande PowerShell de PackagePage de l’ouverture de la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817718"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Console du gestionnaire de packages dans Visual Studio)

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