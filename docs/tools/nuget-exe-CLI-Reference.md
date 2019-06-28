---
title: Référence de l’Interface de ligne de commande (CLI) de NuGet
description: Index de référence de ligne de commande pour l’interface CLI de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426021"
---
# <a name="nuget-cli-reference"></a>Référence CLI de NuGet

L’Interface de ligne de commande (interface CLI NuGet), `nuget.exe`, fournit l’étendue complète de fonctionnalités de NuGet pour installer, créer, publier et gérer les packages sans apporter de modifications aux fichiers de projet.

Pour utiliser n’importe quelle commande, ouvrez une fenêtre de commande ou interpréteur de commandes bash, puis exécutez `nuget` suivie de la commande et les options appropriées, tel que `nuget help pack` (pour afficher l’aide sur la commande pack).

Cette documentation reflète la dernière version de la CLI de NuGet. Pour obtenir des détails précis pour une version donnée que vous utilisez, exécutez `nuget help` pour la commande souhaitée.

Pour savoir comment utiliser des commandes de base avec le `nuget.exe` CLI, consultez [installer et utiliser des packages à l’aide de l’interface CLI de nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>L’installation de nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Pour rendre le CLI NuGet disponible dans la Console du Gestionnaire de Package dans Visual Studio, consultez [à l’aide de l’interface CLI de nuget.exe dans la console](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilité

Consultez [disponibilité des fonctionnalités](../install-nuget-client-tools.md#feature-availability) pour plus d’informations.

- Toutes les commandes sont disponibles sur Windows.
- Toutes les commandes fonctionnent avec nuget.exe en cours d’exécution sur Mono sauf indication contraire pour `pack`, `restore`, et `update`.
- Le `pack`, `restore`, `delete`, `locals`, et `push` commandes sont également disponibles sur Mac et Linux via l’interface CLI dotnet.

## <a name="commands-and-applicability"></a>Commandes et mise en application

Les commandes disponibles ou adéquation à la création du package, la consommation de package et/ou la publication d’un package vers un ordinateur hôte :

| Commandes courantes | Rôles applicables. | Version de NuGet | Description |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Création | 2.7+ | Crée un package NuGet à partir d’un `.nuspec` ou fichier projet. Lors de l’exécution sur Mono, la création d’un package à partir d’un fichier de projet n’est pas pris en charge. |
| [push](cli-ref-push.md) | Publication | Tous | Publie un package à une source de package. |
| [config](cli-ref-config.md) | Tous | Tous | Obtient ou définit les valeurs de configuration NuGet. |
| [help or ?](cli-ref-help.md) | Tous | Tous | Affiche l’aide des informations ou à l’aide d’une commande. |
| [locals](cli-ref-locals.md) | Consommation | 3.3+ | Répertorie les emplacements de la *global-packages*, *http-cache*, et *temp* efface le contenu de ces dossiers et les dossiers. |
| [restore](cli-ref-restore.md) | Consommation | 2.7+ | Restaure tous les packages référencés par le format de gestion de package en cours d’utilisation. Lors de l’exécution sur Mono, la restauration des packages en utilisant le format PackageReference n’est pas pris en charge. |
| [setapikey](cli-ref-setapikey.md) | Publication, la consommation | Tous | Enregistre une clé API pour une source de package donné lors de cette source de package nécessite une clé pour l’accès. |
| [spec](cli-ref-spec.md) | Création | Tous | Génère un `.nuspec` fichier, à l’aide de jetons si la génération du fichier à partir d’un projet Visual Studio. |

| Commandes secondaires | Rôles applicables. | Version de NuGet | Description |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publication | 3.3+ | Ajoute un package à une source de packages non HTTP à l’aide de disposition hiérarchique. Pour les sources HTTP, utilisez *push*. |
| [delete](cli-ref-delete.md) | Publication | Tous | Supprime ou retire un package à partir d’une source de package. |
| [init](cli-ref-init.md) | Création | 3.3+ | Ajoute des packages à partir d’un dossier à une source de package à l’aide de disposition hiérarchique. |
| [install](cli-ref-install.md) | Consommation | Tous | Installe un package en cours de projet mais ne pas modifier des projets ou référencer des fichiers. |
| [liste](cli-ref-list.md) | Consommation, peut-être de publication | Tous | Affiche les packages à partir d’une source donnée. |
| [mirror](cli-ref-mirror.md) | Publication | Déconseillé dans 3.2 + | Reflète un package et ses dépendances à partir d’une source vers un référentiel cible. |
| [sources](cli-ref-sources.md) | La consommation, publication | Tous | Gère les sources de package dans les fichiers de configuration. |
| [update](cli-ref-update.md) | Consommation | Tous | Met à jour les packages d’un projet avec les dernières versions disponibles. Non pris en charge lors de l’exécution sur Mono. |

Assurez-vous de différentes commandes utiliser de divers [variables d’environnement](cli-ref-environment-variables.md).

Commandes CLI NuGet par rôles applicables :

| Rôle | Commandes |
| --- | --- |
| Consommation | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Création | `config`, `help`, `init`, `pack`, `spec` |
| Publication | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Les développeurs soucieux uniquement de consommer des packages, par exemple, seulement besoin de comprendre que le sous-ensemble de commandes NuGet.

> [!Note]
> Noms des options de commande respectent la casse. Les options qui sont déconseillées ne sont pas incluses dans cette référence, tel que `NoPrompt` (remplacé par `NonInteractive`) et `Verbose` (remplacé par `Verbosity`).
