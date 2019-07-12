---
title: Référence de PowerShell NuGet ajouter-BindingRedirect
description: Référence de commande Add-BindingRedirect PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842537"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Console du gestionnaire de packages dans Visual Studio)

*Disponible uniquement dans le [Console du Gestionnaire de Package](package-manager-console.md) dans Visual Studio sur Windows.*

Examine tous les assemblys dans le chemin de sortie pour un projet et ajoute des redirections de liaison au fichier de configuration web ou application lorsque cela est nécessaire. Cette commande est exécutée automatiquement quand vous installez un package.

Pour plus d’informations sur la liaison des redirections et pourquoi ils sont utilisés, consultez [redirection des Versions d’Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .NET.

## <a name="syntax"></a>Syntaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Nom_projet | (Obligatoire) Le projet auquel ajouter des redirections de liaison. Le commutateur - NomProjet proprement dit est facultatif. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Add-BindingRedirect` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```