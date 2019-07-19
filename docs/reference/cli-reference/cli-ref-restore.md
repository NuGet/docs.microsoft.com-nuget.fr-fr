---
title: Commande de restauration de l’interface CLI NuGet
description: Référence pour la commande de restauration de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327636"
---
# <a name="restore-command-nuget-cli"></a>Restore, commande (interface CLI NuGet)

**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 2.7+

Télécharge et installe tous les packages manquants `packages` dans le dossier. Lorsqu’il est utilisé avec NuGet 4.0 + et le format PackageReference, `<project>.nuget.props` génère un fichier, si nécessaire, `obj` dans le dossier. (Le fichier peut être omis dans le contrôle de code source.)

Sur Mac OSX et Linux avec l’interface CLI sur mono, la restauration des packages n’est pas prise en charge avec PackageReference.

## <a name="usage"></a>Usage

```cli
nuget restore <projectPath> [options]
```

où `<projectPath>` spécifie l’emplacement d’une solution ou `packages.config` d’un fichier. Consultez les [Remarques](#remarks) ci-dessous pour obtenir des détails sur le comportement.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| DirectDownload | *(4.0 +)* Télécharge les packages directement sans remplir les caches avec des binaires ou des métadonnées. |
| DisableParallelProcessing | Désactive la restauration de plusieurs packages en parallèle. |
| FallbackSource | *(3.2 +)* Liste de sources de packages à utiliser comme secours si le package est introuvable dans la source principale ou par défaut. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| MSBuildPath | *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild. |
| NoCache | Empêche NuGet d’utiliser les packages mis en cache. Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| OutputDirectory | Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé. Obligatoire lors de la restauration `packages.config` avec un `PackagesDirectory` fichier `SolutionDirectory` , sauf si ou est utilisé.|
| PackageSaveMode | Spécifie les types de fichiers à enregistrer après l’installation du package `nuspec`: `nupkg`l’un `nuspec;nupkg`des éléments, ou. |
| PackagesDirectory | Comme pour `OutputDirectory`. Obligatoire lors de la restauration `packages.config` avec un `OutputDirectory` fichier `SolutionDirectory` , sauf si ou est utilisé. |
| Project2ProjectTimeOut | Délai d’expiration en secondes pour la résolution des références entre projets. |
| Récursive | *(4.0 +)* Restaure tous les projets de référence pour les projets UWP et .NET Core. Ne s’applique pas aux projets `packages.config`qui utilisent. |
| RequireConsent | Vérifie que la restauration des packages est activée avant de télécharger et d’installer les packages. Pour plus d’informations, consultez [restauration de packages](../../consume-packages/package-restore.md). |
| SolutionDirectory | Spécifie le dossier de la solution. Non valide lors de la restauration de packages pour une solution. Obligatoire lors de la restauration `packages.config` avec un `PackagesDirectory` fichier `OutputDirectory` , sauf si ou est utilisé. |
| source | Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour la restauration. En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configuration du comportement de NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="remarks"></a>Notes

La commande Restore effectue les étapes suivantes:

1. Déterminez le mode d’opération de la commande Restore.

   | type de fichier projectPath | Comportement |
   | --- | --- |
   | Solution (dossier) | NuGet recherche un `.sln` fichier et l’utilise s’il est trouvé; sinon, génère une erreur. `(SolutionDir)\.nuget`est utilisé comme dossier de démarrage. |
   | `.sln`txt | Restaurez les packages identifiés par la solution; génère une erreur si `-SolutionDirectory` est utilisé. `$(SolutionDir)\.nuget`est utilisé comme dossier de démarrage. |
   | `packages.config`fichier projet ou | Restaurez les packages listés dans le fichier, en résolvant et en installant les dépendances. |
   | Autre type de fichier | Le fichier est supposé être un `.sln` fichier comme indiqué ci-dessus; s’il ne s’agit pas d’une solution, NuGet génère une erreur. |
   | (projectPath non spécifié) | <ul><li>NuGet recherche les fichiers solution dans le dossier actif. Si un seul fichier est trouvé, il est utilisé pour restaurer les packages. Si plusieurs solutions sont trouvées, NuGet génère une erreur.</li><li>S’il n’existe aucun fichier solution, NuGet recherche un `packages.config` et l’utilise pour restaurer des packages.</li><li>Si aucune solution ou `packages.config` aucun fichier n’est trouvé, NuGet génère une erreur.</ul> |

2. Déterminer le dossier Packages en utilisant l’ordre de priorité suivant (NuGet génère une erreur si aucun de ces dossiers n’est trouvé):

    - Dossier spécifié avec `-PackagesDirectory`.
    - La `repositoryPath` valeur dans`Nuget.Config`
    - Le dossier spécifié avec`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Lors de la restauration de packages pour une solution, NuGet effectue les opérations suivantes:
    - Charge le fichier solution.
    - Restaure les packages de niveau solution listés `$(SolutionDir)\.nuget\packages.config` dans `packages` dans le dossier.
    - Restaurez les packages `$(ProjectDir)\packages.config` listés `packages` dans dans le dossier. Pour chaque package spécifié, restaurez le package en parallèle `-DisableParallelProcessing` , sauf si est spécifié.

## <a name="examples"></a>Exemples

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
