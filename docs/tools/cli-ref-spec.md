---
title: Commande spec de NuGet CLI
description: Informations de référence pour la commande spec nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a>commande spec (NuGet CLI)

**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les

Génère un `.nuspec` fichier pour un nouveau package. Si vous exécutez dans le même dossier dans un fichier de projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier. Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilisation

```cli
nuget spec [<packageID>] [options]
```

où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| AssemblyPath | Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées. |
| Force | Remplace l’existant `.nuspec` fichier. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
