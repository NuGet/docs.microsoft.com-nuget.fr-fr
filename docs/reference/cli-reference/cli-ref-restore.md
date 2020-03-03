---
title: Commande de restauration de l’interface CLI NuGet
description: Référence pour la commande de restauration de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d1768a741e3f1c48e94d854fa7d365ebfa3513ea
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231147"
---
# <a name="restore-command-nuget-cli"></a>Restore, commande (interface CLI NuGet)

**S’applique à :** la consommation des packages &bullet; **versions prises en charge :** 2.7 +

Télécharge et installe tous les packages manquants dans le dossier `packages`. Lorsqu’il est utilisé avec NuGet 4.0 + et le format PackageReference, génère un fichier `<project>.nuget.props`, si nécessaire, dans le dossier `obj`. (Le fichier peut être omis dans le contrôle de code source.)

Sur Mac OSX et Linux avec l’interface CLI sur mono, la restauration des packages n’est pas prise en charge avec PackageReference.

## <a name="usage"></a>Usage

```cli
nuget restore <projectPath> [options]
```

où `<projectPath>` spécifie l’emplacement d’une solution ou d’un fichier `packages.config`. Consultez les [Remarques](#remarks) ci-dessous pour obtenir des détails sur le comportement.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| DirectDownload | *(4.0 +)* Télécharge les packages directement sans remplir les caches avec des binaires ou des métadonnées. |
| DisableParallelProcessing | Désactive la restauration de plusieurs packages en parallèle. |
| FallbackSource | *(3.2 +)* Liste de sources de packages à utiliser comme secours si le package est introuvable dans la source principale ou par défaut. Utilisez un point-virgule pour séparer les entrées de liste. |
| Force | Dans les projets basés sur PackageReference, force la résolution de toutes les dépendances même si la dernière restauration a réussi. La spécification de cet indicateur est semblable à la suppression du fichier `project.assets.json`. Cela ne contourne pas le cache http. |
| ForceEnglishOutput | *(3.5 +)* Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais. |
| ForceEvaluate | Force la restauration à réévaluer toutes les dépendances même si un fichier de verrouillage existe déjà. |
| Aide | Affiche des informations d’aide pour la commande. |
| LockFilePath | Emplacement de sortie où le fichier de verrouillage de projet est écrit. Par défaut, il s’agit de « PROJECT_ROOT \Packages.Lock.JSON ». |
| LockedMode | N’autorise pas la mise à jour du fichier de verrouillage de projet. |
| MSBuildPath | *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande, prioritaire sur `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild. |
| NoCache | Empêche NuGet d’utiliser les packages mis en cache. Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| OutputDirectory | Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé. Obligatoire lors de la restauration avec un fichier `packages.config`, sauf si `PackagesDirectory` ou `SolutionDirectory` est utilisé.|
| PackageSaveMode | Spécifie les types de fichiers à enregistrer après l’installation du package : l’un des `nuspec`, `nupkg`ou `nuspec;nupkg`. |
| PackagesDirectory | Identique à `OutputDirectory`. Obligatoire lors de la restauration avec un fichier `packages.config`, sauf si `OutputDirectory` ou `SolutionDirectory` est utilisé. |
| Project2ProjectTimeOut | Délai d’expiration en secondes pour la résolution des références entre projets. |
| Récursive | *(4.0 +)* Restaure tous les projets de référence pour les projets UWP et .NET Core. Ne s’applique pas aux projets qui utilisent `packages.config`. |
| RequireConsent | Vérifie que la restauration des packages est activée avant de télécharger et d’installer les packages. Pour plus d’informations, consultez [restauration de packages](../../consume-packages/package-restore.md). |
| SolutionDirectory | Spécifie le dossier de la solution. Non valide lors de la restauration de packages pour une solution. Obligatoire lors de la restauration avec un fichier `packages.config`, sauf si `PackagesDirectory` ou `OutputDirectory` est utilisé. |
| Source | Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour la restauration. En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configuration du comportement de NuGet](../../consume-packages/configuring-nuget-behavior.md). Utilisez un point-virgule pour séparer les entrées de liste. |
| UseLockFile | Active la génération et l’utilisation du fichier de verrouillage de projet avec Restore. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="remarks"></a>Notes 

La commande Restore effectue les étapes suivantes :

1. Déterminez le mode d’opération de la commande Restore.

   | type de fichier projectPath | Comportement |
   | --- | --- |
   | Solution (dossier) | NuGet recherche un fichier `.sln` et l’utilise s’il est trouvé ; Sinon, génère une erreur. `(SolutionDir)\.nuget` est utilisé comme dossier de démarrage. |
   | fichier `.sln` | Restaurez les packages identifiés par la solution ; génère une erreur si `-SolutionDirectory` est utilisé. `$(SolutionDir)\.nuget` est utilisé comme dossier de démarrage. |
   | fichier `packages.config` ou projet | Restaurez les packages listés dans le fichier, en résolvant et en installant les dépendances. |
   | Autre type de fichier | Le fichier est supposé être un fichier `.sln` comme indiqué ci-dessus ; s’il ne s’agit pas d’une solution, NuGet génère une erreur. |
   | (projectPath non spécifié) | <ul><li>NuGet recherche les fichiers solution dans le dossier actif. Si un seul fichier est trouvé, il est utilisé pour restaurer les packages. Si plusieurs solutions sont trouvées, NuGet génère une erreur.</li><li>S’il n’existe aucun fichier solution, NuGet recherche une `packages.config` et l’utilise pour restaurer des packages.</li><li>Si aucun fichier solution ou `packages.config` n’est trouvé, NuGet génère une erreur.</ul> |

2. Déterminer le dossier Packages en utilisant l’ordre de priorité suivant (NuGet génère une erreur si aucun de ces dossiers n’est trouvé) :

    - Dossier spécifié avec `-PackagesDirectory`.
    - Valeur `repositoryPath` dans `Nuget.Config`
    - Dossier spécifié avec `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Lors de la restauration de packages pour une solution, NuGet effectue les opérations suivantes :
    - Charge le fichier solution.
    - Restaure les packages de niveau solution figurant dans `$(SolutionDir)\.nuget\packages.config` dans le dossier `packages`.
    - Restaurez les packages listés dans `$(ProjectDir)\packages.config` dans le dossier `packages`. Pour chaque package spécifié, restaurez le package en parallèle, sauf si `-DisableParallelProcessing` est spécifié.

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
