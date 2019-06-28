---
title: commandes de CLI NuGet dotnet
description: Une référence courte pour les commandes liées à NuGet à l’aide de l’interface de ligne de commande dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426005"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="94599-103">commandes CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="94599-103">dotnet CLI commands</span></span>

<span data-ttu-id="94599-104">Le `dotnet` l’interface de ligne de commande (CLI), qui s’exécute sur Windows, Mac OS X et Linux, fournit un nombre de commandes essentielles telles que l’installation, la restauration et la publication des packages.</span><span class="sxs-lookup"><span data-stu-id="94599-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="94599-105">Si dotnet répond à vos besoins, il n’est pas nécessaire d’utiliser `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="94599-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="94599-106">Pour obtenir des exemples d’utilisation de ces commandes pour consommer des packages, consultez [installer et gérer des packages à l’aide de l’interface CLI dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="94599-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="94599-107">Pour obtenir des exemples d’utilisation de ces commandes pour créer des packages, consultez [créer et publier un package à l’aide de l’interface CLI dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="94599-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="94599-108">Pour la référence de commande complète sur `dotnet` CLI, consultez [outils de l’interface de ligne de commande (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="94599-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="94599-109">Consommation de package</span><span class="sxs-lookup"><span data-stu-id="94599-109">Package consumption</span></span>

- <span data-ttu-id="94599-110">[**dotnet ajouter package**](/dotnet/core/tools/dotnet-add-package): Ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="94599-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="94599-111">[**dotnet supprimer package**](/dotnet/core/tools/dotnet-remove-package): Supprime une référence de package à partir du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="94599-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="94599-112">[**restauration de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaure les dépendances et les outils d’un projet.</span><span class="sxs-lookup"><span data-stu-id="94599-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="94599-113">À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="94599-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="94599-114">[**variables locales de dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): Répertorie les emplacements de la *global-packages*, *http-cache*, et *temp* efface le contenu de ces dossiers et les dossiers.</span><span class="sxs-lookup"><span data-stu-id="94599-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="94599-115">Création d’un package</span><span class="sxs-lookup"><span data-stu-id="94599-115">Package creation</span></span>

- <span data-ttu-id="94599-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Place le code dans un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="94599-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="94599-117">À partir de la version 4.0 de NuGet, cette commande exécute le même code que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="94599-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="94599-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Exécute un push d’un package à un serveur et le publie, applicable à nuget.org, Visual Studio Team Services et serveurs de NuGet par des tiers.</span><span class="sxs-lookup"><span data-stu-id="94599-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="94599-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Supprime ou retire un package à partir d’un ordinateur hôte, applicable à nuget.org, Visual Studio Team Services et serveurs de NuGet par des tiers.</span><span class="sxs-lookup"><span data-stu-id="94599-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
