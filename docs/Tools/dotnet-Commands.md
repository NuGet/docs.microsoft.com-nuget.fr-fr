---
title: commandes de NuGet dotNet | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Une référence abrégée pour les commandes NuGet liées à l’aide de l’interface de ligne de commande dotnet."
keywords: commandes de NuGet dotnet, dotnet pack, dotnet restauration, variables locales de nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: fr-FR

# <a name="dotnet-commands"></a>Les Commandes dotnet

L’interface de ligne de commande (CLI) dotnet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles nuget.exe comme listé ci-dessous. Dans le cas où le CLI dotnet répondent à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.

Pour plus d’informations sur `dotnet`, consultez [outils de l’interface de ligne de commande (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consommation de package

- [**Ajouter un package dotnet**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package dans le fichier projet, puis exécute `dotnet restore` pour installer le package.
- [**dotnet supprimer le package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de paquet à partir du fichier projet.
- [**restauration de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.
- [**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): efface ou retire des ressources NuGet locales telles que le cache de requête http, le cache temporaire et le dossier packages global d’échelle de l’ordinateur.

## <a name="package-creation"></a>Création d’un package

- [**pack de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): compresse le code dans un package NuGet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.
- [**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un ordinateur hôte, applicable aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.