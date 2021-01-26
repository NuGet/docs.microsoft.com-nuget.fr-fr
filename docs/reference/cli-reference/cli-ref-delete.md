---
title: Commande de suppression de l’interface CLI NuGet
description: Référence pour la commande nuget.exe Delete
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775948"
---
# <a name="delete-command-nuget-cli"></a>Delete, commande (interface CLI NuGet)

**S’applique à : publication de** packages &bullet; **versions prises en charge :** tout

Supprime ou déliste un package d’une source de package. Pour nuget.org, la commande delete [déliste le package](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Utilisation

```cli
nuget delete <packageID> <packageVersion> [options]
```

où `<packageID>` et `<packageVersion>` identifient le package exact à supprimer ou à supprimer de la liste. Le comportement exact dépend de la source. Pour les dossiers locaux, par exemple, le package est supprimé ; pour nuget.org, le package n’est pas répertorié.

## <a name="options"></a>Options

- **`-ApiKey`**

  Clé API pour le référentiel cible. S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé.

- **`-ConfigFile`**

  Fichier de configuration NuGet à appliquer. S’il n’est pas spécifié, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) est utilisé.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Force l’exécution de nuget.exe à l’aide d’une culture indifférente en anglais.

- **`-?|-help`**

  Affiche des informations d’aide pour la commande.

- **`-NonInteractive`**

  Supprime les invites de saisie ou de confirmation de l’utilisateur.

 - **`-np|-NoPrompt`**

   Ne pas demander lorsque vous supprimez.

 - **`-NoServiceEndpoint`** N’ajoute pas « API/v2/packages » à l’URL source.

- **`-src|-Source`**

  Spécifie l’URL du serveur. L’URL de nuget.org est `https://api.nuget.org/v3/index.json` . Pour les flux privés, remplacez le nom d’hôte, par exemple, *% hostname%/API/V3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Spécifie la quantité de détails affichée dans la sortie : `normal` (valeur par défaut), `quiet` ou `detailed` .

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
