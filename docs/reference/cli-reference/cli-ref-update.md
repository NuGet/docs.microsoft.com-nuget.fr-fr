---
title: Commande de mise à jour de l’interface CLI NuGet
description: Référence pour la commande de mise à jour de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327506"
---
# <a name="update-command-nuget-cli"></a>update (commande, NuGet CLI)

**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: toutes

Mettez à jour tous les packages dans un projet (en utilisant `packages.config`) avec leurs dernières versions disponibles. Il est recommandé d’exécuter [«Restore»](cli-ref-restore.md) avant d' `update`exécuter le. (Pour mettre à jour un package individuel [`nuget install`](cli-ref-install.md) , utilisez sans spécifier de numéro de version, auquel cas NuGet installe la version la plus récente.)

Remarque: `update` ne fonctionne pas avec l’interface CLI s’exécutant sous mono (Mac OSX ou Linux) ou lors de l’utilisation du format PackageReference.

La `update` commande met également à jour les références d’assembly dans le fichier projet, à condition que ces références existent déjà. Si un package mis à jour a un assembly ajouté, une nouvelle référence n’est *pas* ajoutée. Les références d’assembly des nouvelles dépendances de package ne sont pas non plus ajoutées. Pour inclure ces opérations dans le cadre d’une mise à jour, mettez à jour le package dans Visual Studio à l’aide de l’interface utilisateur du gestionnaire de package ou de la console du gestionnaire de package.

Cette commande peut également être utilisée pour mettre à jour NuGet. exe lui-même à l’aide de l’indicateur *-Self* .

## <a name="usage"></a>Usage

```cli
nuget update <configPath> [options]
```

où `<configPath>` identifie un `packages.config` fichier solution ou qui répertorie les dépendances du projet.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| FileConflictAction | Spécifie l’action à entreprendre lorsque le système vous demande de remplacer ou d’ignorer les fichiers existants référencés par le projet. Les valeurs sont *overwrite, ignore, None*. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| Id | Spécifie une liste d’ID de package à mettre à jour. |
| MSBuildPath | *(4.0 +)* Spécifie le chemin d’accès de MSBuild à utiliser avec la commande prioritaire `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Spécifie la version de MSBuild à utiliser avec cette commande. Les valeurs prises en charge sont 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Par défaut, MSBuild dans votre chemin d’accès est choisi, sinon il s’agit par défaut de la version installée la plus récente de MSBuild. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Version préliminaire | Autorise la mise à jour vers les versions préliminaires. Cet indicateur n’est pas nécessaire lors de la mise à jour des packages de version préliminaire déjà installés. |
| RepositoryPath | Spécifie le dossier local dans lequel les packages sont installés. |
| Safe | Spécifie que seules les mises à jour dont la version la plus récente est disponible dans la même version principale et la version mineure que le package installé seront installées. |
| Rythme | Met à jour NuGet. exe vers la dernière version; tous les autres arguments sont ignorés. |
| source | Spécifie la liste des sources de packages (sous forme d’URL) à utiliser pour les mises à jour. En cas d’omission, la commande utilise les sources fournies dans les fichiers de configuration, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md). |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |
| Version | Lorsqu’il est utilisé avec un ID de package, spécifie la version du package à mettre à jour. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
