---
title: NuGet CLI sources commande | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Commande des sources de référence pour le nuget.exe"
keywords: "NuGet sources de référence, des sources de commande"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a>commande de sources (NuGet CLI)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Gère la liste des sources de `%AppData%\NuGet\NuGet.Config` ou le fichier de configuration spécifié.

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Utilisation

```cli
nuget sources <operation> -Name <name> -Source <source>
```

où `<operation>` est un des *liste, ajouter, supprimer, activer, désactiver,* ou *mise à jour*, `<name>` est le nom de la source, et `<source>` est l’URL de la source.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Format | S’applique à la `list` action et peut être `Detailed` (la valeur par défaut) ou `Short`. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Mot de passe | Spécifie le mot de passe pour s’authentifier auprès de la source. |
| StorePasswordInClearText | Indique que le mot de passe en texte non chiffré au lieu du comportement par défaut de stockage sous forme chiffrée. |
| UserName | Spécifie le nom d’utilisateur pour l’authentification avec la source. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

> [!Note]
> Assurez-vous d’ajouter un mot de passe des sources dans le même contexte utilisateur comme le nuget.exe sera ensuite utilisé pour accéder à la source du package. Le mot de passe est stockée chiffrées dans le fichier de configuration et peut être déchiffrée uniquement dans le même contexte utilisateur car il a été chiffré. Par exemple lorsque vous utilisez un serveur de builds pour restaurer les packages NuGet que le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel s’exécute la tâche de serveur de build.

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
