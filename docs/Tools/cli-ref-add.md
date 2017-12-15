---
title: NuGet CLI ajouter commande | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Informations de référence pour le nuget.exe ajouter (commande)"
keywords: "Ajouter une référence de NuGet, ajouter la commande de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a>ajouter des commandes (NuGet CLI)

**S’applique aux**: publication du package &bullet; **versions prises en charge**: 3.3 +

Ajoute un package spécifié à une source de package de non-HTTP (un dossier ou un chemin d’accès UNC) de façon hiérarchique, dans lequel les dossiers sont créés pour le numéro d’ID et la version de package. Exemple :

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Lorsque vous restaurez ou mise à jour par rapport à la source du package, disposition hiérarchique fournit améliorer considérablement les performances.

Pour développer tous les fichiers dans le package à la source de package de destination, utilisez la `-Expand` basculer. Cela se produit généralement dans les sous-dossiers supplémentaires qui apparaissent dans la destination, tel que `tools` et `lib`.

## <a name="usage"></a>Utilisation

```
nuget add <packagePath> -Source <sourcePath> [options]
```

où `<packagePath>` est le chemin d’accès au package à ajouter, et `<sourcePath>` spécifie la source du package de basé sur le dossier dans lequel le package sera ajouté. Les sources HTTP ne sont pas pris en charge.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé.| 
| Expand | Ajoute tous les fichiers dans le package à la source du package. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
