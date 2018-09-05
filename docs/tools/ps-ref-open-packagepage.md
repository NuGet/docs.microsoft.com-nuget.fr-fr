---
title: Référence de PowerShell NuGet Open-PackagePage
description: Référence de commande PowerShell de Open-PackagePage dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547166"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Console du gestionnaire de packages dans Visual Studio)

*Déconseillé dans 3.0 + ; disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*

Lance le navigateur par défaut avec le projet, une licence ou une URL d’abus de rapport pour le package spécifié.

## <a name="syntax"></a>Syntaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | L’ID de package du package souhaité. -Id commutateur proprement dit est facultatif. |
| Version | La version du package, par défaut vers la dernière version. |
| Source | La source du package, par défaut pour la source sélectionnée dans la liste déroulante de la source. |
| Licence | Ouvre le navigateur vers une URL de licence du package. Si - licence ni - ReportAbuse est spécifié, le navigateur ouvre URL du projet du package. |
| ReportAbuse | Ouvre le navigateur vers l’URL un abus de rapport du package. Si - licence ni - ReportAbuse est spécifié, le navigateur ouvre URL du projet du package. |
| PassThru | Affiche l’URL ; Utilisez avec - WhatIf pour supprimer l’ouverture du navigateur. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Open-PackagePage` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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