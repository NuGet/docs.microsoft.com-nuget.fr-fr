---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622809"
---
# <a name="setapikey-command-nuget-cli"></a>commande setapikey (interface CLI NuGet)

**S’applique à : consommation de** packages, publication &bullet; des **versions prises en charge :** toutes

Enregistre une clé API pour une URL de serveur donnée dans `NuGet.Config` afin qu’elle n’ait pas besoin d’être entrée pour les commandes suivantes.

## <a name="usage"></a>Usage

```cli
nuget setapikey <key> -Source <url> [options]
```

où `<source>` identifie le serveur et `<key>` est la clé à enregistrer. Si `<source>` est omis, NuGet.org est utilisé par défaut. 

> [!NOTE]
> La clé API n’est pas utilisée pour l’authentification auprès du flux privé. Reportez-vous à la [ `nuget sources` commande](../cli-reference/cli-ref-sources.md) pour gérer les informations d’identification pour l’authentification auprès de la source.
> Les clés API peuvent être obtenues à partir des serveurs NuGet individuels. Pour créer et gérer des APIKeys pour nuget.org, consultez la rubrique [acquisition d’une clé API](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-src|-Source`**

  URL du serveur où la clé d’API est valide.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
