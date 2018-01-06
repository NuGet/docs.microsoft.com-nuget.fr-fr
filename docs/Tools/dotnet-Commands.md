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
# <a name="dotnet-commands"></a><span data-ttu-id="7bdad-104">commandes dotNet</span><span class="sxs-lookup"><span data-stu-id="7bdad-104">dotNet commands</span></span>

<span data-ttu-id="7bdad-105">L’interface de ligne de commande DotNet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes de nuget.exe essentiels comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7bdad-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="7bdad-106">Où dotnet fournit les commandes souhaitées, il n’est pas nécessaire de télécharger nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="7bdad-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="7bdad-107">[**pack de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): compresse le code dans un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="7bdad-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="7bdad-108">À compter de NuGet 4.0, cette commande exécute le même code que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="7bdad-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="7bdad-109">[**restauration de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet.</span><span class="sxs-lookup"><span data-stu-id="7bdad-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="7bdad-110">À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="7bdad-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="7bdad-111">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): efface ou répertorie les ressources locales de NuGet tels que http-demande de cache, cache temporaire ou dossier packages global d’échelle de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7bdad-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="7bdad-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7bdad-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="7bdad-113">[**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un serveur, applicable à tous les serveurs NuGet tiers, Visual Studio Team Services ou nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7bdad-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
