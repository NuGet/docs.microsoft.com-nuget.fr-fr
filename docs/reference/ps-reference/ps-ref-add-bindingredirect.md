---
title: Informations de référence sur PowerShell Add-BindingRedirect de NuGet
description: Référence pour Add-BindingRedirect commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777619"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (console du gestionnaire de package dans Visual Studio)

*Disponible uniquement dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Examine tous les assemblys dans le chemin de sortie d’un projet et ajoute des redirections de liaison au fichier de configuration d’application ou Web, si nécessaire. Cette commande est exécutée automatiquement lors de l’installation d’un package.

> [!NOTE]
> Cela s’applique uniquement aux scénarios utilisant un fichier packages.config. Pour plus d’informations, consultez informations de référence sur les [fichiers NuGet packages.config](~/reference/packages-config.md).

Pour plus d’informations sur les redirections de liaison et la raison pour laquelle elles sont utilisées, consultez [redirection des versions d’assemblys](/dotnet/framework/configure-apps/redirect-assembly-versions) dans la documentation .net.

## <a name="syntax"></a>Syntaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| ProjectName | Souhaitée Projet auquel ajouter des redirections de liaison. Le commutateur-ProjectName lui-même est facultatif. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Add-BindingRedirect` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```