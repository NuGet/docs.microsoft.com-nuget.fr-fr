---
title: Commande de restauration NuGet CLI
description: Informations de référence pour la commande restore de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4df7685883fea78428c6744bdbf4c66d83e469bc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817916"
---
# <a name="restore-command-nuget-cli"></a>commande de restauration (NuGet CLI)

**S’applique à :** package consommation &bullet; **versions prises en charge :** 2.7 +

Télécharge et installe tous les packages manquants à partir de la `packages` dossier. Lorsqu’il est utilisé avec NuGet 4.0 + et le format PackageReference, génère un `<project>.nuget.props` de fichiers, si nécessaire, dans le `obj` dossier. (Le fichier peut être omis à partir du contrôle de code source.)

Sur Mac OSX et Linux avec l’interface CLI sur Mono, la restauration des packages n’est pas pris en charge avec PackageReference.

## <a name="usage"></a>Utilisation

```cli
nuget restore <projectPath> [options]
```

où `<projectPath>` Spécifie l’emplacement d’une solution ou un `packages.config` fichier. Consultez [notes](#remarks) ci-dessous pour plus d’informations de comportement.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| DirectDownload | *(4.0 +)*  Télécharge les packages directement sans l’alimenter les caches avec des fichiers binaires ou des métadonnées. |
| DisableParallelProcessing | Désactive la restauration de plusieurs lots en parallèle. |
| FallbackSource | *(3.2 +)*  Une liste des sources de package à utiliser comme secours au cas où le package n’est pas trouvé dans le serveur principal ou source par défaut. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| MSBuildPath | *(4.0 +)*  Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Spécifie la version de MSBuild à utiliser avec cette commande. Valeurs prises en charge sont 4, 12, 14, 15. Par défaut que le MSBuild dans votre chemin d’accès est sélectionné, sinon la valeur par défaut pour la version installée la plus élevée de MSBuild. |
| NoCache | NuGet empêche l’utilisation de packages de mise en cache. Consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Supprime les invites de saisie utilisateur ou les confirmations. |
| OutputDirectory | Spécifie le dossier dans lequel les packages sont installés. Si aucun dossier n’est spécifié, le dossier actif est utilisé. Requis lors de la restauration avec un `packages.config` de fichiers, sauf si `PackagesDirectory` ou `SolutionDirectory` est utilisé.|
| PackageSaveMode | Spécifie les types de fichiers à enregistrer après l’installation du package : un des `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| PackagesDirectory | Comme pour `OutputDirectory`. Requis lors de la restauration avec un `packages.config` de fichiers, sauf si `OutputDirectory` ou `SolutionDirectory` est utilisé. |
| Project2ProjectTimeOut | Délai d’expiration en secondes pour la résolution des références entre projets. |
| Récursive | *(4.0 +)*  Restaure toutes les références de projets pour les projets UWP et .NET Core. Ne s’applique pas aux projets à l’aide de `packages.config`. |
| RequireConsent | Vérifie que la restauration des packages est activé avant de télécharger et installer les packages. Pour plus d’informations, consultez [restauration des packages](../consume-packages/package-restore.md). |
| SolutionDirectory | Spécifie le dossier de solution. Non valide lors de la restauration des packages pour une solution. Requis lors de la restauration avec un `packages.config` de fichiers, sauf si `PackagesDirectory` ou `OutputDirectory` est utilisé. |
| Source | Spécifie la liste des sources de package (en tant qu’URL) à utiliser pour la restauration. Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [NuGet de configuration de comportement](../consume-packages/configuring-nuget-behavior.md). |
| Commentaires |> Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="remarks"></a>Notes

La commande restore effectue les étapes suivantes :

1. Déterminer le mode de fonctionnement de la commande restore.

   | type de fichier projectPath | Comportement |
   | --- | --- |
   | Solution (dossier) | NuGet cherche un `.sln` fichier et utilise ce si elle est trouvée ; sinon, renvoie une erreur. `(SolutionDir)\.nuget` est utilisé en tant que le dossier de démarrage. |
   | `.sln` Fichier | Restaurer les packages identifiés par la solution ; génère une erreur si `-SolutionDirectory` est utilisé. `$(SolutionDir)\.nuget` est utilisé en tant que le dossier de démarrage. |
   | `packages.config` ou le fichier projet | Restaurer les packages répertoriés dans le fichier, la résolution et l’installation de dépendances. |
   | Autre type de fichier | Fichier est censé pour être un `.sln` fichier comme indiqué ci-dessus ; s’il n’est pas une solution, donne NuGet une erreur. |
   | (projectPath non spécifié) | <ul><li>NuGet recherche les fichiers de solution dans le dossier actif. Si un fichier unique est trouvé, qui est utilisée pour restaurer les packages ; Si plusieurs solutions sont détectées, NuGet génère une erreur.</li><li>S’il n’y a aucun fichier de solution, NuGet cherche un `packages.config` et l’utilise pour restaurer les packages.</li><li>Si aucune solution ou `packages.config` fichier est trouvé, NuGet génère une erreur.</ul> |

2. Déterminer le dossier de packages à l’aide de l’ordre de priorité suivant (NuGet génère une erreur si aucun de ces dossiers se trouvent) :

    - Le dossier spécifié avec `-PackagesDirectory`.
    - La `repositoryPath` valeur dans `Nuget.Config`
    - Le dossier spécifié avec `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Lors de la restauration des packages pour une solution, NuGet effectue les opérations suivantes :
    - Charge le fichier de solution.
    - Restaure les packages de solution au niveau répertoriés dans `$(SolutionDir)\.nuget\packages.config` dans le `packages` dossier.
    - Restauration des packages répertoriés dans `$(ProjectDir)\packages.config` dans le `packages` dossier. Pour chaque package spécifié, restaurer le package en parallèle, sauf si `-DisableParallelProcessing` est spécifié.

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
