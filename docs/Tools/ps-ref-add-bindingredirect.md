---
title: "Référence de PowerShell NuGet ajouter-BindingRedirect | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Référence de commande Add-BindingRedirect PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Add-BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Ajouter-BindingRedirect (Console du Gestionnaire de Package dans Visual Studio)

*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows.*

Examine tous les assemblys du chemin de sortie pour un projet et ajoute des redirections de liaison au fichier de configuration web ou application en cas de besoin. Cette commande est exécutée automatiquement lors de l’installation d’un package.

Pour plus d’informations sur la liaison des redirections et pourquoi ils sont utilisés, consultez [redirection des Versions d’Assembly](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .NET.

## <a name="syntax"></a>Syntaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Nom_projet | (Obligatoire) Le projet auquel vous souhaitez ajouter des redirections de liaison. Le commutateur - NomProjet lui-même est facultatif. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Add-BindingRedirect`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```