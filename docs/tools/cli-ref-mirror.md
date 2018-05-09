---
title: Commande de mise en miroir de NuGet CLI
description: Référence de la commande de mise en miroir de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5ba13196d385abf42a5af2faa3fe6f0e80fb59d8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="mirror-command-nuget-cli"></a>commande de mise en miroir (NuGet CLI)

**S’applique à :** la publication du package &bullet; **versions prises en charge :** déconseillée dans 3.2 +

Reflète un package et ses dépendances à partir des référentiels source spécifiée dans le référentiel cible.

> [!NOTE]
> Pour activer cette commande pour les versions de NuGet avant 3.2, accédez à [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), sélectionnez la dernière version stable, téléchargez `NuGet.ServerExtensions.dll` et `Nuget-Signed.exe` à votre disque local et le changement de nom `Nuget-Signed.exe` à `nuget.exe`.

## <a name="usage"></a>Utilisation

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

où `<packageID>` est le package pour mettre en miroir, ou `<configFilePath>` identifie les `packages.config` fichier qui répertorie les packages à mettre en miroir.

Le `<listUrlTarget>` Spécifie le référentiel de code source, et `<publishUrlTarget>` Spécifie le référentiel cible.

Si votre référentiel cible se trouve sur `https://machine/repo` qui est en cours d’exécution [NuGet.Server](../hosting-packages/nuget-server.md), les URL de liste et push sera `https://machine/repo/nuget` et `https://machine/repo/api/v2/package`, respectivement.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| apiKey | La clé d’API pour le référentiel cible. Si absent, l’élément spécifié dans le fichier de configuration est utilisé (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Help | Affiche l’aide de la commande. |
| NoCache | NuGet empêche l’utilisation de packages de mise en cache. Consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Journaux seront effectuées, mais n’effectue pas les actions. suppose la réussite des opérations de push. |
| Version préliminaire | Inclut les versions préliminaires des packages dans l’opération de mise en miroir. |
| Source | Liste des sources de package pour mettre en miroir. Si aucune source n’est spécifiées, ceux définis dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisés, nuget.org par défaut si aucune n’est spécifiée. |
| Délai d'expiration | Spécifie le délai d’attente, en secondes, en exécutant un push sur un serveur. La valeur par défaut est 300 secondes (5 minutes). |
| Version | La version du package à installer. Si non spécifié, la version la plus récente est mise en miroir. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
