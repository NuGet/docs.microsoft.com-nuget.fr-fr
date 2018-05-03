---
title: Commande de variables locales NuGet CLI
description: Référence de la commande de variables locales de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>commande de variables locales (NuGet CLI)

**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +

Efface ou répertorie les ressources de NuGet locales telles que la *du cache http*, *global-packages* dossier et le dossier temporaire. Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements. Pour plus d’informations, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Utilisation

```cli
nuget locals <folder> [options]
```

où `<folder>` est un des `all`, `http-cache`, `packages-cache` *(3.5 et versions antérieures)*, `global-packages`, et `temp` *(3.4 +)*.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Effacer | Efface le dossier spécifié. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Liste | Répertorie l’emplacement du dossier spécifié, ou les emplacements de dossiers de tous les cas d’utilisation avec *tous les*. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Pour obtenir des exemples supplémentaires, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).
