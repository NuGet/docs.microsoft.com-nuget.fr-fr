---
title: Commande config de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour la commande config de nuget.exe"
keywords: "référence de configuration NuGet, commande config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 31abc5c1ade0aff9a2f23ec89ec7082acedb3653
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="config-command-nuget-cli"></a>commande de configuration (NuGet CLI)

**S’applique à :** tous les &bullet; **versions prises en charge**: tous les

Obtient ou définit les valeurs de configuration NuGet. Pour l’utilisation supplémentaire, consultez [configuration de comportement de NuGet](../consume-packages/configuring-nuget-behavior.md). Pour plus d’informations sur les noms de clés autorisées, reportez-vous à la [référence du fichier de configuration NuGet](../Schema/nuget-config-file.md).

## <a name="usage"></a>Utilisation

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

où `<name>` et `<value>` spécifier une paire clé-valeur à définir dans la configuration. Vous pouvez spécifier autant de paires comme vous le souhaitez. Pour supprimer une valeur, spécifiez le nom et le `=` signe mais aucune valeur.

Pour les noms de clé autorisées, consultez la [référence du fichier de configuration NuGet](../Schema/nuget-config-file.md).

Dans NuGet 3.4 + `<value>` peut utiliser [variables d’environnement](cli-ref-environment-variables.md).

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AsPath | Renvoie la valeur de la configuration comme un chemin d’accès, ignorées lorsque `-Set` est utilisé. |
| ConfigFile | Le fichier de configuration NuGet à modifier. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemples

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
