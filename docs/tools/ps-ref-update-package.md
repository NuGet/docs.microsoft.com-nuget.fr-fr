---
title: Référence de PowerShell Package de mise à jour de NuGet
description: Référence de commande PowerShell de Package de mise à jour dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546074"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Console du gestionnaire de packages dans Visual Studio)

*Disponible uniquement dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows.*

Met à jour un package et ses dépendances ou tous les packages dans un projet, une version plus récente.

## <a name="syntax"></a>Syntaxe

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

Dans NuGet 2.8 + `Update-Package` peut être utilisé pour passer un package existant dans votre projet. Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Paramètres

|  Paramètre | Description |
| --- | --- |
| Id | L’identificateur du package à mettre à jour. Si omis, met à jour tous les packages. -Id commutateur proprement dit est facultatif. |
| IgnoreDependencies | Ignore la mise à jour les dépendances du package. |
| Nom_projet | Le nom du projet contenant les packages à mettre à jour, par défaut à tous les projets. |
| Version | La version à utiliser pour la mise à niveau, la valeur par défaut : la dernière version. Dans NuGet 3.0 +, la valeur de version doit être un des *plus petit, plus élevé, HighestMinor*, ou *HighestPatch* (équivalent à - Safe). |
| Safe | Contraint les mises à niveau vers des versions uniquement avec la même version principale et secondaire en tant que le package actuellement installé. |
| Source | Le chemin d’accès URL ou un dossier pour la source du package à rechercher. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Update-Package` recherche la source du package actuellement sélectionnée. |
| IncludePrerelease | Inclut les packages de version préliminaire des mises à jour. |
| Réinstallation | Packages de Resintalls à l’aide de leurs versions actuellement installées. Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | L’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *IgnoreAll* (3.0 +). |
| DependencyVersion | La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :<br/><ul><li>*La plus basse* (valeur par défaut) : la version la plus basse</li><li>*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</li><li>*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</li><li>*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</li></ul>Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier. |
| ToHighestPatch | Contraint les mises à niveau uniquement aux versions avec la même version mineure que le package actuellement installée. |
| ToHighestMinor | Contraint les mises à niveau uniquement aux versions avec la même version principale que le package actuellement installée. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer la mise à jour. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

### <a name="common-parameters"></a>Paramètres communs

`Update-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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
