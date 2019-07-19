---
title: Commande setapikey de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327606"
---
# <a name="setapikey-command-nuget-cli"></a>commande setapikey (interface CLI NuGet)

**S’applique à: consommation de** packages &bullet; , publication des **versions prises en charge:** toutes

Enregistre une clé API pour une URL de serveur donnée `NuGet.Config` dans afin qu’elle n’ait pas besoin d’être entrée pour les commandes suivantes.

## <a name="usage"></a>Usage

```cli
nuget setapikey <key> -Source <url> [options]
```

où `<source>` identifie le serveur et `<key>` représente la clé ou le mot de passe à enregistrer. Si `<source>` est omis, NuGet.org est utilisé par défaut.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
