---
title: Informations de référence sur PowerShell Register-TabExpansion de NuGet
description: Référence pour Register-TabExpansion commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777460"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (console du gestionnaire de package dans Visual Studio)

*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Inscrit un expansion de tabulation pour les paramètres de la commande spécifiée, de telle sorte que lorsque la touche Tab est utilisée lors de l’entrée dans une commande, les valeurs développées apparaissent en tant qu’options disponibles pour le paramètre en question. Toutes les expansions précédentes de la commande sont remplacées.

## <a name="syntax"></a>Syntaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Nom | Souhaitée Commande dans laquelle enregistrer les expansions. Le commutateur-Name lui-même est facultatif. |
| Définition | Souhaitée Objet décrivant l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom du paramètre à modifier et chaque `<value>` fournit une expansion spécifique. Les guillemets simples et doubles sont acceptés. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Register-TabExpansion` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

Prenons l’exemple d’une solution qui contient trois projets : EventManager, Utilities et SpecialParser. Le développeur utilise fréquemment la `Update-Package` commande à différents moments avec chacun de ces projets. Elle cherche à ce que la `Update-Package` commande fournisse des expansions de saisie semi-automatique pour l' `-ProjectName` argument, de sorte qu’elle n’a pas besoin de taper un nom de projet à chaque fois. 

La commande suivante inscrit ces trois noms de projet en tant qu’extension pour le `-ProjectName` paramètre :

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Le développeur peut ensuite taper `Update-Package -ProjectName ` , appuyer sur la touche Tab et voir les expansions proposées en tant qu’options de saisie semi-automatique :

![Exemple d’utilisation de Register-TabExpansion](media/Register-TabExpansion-Example.png)