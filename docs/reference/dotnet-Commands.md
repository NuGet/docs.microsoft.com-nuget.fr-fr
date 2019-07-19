---
title: commandes NuGet CLI dotnet
description: Référence concise pour les commandes liées à NuGet à l’aide de l’interface de ligne de commande dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327486"
---
# <a name="dotnet-cli-commands"></a>commandes CLI dotnet

L' `dotnet` interface de ligne de commande (CLI), qui s’exécute sous Windows, Mac OS X et Linux, fournit un certain nombre de commandes essentielles, telles que l’installation, la restauration et la publication de packages. Si dotnet répond à vos besoins, il n’est pas nécessaire d' `nuget.exe`utiliser.

Pour obtenir des exemples d’utilisation de ces commandes pour consommer des packages, consultez [installer et gérer des packages à l’aide de l’interface CLI dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Pour obtenir des exemples d’utilisation de ces commandes pour créer des packages, consultez [créer et publier un package à l’aide de l’interface CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Pour obtenir une référence complète sur `dotnet` les commandes CLI, consultez outils de l' [interface de ligne de commande (CLI) .net Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consommation des packages

- [**Ajouter un package dotnet**](/dotnet/core/tools/dotnet-add-package): Ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.
- [**supprimer le package de dotnet**](/dotnet/core/tools/dotnet-remove-package): Supprime une référence de package du fichier projet.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaure les dépendances et les outils d’un projet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.
- [**locales dotnet NuGet**](/dotnet/core/tools/dotnet-nuget-locals): Répertorie les emplacements des dossiers *Global-packages*, *http-cache*et *temp* et efface le contenu de ces dossiers.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): Crée un [`nuget.config`](../reference/nuget-config-file.md) fichier pour configurer le comportement de NuGet.

## <a name="package-creation"></a>Création de package

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Compresse le code dans un package NuGet.
- [**dotnet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): Publie un package sur un serveur NuGet. Applicable aux [serveurs nuget](../hosting-packages/overview.md)nuget.org, Azure artifacts et tiers.
- [**dotnet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): Supprime ou déliste un package d’un serveur NuGet. Applicable aux [serveurs nuget](../hosting-packages/overview.md)nuget.org, Azure artifacts et tiers.
