---
title: "Référence de l’Interface de ligne de commande (CLI) NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Index de référence de ligne de commande pour l’interface CLI de nuget.exe"
keywords: "index de référence de NuGet.exe, interface de ligne de commande de nuget.exe, nuget.exe CLI, commande nuget"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8b1ee17702f5a54a77dc2cd663e13729a9b4a39f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-cli-reference"></a>Référence de NuGet CLI

Le NuGet Interface de ligne de commande (CLI) `nuget.exe`, fournit l’éventail complet des fonctionnalités de NuGet pour installer, créer, publier et gérer les packages sans apporter de modifications aux fichiers de projet.

Pour utiliser une commande, ouvrez une fenêtre de commande ou bash shell, puis exécutez `nuget` suivie de la commande et les options appropriées, telles que `nuget help pack` (pour afficher l’aide sur la commande pack).

Cette documentation reflète la dernière version CLI NuGet. Pour obtenir des informations exactes pour n’importe quelle version donnée que vous utilisez, exécutez `nuget help` pour la commande souhaitée.

## <a name="installing-nugetexe"></a>L’installation de nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Tip]
> Pour rendre le CLI NuGet disponibles dans la Console du Gestionnaire de Package dans Visual Studio, consultez [à l’aide de l’interface CLI de nuget.exe dans la console](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilité

Consultez [fonctionnalité disponibilité](../install-nuget-client-tools.md#feature-availability) pour plus d’informations exactes.

- Toutes les commandes sont disponibles sur Windows.
- Toutes les commandes de travail avec nuget.exe en cours d’exécution sur Mono sauf indication contraire de `pack`, `restore`, et `update`.
- Le `pack`, `restore`, `delete`, `locals`, et `push` commandes sont également disponibles sur le Mac et Linux via l’interface CLI dotnet.

## <a name="commands-and-applicability"></a>Commandes et mise en application

Commandes disponibles et la mise en application à la création du package, la consommation de package ou publication d’un package vers un ordinateur hôte :

| Commandes courantes | Rôles applicables. | Version de NuGet | Description |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Création | 2.7+ | Crée un package NuGet à partir un `.nuspec` ou fichier projet. Lors de l’exécution sur Mono, la création d’un package à partir d’un fichier de projet n’est pas pris en charge. |
| [push](cli-ref-push.md) | Publication | Tous | Publie un package à une source de package. |
| [config](cli-ref-config.md) | Tous | Tous | Obtient ou définit les valeurs de configuration NuGet. |
| [help ou ?](cli-ref-help.md) | Tous | Tous | Affiche l’aide des informations ou à l’aide d’une commande. |
| [locals](cli-ref-locals.md) | Consommation | 3.3+ | Efface ou répertorie les packages dans des caches différents ou dans le dossier packages global identifie ces dossiers. |
| [restore](cli-ref-restore.md) | Consommation | 2.7+ | Restaure tous les packages référencés par le format de référence de package en cours d’utilisation. Lors de l’exécution sur Mono, la restauration des packages en utilisant le format PackageReference n’est pas pris en charge. |
| [setapikey](cli-ref-setapikey.md) | Publication, la consommation | Tous | Enregistre une clé d’API pour une source de package donné lors de la source du package nécessite une clé d’accès. |
| [spec](cli-ref-spec.md) | Création | Tous | Génère un `.nuspec` de fichiers, l’utilisation de jetons si la génération du fichier à partir d’un projet Visual Studio. |

| Commandes secondaires | Rôles applicables. | Version de NuGet | Description |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publication | 3.3+ | Ajoute un package à une source de package de non-HTTP à l’aide de façon hiérarchique. Pour les sources HTTP, utilisez *push*. |
| [delete](cli-ref-delete.md) | Publication | Tous | Supprime ou unlists un package à partir d’une source de package. |
| [init](cli-ref-init.md) | Création | 3.3+ | Ajoute des packages à partir d’un dossier à une source de package à l’aide de façon hiérarchique. |
| [install](cli-ref-install.md) | Consommation | Tous | Installe un package en cours de projet, mais ne pas modifier des projets ou référencer des fichiers. |
| [list](cli-ref-list.md) | Consommation, voire de publication | Tous | Affiche les packages à partir d’une source donnée. |
| [mirror](cli-ref-mirror.md) | Publication | Déconseillé dans 3.2 + | Reflète un package et ses dépendances à partir d’une source vers un référentiel cible. |
| [sources](cli-ref-sources.md) | La consommation, publication | Tous | Gère les sources de package dans les fichiers de configuration. |
| [update](cli-ref-update.md) | Consommation | Tous | Met à jour les packages d’un projet pour les dernières versions disponibles. Non pris en charge sur Mono. |

Assurez-vous de différentes commandes utiliser différents [variables d’environnement](cli-ref-environment-variables.md).

Commandes de NuGet CLI en rôles applicables :

| Rôle | Commandes |
| --- | --- |
| Consommation | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Création | `config`, `help`, `init`, `pack`, `spec` |
| Publication | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Les développeurs soucieux uniquement à la consommation des packages, par exemple, seulement besoin de comprendre que ce sous-ensemble de commandes NuGet.

> [!Note]
> Noms d’options de commande respectent la casse. Les options qui sont déconseillées ne sont pas incluses dans cette référence, tel que `NoPrompt` (remplacé par `NonInteractive`) et `Verbose` (remplacé par `Verbosity`).
