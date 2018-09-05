---
title: commandes de dotnet NuGet
description: Une référence courte pour les commandes liées à NuGet à l’aide de l’interface de ligne de commande dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546314"
---
# <a name="dotnet-commands"></a>Commandes dotnet

Le `dotnet` interface de ligne de commande (CLI) dotnet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles nuget.exe comme listé ci-dessous. Si dotnet répond à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.

Pour obtenir des informations complètes sur `dotnet`, consultez [outils de l’interface de ligne de commande (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consommation de package

- [**dotnet ajouter package**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.
- [**dotnet supprimer package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de package à partir du fichier projet.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet. À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.
- [**variables locales de dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): répertorie les emplacements de la *global-packages*, *http-cache*, et *temp* dossiers et efface le contenu de ces dossiers.

## <a name="package-creation"></a>Création d’un package

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): crée un package NuGet avec le code. À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicable à nuget.org, Visual Studio Team Services et serveurs de NuGet par des tiers.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou retire un package à partir d’un ordinateur hôte, applicable à nuget.org, Visual Studio Team Services et serveurs de NuGet par des tiers.
