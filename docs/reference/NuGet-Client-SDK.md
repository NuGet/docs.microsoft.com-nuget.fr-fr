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
# <a name="nuget-client-sdk"></a>SDK client NuGet

Le *Kit de développement logiciel (SDK) client NuGet* fait référence à un groupe de packages NuGet centrés autour de [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)et [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Ces packages remplacent la bibliothèque [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) antérieure.

> [!Note]
>  Pour obtenir de la documentation sur le protocole serveur NuGet, consultez l' [API du serveur NuGet](~/api/overview.md).

## <a name="source-code"></a>Code source

Le code source est publié sur GitHub dans le projet [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentation tierce

Vous trouverez des exemples et de la documentation pour certaines API dans la série de blogs suivante de Dave Glick, publié 2016 :

- [Exploration des bibliothèques NuGet v3, partie 1 : introduction et concepts](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploration des bibliothèques NuGet v3, partie 2 : recherche de packages](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Exploration des bibliothèques NuGet v3, partie 3 : installation de packages](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Ces billets de blog ont été écrits peu de fois après la sortie de la version **3.4.3** des packages SDK client NuGet.
> Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.

Martin Björkström a fait un billet de blog sur la série de blogs de Dave Glick, où il présente une approche différente de l’utilisation du kit de développement logiciel (SDK) NuGet client pour l’installation des packages NuGet :

- [Réexaminer les bibliothèques NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
