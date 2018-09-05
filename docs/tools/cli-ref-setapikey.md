---
title: Commande setapikey de NuGet CLI
description: Référence de la commande setapikey de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549218"
---
# <a name="setapikey-command-nuget-cli"></a>commande setapikey (CLI NuGet)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Enregistre une clé API pour une URL de serveur donnée en `NuGet.Config` afin qu’il n’a pas besoin être entrés pour les commandes suivantes.

## <a name="usage"></a>Utilisation

```cli
nuget setapikey <key> -Source <url> [options]
```

où `<source>` identifie le serveur et `<key>` est la clé ou le mot de passe à enregistrer. Si `<source>` est omis, nuget.org est pris en compte.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
