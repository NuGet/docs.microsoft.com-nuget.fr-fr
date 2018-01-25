---
title: Commande delete de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informations de référence pour la commande de suppression de nuget.exe"
keywords: "supprimer la référence de NuGet, supprimer la commande de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a>supprimer la commande (NuGet CLI)

**S’applique à :** la publication du package &bullet; **versions prises en charge :** toutes les

Supprime ou unlists un package à partir d’une source de package. Pour nuget.org, la commande de suppression [unlists le package](../policies/Deleting-Packages.md).

## <a name="usage"></a>Utilisation

```cli
nuget delete <packageID> <packageVersion> [options]
```

où `<packageID>` et `<packageVersion>` identifier le package exact pour supprimer ou retirer de la liste. Le comportement exact dépend de la source. Pour des dossiers locaux, par exemple, la suppression du package ; pour nuget.org le package n’est pas spécifié.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| apiKey | La clé d’API pour le référentiel cible. Si absent, celui spécifié dans *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ConfigFile | Le fichier de configuration NuGet à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Source | Spécifie l’URL du serveur. L’URL de nuget.org est `https://api.nuget.org/v3/index.json`. Pour les flux privés, remplacez le nom d’hôte, par exemple, *%hostname%/api/v3*. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
