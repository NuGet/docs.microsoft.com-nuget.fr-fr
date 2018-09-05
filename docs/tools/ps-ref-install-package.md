---
title: Référence de PowerShell Install-Package NuGet
description: Référence de commande Install-Package PowerShell dans la Console du Gestionnaire de Package NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546024"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Console du gestionnaire de packages dans Visual Studio)

*Cette rubrique décrit la commande dans le [Console du Gestionnaire de Package NuGet](package-manager-console.md) dans Visual Studio sur Windows. Pour la commande PowerShell Install-Package générique, consultez la [PowerShell PackageManagement référence](/powershell/module/packagemanagement/?view=powershell-6).*

Installe un package et ses dépendances dans un projet.

## <a name="syntax"></a>Syntaxe

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Dans NuGet 2.8 + `Install-Package` peuvent passer un package existant dans votre projet. Par exemple, si vous avez 5.1.0-rc1 Microsoft.AspNet.MVC installé, la commande suivante rétrograder il 5.0.0 :

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| Id | (Obligatoire) L’identificateur du package à installer. (*3.0 +*) l’identificateur peut être un chemin d’accès ou l’URL d’un `packages.config` fichier ou un `.nupkg` fichier. -Id commutateur proprement dit est facultatif. |
| IgnoreDependencies | Installer uniquement ce package et pas ses dépendances. |
| Nom_projet | Le projet dans lequel installer le package, par défaut pour le projet par défaut. |
| Source | Le chemin d’accès URL ou un dossier pour la source du package à rechercher. Chemins d’accès du dossier local peuvent être absolu ou relatif du dossier actif. Si omis, `Install-Package` recherche la source du package actuellement sélectionnée. |
| Version | La version du package à installer, par défaut vers la dernière version. |
| IncludePrerelease | Prend en compte pour l’installation des packages de version préliminaire. Si omis, seuls les packages stables sont considérés comme. |
| FileConflictAction | L’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet. Les valeurs possibles sont *remplacer, ignorer, None, OverwriteAll*, et *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La version des packages de dépendance à utiliser, ce qui peut prendre l’une des opérations suivantes :<br/><ul><li>*La plus basse* (valeur par défaut) : la version la plus basse</li><li>*HighestPatch*: la version du correctif plus bas majeure, mineure la plus basse, le plus élevé</li><li>*HighestMinor*: la version avec le plus bas principales, des correctifs mineurs, la plus élevée le plus élevé</li><li>*La plus élevée* (valeur par défaut pour le Package de mise à jour sans paramètres) : la version la plus récente</li></ul>Vous pouvez définir la valeur par défaut en utilisant le [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) définition dans le `Nuget.Config` fichier. |
| WhatIf | Montre ce qui se passerait lors de l’exécution de la commande sans réellement effectuer l’installation. |

Aucun de ces paramètres accepter les caractères d’entrée ou de caractère générique de pipeline.

## <a name="common-parameters"></a>Paramètres communs

`Install-Package` prend en charge les éléments suivants [paramètres PowerShell communs](http://go.microsoft.com/fwlink/?LinkID=113216): débogage, Action d’erreur, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction et WarningVariable.

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
