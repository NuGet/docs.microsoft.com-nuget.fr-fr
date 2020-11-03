---
title: Informations de référence sur PowerShell Install-Package de NuGet
description: Référence pour Install-Package commande PowerShell dans la console du gestionnaire de package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5bda888e0fb526faca79e88da93b0ceb9aff5348
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237203"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (console du gestionnaire de package dans Visual Studio)

*Cette rubrique décrit la commande dans la [console du gestionnaire de package](../../consume-packages/install-use-packages-powershell.md) dans Visual Studio sur Windows. Pour obtenir la commande Install-Package PowerShell générique, consultez la référence de la page [PackageManagement de PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Installe un package et ses dépendances dans un projet.

## <a name="syntax"></a>Syntaxe

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Dans NuGet 2.8 +, `Install-Package` peut rétrograder un package existant dans votre projet. Par exemple, si vous avez installé Microsoft. AspNet. MVC 5.1.0-RC1, la commande suivante le rétrograde à 5.0.0 :

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | Souhaitée Identificateur du package à installer. ( *3.0 +* ) L’identificateur peut être un chemin d’accès ou une URL d’un `packages.config` fichier ou d’un `.nupkg` fichier. Le commutateur-ID lui-même est facultatif. |
| IgnoreDependencies | Installez uniquement ce package et non ses dépendances. |
| ProjectName | Projet dans lequel installer le package, par défaut au projet par défaut. |
| Source | URL ou chemin d’accès de dossier de la source du package à rechercher. Les chemins d’accès des dossiers locaux peuvent être absolus ou relatifs au dossier actif. En cas d’omission, `Install-Package` effectue une recherche dans la source du package actuellement sélectionnée. |
| Version | Version du package à installer, avec la version la plus récente par défaut. |
| IncludePrerelease | Prend en compte les packages de version préliminaire pour l’installation. En l’absence d’indications, seuls les packages stables sont considérés. |
| FileConflictAction | Action à exécuter lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *overwrite, ignore, None, OverwriteAll* et *(3.0 +)* *IgnoreAll* . |
| DependencyVersion | Version des packages de dépendance à utiliser, qui peut être l’une des suivantes :<br/><ul><li>La *plus basse* (par défaut) : la version la plus basse</li><li>*HighestPatch* : version avec le correctif le plus bas, le plus petit minimum, le plus élevé.</li><li>*HighestMinor* : version avec le correctif le plus bas, le plus élevé, le plus élevé, le plus élevé</li><li>La *plus élevée* (valeur par défaut pour Update-Package sans paramètres) : la version la plus élevée</li></ul>Vous pouvez définir la valeur par défaut à l’aide du [`dependencyVersion`](../nuget-config-file.md#config-section) paramètre dans le `Nuget.Config` fichier. |
| WhatIf | Montre ce qui se passe lors de l’exécution de la commande sans réellement effectuer l’installation. |

Aucun de ces paramètres n’accepte d’entrée de pipeline ou de caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Install-Package` prend en charge les [paramètres PowerShell communs](/powershell/module/microsoft.powershell.core/about/about_commonparameters)suivants : Debug, Error action, ErrorVariable, labuffer, unvariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```