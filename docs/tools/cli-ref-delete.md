---
title: Commande de suppression de CLI de NuGet
description: Référence pour la commande de suppression nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548508"
---
# <a name="delete-command-nuget-cli"></a>supprimer la commande (CLI NuGet)

**S’applique à :** publication du package &bullet; **versions prises en charge :** toutes les

Supprime ou retire un package à partir d’une source de package. Pour nuget.org, la commande de suppression [retire le package](../policies/deleting-packages.md).

## <a name="usage"></a>Utilisation

```cli
nuget delete <packageID> <packageVersion> [options]
```

où `<packageID>` et `<packageVersion>` identifier le package exact pour supprimer ou retirer de la liste. Le comportement exact dépend de la source. Pour les dossiers locaux, par exemple, la suppression du package ; pour nuget.org le package n’est pas répertorié.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ApiKey | La clé API pour le référentiel cible. Si elle est absente, celle spécifiée dans le fichier de configuration est utilisé. |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Source | Spécifie l’URL du serveur. L’URL de nuget.org est `https://api.nuget.org/v3/index.json`. Pour les flux privés, remplacez le nom d’hôte, par exemple, *%hostname%/api/v3*. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
