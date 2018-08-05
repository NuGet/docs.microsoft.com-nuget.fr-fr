---
title: SDK du Client NuGet
description: L’API est en constante évolution et pas encore documenté, mais les exemples sont disponibles sur le blog de Dave Glick.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: f814b0c0e7fac719e4221a8d8e945de703348aba
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508060"
---
# <a name="nuget-client-sdk"></a>SDK du Client NuGet

> [!Note]
> À ne pas confondre avec le [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

Le *NuGet Client SDK* fait référence à un groupe de bibliothèques .NET centrée autour de [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), et [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Ces packages remplacent l’ancien [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) bibliothèque.

Nous travaillons sur l’existence d’une zone de surface stable qui nous pouvons documentent bientôt.

## <a name="source-code"></a>Code source

Le code source est publié sur GitHub dans le projet [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentation tierce

Vous trouverez des exemples et documentation pour certaines API dans la série du blog par Dave Glick, publié 2016 :

- [Explorer les bibliothèques NuGet v3, partie 1 : présentation et concepts](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Explorer les bibliothèques NuGet v3, partie 2 : recherche des packages](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Explorer les bibliothèques NuGet v3, partie 3 : installation des packages](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Ces billets de blog ont été écrits peu après le **3.4.3** version de NuGet packages du Kit de développement logiciel client ont été publiées.
> Les versions plus récentes des packages peuvent être incompatibles avec les informations contenues dans les billets de blog.
