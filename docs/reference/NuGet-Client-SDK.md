---
title: Kit SDK du client NuGet
description: L’API évolue et n’est pas encore documentée, mais des exemples sont disponibles sur le blog de Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387385"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="8efe6-103">Kit SDK du client NuGet</span><span class="sxs-lookup"><span data-stu-id="8efe6-103">NuGet Client SDK</span></span>

<span data-ttu-id="8efe6-104">Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="8efe6-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="8efe6-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Utilisé pour interagir avec les flux NuGet HTTP et basés sur des fichiers</span><span class="sxs-lookup"><span data-stu-id="8efe6-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="8efe6-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Utilisé pour interagir avec les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="8efe6-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="8efe6-107">`NuGet.Protocol` dépend de ce package</span><span class="sxs-lookup"><span data-stu-id="8efe6-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="8efe6-108">Vous pouvez trouver le code source de ces packages dans le référentiel GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="8efe6-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="8efe6-109">Vous pouvez trouver le code source de ces exemples sur le projet [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="8efe6-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="8efe6-110">Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="8efe6-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="8efe6-111">NuGet. Protocole</span><span class="sxs-lookup"><span data-stu-id="8efe6-111">NuGet.Protocol</span></span>

<span data-ttu-id="8efe6-112">Installez le `NuGet.Protocol` package pour interagir avec les flux de package NUGET http et basés sur les dossiers :</span><span class="sxs-lookup"><span data-stu-id="8efe6-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="8efe6-113">`Repository.Factory` est défini dans l' `NuGet.Protocol.Core.Types` espace de noms, et la `GetCoreV3` méthode est une méthode d’extension définie dans l' `NuGet.Protocol` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="8efe6-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="8efe6-114">Par conséquent, vous devrez ajouter `using` des instructions pour les deux espaces de noms.</span><span class="sxs-lookup"><span data-stu-id="8efe6-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="8efe6-115">Répertorier les versions de package</span><span class="sxs-lookup"><span data-stu-id="8efe6-115">List package versions</span></span>

<span data-ttu-id="8efe6-116">Recherchez toutes les versions de Newtonsoft.Jssur l’utilisation de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="8efe6-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="8efe6-117">Télécharger un package</span><span class="sxs-lookup"><span data-stu-id="8efe6-117">Download a package</span></span>

<span data-ttu-id="8efe6-118">Téléchargez Newtonsoft.Jssur v 12.0.1 à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8efe6-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="8efe6-119">Obtient les métadonnées du package</span><span class="sxs-lookup"><span data-stu-id="8efe6-119">Get package metadata</span></span>

<span data-ttu-id="8efe6-120">Obtenir les métadonnées du package « Newtonsoft.Json » à l’aide de l' [API de métadonnées de package NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8efe6-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="8efe6-121">Rechercher des packages</span><span class="sxs-lookup"><span data-stu-id="8efe6-121">Search packages</span></span>

<span data-ttu-id="8efe6-122">Recherchez des packages « JSON » à l’aide de l' [API de recherche NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8efe6-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="8efe6-123">Envoyer (push) un package</span><span class="sxs-lookup"><span data-stu-id="8efe6-123">Push a package</span></span>

<span data-ttu-id="8efe6-124">Transmettre un package à l’aide de l' [API de push et de suppression NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8efe6-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="8efe6-125">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="8efe6-125">Delete a package</span></span>

<span data-ttu-id="8efe6-126">Supprimer un package à l’aide de l' [API de push et de suppression NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="8efe6-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="8efe6-127">Les serveurs NuGet sont libres d’interpréter une demande de suppression de package en tant que « suppression forcée », « suppression réversible » ou « supprimer la liste ».</span><span class="sxs-lookup"><span data-stu-id="8efe6-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="8efe6-128">Par exemple, nuget.org interprète la demande de suppression du package comme une « annulation de la liste ».</span><span class="sxs-lookup"><span data-stu-id="8efe6-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="8efe6-129">Pour plus d’informations sur cette pratique, consultez la stratégie [Suppression de packages](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="8efe6-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="8efe6-130">Utiliser des flux authentifiés</span><span class="sxs-lookup"><span data-stu-id="8efe6-130">Work with authenticated feeds</span></span>

<span data-ttu-id="8efe6-131">Utilisez [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) pour travailler avec des flux authentifiés.</span><span class="sxs-lookup"><span data-stu-id="8efe6-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="8efe6-132">NuGet. Packaging</span><span class="sxs-lookup"><span data-stu-id="8efe6-132">NuGet.Packaging</span></span>

<span data-ttu-id="8efe6-133">Installez le `NuGet.Packaging` package pour interagir avec `.nupkg` les `.nuspec` fichiers et à partir d’un flux :</span><span class="sxs-lookup"><span data-stu-id="8efe6-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="8efe6-134">Créer un package</span><span class="sxs-lookup"><span data-stu-id="8efe6-134">Create a package</span></span>

<span data-ttu-id="8efe6-135">Créer un package, définir des métadonnées et ajouter des dépendances à l’aide de [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="8efe6-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8efe6-136">Il est fortement recommandé de créer des packages NuGet à l’aide des outils NuGet officiels et de **ne pas** utiliser cette API de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="8efe6-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="8efe6-137">Il existe plusieurs caractéristiques importantes pour un package bien formé et la dernière version des outils permet d’intégrer ces meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="8efe6-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="8efe6-138">Pour plus d’informations sur la création de packages NuGet, consultez la vue d’ensemble du [flux de travail de création de package](../create-packages/overview-and-workflow.md) et la documentation relative aux outils à en-tête pack officiels (par exemple, [à l’aide de l’interface CLI dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="8efe6-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="8efe6-139">Lire un package</span><span class="sxs-lookup"><span data-stu-id="8efe6-139">Read a package</span></span>

<span data-ttu-id="8efe6-140">Lire un package à partir d’un flux de fichier à l’aide de [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="8efe6-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="8efe6-141">Documentation tierce</span><span class="sxs-lookup"><span data-stu-id="8efe6-141">Third-party documentation</span></span>

<span data-ttu-id="8efe6-142">Vous trouverez des exemples et de la documentation pour certaines API dans la série de blogs suivante de Dave Glick, publié 2016 :</span><span class="sxs-lookup"><span data-stu-id="8efe6-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="8efe6-143">Exploration des bibliothèques NuGet v3, partie 1 : introduction et concepts</span><span class="sxs-lookup"><span data-stu-id="8efe6-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="8efe6-144">Exploration des bibliothèques NuGet v3, partie 2 : recherche de packages</span><span class="sxs-lookup"><span data-stu-id="8efe6-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="8efe6-145">Exploration des bibliothèques NuGet v3, partie 3 : installation de packages</span><span class="sxs-lookup"><span data-stu-id="8efe6-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="8efe6-146">Ces billets de blog ont été écrits peu de fois après la sortie de la version **3.4.3** des packages SDK client NuGet.</span><span class="sxs-lookup"><span data-stu-id="8efe6-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="8efe6-147">Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.</span><span class="sxs-lookup"><span data-stu-id="8efe6-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="8efe6-148">Martin Björkström a fait un billet de blog sur la série de blogs de Dave Glick, où il a introduit une approche différente sur l’utilisation du kit de développement logiciel (SDK) NuGet client pour installer les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="8efe6-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="8efe6-149">Réexaminer les bibliothèques NuGet v3</span><span class="sxs-lookup"><span data-stu-id="8efe6-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
