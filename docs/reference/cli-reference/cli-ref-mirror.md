---
title: Commande Mirror CLI NuGet
description: Référence pour la commande NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327666"
---
# <a name="mirror-command-nuget-cli"></a>mirror (commande, NuGet CLI)

**S’applique à:** publication &bullet; de packages **versions prises en charge:** déconseillé dans 3.2 +

Met en miroir un package et ses dépendances à partir des dépôts source spécifiés vers le référentiel cible.

> [!NOTE]
> Pour activer cette commande pour les versions de NuGet antérieures à 3,2 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), accédez à, sélectionnez la version stable `NuGet.ServerExtensions.dll` la `Nuget-Signed.exe` plus récente, téléchargez et `nuget.exe` sur votre `Nuget-Signed.exe` disque local et renommez-la.

## <a name="usage"></a>Usage

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

où `<packageID>` est le package à mettre en miroir `<configFilePath>` , ou `packages.config` identifie le fichier qui répertorie les packages à mettre en miroir.

Spécifie le référentiel source et `<publishUrlTarget>` spécifie le référentiel cible. `<listUrlTarget>`

Si votre dépôt cible `https://machine/repo` se trouve sur qui exécute [NuGet. Server](../../hosting-packages/nuget-server.md), la liste et les URL de `https://machine/repo/nuget` transmission sont et `https://machine/repo/api/v2/package`, respectivement.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ApiKey | Clé API pour le référentiel cible. S’il n’est pas présent, celui spécifié dans le fichier de configuration`%AppData%\NuGet\NuGet.Config` est utilisé (( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux)). |
| Aide | Affiche des informations d’aide pour la commande. |
| NoCache | Empêche NuGet d’utiliser les packages mis en cache. Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Journalise ce qui serait fait, mais n’effectue pas les actions. suppose la réussite des opérations push. |
| Version préliminaire | Comprend des packages de version préliminaire dans l’opération de mise en miroir. |
| source | Liste des sources de package à mettre en miroir. Si aucune source n’est spécifiée, celles définies dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisées, par défaut nuget.org si aucune n’est spécifiée. |
| Délai | Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur. La valeur par défaut est 300 secondes (5 minutes). |
| Version | Version du package à installer. S’il n’est pas spécifié, la version la plus récente est mise en miroir. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
