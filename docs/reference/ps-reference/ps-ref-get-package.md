---
title: Informations de référence sur PowerShell Get-Package de NuGet
description: Référence pour Get-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237229"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (console du gestionnaire de package dans Visual Studio)

*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Get-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Récupère la liste des packages installés dans le référentiel local, répertorie les packages disponibles à partir d’une source de package lorsqu’ils sont utilisés avec le commutateur-ListAvailable, ou répertorie les mises à jour disponibles lorsqu’elles sont utilisées avec le commutateur-Update.

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
| Source | URL ou chemin d’accès du dossier pour le package. Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif. En cas d’omission, `Get-Package` effectue une recherche dans la source du package actuellement sélectionnée. En cas d’utilisation avec-ListAvailable, la valeur par défaut est nuget.org. |
| ListAvailable | Répertorie les packages disponibles à partir d’une source de package, par défaut nuget.org. Affiche la valeur par défaut de 50 packages, sauf si-PageSize et/ou-First sont spécifiés. |
| Mises à jour | Répertorie les packages dont la mise à jour est disponible à partir de la source du package. |
| ProjectName | Projet à partir duquel les packages installés doivent être installés. En cas d’omission, retourne les projets installés pour l’ensemble de la solution. |
| Filtrer | Chaîne de filtrage utilisée pour limiter la liste des packages en l’appliquant à l’ID de package, à la description et aux balises. |
| Premier | Nombre de packages à retourner à partir du début de la liste. S’il n’est pas spécifié, la valeur par défaut est 50. |
| Ignorer | Omet les premiers &lt; packages int &gt; de la liste affichée.  |
| AllVersions | Affiche toutes les versions disponibles de chaque package, et non uniquement la version la plus récente. |
| IncludePrerelease | Contient des packages de version préliminaire dans les résultats. |
| PageSize | *(3.0 +)* En cas d’utilisation avec-ListAvailable (obligatoire), nombre de packages à répertorier avant de donner une invite pour continuer. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Get-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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