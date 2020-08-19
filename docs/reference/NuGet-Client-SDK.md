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
# <a name="nuget-client-sdk"></a>Kit SDK du client NuGet

Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet :

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Utilisé pour interagir avec les flux NuGet HTTP et basés sur des fichiers
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Utilisé pour interagir avec les packages NuGet. `NuGet.Protocol` dépend de ce package

Vous pouvez trouver le code source de ces packages dans le référentiel GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).

## <a name="getting-started"></a>Prise en main

### <a name="install-the-packages"></a>Installer les packages

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>Exemples

Vous trouverez ces exemples sur le projet [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) sur GitHub.

### <a name="list-package-versions"></a>Répertorier les versions de package

Recherchez toutes les versions de Newtonsoft.Jssur l’utilisation de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Télécharger un package

Téléchargez Newtonsoft.Jssur v 12.0.1 à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Obtient les métadonnées du package

Obtenir les métadonnées du package « Newtonsoft.Json » à l’aide de l' [API de métadonnées de package NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Rechercher des packages

Recherchez des packages « JSON » à l’aide de l' [API de recherche NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a>Créer un package

Créer un package, définir des métadonnées et ajouter des dépendances à l’aide de [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Il est fortement recommandé de créer des packages NuGet à l’aide des outils NuGet officiels et de **ne pas** utiliser cette API de bas niveau. Il existe plusieurs caractéristiques importantes pour un package bien formé et la dernière version des outils permet d’intégrer ces meilleures pratiques.
> 
> Pour plus d’informations sur la création de packages NuGet, consultez la vue d’ensemble du [flux de travail de création de package](../create-packages/overview-and-workflow.md) et la documentation relative aux outils à en-tête pack officiels (par exemple, [à l’aide de l’interface CLI dotnet](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Lire un package

Lire un package à partir d’un flux de fichier à l’aide de [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Documentation tierce

Vous trouverez des exemples et de la documentation pour certaines API dans la série de blogs suivante de Dave Glick, publié 2016 :

- [Exploration des bibliothèques NuGet v3, partie 1 : introduction et concepts](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploration des bibliothèques NuGet v3, partie 2 : recherche de packages](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Exploration des bibliothèques NuGet v3, partie 3 : installation de packages](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Ces billets de blog ont été écrits peu de fois après la sortie de la version **3.4.3** des packages SDK client NuGet.
> Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.

Martin Björkström a fait un billet de blog sur la série de blogs de Dave Glick, où il a introduit une approche différente sur l’utilisation du kit de développement logiciel (SDK) NuGet client pour installer les packages NuGet :

- [Réexaminer les bibliothèques NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
