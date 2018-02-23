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
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="1b0af-104">commandes dotNet</span><span class="sxs-lookup"><span data-stu-id="1b0af-104">dotNet commands</span></span>

<span data-ttu-id="1b0af-105">Le `dotnet` interface de ligne de commande, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes de nuget.exe essentiels, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1b0af-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="1b0af-106">Dotnet répondent à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="1b0af-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="1b0af-107">Pour plus d’informations sur `dotnet`, consultez [outils de l’interface de ligne de commande (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="1b0af-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="1b0af-108">Consommation de package</span><span class="sxs-lookup"><span data-stu-id="1b0af-108">Package consumption</span></span>

- <span data-ttu-id="1b0af-109">[**Ajouter un package dotnet**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package dans le fichier projet, puis exécute `dotnet restore` pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="1b0af-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="1b0af-110">[**dotnet supprimer le package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de package à partir du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="1b0af-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="1b0af-111">[**restauration de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet.</span><span class="sxs-lookup"><span data-stu-id="1b0af-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="1b0af-112">À compter de NuGet 4.0, cette commande exécute le même code que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="1b0af-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="1b0af-113">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): efface ou des listes de ressources NuGet locales telles que le cache de requête http, le cache temporaire et le dossier packages global d’échelle de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1b0af-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="1b0af-114">Création d’un package</span><span class="sxs-lookup"><span data-stu-id="1b0af-114">Package creation</span></span>

- <span data-ttu-id="1b0af-115">[**pack de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): compresse le code dans un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b0af-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="1b0af-116">À compter de NuGet 4.0, cette commande exécute le même code que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="1b0af-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="1b0af-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.</span><span class="sxs-lookup"><span data-stu-id="1b0af-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="1b0af-118">[**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un ordinateur hôte, applicable aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.</span><span class="sxs-lookup"><span data-stu-id="1b0af-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
