---
title: Commande Add de l’interface CLI NuGet
description: Référence pour la commande d’ajout de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327856"
---
# <a name="add-command-nuget-cli"></a>add (commande, NuGet CLI)

**S’applique à**: publication &bullet; de packages **prises en charge**: 3.3+

Ajoute un package spécifié à une source de package non-HTTP (dossier ou chemin d’accès UNC) dans une disposition hiérarchique, où les dossiers sont créés pour l’ID de package et le numéro de version. Par exemple :

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Lors de la restauration ou de la mise à jour par rapport à la source du package, la disposition hiérarchique offre des performances nettement meilleures.

Pour développer tous les fichiers du package vers la source du package de destination, utilisez `-Expand` le commutateur. Cela entraîne généralement l’affichage de sous-dossiers supplémentaires dans la destination, tels `tools` que `lib`et.

## <a name="usage"></a>Usage

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

où `<packagePath>` est le nom du chemin d’accès au package à `<sourcePath>` ajouter et spécifie la source du package basée sur le dossier à laquelle le package sera ajouté. Les sources HTTP ne sont pas prises en charge.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| Expand | Ajoute tous les fichiers du package à la source du package. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
