---
title: Commande paramètres régionaux de l’interface CLI NuGet
description: Référence pour la commande NuGet. exe variables locales
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327806"
---
# <a name="locals-command-nuget-cli"></a>locals (commande, NuGet CLI)

**S’applique à:** &bullet; **versions prises en charge par** la consommation des packages: 3.3+

Efface ou répertorie les ressources NuGet locales, telles que le dossier *http-cache*, *Global-packages* et le dossier Temp. La `locals` commande peut également être utilisée pour afficher une liste de ces emplacements. Pour plus d’informations, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Usage

```cli
nuget locals <folder> [options]
```

où `<folder>` est l' `plugins-cache` un `all` `packages-cache` `temp` `global-packages`   des, ,(3,5etversionsantérieures),,(3.4+)et(4.8+).`http-cache`

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Effacer | Efface le dossier spécifié. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| Énumérer | Répertorie l’emplacement du dossier spécifié, ou les emplacements de tous les dossiers lorsqu’ils sont utilisés avec *tous*. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Pour obtenir des exemples supplémentaires, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
