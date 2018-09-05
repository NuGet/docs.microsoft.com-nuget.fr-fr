---
title: SDK du Client NuGet
description: L’API est en constante évolution et pas encore documenté, mais les exemples sont disponibles sur le blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8e612d9f86bcffc99870c5541aa6091e678db512
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547087"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="df3d8-103">SDK du Client NuGet</span><span class="sxs-lookup"><span data-stu-id="df3d8-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="df3d8-104">À ne pas confondre avec le [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="df3d8-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="df3d8-105">Le *NuGet Client SDK* fait référence à un groupe de bibliothèques .NET centrée autour de [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), et [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="df3d8-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="df3d8-106">Ces packages remplacent l’ancien [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="df3d8-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="df3d8-107">Nous travaillons sur l’existence d’une zone de surface stable qui nous pouvons documentent bientôt.</span><span class="sxs-lookup"><span data-stu-id="df3d8-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="df3d8-108">Code source</span><span class="sxs-lookup"><span data-stu-id="df3d8-108">Source code</span></span>

<span data-ttu-id="df3d8-109">Le code source est publié sur GitHub dans le projet [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="df3d8-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="df3d8-110">Documentation tierce</span><span class="sxs-lookup"><span data-stu-id="df3d8-110">Third-party documentation</span></span>

<span data-ttu-id="df3d8-111">Vous trouverez des exemples et documentation pour certaines API dans la série du blog par Dave Glick, publié 2016 :</span><span class="sxs-lookup"><span data-stu-id="df3d8-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="df3d8-112">Explorer les bibliothèques NuGet v3, partie 1 : présentation et concepts</span><span class="sxs-lookup"><span data-stu-id="df3d8-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="df3d8-113">Explorer les bibliothèques NuGet v3, partie 2 : recherche des packages</span><span class="sxs-lookup"><span data-stu-id="df3d8-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="df3d8-114">Explorer les bibliothèques NuGet v3, partie 3 : installation des packages</span><span class="sxs-lookup"><span data-stu-id="df3d8-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="df3d8-115">Ces billets de blog ont été écrits peu après le **3.4.3** version de NuGet packages du Kit de développement logiciel client ont été publiées.</span><span class="sxs-lookup"><span data-stu-id="df3d8-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="df3d8-116">Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.</span><span class="sxs-lookup"><span data-stu-id="df3d8-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>
