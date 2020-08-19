---
title: Commande de configuration de l’interface CLI NuGet
description: Référence pour la commande nuget.exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622874"
---
# <a name="config-command-nuget-cli"></a>commande config (interface CLI NuGet)

**S’applique à :** toutes les &bullet; **versions prises en charge**: toutes

Obtient ou définit les valeurs de configuration NuGet. Pour une utilisation supplémentaire, consultez [configurations NuGet courantes](../../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur les noms de clé autorisés, reportez-vous à la [Référence du fichier de configuration NuGet](../nuget-config-file.md).

## <a name="usage"></a>Usage

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

où `<name>` et `<value>` spécifient une paire clé-valeur à définir dans la configuration. Vous pouvez spécifier autant de paires que vous le souhaitez. Pour supprimer une valeur, spécifiez le nom et le `=` signe, mais aucune valeur.

Pour les noms de clé autorisés, consultez la [Référence du fichier de configuration NuGet](../nuget-config-file.md).

Dans NuGet 3.4 +, `<value>` peut utiliser des [variables d’environnement](cli-ref-environment-variables.md).

## <a name="options"></a>Options


- **`AsPath`**

  Retourne la valeur de configuration sous la forme d’un chemin d’accès, ignoré lorsque `-Set` est utilisé.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Set`**

  Une sur plus de paires clé-valeur à définir dans la configuration.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemples

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
