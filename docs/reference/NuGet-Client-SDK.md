---
title: SDK client NuGet
description: L’API évolue et n’est pas encore documentée, mais des exemples sont disponibles sur le blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231238"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="f0975-103">SDK client NuGet</span><span class="sxs-lookup"><span data-stu-id="f0975-103">NuGet Client SDK</span></span>

<span data-ttu-id="f0975-104">Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="f0975-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="f0975-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -utilisé pour interagir avec les flux NuGet http et basés sur des fichiers</span><span class="sxs-lookup"><span data-stu-id="f0975-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="f0975-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : utilisé pour interagir avec les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0975-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="f0975-107">`NuGet.Protocol` dépend de ce package</span><span class="sxs-lookup"><span data-stu-id="f0975-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="f0975-108">Vous pouvez trouver le code source de ces packages dans le référentiel GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="f0975-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="f0975-109">Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0975-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="f0975-110">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f0975-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="f0975-111">Installer le package</span><span class="sxs-lookup"><span data-stu-id="f0975-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="f0975-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="f0975-112">Examples</span></span>

<span data-ttu-id="f0975-113">Vous trouverez ces exemples sur le projet [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0975-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="f0975-114">Répertorier les versions de package</span><span class="sxs-lookup"><span data-stu-id="f0975-114">List package versions</span></span>

<span data-ttu-id="f0975-115">Recherchez toutes les versions de Newtonsoft. JSON à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="f0975-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="f0975-116">Télécharger un package</span><span class="sxs-lookup"><span data-stu-id="f0975-116">Download a package</span></span>

<span data-ttu-id="f0975-117">Téléchargez Newtonsoft. JSON v 12.0.1 à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="f0975-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="f0975-118">Obtient les métadonnées du package</span><span class="sxs-lookup"><span data-stu-id="f0975-118">Get package metadata</span></span>

<span data-ttu-id="f0975-119">Obtenir les métadonnées du package « Newtonsoft. JSON » à l’aide de l' [API de métadonnées de package NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="f0975-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="f0975-120">Rechercher des packages</span><span class="sxs-lookup"><span data-stu-id="f0975-120">Search packages</span></span>

<span data-ttu-id="f0975-121">Recherchez des packages « JSON » à l’aide de l' [API de recherche NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="f0975-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="f0975-122">Documentation tierce</span><span class="sxs-lookup"><span data-stu-id="f0975-122">Third-party documentation</span></span>

<span data-ttu-id="f0975-123">Vous trouverez des exemples et de la documentation pour certaines API dans la série de blogs suivante de Dave Glick, publié 2016 :</span><span class="sxs-lookup"><span data-stu-id="f0975-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="f0975-124">Exploration des bibliothèques NuGet v3, partie 1 : introduction et concepts</span><span class="sxs-lookup"><span data-stu-id="f0975-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="f0975-125">Exploration des bibliothèques NuGet v3, partie 2 : recherche de packages</span><span class="sxs-lookup"><span data-stu-id="f0975-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="f0975-126">Exploration des bibliothèques NuGet v3, partie 3 : installation de packages</span><span class="sxs-lookup"><span data-stu-id="f0975-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="f0975-127">Ces billets de blog ont été écrits peu de fois après la sortie de la version **3.4.3** des packages SDK client NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0975-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="f0975-128">Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.</span><span class="sxs-lookup"><span data-stu-id="f0975-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="f0975-129">Martin Björkström a fait un billet de blog sur la série de blogs de Dave Glick, où il a introduit une approche différente sur l’utilisation du kit de développement logiciel (SDK) NuGet client pour installer les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="f0975-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="f0975-130">Réexaminer les bibliothèques NuGet v3</span><span class="sxs-lookup"><span data-stu-id="f0975-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
