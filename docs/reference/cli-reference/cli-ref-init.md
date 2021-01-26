---
title: Commande init de l’interface CLI NuGet
description: Référence pour la commande nuget.exe init
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780069"
---
# <a name="init-command-nuget-cli"></a>Init, commande (interface CLI NuGet)

**S’applique à :** &bullet; **versions prises en charge** pour la création de package : 3.3 +

Copie tous les packages d’un dossier plat dans un dossier de destination à l’aide d’une disposition hiérarchique comme décrit pour la [commande Ajouter](cli-ref-add.md). Autrement dit, l’utilisation de équivaut `init` à utiliser la `add` commande sur chaque package dans le dossier.

Comme avec `add` , la destination doit être un dossier local ou un chemin d’accès UNC ; Les référentiels de packages HTTP comme nuget.org ou les serveurs privés ne sont pas pris en charge.

## <a name="usage"></a>Utilisation

```cli
nuget init <source> <destination> [options]
```

où `<source>` est le dossier contenant les packages et `<destination>` est le dossier local ou le chemin d’accès UNC dans lequel les packages sont copiés.

## <a name="options"></a>Options

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-Expand`**

  Ajoute tous les fichiers de chaque package qui est ajouté à la source du package ; identique `-Expand` à la `add` commande.

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
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
