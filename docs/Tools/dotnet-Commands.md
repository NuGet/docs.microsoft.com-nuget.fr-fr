---
title: commandes de NuGet dotNet | Documents Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Une référence abrégée pour les commandes NuGet liées à l’aide de l’interface de ligne de commande dotnet.
keywords: commandes de NuGet dotnet, dotnet pack, dotnet restauration, variables locales de nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="22089-104">Les Commandes dotnet</span><span class="sxs-lookup"><span data-stu-id="22089-104">dotNet commands</span></span>

<span data-ttu-id="22089-105">Le `dotnet` interface de ligne de commande (CLI) dotnet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles nuget.exe comme listé ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="22089-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="22089-106">Dotnet répondent à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="22089-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="22089-107">Pour plus d’informations sur `dotnet`, consultez [outils de l’interface de ligne de commande (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="22089-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="22089-108">Consommation de package</span><span class="sxs-lookup"><span data-stu-id="22089-108">Package consumption</span></span>

- <span data-ttu-id="22089-109">[**Ajouter un package dotnet**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package dans le fichier projet, puis exécute `dotnet restore` pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="22089-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="22089-110">[**dotnet supprimer le package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de package à partir du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="22089-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="22089-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet.</span><span class="sxs-lookup"><span data-stu-id="22089-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="22089-112">À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="22089-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="22089-113">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): répertorie les emplacements de la *global-packages*, *du cache http*, et *temp* dossiers et efface le contenu de ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="22089-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="22089-114">Création d’un package</span><span class="sxs-lookup"><span data-stu-id="22089-114">Package creation</span></span>

- <span data-ttu-id="22089-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): crée un package NuGet avec le code.</span><span class="sxs-lookup"><span data-stu-id="22089-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="22089-116">À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="22089-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="22089-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.</span><span class="sxs-lookup"><span data-stu-id="22089-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="22089-118">[**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un ordinateur hôte, applicable aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.</span><span class="sxs-lookup"><span data-stu-id="22089-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
