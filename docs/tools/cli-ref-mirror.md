---
title: Commande de mise en miroir de CLI de NuGet
description: Référence de la commande de mise en miroir de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550204"
---
# <a name="mirror-command-nuget-cli"></a>mirror (commande, NuGet CLI)

**S’applique à :** publication du package &bullet; **versions prises en charge :** déconseillées dans 3.2 +

Reflète un package et ses dépendances à partir des référentiels source spécifiée dans le référentiel cible.

> [!NOTE]
> Pour activer cette commande pour les versions de NuGet avant 3.2, accédez à [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), sélectionnez la version stable la plus récente, téléchargez `NuGet.ServerExtensions.dll` et `Nuget-Signed.exe` vers votre disque local et le changement de nom `Nuget-Signed.exe` à `nuget.exe`.

## <a name="usage"></a>Utilisation

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

où `<packageID>` est le package pour mettre en miroir, ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à mettre en miroir.

Le `<listUrlTarget>` Spécifie le référentiel source, et `<publishUrlTarget>` Spécifie le référentiel cible.

Si votre référentiel cible se trouve sur `https://machine/repo` qui est en cours d’exécution [NuGet.Server](../hosting-packages/nuget-server.md), les URL de la liste et push sera `https://machine/repo/nuget` et `https://machine/repo/api/v2/package`, respectivement.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ApiKey | La clé API pour le référentiel cible. Si absent, celle spécifiée dans le fichier de configuration est utilisée (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Help | Affiche l’aide de la commande. |
| NoCache | Empêche NuGet d’utiliser les packages mis en cache. Consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Enregistre ce qui aurait fait, mais n’effectue pas les actions ; part du principe de réussite pour les opérations de push. |
| Version préliminaire | Inclut les packages de version préliminaire dans l’opération de mise en miroir. |
| Source | Une liste des sources de package pour mettre en miroir. Si aucune source n’est spécifiées, ceux définis dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisés à la valeur par défaut : nuget.org si aucun n’est spécifié. |
| Délai d'expiration | Spécifie le délai d’attente, en secondes, pour envoyer vers un serveur. La valeur par défaut est 300 secondes (5 minutes). |
| Version | La version du package à installer. Si non spécifié, la version la plus récente est mise en miroir. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
