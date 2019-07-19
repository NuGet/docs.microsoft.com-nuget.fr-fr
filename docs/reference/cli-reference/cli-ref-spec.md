---
title: Commande spec de l’interface CLI NuGet
description: Référence pour la commande de spécification NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327566"
---
# <a name="spec-command-nuget-cli"></a>Spec, commande (interface CLI NuGet)

**S’applique à:** &bullet; **versions prises en charge** pour la création de package: All

Génère un `.nuspec` fichier pour un nouveau package. Si l’exécution s’exécute dans le même dossier qu’un`.csproj`fichier `.vbproj`projet `.fsproj`(, `spec` ,), crée `.nuspec` un fichier sous forme de jeton. Pour plus d’informations, consultez [création d’un package](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Usage

```cli
nuget spec [<packageID>] [options]
```

où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AssemblyPath | Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées. |
| Appliqués | Remplace tout fichier existant `.nuspec` . |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
