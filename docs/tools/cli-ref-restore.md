---
title: Commande de restauration NuGet CLI
description: Référence de la commande de restauration de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: adf97196f50f2a55d6b8ceed93d53ff12b67657b
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145629"
---
# <a name="restore-command-nuget-cli"></a>commande de restauration (CLI NuGet)

**S’applique à :** la consommation de package &bullet; **versions prises en charge :** 2.7+

Télécharge et installe tous les packages manquants à partir de la `packages` dossier. Lorsqu’il est utilisé avec NuGet 4.0 + et le format PackageReference, génère un `<project>.nuget.props` fichier, le cas échéant, dans le `obj` dossier. (Le fichier peut être omis à partir du contrôle de code source).

Sur Mac OSX et Linux avec l’interface CLI sur Mono, la restauration des packages n’est pas pris en charge avec PackageReference.

## <a name="usage"></a>Utilisation

```cli
nuget restore <projectPath> [options]
```

où `<projectPath>` Spécifie l’emplacement d’une solution ou un `packages.config` fichier. Consultez [notes](#remarks) ci-dessous pour plus d’informations de comportements.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| DirectDownload | *(4.0 +)*  Télécharge les packages directement sans le remplir les caches avec des fichiers binaires ou des métadonnées. |
| DisableParallelProcessing | Désactive la restauration de plusieurs packages en parallèle. |
| FallbackSource | *(3.2 +)*  Une liste des sources de package à utiliser comme solutions de secours dans le cas où le package n’est pas trouvé dans le réplica principal ou source par défaut. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| MSBuildPath | *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Valeurs prises en charge sont 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Par défaut que le MSBuild dans votre chemin d’accès est récupéré, sinon il est par défaut à la version installée la plus élevée de MSBuild. |
| NoCache | Empêche NuGet d’utiliser les packages mis en cache. Consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| OutputDirectory | Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé. Requis lors de la restauration avec un `packages.config` de fichiers, sauf si `PackagesDirectory` ou `SolutionDirectory` est utilisé.|
| PackageSaveMode | Spécifie les types de fichiers à enregistrer après l’installation de package : un des `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| PackagesDirectory | Comme pour `OutputDirectory`. Requis lors de la restauration avec un `packages.config` de fichiers, sauf si `OutputDirectory` ou `SolutionDirectory` est utilisé. |
| Project2ProjectTimeOut | Délai d’expiration en secondes pour la résolution des références entre projets. |
| Récursive | *(4.0 +)*  Restaure tous les projets de références pour les projets UWP et .NET Core. Ne s’applique pas aux projets utilisant `packages.config`. |
| RequireConsent | Vérifie que la restauration des packages est activé avant de télécharger et installer les packages. Pour plus d’informations, consultez [la restauration des packages](../consume-packages/package-restore.md). |
| SolutionDirectory | Spécifie le dossier de solution. Non valide lors de la restauration des packages pour une solution. Requis lors de la restauration avec un `packages.config` de fichiers, sauf si `PackagesDirectory` ou `OutputDirectory` est utilisé. |
| Source | Spécifie la liste des sources de package (en tant qu’URL) à utiliser pour la restauration. Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity |> Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="remarks"></a>Notes

La commande restore effectue les étapes suivantes :

1. Déterminer le mode de fonctionnement de la commande restore.

   | type de fichier projectPath | Comportement |
   | --- | --- |
   | Solution (dossier) | NuGet recherche un `.sln` fichier et utilise ce s’il existe ; sinon, génère une erreur. `(SolutionDir)\.nuget` est utilisé en tant que le dossier de démarrage. |
   | `.sln` Fichier | Restaurer les packages identifiés par la solution. génère une erreur si `-SolutionDirectory` est utilisé. `$(SolutionDir)\.nuget` est utilisé en tant que le dossier de démarrage. |
   | `packages.config` ou un fichier de projet | Restaurer les packages répertoriés dans le fichier, résolution et l’installation des dépendances. |
   | Autre type de fichier | Fichier est supposé pour être un `.sln` fichier comme indiqué ci-dessus ; si elle n’est pas une solution, donne NuGet une erreur. |
   | (projectPath sauf indication contraire) | <ul><li>NuGet recherche les fichiers de solution dans le dossier actif. Si un seul fichier est trouvé, que l’une est utilisée pour restaurer des packages ; Si plusieurs solutions sont détectées, NuGet génère une erreur.</li><li>S’il n’y a aucun fichier de solution, il le recherche un `packages.config` et l’utilise pour restaurer les packages.</li><li>Si aucune solution ou `packages.config` fichier est trouvé, NuGet génère une erreur.</ul> |

2. Déterminer le dossier de packages à l’aide de l’ordre de priorité suivant (NuGet génère une erreur si aucun de ces dossiers sont trouvés) :

    - Le dossier spécifié avec `-PackagesDirectory`.
    - La `repositoryPath` valeur dans `Nuget.Config`
    - Le dossier spécifié avec `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Lors de la restauration des packages pour une solution, NuGet effectue les opérations suivantes :
    - Charge le fichier de solution.
    - Restaure les packages de niveau solution répertoriés dans `$(SolutionDir)\.nuget\packages.config` dans le `packages` dossier.
    - Restaurer les packages répertoriés dans `$(ProjectDir)\packages.config` dans le `packages` dossier. Pour chaque package spécifié, restaurer le package en parallèle, sauf si `-DisableParallelProcessing` est spécifié.

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
