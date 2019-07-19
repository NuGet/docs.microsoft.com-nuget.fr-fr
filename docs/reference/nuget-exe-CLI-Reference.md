---
title: Informations de référence sur l’interface de ligne de commande (CLI) NuGet
description: Index de référence de ligne de commande pour l’interface CLI de NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327466"
---
# <a name="nuget-cli-reference"></a>Informations de référence sur l’interface CLI NuGet

L’interface de ligne de commande (CLI) `nuget.exe`NuGet,, fournit l’étendue complète de la fonctionnalité NuGet pour installer, créer, publier et gérer des packages sans apporter de modifications aux fichiers projet.

Pour utiliser une commande, ouvrez une fenêtre de commande ou un interpréteur de `nuget` commandes bash, puis exécutez suivi par la commande et `nuget help pack` les options appropriées, telles que (pour afficher l’aide sur la commande Pack).

Cette documentation reflète la dernière version de l’interface CLI NuGet. Pour obtenir des détails exacts sur une version donnée que vous utilisez `nuget help` , exécutez pour la commande souhaitée.

Pour savoir comment utiliser les commandes de base avec l’interface CLI `nuget.exe`, consultez [Installer et utiliser des packages à l’aide de l’interface CLI nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Installation de NuGet. exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Pour rendre l’interface CLI NuGet disponible dans la console du gestionnaire de package dans Visual Studio, consultez [utilisation de l’interface CLI NuGet. exe dans la console](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilité

Pour plus d’informations, consultez [disponibilité des fonctionnalités](../install-nuget-client-tools.md#feature-availability) .

- Toutes les commandes sont disponibles sur Windows.
- Toutes les commandes fonctionnent avec NuGet. exe s’exécutant sur mono, sauf `pack`indication `restore`contraire pour `update`, et.
- Les `pack`commandes `restore`, ,`delete` ,et`push` sont également disponibles sur Mac et Linux par le biais de l’interface CLI dotnet. `locals`

## <a name="commands-and-applicability"></a>Commandes et applicabilité

Commandes disponibles et applicabilité pour la création de packages, la consommation des packages et/ou la publication d’un package sur un ordinateur hôte:

| Commandes courantes | Rôles applicables | Version de NuGet | Description |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Constitution | 2.7+ | Crée un package NuGet à partir `.nuspec` d’un fichier projet ou. En cas d’exécution sur mono, la création d’un package à partir d’un fichier projet n’est pas prise en charge. |
| [push](cli-reference/cli-ref-push.md) | Publication | Tous | Publie un package dans une source de package. |
| [config](cli-reference/cli-ref-config.md) | Tous | Tous | Obtient ou définit les valeurs de configuration NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Tous | Tous | Affiche des informations d’aide ou de l’aide pour une commande. |
| [locals](cli-reference/cli-ref-locals.md) | Consommation | 3.3+ | Répertorie les emplacements des dossiers *Global-packages*, *http-cache*et *temp* et efface le contenu de ces dossiers. |
| [restore](cli-reference/cli-ref-restore.md) | Consommation | 2.7+ | Restaure tous les packages référencés par le format de gestion des packages en cours d’utilisation. En cas d’exécution sur mono, la restauration de packages à l’aide du format PackageReference n’est pas prise en charge. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Publication, consommation | Tous | Enregistre une clé API pour une source de package donnée lorsque cette source de package requiert une clé pour l’accès. |
| [spec](cli-reference/cli-ref-spec.md) | Constitution | Tous | Génère un `.nuspec` fichier en utilisant des jetons en cas de génération du fichier à partir d’un projet Visual Studio. |

| Commandes secondaires | Rôles applicables | Version de NuGet | Description |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publication | 3.3+ | Ajoute un package à une source de package non-HTTP à l’aide de la disposition hiérarchique. Pour les sources HTTP, utilisez *Push*. |
| [delete](cli-reference/cli-ref-delete.md) | Publication | Tous | Supprime ou déliste un package d’une source de package. |
| [init](cli-reference/cli-ref-init.md) | Constitution | 3.3+ | Ajoute des packages à partir d’un dossier à une source de package à l’aide d’une disposition hiérarchique. |
| [install](cli-reference/cli-ref-install.md) | Consommation | Tous | Installe un package dans le projet actuel, mais ne modifie pas les projets ou les fichiers de référence. |
| [liste](cli-reference/cli-ref-list.md) | Consommation, éventuellement la publication | Tous | Affiche les packages d’une source donnée. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publication | Déconseillé dans 3.2 + | Met en miroir un package et ses dépendances d’une source vers un référentiel cible. |
| [sources](cli-reference/cli-ref-sources.md) | Consommation, publication | Tous | Gère les sources de package dans les fichiers de configuration. |
| [update](cli-reference/cli-ref-update.md) | Consommation | Tous | Met à jour les packages d’un projet vers les versions les plus récentes disponibles. Non pris en charge lors de l’exécution sur mono. |

Différentes commandes utilisent différentes variables d' [environnement](cli-reference/cli-ref-environment-variables.md).

Commandes CLI NuGet par rôles applicables:

| Rôle | Commandes |
| --- | --- |
| Consommation | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Constitution | `config`, `help`, `init`, `pack`, `spec` |
| Publication | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Les développeurs concernés uniquement par la consommation de packages, par exemple, ont uniquement besoin de comprendre ce sous-ensemble de commandes NuGet.

> [!Note]
> Les noms des options de commande ne respectent pas la casse. Les options dépréciées ne sont pas incluses dans cette référence, telles `NoPrompt` que (remplacé `NonInteractive`par) `Verbose` et (remplacées par `Verbosity`).
