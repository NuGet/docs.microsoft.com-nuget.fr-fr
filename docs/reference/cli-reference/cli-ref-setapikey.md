---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231225"
---
# <a name="setapikey-command-nuget-cli"></a>commande setapikey (interface CLI NuGet)

**S’applique à : consommation de** packages, publication &bullet; **versions prises en charge :** tout

Enregistre une clé API pour une URL de serveur donnée dans `NuGet.Config` afin qu’il n’ait pas besoin d’être entré pour les commandes suivantes.

## <a name="usage"></a>Usage

```cli
nuget setapikey <key> -Source <url> [options]
```

où `<source>` identifie le serveur et `<key>` est la clé à enregistrer. Si `<source>` est omis, nuget.org est utilisé par défaut. 

> [!NOTE]
> La clé API n’est pas utilisée pour l’authentification auprès du flux privé. Reportez-vous à [`nuget sources` commande](../cli-reference/cli-ref-sources.md) pour gérer les informations d’identification pour l’authentification auprès de la source.
> Les clés API peuvent être obtenues à partir des serveurs NuGet individuels. Pour créer et gérer des APIKeys pour nuget.org, reportez-vous à la rubrique [Publish-API-Key](../../quickstart/includes/publish-api-key.md)

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force l’exécution de NuGet. exe à l’aide d’une culture indifférente basée sur l’anglais. |
| Aide | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie : *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
