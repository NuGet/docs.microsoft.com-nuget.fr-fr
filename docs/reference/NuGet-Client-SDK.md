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
# <a name="nuget-client-sdk"></a>SDK client NuGet

Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet :

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -utilisé pour interagir avec les flux NuGet http et basés sur des fichiers
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : utilisé pour interagir avec les packages NuGet. `NuGet.Protocol` dépend de ce package

Vous pouvez trouver le code source de ces packages dans le référentiel GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).

## <a name="getting-started"></a>Prise en main

### <a name="install-the-package"></a>Installer le package

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Exemples

Vous trouverez ces exemples sur le projet [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) sur GitHub.

### <a name="list-package-versions"></a>Répertorier les versions de package

Recherchez toutes les versions de Newtonsoft. JSON à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Télécharger un package

Téléchargez Newtonsoft. JSON v 12.0.1 à l’aide de l' [API de contenu du package NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Obtient les métadonnées du package

Obtenir les métadonnées du package « Newtonsoft. JSON » à l’aide de l' [API de métadonnées de package NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Rechercher des packages

Recherchez des packages « JSON » à l’aide de l' [API de recherche NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

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
