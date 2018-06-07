---
title: Commande de variables locales NuGet CLI
description: Référence de la commande de variables locales de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818199"
---
# <a name="locals-command-nuget-cli"></a>locals (commande, NuGet CLI)

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
| NonInteractive | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Pour obtenir des exemples supplémentaires, consultez [gestion des packages globaux et des dossiers cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).
