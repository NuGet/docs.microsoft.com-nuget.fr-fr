---
title: commandes de NuGet dotnet
description: Une référence abrégée pour les commandes NuGet liées à l’aide de l’interface de ligne de commande dotnet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a>Commandes dotnet

Le `dotnet` interface de ligne de commande (CLI) dotnet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles nuget.exe comme listé ci-dessous. Dotnet répondent à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.

Pour plus d’informations sur `dotnet`, consultez [outils de l’interface de ligne de commande (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consommation de package

- [**Ajouter un package dotnet**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package dans le fichier projet, puis exécute `dotnet restore` pour installer le package.
- [**dotnet supprimer le package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de package à partir du fichier projet.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet. À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.
- [**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): répertorie les emplacements de la *global-packages*, *du cache http*, et *temp* dossiers et efface le contenu de ces dossiers.

## <a name="package-creation"></a>Création d’un package

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): crée un package NuGet avec le code. À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.
- [**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un ordinateur hôte, applicable aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.
