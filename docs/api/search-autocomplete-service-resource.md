---
title: Saisie semi-automatique, API NuGet
description: Le service de la saisie semi-automatique de recherche prend en charge les versions et découverte interactive de l’ID de package.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911047"
---
# <a name="autocomplete"></a>Saisie semi-automatique

Il est possible de créer un package ID et la version la saisie semi-automatique expérience à l’aide de l’API V3. La ressource utilisée pour effectuer des requêtes de la saisie semi-automatique est la `SearchAutocompleteService` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur@type                           | Notes
------------------------------------ | -----
SearchAutocompleteService            | La version initiale
SearchAutocompleteService/3.0.0-beta | Alias de `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias de `SearchAutocompleteService`

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge de la ressource d’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="search-for-package-ids"></a>Recherchez les ID de package

La saisie semi-automatique première API prend en charge la recherche pour une partie d’une chaîne d’ID de package. C’est formidable lorsque vous souhaitez fournir une fonctionnalité de prédictives de package dans une interface utilisateur intégrée à une source de package NuGet.

Un package avec uniquement les versions non listées n’apparaîtra pas dans les résultats.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Vers l'avant     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Non       | La chaîne à comparer à l’ID de package
skip        | URL    | entiers | Non       | Le nombre de résultats à ignorer, pour la pagination
Take        | URL    | entiers | Non       | Le nombre de résultats à retourner pour la pagination
version préliminaire  | URL    | boolean | Non       | `true` ou `false` déterminer s’il faut inclure [packages de préversion](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Non       | Une chaîne de version SemVer 1.0.0 

La requête de la saisie semi-automatique `q` est analysé d’une manière qui est définie par l’implémentation du serveur. NuGet.org prend en charge l’interrogation d’origine pour le préfixe de jetons d’ID de package, qui sont des éléments de l’ID de produit par fractionnement par des caractères de cas et le symbole mixte.

Le `skip` paramètre valeur par défaut est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de participer à la [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, ID de package uniquement avec les versions compatibles de SemVer 1.0.0 seront retourné (avec le [le contrôle de version NuGet standard](../reference/package-versioning.md) mises en garde, tels que les chaînes de version avec 4 éléments entier).
Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et packages compatibles SemVer 2.0.0 seront retournés. Consultez le [prise en charge de SemVer 2.0.0 pour nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.

### <a name="response"></a>Réponse

La réponse est document JSON contenant jusqu'à `take` les résultats de la saisie semi-automatique.

L’objet JSON racine a les propriétés suivantes :

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
totalHits | entiers          | oui      | Le nombre total de correspondances, en ignorant `skip` et `take`
Données      | tableau de chaînes | oui      | Les ID mis en correspondance par la demande de package

### <a name="sample-request"></a>Exemple de demande

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Énumérer les versions de package

Une fois qu’un ID de package est découvert à l’aide de l’API précédente, un client peut utiliser l’API de saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.

Une version de package n’est pas répertoriée n’apparaîtra pas dans les résultats.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Vers l'avant     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
ID          | URL    | string  | oui      | L’ID de package pour extraire les versions pour
version préliminaire  | URL    | boolean | Non       | `true` ou `false` déterminer s’il faut inclure [packages de préversion](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Non       | Une chaîne de version SemVer 2.0.0 

Si `prerelease` n’est pas fourni, packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de participer aux packages de SemVer 2.0.0. Si ce paramètre de requête est exclu, seules les versions de SemVer 1.0.0 seront affichera. Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et les versions de SemVer 2.0.0 seront retournées. Consultez le [prise en charge de SemVer 2.0.0 pour nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.

### <a name="response"></a>Réponse

La réponse est un document JSON contenant toutes les versions de package de l’ID de package fourni, le filtrage par les paramètres de requête donnée.

L’objet JSON racine a la propriété suivante :

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
Données      | tableau de chaînes | oui      | Les versions de package correspondance à la demande

Les versions de package dans le `data` tableau peut-être contenir des métadonnées de build de SemVer 2.0.0 (par exemple, `1.0.0+metadata`) si le `semVerLevel=2.0.0` est fourni dans la chaîne de requête.

### <a name="sample-request"></a>Exemple de demande

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
