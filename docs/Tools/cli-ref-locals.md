---
title: Commande de variables locales NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Référence de la commande de variables locales de nuget.exe"
keywords: "référence de variables locales de NuGet, commande de variables locales"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>commande de variables locales (NuGet CLI)

**S’applique à :** package consommation &bullet; **versions prises en charge :** 3.3 +

Efface ou des listes de ressources NuGet locales telles que le cache de requête http, le cache de packages et le dossier packages global d’échelle de l’ordinateur. Le `locals` commande peut également être utilisée pour afficher une liste de ces emplacements. Pour plus d’informations, consultez [gestion du NuGet Cache](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Utilisation

```
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

```
nuget locals all -list
nuget locals http-cache -clear
```
