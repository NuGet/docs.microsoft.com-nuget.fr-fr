---
title: SDK client NuGet
description: L’API évolue et n’est pas encore documentée, mais des exemples sont disponibles sur le blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924604"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="7fc25-103">SDK client NuGet</span><span class="sxs-lookup"><span data-stu-id="7fc25-103">NuGet Client SDK</span></span>

<span data-ttu-id="7fc25-104">Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet centrés autour de [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)et [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="7fc25-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="7fc25-105">Ces packages remplacent la bibliothèque [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) antérieure.</span><span class="sxs-lookup"><span data-stu-id="7fc25-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="7fc25-106">Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="7fc25-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="7fc25-107">Code source</span><span class="sxs-lookup"><span data-stu-id="7fc25-107">Source code</span></span>

<span data-ttu-id="7fc25-108">Le code source est publié sur GitHub dans le projet [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="7fc25-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="7fc25-109">Documentation tierce</span><span class="sxs-lookup"><span data-stu-id="7fc25-109">Third-party documentation</span></span>

<span data-ttu-id="7fc25-110">Vous trouverez des exemples et de la documentation pour certaines API dans la série de blogs suivante de Dave Glick, publié 2016 :</span><span class="sxs-lookup"><span data-stu-id="7fc25-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="7fc25-111">Exploration des bibliothèques NuGet v3, partie 1 : introduction et concepts</span><span class="sxs-lookup"><span data-stu-id="7fc25-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="7fc25-112">Exploration des bibliothèques NuGet v3, partie 2 : recherche de packages</span><span class="sxs-lookup"><span data-stu-id="7fc25-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="7fc25-113">Exploration des bibliothèques NuGet v3, partie 3 : installation de packages</span><span class="sxs-lookup"><span data-stu-id="7fc25-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="7fc25-114">Ces billets de blog ont été écrits peu de fois après la sortie de la version **3.4.3** des packages SDK client NuGet.</span><span class="sxs-lookup"><span data-stu-id="7fc25-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="7fc25-115">Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.</span><span class="sxs-lookup"><span data-stu-id="7fc25-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="7fc25-116">Martin Björkström a fait un billet de blog sur la série de blogs de Dave Glick, où il présente une approche différente de l’utilisation du kit de développement logiciel (SDK) NuGet client pour l’installation des packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="7fc25-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="7fc25-117">Réexaminer les bibliothèques NuGet v3</span><span class="sxs-lookup"><span data-stu-id="7fc25-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
