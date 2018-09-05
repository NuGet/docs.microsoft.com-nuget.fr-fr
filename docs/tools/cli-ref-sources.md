---
title: NuGet CLI sources de commande
description: Référence pour nuget.exe sources de commande
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548106"
---
# <a name="sources-command-nuget-cli"></a>sources (commande, NuGet CLI)

**S’applique à :** consommation de package, publication &bullet; **versions prises en charge :** toutes les

Gère la liste des sources situées dans le fichier de configuration d’étendue utilisateur ou un fichier de configuration spécifié. Le fichier de configuration d’étendue utilisateur se trouve à `%appdata%\NuGet\NuGet.Config` (Windows) et `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Utilisation

```cli
nuget sources <operation> -Name <name> -Source <source>
```

où `<operation>` est un des *liste, ajouter, supprimer, activer, désactiver,* ou *mise à jour*, `<name>` est le nom de la source, et `<source>` est l’URL de la source.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Format | S’applique à la `list` action et peut être `Detailed` (la valeur par défaut) ou `Short`. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Mot de passe | Spécifie le mot de passe pour l’authentification auprès de la source. |
| StorePasswordInClearText | Indique que le mot de passe en texte non chiffré au lieu du comportement par défaut de stockage sous une forme chiffrée. |
| UserName | Spécifie le nom d’utilisateur pour l’authentification auprès de la source. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

> [!Note]
> Veillez à ajouter le mot de passe des sources dans le même contexte utilisateur comme nuget.exe est utilisée ultérieurement pour accéder à la source du package. Le mot de passe sera stocké chiffré dans le fichier de configuration et peut uniquement être déchiffré dans le même contexte utilisateur, car il a été chiffré. Ainsi, par exemple lorsque vous utilisez un serveur de builds pour restaurer les packages NuGet que le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel s’exécute la tâche de serveur de build.

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
