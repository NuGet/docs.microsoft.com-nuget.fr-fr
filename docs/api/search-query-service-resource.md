---
title: Recherche, API NuGet
description: Le service de recherche permet aux clients d’interroger des packages par mot clé et de filtrer les résultats sur certains champs de package.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235123"
---
# <a name="search"></a>Rechercher

Il est possible de rechercher des packages disponibles sur une source de package à l’aide de l’API V3. La ressource utilisée pour la recherche est `SearchQueryService` la ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les valeurs `@type` suivantes sont utilisées :

Valeur@type                   | Notes
----------------------------- | -----
SearchQueryService            | La version initiale
SearchQueryService/3.0.0-bêta | Alias de`SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias de`SearchQueryService`

## <a name="base-url"></a>URL de base

L’URL de base de l’API suivante est la valeur de `@id` la propriété associée à l’une des valeurs `@type` de ressource mentionnées ci-dessus. Dans le document suivant, l’URL `{@id}` de base de l’espace réservé sera utilisée.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource d’inscription prennent en `GET` charge `HEAD`les méthodes http et.

## <a name="search-for-packages"></a>Rechercher des packages

L’API de recherche permet à un client de demander une page de packages correspondant à une requête de recherche spécifiée. L’interprétation de la requête de recherche (par exemple, la création de jetons des termes de recherche) est déterminée par l’implémentation du serveur, mais l’attente générale est que la requête de recherche est utilisée pour faire correspondre des ID de package, des titres, des descriptions et des balises. D’autres champs de métadonnées de package peuvent également être pris en compte.

Un package non répertorié ne doit jamais apparaître dans les résultats de la recherche.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Name        | Dans     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Non       | Termes de recherche à utiliser pour filtrer les packages
skip        | URL    | integer | Non       | Nombre de résultats à ignorer pour la pagination
prendre        | URL    | integer | Non       | Nombre de résultats à retourner, pour la pagination
version préliminaire  | URL    | booléenne | Non       | `true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion
semVerLevel | URL    | string  | Non       | Chaîne de version SemVer 1.0.0 

La requête `q` de recherche est analysée d’une manière définie par l’implémentation du serveur. nuget.org prend en charge le filtrage de base sur un [large éventail de champs](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si aucun `q` package n’est fourni, tous les packages doivent être retournés, dans les limites imposées par Skip et Take. Cela active l’onglet « Parcourir » dans l’expérience NuGet Visual Studio.

La `skip` valeur par défaut du paramètre est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de s’abonner à des [packages SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, seuls les packages avec des versions compatibles SemVer 1.0.0 sont retournés (avec les avertissements de [version NuGet standard](../concepts/package-versioning.md) , tels que les chaînes de version avec 4 éléments entiers).
Si `semVerLevel=2.0.0` est fourni, les packages compatibles SemVer 1.0.0 et SemVer 2.0.0 sont retournés. Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>response

La réponse est un document JSON contenant les `take` résultats de recherche. Les résultats de la recherche sont regroupés par ID de package.

L’objet JSON racine a les propriétés suivantes :

Name      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
totalHits | integer          | oui      | Nombre total de correspondances, à l' `skip` égard de et`take`
data      | Tableau d’objets | oui      | Résultats de la recherche correspondant à la requête

### <a name="search-result"></a>Résultat de la recherche

Chaque élément `data` du tableau est un objet JSON constitué d’un groupe de versions de packages partageant le même ID de package.
L’objet a les propriétés suivantes :

Name           | Type                       | Obligatoire | Notes
-------------- | -------------------------- | -------- | -----
id             | string                     | oui      | ID du package mis en correspondance
version        | string                     | oui      | La chaîne de version SemVer 2.0.0 complète du package (peut contenir des métadonnées de Build)
description    | string                     | Non       | 
versions       | Tableau d’objets           | oui      | Toutes les versions du package correspondant au `prerelease` paramètre
authors        | chaîne ou tableau de chaînes | Non       | 
iconUrl        | string                     | Non       | 
licenseUrl     | string                     | Non       | 
owners         | chaîne ou tableau de chaînes | Non       | 
projectUrl     | string                     | Non       | 
inscription   | string                     | Non       | URL absolue de l' [index d’inscription](registration-base-url-resource.md#registration-index) associé
résumé        | string                     | Non       | 
balises           | chaîne ou tableau de chaînes | Non       | 
title          | string                     | Non       | 
totalDownloads | integer                    | Non       | Cette valeur peut être déduite par la somme des téléchargements dans `versions` le tableau.
verifi       | booléenne                    | Non       | Valeur booléenne JSON indiquant si le package est [vérifié](../nuget-org/id-prefix-reservation.md)

Sur nuget.org, un package vérifié est un package dont l’ID de package correspond à un préfixe d’ID réservé et qui appartient à l’un des propriétaires du préfixe réservé. Pour plus d’informations, consultez la [documentation relative à la réservation du préfixe d’ID](../reference/id-prefix-reservation.md).

Les métadonnées contenues dans l’objet de résultat de la recherche proviennent de la dernière version du package. Chaque élément `versions` du tableau est un objet JSON avec les propriétés suivantes :

Nom      | Type    | Obligatoire | Notes
--------- | ------- | -------- | -----
@id       | string  | oui      | URL absolue de la [feuille d’inscription](registration-base-url-resource.md#registration-leaf) associée
version   | string  | oui      | La chaîne de version SemVer 2.0.0 complète du package (peut contenir des métadonnées de Build)
disponibles | integer | oui      | Nombre de téléchargements pour cette version de package spécifique

### <a name="sample-request"></a>Exemple de requête

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [search-result.json](./_data/search-result.json)]
