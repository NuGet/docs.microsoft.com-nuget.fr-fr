---
title: Commande Mirror CLI NuGet
description: Référence pour la commande nuget.exe Mirror
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779171"
---
# <a name="mirror-command-nuget-cli"></a>commande Mirror (interface CLI NuGet)

**S’applique à :** publication de packages &bullet; **versions prises en charge :** déconseillé dans 3.2 +

Met en miroir un package et ses dépendances à partir des dépôts source spécifiés vers le référentiel cible.

> [!NOTE]
> NuGet.ServerExtensions.dll et NuGet-Signed.exe qui prenait déjà en charge cette commande dans NuGet 2. x (en renommant NuGet-Signed.exe en nuget.exe) ne sont plus disponibles au téléchargement. Pour utiliser une commande similaire à celle-ci, essayez [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Utilisation

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

où `<packageID>` est le package à mettre en miroir, ou `<configFilePath>` identifie le `packages.config` fichier qui répertorie les packages à mettre en miroir.

`<listUrlTarget>`Spécifie le référentiel source et `<publishUrlTarget>` spécifie le référentiel cible.

Si votre dépôt cible se trouve sur `https://machine/repo` qui exécute [NuGet. Server](../../hosting-packages/nuget-server.md), la liste et les URL de transmission sont `https://machine/repo/nuget` et `https://machine/repo/api/v2/package` , respectivement.

## <a name="options"></a>Options

- **`-ApiKey`**

  Clé API pour le référentiel cible. S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé ( `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Affiche des informations d’aide pour la commande.

- **`-NoCache`**

  Empêche NuGet d’utiliser les packages mis en cache. Consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Journalise ce qui serait fait, mais n’effectue pas les actions. suppose la réussite des opérations push.

- **`-PreRelease`**

  Comprend des packages de version préliminaire dans l’opération de mise en miroir.

- **`-Source`**

  Liste des sources de package à mettre en miroir. Si aucune source n’est spécifiée, celles définies dans le fichier de configuration (voir ApiKey ci-dessus) sont utilisées, par défaut nuget.org si aucune n’est spécifiée.

- **`-Timeout`**

  Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur. La valeur par défaut est de 300 secondes (5 minutes).

- **`-Version`**

  Version du package à installer. S’il n’est pas spécifié, la version la plus récente est mise en miroir.

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
