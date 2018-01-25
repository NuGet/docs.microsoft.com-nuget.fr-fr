---
title: "Référence de PowerShell NuGet Register-TabExpansion | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de commande Register-TabExpansion PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Register-TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Console du Gestionnaire de Package dans Visual Studio)

*Disponible uniquement dans les [Console du Gestionnaire de Package NuGet](Package-Manager-Console.md) dans Visual Studio sous Windows.*

Inscrit une tabulation pour les paramètres de la commande spécifiée, telle que lorsque l’onglet est utilisé lorsque vous entrez une commande, les valeurs de développé s’affichent en tant que les options disponibles pour le paramètre en question. Les expansions précédentes de la commande sont remplacées.

## <a name="syntax"></a>Syntaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Name | (Obligatoire) La commande pour laquelle inscrire les expansions. -Nom de commutateur lui-même est facultative. |
| Définition | (Obligatoire) Un objet qui décrit l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom de paramètre à modifier et à chaque `<value>` fournit une extension spécifique. Les guillemets simples et doubles sont acceptés. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Register-TabExpansion`prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

Adoptez une solution qui contient trois noms de projets Gestionnaire d’événements, des utilitaires et SpecialParser. Le développeur utilise fréquemment la `Update-Package` commande à différents moments avec chacun de ces projets. Elle trouve utile d’avoir le `Update-Package` commande fournissent des extensions de la saisie semi-automatique pour le `-ProjectName` argument afin qu’elle n’a pas besoin de taper un nom de projet chaque fois. 

La commande suivante, enregistre ensuite, ces noms de trois projet comme une extension pour le `-ProjectName` paramètre :

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Le développeur peut puis tapez `Update-Package -ProjectName `, appuyez sur Tab et consultez les expansions proposées comme options de saisie semi-automatique :

![Exemple d’utilisation de TabExpansion de Registre](media/Register-TabExpansion-Example.png)
