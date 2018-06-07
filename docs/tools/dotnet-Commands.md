---
title: commandes de NuGet dotnet
description: Une référence abrégée pour les commandes NuGet liées à l’aide de l’interface de ligne de commande dotnet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817012"
---
# <a name="dotnet-commands"></a><span data-ttu-id="cb4af-103">Commandes dotnet</span><span class="sxs-lookup"><span data-stu-id="cb4af-103">dotnet commands</span></span>

<span data-ttu-id="cb4af-104">Le `dotnet` interface de ligne de commande (CLI) dotnet, qui s’exécute sous Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles nuget.exe comme listé ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb4af-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="cb4af-105">Dotnet répondent à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="cb4af-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="cb4af-106">Pour plus d’informations sur `dotnet`, consultez [outils de l’interface de ligne de commande (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="cb4af-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="cb4af-107">Consommation de package</span><span class="sxs-lookup"><span data-stu-id="cb4af-107">Package consumption</span></span>

- <span data-ttu-id="cb4af-108">[**Ajouter un package dotnet**](/dotnet/core/tools/dotnet-add-package): ajoute une référence de package dans le fichier projet, puis exécute `dotnet restore` pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="cb4af-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="cb4af-109">[**dotnet supprimer le package**](/dotnet/core/tools/dotnet-remove-package): supprime une référence de package à partir du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="cb4af-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="cb4af-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaure les dépendances et les outils d’un projet.</span><span class="sxs-lookup"><span data-stu-id="cb4af-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="cb4af-111">À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="cb4af-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="cb4af-112">[**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): répertorie les emplacements de la *global-packages*, *du cache http*, et *temp* dossiers et efface le contenu de ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="cb4af-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="cb4af-113">Création d’un package</span><span class="sxs-lookup"><span data-stu-id="cb4af-113">Package creation</span></span>

- <span data-ttu-id="cb4af-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): crée un package NuGet avec le code.</span><span class="sxs-lookup"><span data-stu-id="cb4af-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="cb4af-115">À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="cb4af-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="cb4af-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): exécute un push d’un package à un serveur et le publie, applicables aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.</span><span class="sxs-lookup"><span data-stu-id="cb4af-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="cb4af-117">[**dotnet nuget supprimer**](/dotnet/core/tools/dotnet-nuget-delete): supprime ou unlists un package à partir d’un ordinateur hôte, applicable aux nuget.org, Visual Studio Team Services et serveurs de NuGet tiers.</span><span class="sxs-lookup"><span data-stu-id="cb4af-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
