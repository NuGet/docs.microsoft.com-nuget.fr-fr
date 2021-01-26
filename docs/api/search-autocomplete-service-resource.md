---
title: Saisie semi-automatique, API NuGet
description: Le service de saisie semi-automatique de la recherche prend en charge la découverte interactive des ID de package et des versions.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773958"
---
# <a name="autocomplete"></a>Autocomplétion

Il est possible de générer un ID de package et une expérience de saisie semi-automatique de version à l’aide de l’API V3. La ressource utilisée pour effectuer des requêtes de saisie semi-automatique est la `SearchAutocompleteService` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Contrôle de version

Les `@type` valeurs suivantes sont utilisées :

Valeur @type                          | Notes
------------------------------------ | -----
SearchAutocompleteService            | La version initiale
SearchAutocompleteService/3.0.0-bêta | Alias de `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias de `SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Prend en charge le `packageType` paramètre de requête

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Cette version introduit la prise en charge du `packageType` paramètre de requête, ce qui permet de filtrer les types de packages définis par l’auteur. Elle est entièrement compatible avec les requêtes à `SearchAutocompleteService` .

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à l’une des valeurs de ressource mentionnées ci-dessus `@type` . Dans le document suivant, l’URL de base de l’espace réservé `{@id}` sera utilisée.

## <a name="http-methods"></a>HTTP Methods

Toutes les URL trouvées dans la ressource d’inscription prennent en charge les méthodes HTTP `GET` et `HEAD` .

## <a name="search-for-package-ids"></a>Rechercher des ID de package

La première API de saisie semi-automatique prend en charge la recherche d’une partie d’une chaîne d’ID de package. C’est très utile lorsque vous souhaitez fournir une fonctionnalité TypeAhead de package dans une interface utilisateur intégrée à une source de package NuGet.

Un package avec uniquement des versions non répertoriées n’apparaît pas dans les résultats.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Dans     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | non       | Chaîne à comparer aux ID de package
skip        | URL    | entier | non       | Nombre de résultats à ignorer pour la pagination
take        | URL    | entier | non       | Nombre de résultats à retourner, pour la pagination
prerelease  | URL    | boolean | non       | `true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion
semVerLevel | URL    | string  | non       | Chaîne de version SemVer 1.0.0 
packageType | URL    | string  | non       | Type de package à utiliser pour filtrer les packages (ajouté dans `SearchAutocompleteService/3.5.0` )

La requête de saisie semi-automatique `q` est analysée d’une manière définie par l’implémentation du serveur. nuget.org prend en charge l’interrogation du préfixe des jetons d’ID de package, qui sont des éléments de l’ID produit par le fractionnement de la casse et des caractères de symboles mixtes originaux.

La `skip` valeur par défaut du paramètre est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de s’abonner à des [packages SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, seuls les ID de package avec des versions compatibles SemVer 1.0.0 sont retournés (avec les avertissements de [version NuGet standard](../concepts/package-versioning.md) , tels que les chaînes de version avec 4 éléments entiers).
Si `semVerLevel=2.0.0` est fourni, les packages compatibles SemVer 1.0.0 et SemVer 2.0.0 sont retournés. Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Le `packageType` paramètre est utilisé pour filtrer les résultats de la saisie semi-automatique uniquement pour les packages qui ont au moins un type de package correspondant au nom du type de package.
Si le type de package fourni n’est pas un type de package valide tel que défini par le [document de type de package](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), un résultat vide est retourné.
Si le type de package fourni est vide, aucun filtre n’est appliqué. En d’autres termes, le passage d’aucune valeur au `packageType` paramètre se comporte comme si le paramètre n’était pas passé.

### <a name="response"></a>response

La réponse est un document JSON contenant des `take` résultats de saisie semi-automatique.

L’objet JSON racine a les propriétés suivantes :

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
totalHits | entier          | Oui      | Nombre total de correspondances, à l’égard de `skip` et `take`
data      | tableau de chaînes | Oui      | ID de package correspondants à la requête

### <a name="sample-request"></a>Exemple de requête

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Énumérer les versions du package

Une fois qu’un ID de package est découvert à l’aide de l’API précédente, un client peut utiliser l’API de saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.

Une version de package non listée n’apparaît pas dans les résultats.

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Dans     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | Oui      | ID de package pour lequel extraire les versions
prerelease  | URL    | boolean | non       | `true`ou `false` déterminer s’il faut inclure [les packages](../create-packages/prerelease-packages.md) de préversion
semVerLevel | URL    | string  | non       | Une chaîne de version SemVer 2.0.0 

Si `prerelease` n’est pas fourni, les packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de s’abonner à des packages SemVer 2.0.0. Si ce paramètre de requête est exclu, seules les versions de SemVer 1.0.0 sont retournées. Si `semVerLevel=2.0.0` est fourni, les versions SemVer 1.0.0 et SemVer 2.0.0 sont retournées. Pour plus d’informations, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>response

La réponse est un document JSON contenant toutes les versions de package de l’ID de package fourni, en filtrant par les paramètres de requête donnés.

L’objet JSON racine a la propriété suivante :

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
data      | tableau de chaînes | Oui      | Versions du package correspondant à la requête

Les versions de package dans le `data` tableau peuvent contenir des métadonnées de build SemVer 2.0.0 (par exemple `1.0.0+metadata` ,) si le `semVerLevel=2.0.0` est fourni dans la chaîne de requête.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
