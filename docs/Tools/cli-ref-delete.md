---
title: Commande delete de NuGet CLI | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Informations de référence pour la commande de suppression de nuget.exe"
keywords: "supprimer la référence de NuGet, supprimer la commande de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>supprimer la commande (NuGet CLI)

**S’applique à :** la publication du package &bullet; **versions prises en charge :** toutes les

Supprime ou unlists un package à partir d’une source de package. Pour nuget.org, la commande de suppression [unlists le package](../policies/Deleting-Packages.md).

## <a name="usage"></a>Utilisation

```
nuget delete <packageID> <packageVersion> [options]
```

où `<packageID>` et `<packageVersion>` identifier le package exact pour supprimer ou retirer de la liste. Le comportement exact dépend de la source. Pour des dossiers locaux, par exemple, la suppression du package ; pour nuget.org le package n’est pas spécifié.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| apiKey | La clé d’API pour le référentiel cible. Si absent, celui spécifié dans *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ConfigFile | *(2.5 +)*  NuGet le fichier de configuration à appliquer. Si non spécifié, *%AppData%\NuGet\NuGet.Config* est utilisé. |
| ForceEnglishOutput | *(3.5 +)*  Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche l’aide de la commande. |
| Non interactif | Supprime les invites de saisie utilisateur ou les confirmations. |
| Source | Spécifie l’URL du serveur. L’URL de nuget.org est `https://api.nuget.org/v3/index.json`. Pour les flux privés, remplacez le nom d’hôte, par exemple, *%hostname%/api/v3*. |
| Commentaires | Spécifie la quantité de détails affichés dans la sortie : *normal*, *silencieux*, *détaillées (2.5 +)*. |

Consultez également [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
