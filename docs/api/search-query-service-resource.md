---
title: Recherche, API NuGet
description: Le service de recherche permet aux clients d’interroger des packages par mot clé et de filtrer les résultats sur certains champs de package.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aed591ceba00f1820a573eacf312112db0a1c69e
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292270"
---
# <a name="search"></a>Recherche

Il est possible de rechercher des packages disponibles sur une source de package à l’aide de l’API V3. La ressource utilisée pour la recherche est la `SearchQueryService` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Contrôle de version

Les `@type` valeurs suivantes sont utilisées :

Valeur @type                   | Notes
----------------------------- | -----
SearchQueryService            | La version initiale
SearchQueryService/3.0.0-bêta | Alias de`SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias de`SearchQueryService`
SearchQueryService/3.5.0      | Prend en charge le `packageType` paramètre de requête

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Cette version introduit la prise en charge du `packageType` paramètre de requête et de la `packageTypes` propriété de réponse, ce qui permet de filtrer les types de packages définis par l’auteur. Elle est entièrement compatible avec les requêtes à `SearchQueryService` .

## <a name="base-url"></a>URL de base

L’URL de base de l’API suivante est la valeur de la `@id` propriété associée à l’une des valeurs de ressource mentionnées ci-dessus `@type` . Dans le document suivant, l’URL de base de l’espace réservé `{@id}` sera utilisée.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource d’inscription prennent en charge les méthodes HTTP `GET` et `HEAD` .

## <a name="search-for-packages"></a>Rechercher des packages

L’API de recherche permet à un client de demander une page de packages correspondant à une requête de recherche spécifiée. L’interprétation de la requête de recherche (par exemple, la création de jetons des termes de recherche) est déterminée par l’implémentation du serveur, mais l’attente générale est que la requête de recherche est utilisée pour faire correspondre des ID de package, des titres, des descriptions et des balises. D’autres champs de métadonnées de package peuvent également être pris en compte.

Un package non répertorié ne doit jamais apparaître dans les résultats de la recherche.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Dans     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | non       | Termes de recherche à utiliser pour filtrer les packages
skip        | URL    | entier | non       | Nombre de résultats à ignorer pour la pagination
take        | URL    | entier | non       | Nombre de résultats à retourner, pour la pagination
prerelease  | URL    | boolean | non       | `true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion
semVerLevel | URL    | string  | non       | Chaîne de version SemVer 1.0.0 
packageType | URL    | string  | non       | Type de package à utiliser pour filtrer les packages (ajouté dans `SearchQueryService/3.5.0` )

La requête `q` de recherche est analysée d’une manière définie par l’implémentation du serveur. nuget.org prend en charge le filtrage de base sur un [large éventail de champs](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si aucun `q` package n’est fourni, tous les packages doivent être retournés, dans les limites imposées par Skip et Take. Cela active l’onglet « Parcourir » dans l’expérience NuGet Visual Studio.

La `skip` valeur par défaut du paramètre est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de s’abonner à des [packages SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, seuls les packages avec des versions compatibles SemVer 1.0.0 sont retournés (avec les avertissements de [version NuGet standard](../concepts/package-versioning.md) , tels que les chaînes de version avec 4 éléments entiers).
Si `semVerLevel=2.0.0` est fourni, les packages compatibles SemVer 1.0.0 et SemVer 2.0.0 sont retournés. Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Le `packageType` paramètre est utilisé pour filtrer les résultats de la recherche uniquement sur les packages qui ont au moins un type de package correspondant au nom du type de package.
Si le type de package fourni n’est pas un type de package valide tel que défini par le [document de type de package](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), un résultat vide est retourné.
Si le type de package fourni est vide, aucun filtre n’est appliqué. En d’autres termes, le passage d’aucune valeur au paramètre packageType se comporte comme si le paramètre n’était pas passé.

### <a name="response"></a>response

La réponse est un document JSON contenant les `take` résultats de recherche. Les résultats de la recherche sont regroupés par ID de package.

L’objet JSON racine a les propriétés suivantes :

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
totalHits | entier          | oui      | Nombre total de correspondances, à l’égard de `skip` et`take`
data      | tableau d’objets | oui      | Résultats de la recherche correspondant à la requête

### <a name="search-result"></a>Résultat de la recherche

Chaque élément du `data` tableau est un objet JSON constitué d’un groupe de versions de packages partageant le même ID de package.
L'objet a les propriétés suivantes :

Nom           | Type                       | Obligatoire | Notes
-------------- | -------------------------- | -------- | -----
id             | string                     | oui      | ID du package mis en correspondance
version        | string                     | oui      | La chaîne de version SemVer 2.0.0 complète du package (peut contenir des métadonnées de Build)
description    | string                     | non       | 
versions       | tableau d’objets           | oui      | Toutes les versions du package correspondant au `prerelease` paramètre
authors        | chaîne ou tableau de chaînes | non       | 
iconUrl        | string                     | non       | 
licenseUrl     | string                     | non       | 
owners         | chaîne ou tableau de chaînes | non       | 
projectUrl     | string                     | non       | 
inscription   | string                     | non       | URL absolue de l' [index d’inscription](registration-base-url-resource.md#registration-index) associé
summary        | string                     | non       | 
tags           | chaîne ou tableau de chaînes | non       | 
title          | string                     | non       | 
totalDownloads | entier                    | non       | Cette valeur peut être déduite par la somme des téléchargements dans le `versions` tableau.
verifi       | boolean                    | non       | Valeur booléenne JSON indiquant si le package est [vérifié](../nuget-org/id-prefix-reservation.md)
packageTypes   | tableau d’objets           | oui      | Types de packages définis par l’auteur du package (ajouté dans `SearchQueryService/3.5.0` )

Sur nuget.org, un package vérifié est un package dont l’ID de package correspond à un préfixe d’ID réservé et qui appartient à l’un des propriétaires du préfixe réservé. Pour plus d’informations, consultez la [documentation relative à la réservation du préfixe d’ID](../reference/id-prefix-reservation.md).

Les métadonnées contenues dans l’objet de résultat de la recherche proviennent de la dernière version du package. Chaque élément du `versions` tableau est un objet JSON avec les propriétés suivantes :

Nom      | Type    | Obligatoire | Notes
--------- | ------- | -------- | -----
@id       | string  | oui      | URL absolue de la [feuille d’inscription](registration-base-url-resource.md#registration-leaf) associée
version   | string  | oui      | La chaîne de version SemVer 2.0.0 complète du package (peut contenir des métadonnées de Build)
disponibles | entier | oui      | Nombre de téléchargements pour cette version de package spécifique

Le `packageTypes` tableau se compose toujours d’au moins un élément (1). Le type de package d’un ID de package donné est considéré comme les types de packages définis par la dernière version du package par rapport aux autres paramètres de recherche. Chaque élément du `packageTypes` tableau est un objet JSON avec les propriétés suivantes :

Nom      | Type    | Obligatoire | Notes
--------- | ------- | -------- | -----
name      | string  | oui      | Nom du type de package.

### <a name="sample-request"></a>Exemple de requête

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [search-result.json](./_data/search-result.json)]
