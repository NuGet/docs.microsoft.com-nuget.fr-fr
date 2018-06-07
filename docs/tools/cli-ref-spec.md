---
title: Commande spec de NuGet CLI
description: Informations de référence pour la commande spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817084"
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
| NonInteractive | Supprime les invites de saisie utilisateur ou les confirmations. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
