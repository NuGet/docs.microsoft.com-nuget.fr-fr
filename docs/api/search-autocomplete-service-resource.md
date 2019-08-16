---
title: Saisie semi-automatique, API NuGet
description: Le service de saisie semi-automatique de la recherche prend en charge la découverte interactive des ID de package et des versions.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488307"
---
# <a name="autocomplete"></a>Saisie semi-automatique

Il est possible de générer un ID de package et une expérience de saisie semi-automatique de version à l’aide de l’API V3. La ressource utilisée pour effectuer des requêtes de saisie semi `SearchAutocompleteService` -automatique est la ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les valeurs `@type` suivantes sont utilisées:

Valeur@type                          | Notes
------------------------------------ | -----
SearchAutocompleteService            | La version initiale
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias de`SearchAutocompleteService`

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de `@id` la propriété associée à l’une des valeurs `@type` de ressource mentionnées ci-dessus. Dans le document suivant, l’URL `{@id}` de base de l’espace réservé sera utilisée.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource d’inscription prennent en `GET` charge `HEAD`les méthodes http et.

## <a name="search-for-package-ids"></a>Rechercher des ID de package

La première API de saisie semi-automatique prend en charge la recherche d’une partie d’une chaîne d’ID de package. C’est très utile lorsque vous souhaitez fournir une fonctionnalité TypeAhead de package dans une interface utilisateur intégrée à une source de package NuGet.

Un package avec uniquement des versions non répertoriées n’apparaît pas dans les résultats.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Dans     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Non       | Chaîne à comparer aux ID de package
skip        | URL    | integer | Non       | Nombre de résultats à ignorer pour la pagination
prendre        | URL    | integer | Non       | Nombre de résultats à retourner, pour la pagination
version préliminaire  | URL    | booléenne | Non       | `true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion
semVerLevel | URL    | string  | Non       | Chaîne de version SemVer 1.0.0 

La requête `q` de saisie semi-automatique est analysée d’une manière définie par l’implémentation du serveur. nuget.org prend en charge l’interrogation du préfixe des jetons d’ID de package, qui sont des éléments de l’ID produit par le fractionnement de la casse et des caractères de symboles mixtes originaux.

La `skip` valeur par défaut du paramètre est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de s’abonner à des [packages SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, seuls les ID de package avec des versions compatibles SemVer 1.0.0 sont retournés (avec les avertissements de [version NuGet standard](../concepts/package-versioning.md) , tels que les chaînes de version avec 4 éléments entiers).
Si `semVerLevel=2.0.0` est fourni, les packages compatibles SemVer 1.0.0 et SemVer 2.0.0 sont retournés. Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>response

La réponse est un document JSON contenant des `take` résultats de saisie semi-automatique.

L’objet JSON racine a les propriétés suivantes:

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
totalHits | integer          | oui      | Nombre total de correspondances, à l' `skip` égard de et`take`
data      | Tableau de chaînes | oui      | ID de package correspondants à la requête

### <a name="sample-request"></a>Exemple de requête

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Énumérer les versions du package

Une fois qu’un ID de package est découvert à l’aide de l’API précédente, un client peut utiliser l’API de saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.

Une version de package non listée n’apparaît pas dans les résultats.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Name        | Dans     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | oui      | ID de package pour lequel extraire les versions
version préliminaire  | URL    | booléenne | Non       | `true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion
semVerLevel | URL    | string  | Non       | Une chaîne de version SemVer 2.0.0 

Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de s’abonner à des packages SemVer 2.0.0. Si ce paramètre de requête est exclu, seules les versions de SemVer 1.0.0 sont retournées. Si `semVerLevel=2.0.0` est fourni, les versions SemVer 1.0.0 et SemVer 2.0.0 sont retournées. Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>response

La réponse est un document JSON contenant toutes les versions de package de l’ID de package fourni, en filtrant par les paramètres de requête donnés.

L’objet JSON racine a la propriété suivante:

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
data      | Tableau de chaînes | oui      | Versions du package correspondant à la requête

Les versions de package dans `data` le tableau peuvent contenir des métadonnées de build SemVer `1.0.0+metadata`2.0.0 (par `semVerLevel=2.0.0` exemple,) si le est fourni dans la chaîne de requête.

### <a name="sample-request"></a>Exemple de requête

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
