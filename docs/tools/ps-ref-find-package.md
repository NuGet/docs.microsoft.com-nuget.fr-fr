---
title: Référence de PowerShell NuGet Find-Package
description: Référence de commande PowerShell de Find-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550976"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Console du gestionnaire de packages dans Visual Studio)

*Version 3.0 et versions ultérieures ; Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Find-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*

Obtient l’ensemble des packages à distance avec l’ID spécifié ou des mots clés à partir de la source du package.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| ID &lt;mots clés&gt; | (Obligatoire) Mots clés à utiliser pour rechercher la source du package. Utilisez - ExactMatch pour retourner uniquement les packages dont l’ID de package correspond aux mots clés. Si aucun mot clé n’est fournies, `Find-Package` retourne une liste des packages top 20 par téléchargements ou le nombre spécifiée par - tout d’abord. Notez que - Id est facultatif et une absence d’opération. |
| Source | Le chemin d’accès URL ou un dossier pour la source du package à rechercher. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Find-Package` recherche la source du package actuellement sélectionnée. |
| AllVersions | Affiche toutes les versions disponibles de chaque package plutôt que seule la dernière version. |
| First | Le nombre de packages à retourner à partir du début de la liste. la valeur par défaut est 20. |
| Ignorer | Omet le premier &lt;int&gt; packages à partir de la liste affichée.  |
| IncludePrerelease | Inclut les packages de version préliminaire dans les résultats. |
| ExactMatch | Spécifié à utiliser &lt;mots clés&gt; qu’un ID de package respectant la casse. |
| StartWith | Retourne les packages dont package ID commence par &lt;mots clés&gt;. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Find-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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
