---
title: Référence de PowerShell Get-Package NuGet
description: Référence de commande PowerShell de Get-Package dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551440"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Console du gestionnaire de packages dans Visual Studio)

*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Get-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*

Récupère la liste des packages installés dans le référentiel local, répertorie les packages disponibles à partir d’une source de package lorsqu’il est utilisé avec le commutateur - ListAvailable ou répertorie les mises à jour disponibles lorsqu’il est utilisé avec le commutateur - mise à jour.

## <a name="syntax"></a>Syntaxe

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Sans paramètres, `Get-Package` affiche la liste des packages installés dans le projet par défaut.

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Source | Le chemin d’accès URL ou un dossier pour le package. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Get-Package` recherche la source du package actuellement sélectionnée. Lorsqu’il est utilisé avec - ListAvailable, par défaut sur nuget.org. |
| ListAvailable | Répertorie les packages disponibles à partir d’une source de package, par défaut sur nuget.org. Affiche une valeur par défaut des 50 packages, sauf si - PageSize et/ou - premier est spécifié. |
| Mises à jour | Répertorie les packages qui ont une mise à jour est disponible à partir de la source du package. |
| Nom_projet | Le projet à partir duquel obtenir les packages installés. Si omis, retourne installées projets pour la solution entière. |
| Filtre | Une chaîne de filtre utilisée pour limiter la liste des packages en l’appliquant à l’ID de package, la description et les balises. |
| First | Le nombre de packages à retourner à partir du début de la liste. Si non spécifié, par défaut est 50. |
| Ignorer | Omet le premier &lt;int&gt; packages à partir de la liste affichée.  |
| AllVersions | Affiche toutes les versions disponibles de chaque package plutôt que seule la dernière version. |
| IncludePrerelease | Inclut les packages de version préliminaire dans les résultats. |
| PageSize | *(3.0 +)*  Lorsqu’il est utilisé avec - ListAvailable (obligatoire), le nombre de packages à la liste avant de donner une invite pour continuer. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Get-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
