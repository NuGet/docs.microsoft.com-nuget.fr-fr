---
title: Commande spec de l’interface CLI NuGet
description: Référence pour la commande nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622562"
---
# <a name="spec-command-nuget-cli"></a>Spec, commande (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge** pour la création de package : All

Génère un `.nuspec` fichier pour un nouveau package. Si l’exécution s’exécute dans le même dossier qu’un fichier projet ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` crée un `.nuspec` fichier sous forme de jeton. Pour plus d’informations, consultez [création d’un package](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Usage

```cli
nuget spec [<packageID>] [options]
```

où `<packageID>` est un identificateur de package facultatif à enregistrer dans le `.nuspec` fichier.

## <a name="options"></a>Options

- **`-AssemblyPath`**

  Spécifie le chemin d’accès à l’assembly à utiliser pour les métadonnées.

- **`-Force`**

  Remplace tout `.nuspec` fichier existant.


- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
