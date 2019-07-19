---
title: Commande Push de l’interface CLI NuGet
description: Référence pour la commande Push de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327626"
---
# <a name="push-command-nuget-cli"></a>Push, commande (interface CLI NuGet)

**S’applique à:** publication &bullet; de packages **versions prises en charge:** All; 4.1.0 + required for NuGet.org

> [!Important]
> Pour transmettre des packages à nuget.org, vous devez utiliser NuGet. exe v 4.1.0 +, qui implémente les [protocoles NuGet](../../api/nuget-protocols.md)requis.

Exécute un push d’un package vers une source de package et le publie.

La configuration par défaut de NuGet est obtenue `%AppData%\NuGet\NuGet.Config` en chargeant (Windows `~/.nuget/NuGet/NuGet.Config` ) ou (Mac/Linux), puis `Nuget.Config` en `.nuget\Nuget.Config` chargeant tous les fichiers ou à partir de la racine du lecteur jusqu’au répertoire actif (consultez [NuGet courant configurations](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Usage

```cli
nuget push <packagePath> [options]
```

où `<packagePath>` identifie le package à envoyer au serveur.

## <a name="options"></a>Options

| Option | Description |
| --- | --- |
| ApiKey | Clé API pour le référentiel cible. S’il n’est pas présent, celui spécifié dans le fichier de configuration est utilisé. |
| ConfigFile | Fichier de configuration NuGet à appliquer. S’il n’est `%AppData%\NuGet\NuGet.Config` pas spécifié, ( `~/.nuget/NuGet/NuGet.Config` Windows) ou (Mac/Linux) est utilisé.|
| DisableBuffering | Désactive la mise en mémoire tampon lors d’un push vers un serveur HTTP (s) pour réduire l’utilisation de la mémoire. ATTENTION: quand cette option est utilisée, l’authentification Windows intégrée peut ne pas fonctionner. |
| ForceEnglishOutput | *(3.5 +)* Force nuget.exe pour exécuter à l’aide d’une culture dite indifférente, en anglais. |
| Help | Affiche des informations d’aide pour la commande. |
| NonInteractive | Supprime les invites de saisie ou de confirmation de l’utilisateur. |
| Nosymbols | *(3.5 +)* Si un package de symboles existe, il ne fera pas l’objet d’un push vers un serveur de symboles. |
| source | Spécifie l’URL du serveur. NuGet identifie une source de dossier local ou UNC et copie simplement le fichier ici au lieu de l’envoyer à l’aide du protocole HTTP.  En outre, à compter de NuGet 3.4.2, il s’agit d’un `NuGet.Config` paramètre obligatoire, sauf si le fichier spécifie une valeur *DefaultPushSource* (voir [configuration du comportement de NuGet](../../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | *(5.1 +)* Si un package et une version existent déjà, ignorez-le et poursuivez avec le package suivant dans l’envoi (push), le cas échéant. |
| SymbolSource | *(3.5 +)* Spécifie l’URL du serveur de symboles; nuget.smbsrc.net est utilisé lors du push vers nuget.org |
| SymbolApiKey | *(3.5 +)* Spécifie la clé API pour l’URL spécifiée `-SymbolSource`dans. |
| Délai | Spécifie le délai d’attente, en secondes, pour effectuer un push vers un serveur. La valeur par défaut est 300 secondes (5 minutes). |
| Commentaires | Spécifie la quantité de détails affichée dans la sortie: *normal*, *Quiet*, *detailed*. |

Voir aussi [variables d’environnement](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemples

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
