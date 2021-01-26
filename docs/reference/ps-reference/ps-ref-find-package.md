---
title: Informations de référence sur PowerShell Find-Package de NuGet
description: Référence pour Find-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777510"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (console du gestionnaire de package dans Visual Studio)

*Version 3.0 +; Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Find-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Obtient le jeu de packages distants avec l’ID ou les mots clés spécifiés à partir de la source du package.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| &lt;Mots clés d’ID&gt; | Souhaitée Mots clés à utiliser lors de la recherche de la source du package. Utilisez-ExactMatch pour retourner uniquement les packages dont l’ID de package correspond aux mots clés. Si aucun mot clé n’est donné, `Find-Package` retourne la liste des 20 premiers packages par téléchargement ou le nombre spécifié par-First. Notez que-ID est facultatif et qu’il n’y a pas d’opération. |
| Source | URL ou chemin d’accès de dossier de la source du package à rechercher. Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif. En cas d’omission, `Find-Package` effectue une recherche dans la source du package actuellement sélectionnée. |
| AllVersions | Affiche toutes les versions disponibles de chaque package, et non uniquement la version la plus récente. |
| Premier | Nombre de packages à retourner à partir du début de la liste ; la valeur par défaut est 20. |
| Ignorer | Omet les premiers &lt; packages int &gt; de la liste affichée.  |
| IncludePrerelease | Contient des packages de version préliminaire dans les résultats. |
| ExactMatch | Spécifié pour utiliser &lt; des mots clés &gt; en tant qu’ID de package qui respecte la casse. |
| StartWith | Retourne les packages dont l’ID de package commence par des &lt; Mots clés &gt; . |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Find-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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