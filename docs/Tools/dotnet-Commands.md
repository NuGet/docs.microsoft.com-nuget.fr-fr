---
title: commandes de NuGet dotNet | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Une référence abrégée pour les commandes NuGet liées à l’aide de l’interface de ligne de commande dotnet."
keywords: commandes de NuGet dotnet, dotnet pack, dotnet restauration, variables locales de nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a>Les Commandes dotnet

L’interface de ligne de commande (CLI) dotnet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes de essentielles nuget.exe comme listé ci-dessous. Si le CLI dotnet fournit les commandes souhaitées, il n’est pas nécessaire de télécharger nuget.exe.

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): crée un package NuGet avec le code. À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget pack`.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet.À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): efface ou liste les ressources locales de NuGet tels que http requête le cache, le cache temporaire ou le dossier packages global d’échelle de l’ordinateur.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute la téléverse un package NuGet sur un serveur et le publie, applicables à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou déliste un package à partir d’un serveur, applicable à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.
