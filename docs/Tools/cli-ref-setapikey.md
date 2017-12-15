---
title: Commande setapikey de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Référence de la commande setapikey de nuget.exe"
keywords: "référence setapikey de NuGet, setapikey commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>commande de setapikey (NuGet CLI)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Enregistre une clé d’API pour une URL de serveur donnée en `NuGet.Config` afin qu’il n’a pas besoin d’être entrés pour les commandes suivantes.

## <a name="usage"></a>Utilisation

```
nuget setapikey <key> -Source <url> [options]
```

où `<source>` identifie le serveur et `<key>` est la clé ou le mot de passe à enregistrer. Si `<source>` est omis, nuget.org est supposé.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet le fichier de configuration à modifier. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
