---
title: commandes de NuGet dotNet | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Une référence abrégée pour les commandes NuGet liées à l’aide de l’interface de ligne de commande dotnet."
keywords: commandes de NuGet dotnet, dotnet pack, dotnet restauration, variables locales de nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a>commandes dotNet

L’interface de ligne de commande DotNet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes de nuget.exe essentiels comme indiqué ci-dessous. Où dotnet fournit les commandes souhaitées, il n’est pas nécessaire de télécharger nuget.exe.

- [**pack de dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code NETCore SDK projets dans un package NuGet. Tous les autres types de projet doivent utiliser.[`nuget pack`](cli-ref-pack.md)
- [**restauration de dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.
- [**variables locales de nuget dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): efface ou répertorie les ressources locales de NuGet tels que http-demande de cache, cache temporaire ou dossier packages global d’échelle de l’ordinateur.
- [**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.
- [**dotnet nuget supprimer**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un serveur, applicable à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.
