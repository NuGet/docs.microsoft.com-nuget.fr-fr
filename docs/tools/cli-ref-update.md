---
title: Commande de mise à jour de CLI de NuGet
description: Référence de la commande de mise à jour de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc34550b3669d83466318645987cfd3078bc3c18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545098"
---
# <a name="update-command-nuget-cli"></a>update (commande, NuGet CLI)

**S’applique à :** la consommation de package &bullet; **versions prises en charge :** toutes les

Met à jour tous les packages dans un projet (à l’aide de `packages.config`) avec leurs dernières versions disponibles. Il est recommandé d’exécuter ['restore'](cli-ref-restore.md) avant d’exécuter le `update`. (Pour mettre à jour un package individuel, utilisez [ `nuget install` ](cli-ref-install.md) sans spécifier un numéro de version, dans lequel cas NuGet installe la dernière version.)

Remarque : `update` ne fonctionne pas avec l’interface CLI en cours d’exécution sous Mono (Mac OSX ou Linux) ou lorsque vous utilisez le format PackageReference.

Le `update` commande met également à jour les références d’assembly dans le fichier projet, sous réserve ceux référence déjà existe. Si un package de mise à jour a un assembly ajouté, une nouvelle référence est *pas* ajouté. Nouvelles dépendances de package est également inutile leurs références d’assembly ajoutés. Pour inclure ces opérations dans le cadre d’une mise à jour, mettre à jour le package dans Visual Studio à l’aide de l’UI du Gestionnaire de Package ou la Console du Gestionnaire de Package.

Cette commande peut également être utilisée pour mettre à jour de nuget.exe lui-même à l’aide de la *-self* indicateur.

## <a name="usage"></a>Utilisation

```cli
nuget update <configPath> [options]
```

où `<configPath>` soit identifie un `packages.config` ou le fichier de solution qui répertorie les dépendances du projet.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| FileConflictAction | Spécifie l’action à entreprendre lorsque vous êtes invité à écraser ou ignorer les fichiers existants référencés par le projet. Les valeurs sont *remplacer, ignorer, aucun*. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Id | Spécifie une liste d’ID pour mettre à jour de package. |
| MSBuildPath | *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Valeurs prises en charge sont 4, 12, 14, 15. Par défaut que le MSBuild dans votre chemin d’accès est récupéré, sinon il est par défaut à la version installée la plus élevée de MSBuild. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Version préliminaire | Permet la mise à jour aux versions préliminaires. Cet indicateur n’est pas nécessaire lors de la mise à jour des packages de version préliminaire qui sont déjà installés. |
| RepositoryPath | Spécifie le dossier local dans lequel les packages sont installés. |
| Safe | Spécifie qui met à jour uniquement avec la version la plus récente disponible au sein de la même version majeure et mineure comme le package installé sera installé. |
| Self | Nuget.exe mises à jour vers la dernière version ; tous les autres arguments sont ignorés. |
| Source | Spécifie la liste des sources de package (en tant qu’URL) à utiliser pour les mises à jour. Si omis, la commande utilise les sources fournies dans les fichiers de configuration, consultez [du comportement de NuGet configuration](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |
| Version | Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
