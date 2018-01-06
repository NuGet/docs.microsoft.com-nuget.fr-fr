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
ms.openlocfilehash: d020e62b8bd04c8f4a75756fb30ebcf13ffdb1b3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="dotnet-commands"></a>commandes dotNet

L’interface de ligne de commande DotNet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes de nuget.exe essentiels comme indiqué ci-dessous. Où dotnet fournit les commandes souhaitées, il n’est pas nécessaire de télécharger nuget.exe.

- [**pack de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): compresse le code dans un package NuGet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget pack`.
- [**restauration de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet. À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.
- [**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): efface ou répertorie les ressources locales de NuGet tels que http-demande de cache, cache temporaire ou dossier packages global d’échelle de l’ordinateur.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.
- [**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un serveur, applicable à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.
