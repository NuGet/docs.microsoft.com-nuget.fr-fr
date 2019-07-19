---
title: Commande de sources de l’interface CLI NuGet
description: Référence pour la commande de sources NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327596"
---
# <a name="sources-command-nuget-cli"></a>sources (commande, NuGet CLI)

**S’applique à: consommation de** packages &bullet; , publication des **versions prises en charge:** toutes

Gère la liste des sources situées dans le fichier de configuration de l’étendue de l’utilisateur ou dans un fichier de configuration spécifié. Le fichier de configuration de l’étendue de `%appdata%\NuGet\NuGet.Config` l’utilisateur se trouve `~/.nuget/NuGet/NuGet.Config` à l’emplacement (Windows) et (Mac/Linux).

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Usage

```cli
nuget sources <operation> -Name <name> -Source <source>
```

où `<operation>` est l’une des *listes, ajouter, supprimer, activer, désactiver* ou *mettre à jour*, `<name>` est le nom de la source `<source>` et est l’URL de la source. Vous ne pouvez utiliser qu’une seule source à la fois.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Format | S’applique à `list` l’action et peut `Detailed` avoir la valeur (valeur `Short`par défaut) ou. |
| Aide | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Mot de passe | Spécifie le mot de passe pour l’authentification auprès de la source. |
| StorePasswordInClearText | Indique de stocker le mot de passe dans du texte non chiffré au lieu du comportement par défaut du stockage d’un formulaire chiffré. |
| UserName | Spécifie le nom d’utilisateur pour l’authentification auprès de la source. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

> [!Note]
> Veillez à ajouter le mot de passe de la source dans le même contexte utilisateur, car NuGet. exe sera utilisé ultérieurement pour accéder à la source du package. Le mot de passe est stocké de manière chiffrée dans le fichier de configuration et ne peut être déchiffré que dans le même contexte utilisateur que celui dans lequel il a été chiffré. Par exemple, lorsque vous utilisez un serveur de builds pour restaurer des packages NuGet, le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel la tâche de serveur de builds s’exécutera.

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
