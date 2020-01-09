---
title: Informations de référence sur PowerShell Find-package de NuGet
description: Référence de la commande PowerShell Find-package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384631"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Console du gestionnaire de packages dans Visual Studio)

*Version 3.0 +; Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande PowerShell Find-package générique, consultez les informations de référence sur le fichier [PackageManagement](/powershell/module/packagemanagement/?view=powershell-6)de la page.*

Obtient le jeu de packages distants avec l’ID ou les mots clés spécifiés à partir de la source du package.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Paramètre | Description |
| --- | --- |
| Mots clés d’ID &lt;&gt; | Souhaitée Mots clés à utiliser lors de la recherche de la source du package. Utilisez-ExactMatch pour retourner uniquement les packages dont l’ID de package correspond aux mots clés. Si aucun mot clé n’est donné, `Find-Package` retourne la liste des 20 premiers packages par téléchargement, ou le nombre spécifié par-First. Notez que-ID est facultatif et qu’il n’y a pas d’opération. |
| Source | URL ou chemin d’accès de dossier de la source du package à rechercher. Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif. En cas d’omission, `Find-Package` recherche la source de package actuellement sélectionnée. |
| AllVersions | Affiche toutes les versions disponibles de chaque package, et non uniquement la version la plus récente. |
| First | Nombre de packages à retourner à partir du début de la liste ; la valeur par défaut est 20. |
| Skip | Omet les premiers packages de&gt; &lt;int de la liste affichée.  |
| IncludePrerelease | Contient des packages de version préliminaire dans les résultats. |
| ExactMatch | Spécifié pour utiliser &lt;Mots clés&gt; en tant qu’ID de package qui respecte la casse. |
| StartWith | Retourne les packages dont l’ID de package commence par &lt;Mots clés&gt;. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Find-Package` prend en charge les [paramètres PowerShell communs](https://go.microsoft.com/fwlink/?LinkID=113216)suivants : Debug, Error action, ErrorVariable, unbuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
