---
title: Référence de PowerShell NuGet Register-TabExpansion
description: Référence de commande Register-TabExpansion PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546603"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Console du Gestionnaire de Package dans Visual Studio)

*Disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*

Inscrit une tabulation pour les paramètres de la commande spécifiée, telle que lors de l’onglet est utilisé lorsque vous entrez une commande, les valeurs de développé s’affichent en tant qu’options disponibles pour le paramètre en question. Les expansions précédentes de la commande sont remplacées.

## <a name="syntax"></a>Syntaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Name | (Obligatoire) La commande pour laquelle inscrire les expansions. -Nom du commutateur proprement dit est facultatif. |
| Définition | (Obligatoire) Objet décrivant l’argument dans la syntaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` où `<parameter>` est le nom du paramètre à modifier et chacun `<value>` fournit une expansion spécifique. Les guillemets simples et doubles sont acceptés. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Register-TabExpansion` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

Envisagez une solution qui contient trois noms de projets EventManager, d’utilitaires et SpecialParser. Le développeur utilise fréquemment la `Update-Package` commande à des moments différents avec chacun de ces projets. Elle estime qu’il est utile de disposer la `Update-Package` commande fournir des expansions de la saisie semi-automatique pour le `-ProjectName` argument afin qu’elle n’a pas besoin de taper un nom de projet chaque fois. 

La commande suivante, inscrit ensuite, ces noms de trois projet comme une extension pour le `-ProjectName` paramètre :

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Le développeur peut puis tapez `Update-Package -ProjectName `, appuyez sur Tab et consultez les expansions proposées comme options de la saisie semi-automatique :

![Exemple d’utilisation de Register-TabExpansion](media/Register-TabExpansion-Example.png)
