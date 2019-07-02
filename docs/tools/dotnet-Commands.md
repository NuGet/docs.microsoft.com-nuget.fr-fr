---
title: commandes de CLI NuGet dotnet
description: Une référence courte pour les commandes liées à NuGet à l’aide de l’interface de ligne de commande dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496481"
---
# <a name="dotnet-cli-commands"></a>commandes CLI dotnet

Le `dotnet` l’interface de ligne de commande (CLI), qui s’exécute sur Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles telles que l’installation, la restauration et la publication des packages. Si dotnet répond à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.

Pour obtenir des exemples d’utilisation de ces commandes pour consommer des packages, consultez [installer et gérer des packages à l’aide de l’interface CLI dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Pour obtenir des exemples d’utilisation de ces commandes pour créer des packages, consultez [créer et publier un package à l’aide de l’interface CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Pour la référence de commande complète sur `dotnet` CLI, consultez [outils de l’interface de ligne de commande (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consommation de package

- [**dotnet ajouter package**](/dotnet/core/tools/dotnet-add-package): Ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.
- [**dotnet supprimer package**](/dotnet/core/tools/dotnet-remove-package): Supprime une référence de package à partir du fichier projet.
- [**restauration de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaure les dépendances et les outils d’un projet. À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.
- [**variables locales de dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): Répertorie les emplacements de la *global-packages*, *http-cache*, et *temp* efface le contenu de ces dossiers et les dossiers.
- [**nugetconfig nouvelle dotnet**](/dotnet/core/tools/dotnet-new): Crée un [ `nuget.config` ](../reference/nuget-config-file.md) fichier pour configurer le comportement de NuGet.

## <a name="package-creation"></a>Création d’un package

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Place le code dans un package NuGet.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publie un package sur un serveur NuGet. Applicable à nuget.org, artefacts Azure, et [des NuGet serveurs tiers](../hosting-packages/overview.md).
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Supprime ou retire un package à partir d’un serveur NuGet. Applicable à nuget.org, artefacts Azure, et [des NuGet serveurs tiers](../hosting-packages/overview.md).
