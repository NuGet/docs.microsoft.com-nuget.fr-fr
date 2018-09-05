---
title: Commande spec CLI NuGet
description: Référence pour la commande spec nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546447"
---
# <a name="spec-command-nuget-cli"></a>spécification de commande (CLI NuGet)

**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les

Génère un `.nuspec` fichier d’un nouveau package. Si vous exécutez dans le même dossier que le fichier projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier. Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilisation

```cli
nuget spec [<packageID>] [options]
```

où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AssemblyPath | Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées. |
| Force | Remplace tout existant `.nuspec` fichier. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| NonInteractive | Supprime les invites pour l’entrée de l’utilisateur ou de confirmations. |
| Verbosity | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
