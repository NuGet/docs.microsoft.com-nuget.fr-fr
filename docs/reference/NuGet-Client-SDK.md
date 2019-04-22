---
title: SDK du Client NuGet
description: L’API est en constante évolution et pas encore documenté, mais les exemples sont disponibles sur le blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911034"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="3b6d7-103">SDK du Client NuGet</span><span class="sxs-lookup"><span data-stu-id="3b6d7-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="3b6d7-104">À ne pas confondre avec le [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="3b6d7-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="3b6d7-105">Le *NuGet Client SDK* fait référence à un groupe de bibliothèques .NET centrée autour de [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), et [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="3b6d7-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="3b6d7-106">Ces packages remplacent l’ancien [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="3b6d7-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="3b6d7-107">Nous travaillons sur l’existence d’une zone de surface stable qui nous pouvons documentent bientôt.</span><span class="sxs-lookup"><span data-stu-id="3b6d7-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="3b6d7-108">Code source</span><span class="sxs-lookup"><span data-stu-id="3b6d7-108">Source code</span></span>

<span data-ttu-id="3b6d7-109">Le code source est publié sur GitHub dans le projet [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="3b6d7-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="3b6d7-110">Documentation tierce</span><span class="sxs-lookup"><span data-stu-id="3b6d7-110">Third-party documentation</span></span>

<span data-ttu-id="3b6d7-111">Vous trouverez des exemples et documentation pour certaines API dans la série du blog par Dave Glick, publié 2016 :</span><span class="sxs-lookup"><span data-stu-id="3b6d7-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="3b6d7-112">Explorer les bibliothèques NuGet v3, partie 1 : Présentation et concepts</span><span class="sxs-lookup"><span data-stu-id="3b6d7-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="3b6d7-113">Explorer les bibliothèques NuGet v3, partie 2 : Recherche des packages</span><span class="sxs-lookup"><span data-stu-id="3b6d7-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="3b6d7-114">Explorer les bibliothèques NuGet v3, partie 3 : Installation des packages</span><span class="sxs-lookup"><span data-stu-id="3b6d7-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="3b6d7-115">Ces billets de blog ont été écrits peu après le **3.4.3** version de NuGet packages du Kit de développement logiciel client ont été publiées.</span><span class="sxs-lookup"><span data-stu-id="3b6d7-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="3b6d7-116">Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.</span><span class="sxs-lookup"><span data-stu-id="3b6d7-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="3b6d7-117">Martin Björkström fait un billet de blog de suivi pour la série de blogs de Dave Glick où il présente une approche différente sur l’utilisation du kit SDK du Client NuGet pour installer les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="3b6d7-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="3b6d7-118">Nouvelle exploration des bibliothèques NuGet v3</span><span class="sxs-lookup"><span data-stu-id="3b6d7-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
