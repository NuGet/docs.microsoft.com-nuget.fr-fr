---
title: commandes NuGet CLI dotnet
description: Référence concise pour les commandes liées à NuGet à l’aide de l’interface de ligne de commande dotnet.
author: JonDouglas
ms.author: jodou
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5438354729ccc851bbbae6c0e7b9394d4226da52
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779993"
---
# <a name="dotnet-cli-commands"></a>Commandes CLI dotnet

L' `dotnet` interface de ligne de commande (CLI), qui s’exécute sous Windows, Mac OS X et Linux, fournit un certain nombre de commandes essentielles, telles que l’installation, la restauration et la publication de packages. Si dotnet répond à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe` .

Pour obtenir des exemples d’utilisation de ces commandes pour consommer des packages, consultez [installer et gérer des packages à l’aide de l’interface CLI dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Pour obtenir des exemples d’utilisation de ces commandes pour créer des packages, consultez [créer et publier un package à l’aide de l’interface CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Pour obtenir une référence complète sur les commandes `dotnet` CLI, consultez outils de l' [interface de ligne de commande (CLI) .net Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consommation des packages

- [**dotnet Add Package**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.
- [**dotnet Remove Package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de package du fichier projet.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.
- [**locales dotnet NuGet**](/dotnet/core/tools/dotnet-nuget-locals): répertorie les emplacements des dossiers *Global-packages*, *http-cache* et *temp* et efface le contenu de ces dossiers.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): crée un [`nuget.config`](../reference/nuget-config-file.md) fichier pour configurer le comportement de NuGet.

## <a name="package-creation"></a>Création de package

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): compresse le code dans un package NuGet.
- [**dotnet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): publie un package sur un serveur NuGet. Applicable aux [serveurs nuget](../hosting-packages/overview.md)nuget.org, Azure artifacts et tiers.
- [**dotnet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou déliste un package d’un serveur NuGet. Applicable aux [serveurs nuget](../hosting-packages/overview.md)nuget.org, Azure artifacts et tiers.
- [**dotnet NuGet Verify**](/dotnet/core/tools/dotnet-nuget-verify): vérifie un package NuGet signé.
