---
title: Kit SDK du client NuGet
description: L’API évolue et n’est pas encore documentée, mais des exemples sont disponibles sur le blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622926"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="7e488-103">Kit SDK du client NuGet</span><span class="sxs-lookup"><span data-stu-id="7e488-103">NuGet Client SDK</span></span>

<span data-ttu-id="7e488-104">Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="7e488-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="7e488-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Utilisé pour interagir avec les flux NuGet HTTP et basés sur des fichiers</span><span class="sxs-lookup"><span data-stu-id="7e488-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="7e488-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Utilisé pour interagir avec les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="7e488-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="7e488-107">`NuGet.Protocol` dépend de ce package</span><span class="sxs-lookup"><span data-stu-id="7e488-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="7e488-108">Vous pouvez trouver le code source de ces packages dans le référentiel GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="7e488-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="7e488-109">Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e488-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="7e488-110">Prise en main</span><span class="sxs-lookup"><span data-stu-id="7e488-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="7e488-111">Installer les packages</span><span class="sxs-lookup"><span data-stu-id="7e488-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="7e488-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="7e488-112">Examples</span></span>

<span data-ttu-id="7e488-113">Vous trouverez ces exemples sur le projet [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="7e488-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="7e488-114">Répertorier les versions de package</span><span class="sxs-lookup"><span data-stu-id="7e488-114">List package versions</span></span>

<span data-ttu-id="7e488-115">Recherchez toutes les versions de Newtonsoft.Jssur l’utilisation de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="7e488-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="7e488-116">Télécharger un package</span><span class="sxs-lookup"><span data-stu-id="7e488-116">Download a package</span></span>

<span data-ttu-id="7e488-117">Téléchargez Newtonsoft.Jssur v 12.0.1 à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="7e488-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="7e488-118">Obtient les métadonnées du package</span><span class="sxs-lookup"><span data-stu-id="7e488-118">Get package metadata</span></span>

<span data-ttu-id="7e488-119">Obtenir les métadonnées du package « Newtonsoft.Json » à l’aide de l' [API de métadonnées de package NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="7e488-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="7e488-120">Rechercher des packages</span><span class="sxs-lookup"><span data-stu-id="7e488-120">Search packages</span></span>

<span data-ttu-id="7e488-121">Recherchez des packages « JSON » à l’aide de l' [API de recherche NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="7e488-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="7e488-122">Créer un package</span><span class="sxs-lookup"><span data-stu-id="7e488-122">Create a package</span></span>

<span data-ttu-id="7e488-123">Créer un package, définir des métadonnées et ajouter des dépendances à l’aide de [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="7e488-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e488-124">Il est fortement recommandé de créer des packages NuGet à l’aide des outils NuGet officiels et de **ne pas** utiliser cette API de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="7e488-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="7e488-125">Il existe plusieurs caractéristiques importantes pour un package bien formé et la dernière version des outils permet d’intégrer ces meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="7e488-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="7e488-126">Pour plus d’informations sur la création de packages NuGet, consultez la vue d’ensemble du [flux de travail de création de package](../create-packages/overview-and-workflow.md) et la documentation relative aux outils à en-tête pack officiels (par exemple, [à l’aide de l’interface CLI dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="7e488-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="7e488-127">Lire un package</span><span class="sxs-lookup"><span data-stu-id="7e488-127">Read a package</span></span>

<span data-ttu-id="7e488-128">Lire un package à partir d’un flux de fichier à l’aide de [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="7e488-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="7e488-129">Documentation tierce</span><span class="sxs-lookup"><span data-stu-id="7e488-129">Third-party documentation</span></span>

<span data-ttu-id="7e488-130">Vous trouverez des exemples et de la documentation pour certaines API dans la série de blogs suivante de Dave Glick, publié 2016 :</span><span class="sxs-lookup"><span data-stu-id="7e488-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="7e488-131">Exploration des bibliothèques NuGet v3, partie 1 : introduction et concepts</span><span class="sxs-lookup"><span data-stu-id="7e488-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="7e488-132">Exploration des bibliothèques NuGet v3, partie 2 : recherche de packages</span><span class="sxs-lookup"><span data-stu-id="7e488-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="7e488-133">Exploration des bibliothèques NuGet v3, partie 3 : installation de packages</span><span class="sxs-lookup"><span data-stu-id="7e488-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="7e488-134">Ces billets de blog ont été écrits peu de fois après la sortie de la version **3.4.3** des packages SDK client NuGet.</span><span class="sxs-lookup"><span data-stu-id="7e488-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="7e488-135">Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.</span><span class="sxs-lookup"><span data-stu-id="7e488-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="7e488-136">Martin Björkström a fait un billet de blog sur la série de blogs de Dave Glick, où il a introduit une approche différente sur l’utilisation du kit de développement logiciel (SDK) NuGet client pour installer les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="7e488-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="7e488-137">Réexaminer les bibliothèques NuGet v3</span><span class="sxs-lookup"><span data-stu-id="7e488-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
