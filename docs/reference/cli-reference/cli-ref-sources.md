---
title: Commande de sources de l’interface CLI NuGet
description: Référence pour la commande nuget.exe sources
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780010"
---
# <a name="sources-command-nuget-cli"></a>commande sources (interface CLI NuGet)

**S’applique à : consommation de** packages, publication &bullet; des **versions prises en charge :** toutes

Gère la liste des sources situées dans le fichier de configuration de l’étendue de l’utilisateur ou dans un fichier de configuration spécifié. Le fichier de configuration de l’étendue de l’utilisateur se trouve à l’emplacement `%appdata%\NuGet\NuGet.Config` (Windows) et `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Notez que l’URL source pour nuget.org est `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Utilisation

```cli
nuget sources <operation> -Name <name> -Source <source>
```

où `<operation>` est l’une des *listes, ajouter, supprimer, activer, désactiver* ou *mettre à jour*, `<name>` est le nom de la source et `<source>` est l’URL de la source. Vous ne pouvez utiliser qu’une seule source à la fois.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-Format`**

  S’applique à l' `list` action et peut avoir `Detailed` la valeur (valeur par défaut) ou `Short` .

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-Name`**

  Nom de la source.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Password`**

  Spécifie le mot de passe pour l’authentification auprès de la source.

- **`-src|-Source`**

  Chemin d’accès à la source du ou des packages.

- **`-StorePasswordInClearText`**

  Indique de stocker le mot de passe dans du texte non chiffré au lieu du comportement par défaut du stockage d’un formulaire chiffré.

- **`-UserName`**

  Spécifie le nom d’utilisateur pour l’authentification auprès de la source.

- **`-ValidAuthenticationTypes`**

  Liste séparée par des virgules des types d’authentification valides pour cette source. Par défaut, tous les types d’authentification sont valides. Exemple : `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

> [!Note]
> Veillez à ajouter le mot de passe des sources dans le même contexte utilisateur, car le nuget.exe est utilisé ultérieurement pour accéder à la source du package. Le mot de passe est stocké de manière chiffrée dans le fichier de configuration et ne peut être déchiffré que dans le même contexte utilisateur que celui dans lequel il a été chiffré. Par exemple, lorsque vous utilisez un serveur de builds pour restaurer des packages NuGet, le mot de passe doit être chiffré avec le même utilisateur Windows sous lequel la tâche de serveur de builds s’exécutera.

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
