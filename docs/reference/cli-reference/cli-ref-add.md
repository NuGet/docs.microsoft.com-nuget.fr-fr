---
title: Commande Add de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622900"
---
# <a name="add-command-nuget-cli"></a>Add, commande (interface CLI NuGet)

**S’applique à**: publication de packages &bullet; **versions prises en charge**: 3.3 +

Ajoute un package spécifié à une source de package non-HTTP (dossier ou chemin d’accès UNC) dans une disposition hiérarchique, où les dossiers sont créés pour l’ID de package et le numéro de version. Par exemple :

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Lors de la restauration ou de la mise à jour par rapport à la source du package, la disposition hiérarchique offre des performances nettement meilleures.

Pour développer tous les fichiers du package vers la source du package de destination, utilisez le `-Expand` commutateur. Cela entraîne généralement l’affichage de sous-dossiers supplémentaires dans la destination, tels que `tools` et `lib` .

## <a name="usage"></a>Usage

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

où `<packagePath>` est le nom du chemin d’accès au package à ajouter et `<sourcePath>` spécifie la source du package basée sur le dossier à laquelle le package sera ajouté. Les sources HTTP ne sont pas prises en charge.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-Expand`**

  Ajoute tous les fichiers du package à la source du package.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.
Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-src|-Source`**

   Spécifie la source du package, qui est un dossier ou un partage UNC auquel le nupkg sera ajouté. Les sources http ne sont pas prises en charge.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
