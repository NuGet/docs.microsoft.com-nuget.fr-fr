---
title: Commande spec de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Informations de référence pour la commande spec nuget.exe"
keywords: "référence technique de NuGet, commande spec"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>commande spec (NuGet CLI)

**S’applique à :** la création de package &bullet; **versions prises en charge :** toutes les

Génère un `.nuspec` fichier pour un nouveau package. Si vous exécutez dans le même dossier dans un fichier de projet (`.csproj`, `.vbproj`, `.fsproj`), `spec` crée un jeton `.nuspec` fichier. Pour plus d’informations, consultez [création d’un Package](../create-packages/creating-a-package.md).

## <a name="usage"></a>Utilisation

```
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
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
