---
title: Ajouter des commandes CLI NuGet
description: Référence pour nuget.exe ajouter la commande
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545832"
---
# <a name="add-command-nuget-cli"></a>add (commande, NuGet CLI)

**S’applique aux**: publication du package &bullet; **versions prises en charge**: 3.3 +

Ajoute un package spécifié à une source de packages non HTTP (un dossier ou un chemin d’accès UNC) de façon hiérarchique, où les dossiers sont créés pour le numéro d’ID et la version de package. Exemple :

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Lorsque vous restaurez ou la mise à jour par rapport à la source du package, disposition hiérarchique considérablement plus performante.

Pour développer tous les fichiers dans le package à la source de package de destination, utilisez la `-Expand` basculer. Cela se produit généralement dans les sous-dossiers supplémentaires qui apparaissent dans la destination, tel que `tools` et `lib`.

## <a name="usage"></a>Utilisation

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

où `<packagePath>` est le chemin d’accès au package à ajouter, et `<sourcePath>` spécifie la source de package basé sur le dossier dans lequel le package sera ajouté. Les sources HTTP ne sont pas pris en charge.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration de NuGet à appliquer. Si non spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) est utilisé.|
| Expand | Ajoute tous les fichiers dans le package à la source du package. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
