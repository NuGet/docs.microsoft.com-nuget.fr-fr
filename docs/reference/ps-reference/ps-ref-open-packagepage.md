---
title: Informations de référence sur PowerShell Open-PackagePage de NuGet
description: Référence pour la commande PowerShell Open-PackagePage dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327376"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Console du gestionnaire de packages dans Visual Studio)

*Déconseillé dans 3.0 +; disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Lance le navigateur par défaut avec l’URL du projet, de la licence ou du rapport d’abus pour le package spécifié.

## <a name="syntax"></a>Syntaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | ID de package du package souhaité. Le commutateur-ID lui-même est facultatif. |
| Version | Version du package, avec la version la plus récente par défaut. |
| source | Source du package, par défaut à la source sélectionnée dans la liste déroulante source. |
| Licence | Ouvre le navigateur à l’URL de licence du package. Si ni-License ni-ReportAbuse n’est spécifié, le navigateur ouvre l’URL du projet du package. |
| ReportAbuse | Ouvre le navigateur sur l’URL d’abus de rapport du package. Si ni-License ni-ReportAbuse n’est spécifié, le navigateur ouvre l’URL du projet du package. |
| PassThru | Affiche l’URL; Utilisez avec-WhatIf pour supprimer l’ouverture du navigateur. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Open-PackagePage`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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