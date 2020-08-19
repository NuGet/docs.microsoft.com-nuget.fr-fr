---
title: Commande paramètres régionaux de l’interface CLI NuGet
description: Référence pour la commande nuget.exe variables locales
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623056"
---
# <a name="locals-command-nuget-cli"></a>commande variables locales (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge par** la consommation de packages : 3.3 +

Efface ou répertorie les ressources NuGet locales, telles que le dossier *http-cache*, *Global-packages* et le dossier Temp. La `locals` commande peut également être utilisée pour afficher une liste de ces emplacements. Pour plus d’informations, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Usage

```cli
nuget locals <folder> [options]
```

où `<folder>` est l’un des, `all` `http-cache` , `packages-cache` *(3,5 et versions antérieures)*, `global-packages` , `temp` *(3.4 +)* et `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Options

- **`-Clear`**

  Efface le dossier spécifié.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-List`**

  Répertorie l’emplacement du dossier spécifié, ou les emplacements de tous les dossiers lorsqu’ils sont utilisés avec *tous*.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Pour obtenir des exemples supplémentaires, consultez [gestion des dossiers de packages globaux et de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
