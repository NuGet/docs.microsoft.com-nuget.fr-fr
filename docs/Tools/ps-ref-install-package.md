---
title: "Référence de PowerShell Install-Package NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Référence de commande PowerShell de Package d’installation de la Console du Gestionnaire de Package NuGet dans Visual Studio."
keywords: "NuGet package manager console, commandes Powershell de NuGet, référence NuGet Powershell, Install-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f5f6b3dffb27af510b750650561cdff597c927e0
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Package Manager Console dans Visual Studio)

*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sous Windows. Pour la commande PowerShell Install-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*

Installe un package et ses dépendances dans un projet.

## <a name="syntax"></a>Syntaxe

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Dans NuGet 2.8 + `Install-Package` peut passer un package existant dans votre projet. Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

NuGet 2.7 et versions antérieur génère une erreur indiquant qu’une version plus récente est déjà installée.
  
## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | (Obligatoire) L’identificateur du package à installer. (*3.0 +*) l’identificateur peut être un chemin d’accès ou l’URL d’un `packages.config` fichier ou un `.nupkg` fichier. -Id commutateur lui-même est facultative. |
| IgnoreDependencies | Installer ce package uniquement, sans ses dépendances. |
| Nom_projet | Le projet dans lequel installer le package, par défaut pour le projet par défaut. |
| Source | Le chemin d’accès URL ou un dossier pour la source du package à rechercher. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Install-Package` recherche la source du package actuellement sélectionnée. |
| Version | La version du package à installer, par défaut pour la version la plus récente. |
| IncludePrerelease | Prend en compte les versions préliminaires des packages pour l’installation. Si omis, seuls les packages stables sont pris en compte. |
| FileConflictAction | Action à prendre lorsque vous êtes invité à remplacer ou ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :<br/><ul><li>*La plus basse* (par défaut) : la version la plus basse</li><li>*HighestPatch*: la version avec le correctif logiciel le plus bas majeure, mineure la plus basse, la plus élevée</li><li>*HighestMinor*: la version avec le plus bas principales, le correctif plus élevé de secondaire, la plus élevée</li><li>*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</li></ul>Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer l’installation. |

Aucun de ces paramètres accepter pipeline entrée ni les caractères génériques.

## <a name="common-parameters"></a>Paramètres communs

`Install-Package` prend en charge les [les paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

## <a name="examples"></a>Exemples

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
