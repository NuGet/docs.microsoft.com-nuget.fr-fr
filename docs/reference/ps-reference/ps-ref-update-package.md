---
title: Mise à jour NuGet-référence PowerShell du package
description: Référence de la commande PowerShell Update-Package dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327266"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Console du gestionnaire de packages dans Visual Studio)

*Disponible uniquement dans la [console du gestionnaire de package NuGet](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows.*

Met à jour un package et ses dépendances, ou tous les packages d’un projet, vers une version plus récente.

## <a name="syntax"></a>Syntaxe

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

Dans NuGet 2.8 +, `Update-Package` peut être utilisé pour rétrograder un package existant dans votre projet. Par exemple, si vous avez installé Microsoft. AspNet. MVC 5.1.0-RC1, la commande suivante le rétrograde à 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Paramètres

|  Paramètre | Description |
| --- | --- |
| Id | Identificateur du package à mettre à jour. En cas d’omission, met à jour tous les packages. Le commutateur-ID lui-même est facultatif. |
| IgnoreDependencies | Ignore la mise à jour des dépendances du package. |
| Nom_projet | Nom du projet contenant les packages à mettre à jour, par défaut pour tous les projets. |
| Version | Version à utiliser pour la mise à niveau, avec la version la plus récente par défaut. Dans NuGet 3.0 +, la valeur de version doit être l’une des valeurs les *plus basses, les plus élevées, les HighestMinor*ou les *HighestPatch* (équivalent à-Safe). |
| Safe | Limite les mises à niveau vers des versions avec la même version principale et la version mineure que le package actuellement installé. |
| source | URL ou chemin d’accès de dossier de la source du package à rechercher. Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif. En cas d’omission `Update-Package` , effectue une recherche dans la source du package actuellement sélectionnée. |
| IncludePrerelease | Contient des packages de version préliminaire pour les mises à jour. |
| Réinstallation | Resintalls les packages en utilisant les versions actuellement installées. Consultez [Réinstallation et mise à jour des packages](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll*et *IgnoreAll* (3.0 +). |
| DependencyVersion | Version des packages de dépendance à utiliser, qui peut être l’une des suivantes:<br/><ul><li>La *plus basse* (par défaut): la version la plus basse</li><li>*HighestPatch*: version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</li><li>*HighestMinor*: version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</li><li>La *plus élevée* (valeur par défaut pour Update-Package sans paramètres): la version la plus élevée</li></ul>Vous pouvez définir la valeur par défaut à [`dependencyVersion`](../nuget-config-file.md#config-section) l’aide du `Nuget.Config` paramètre dans le fichier. |
| ToHighestPatch | équivalent à-Safe. |
| ToHighestMinor | Limite les mises à niveau à des versions avec la même version principale que le package actuellement installé. |
| WhatIf | Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer la mise à jour. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

### <a name="common-parameters"></a>Paramètres communs

`Update-Package`prend en charge les [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216)suivants: Débogage, action d’erreur, ErrorVariable, mise en mémoire tampon, dévariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

### <a name="examples"></a>Exemples

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
