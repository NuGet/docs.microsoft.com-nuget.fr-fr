---
title: Commande de config NuGet CLI
description: Référence pour la commande config de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546476"
---
# <a name="config-command-nuget-cli"></a>commande config (CLI NuGet)

**S’applique à :** tous les &bullet; **versions prises en charge**: tous les

Obtient ou définit les valeurs de configuration NuGet. Pour une utilisation supplémentaire, consultez [configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur les noms de clés autorisées, reportez-vous à la [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Utilisation

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

où `<name>` et `<value>` spécifier une paire clé-valeur à définir dans la configuration. Vous pouvez spécifier autant de paires comme vous le souhaitez. Pour supprimer une valeur, spécifiez le nom et le `=` connexion, mais aucune valeur.

Pour les noms de clés autorisées, consultez le [référence du fichier de configuration NuGet](../reference/nuget-config-file.md).

Dans NuGet 3.4 + `<value>` peut utiliser [variables d’environnement](cli-ref-environment-variables.md).

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AsPath | Renvoie la valeur de la configuration comme un chemin d’accès, ignorées lorsque `-Set` est utilisé. |
| ConfigFile | Le fichier de configuration de NuGet à modifier. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemples

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
