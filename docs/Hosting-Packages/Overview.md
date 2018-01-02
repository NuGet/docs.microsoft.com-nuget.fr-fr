---
title: "Vue d’ensemble de l’hébergement de vos propres flux NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 97577ddd-c294-432d-81a7-b4aebe88bd1c
description: "Vue d’ensemble des possibilités d’hébergement de vos propres galeries ou flux de packages NuGet localement ou à distance."
keywords: "flux NuGet, galerie NuGet, flux de packages personnalisé, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: c3c6b17cdeb4fe959adbc56bdc6ace73202a98fc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="32cf8-104">Hébergement de vos propres flux NuGet</span><span class="sxs-lookup"><span data-stu-id="32cf8-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="32cf8-105">Plutôt que de mettre les packages à la disposition de tous, vous pouvez les réserver à un public limité, tel que votre organisation ou groupe de travail.</span><span class="sxs-lookup"><span data-stu-id="32cf8-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="32cf8-106">De plus, certaines sociétés peuvent souhaiter restreindre les bibliothèques tierces que sont susceptibles d’utiliser leurs développeurs en leur demandant de puiser dans une source de packages limitée plutôt que dans nuget.org.</span><span class="sxs-lookup"><span data-stu-id="32cf8-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="32cf8-107">À ces fins, NuGet prend en charge la configuration de sources de packages privées des façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="32cf8-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="32cf8-108">Flux local : les packages sont simplement placés sur un partage de fichiers réseau approprié, dans l’idéal, en utilisant `nuget init` et `nuget add` pour créer une structure de dossiers hiérarchique (NuGet 3.3+).</span><span class="sxs-lookup"><span data-stu-id="32cf8-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="32cf8-109">Pour plus d’informations, consultez [Flux locaux](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="32cf8-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="32cf8-110">NuGet.Server : les packages sont accessibles via un serveur HTTP local.</span><span class="sxs-lookup"><span data-stu-id="32cf8-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="32cf8-111">Pour plus d’informations, consultez [NuGet.Server](../hosting-packages/NuGet-Server.md).</span><span class="sxs-lookup"><span data-stu-id="32cf8-111">For details, see [NuGet.Server](../hosting-packages/NuGet-Server.md).</span></span>
- <span data-ttu-id="32cf8-112">Galerie NuGet : les packages sont hébergés sur un serveur Internet à l’aide du [projet de Galerie NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span><span class="sxs-lookup"><span data-stu-id="32cf8-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="32cf8-113">Avec la Galerie NuGet, gérez les utilisateurs et profitez de fonctionnalités telles qu’une interface utilisateur web complète qui permet de rechercher et d’explorer les packages à partir du navigateur, comme nuget.org.</span><span class="sxs-lookup"><span data-stu-id="32cf8-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="32cf8-114">Il existe également plusieurs autres produits d’hébergement NuGet qui prennent en charge les flux privés distants, notamment les suivants :</span><span class="sxs-lookup"><span data-stu-id="32cf8-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="32cf8-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), qui est également disponible sur Team Foundation Server 2017 et ultérieur.</span><span class="sxs-lookup"><span data-stu-id="32cf8-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="32cf8-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="32cf8-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="32cf8-117">[ProGet](http://inedo.com/proget) d’Inedo</span><span class="sxs-lookup"><span data-stu-id="32cf8-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="32cf8-118">[NuGet Server](http://nugetserver.net/) : projet communautaire d’Inedo</span><span class="sxs-lookup"><span data-stu-id="32cf8-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="32cf8-119">[NuGet Server (Open Source)](http://nuget-server.net) : implémentation open source similaire à NuGet Server d’Inedo</span><span class="sxs-lookup"><span data-stu-id="32cf8-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="32cf8-120">[Artifactory](https://www.jfrog.com/artifactory/) de JFrog</span><span class="sxs-lookup"><span data-stu-id="32cf8-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="32cf8-121">[Nexus](http://www.sonatype.org/nexus/) de Sonatype</span><span class="sxs-lookup"><span data-stu-id="32cf8-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="32cf8-122">[TeamCity](https://www.jetbrains.com/teamcity/) de JetBrains</span><span class="sxs-lookup"><span data-stu-id="32cf8-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="32cf8-123">Quelle que soit la façon dont les packages sont hébergés, vous y accédez en les ajoutant à la liste des sources disponibles dans `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="32cf8-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="32cf8-124">Vous pouvez effectuer cette opération dans Visual Studio, comme décrit dans [Sources de packages](../tools/package-manager-ui.md#package-sources), ou à partir de la ligne de commande à l’aide de [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="32cf8-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="32cf8-125">Le chemin d’une source peut être le chemin d’un dossier local, le nom d’un réseau ou une URL.</span><span class="sxs-lookup"><span data-stu-id="32cf8-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
