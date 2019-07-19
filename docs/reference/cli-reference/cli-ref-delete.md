---
title: Commande de suppression de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327836"
---
# <a name="delete-command-nuget-cli"></a>Delete, commande (interface CLI NuGet)

**S’applique à:** publication &bullet; de packages **versions prises en charge:** tout

Supprime ou déliste un package d’une source de package. Pour nuget.org, la commande delete [déliste le package](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Usage

```cli
nuget delete <packageID> <packageVersion> [options]
```

où `<packageID>` et`<packageVersion>` identifient le package exact à supprimer ou à supprimer de la liste. Le comportement exact dépend de la source. Pour les dossiers locaux, par exemple, le package est supprimé; pour nuget.org, le package n’est pas répertorié.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ApiKey | Clé API pour le référentiel cible. S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| source | Spécifie l’URL du serveur. L’URL de nuget.org est `https://api.nuget.org/v3/index.json`. Pour les flux privés, remplacez le nom d’hôte, par exemple, *% hostname%/API/V3*. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
