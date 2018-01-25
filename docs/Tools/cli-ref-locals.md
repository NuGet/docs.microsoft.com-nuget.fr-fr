---
title: Commande de variables locales NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Référence de la commande de variables locales de nuget.exe"
keywords: "référence de variables locales de NuGet, commande de variables locales"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a>commande de variables locales (NuGet CLI)

**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +

Efface ou des listes de ressources NuGet locales telles que le cache de requête http, le cache de packages et le dossier packages global d’échelle de l’ordinateur. Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements. Pour plus d’informations, consultez [gestion du NuGet Cache](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Utilisation

```cli
nuget locals <cache> [options]
```

où `<cache>` est un des `all`, `http-cache`, `packages-cache`, `global-packages`, et `temp` *(3.4 +)*.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| Effacer | Efface le cache spécifié. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Liste | Répertorie l’emplacement du cache spécifié, ou les emplacements de tous les caches lorsqu’il est utilisé avec *tous les*. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget locals all -list
nuget locals http-cache -clear
```
