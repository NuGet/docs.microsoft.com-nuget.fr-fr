---
title: La saisie semi-automatique, NuGet API | Documents Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Le service de la saisie semi-automatique search prend en charge les versions et découverte interactive de l’ID de package."
keywords: "API de la saisie semi-automatique de NuGet, ID de package NuGet recherche, ID de package de sous-chaîne"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a>Saisie semi-automatique

Il est possible de générer un package ID et la version la saisie semi-automatique expérience à l’aide de l’API V3. La ressource utilisée pour effectuer des requêtes de la saisie semi-automatique est la `SearchAutocompleteService` ressource trouvée dans le [index service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur @type                          | Notes
------------------------------------ | -----
SearchAutocompleteService            | La version initiale
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias de`SearchAutocompleteService`

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="search-for-package-ids"></a>Recherchez les ID de package

La saisie semi-automatique la première API prend en charge la recherche d’une partie d’une chaîne d’ID de package. Il s’agit très lorsque vous souhaitez fournir une fonctionnalité de tampon clavier de package dans une interface utilisateur intégrée à une source de package NuGet.

Un package avec uniquement les versions non listées n’apparaîtra pas dans les résultats.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Name        | Vers l'avant     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | chaîne  | Non       | La chaîne à comparer à l’ID de package
skip        | URL    | entiers | Non       | Le nombre de résultats à ignorer, pour la pagination
prendre        | URL    | entiers | Non       | Le nombre de résultats à retourner pour la pagination
version préliminaire  | URL    | boolean | Non       | `true`ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)
semVerLevel | URL    | chaîne  | Non       | Une chaîne de version SemVer 1.0.0 

La requête de la saisie semi-automatique `q` est analysé de manière définie par l’implémentation du serveur. NuGet.org prend en charge l’interrogation d’origine pour le préfixe de jetons d’ID de package, qui sont des éléments de l’ID de produit par spliting par des caractères de cas et le symbole mixte.

Le `skip` paramètre valeur par défaut est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.

Le `semVerLevel` paramètre de requête permet de choisir de [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, ID de package uniquement avec les versions compatibles de SemVer 1.0.0 seront retourné (avec la [version standard de NuGet](../reference/package-versioning.md) avertissements, telles que des chaînes de version avec 4 parties entier).
Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et les packages compatibles SemVer 2.0.0 seront retournés. Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.

### <a name="response"></a>Réponse

La réponse est document JSON contenant jusqu'à `take` les résultats de la saisie semi-automatique.

L’objet JSON racine a les propriétés suivantes :

Name      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
total des accès | entiers          | oui      | Le nombre total de correspondances, ignorant `skip` et`take`
Données      | Tableau de chaînes | oui      | Les ID correspondant à la demande de package

### <a name="sample-request"></a>Exemple de demande

GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Énumérer des versions de package

Une fois qu’un ID de package a été détecté à l’aide de l’API précédente, un client peut utiliser l’API de la saisie semi-automatique pour énumérer les versions de package pour un ID de package fourni.

Une version de package qui n’est pas spécifiée n’apparaîtra pas dans les résultats.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Name        | Vers l'avant     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
ID          | URL    | chaîne  | oui      | Pour récupérer des versions pour l’ID de package
version préliminaire  | URL    | boolean | Non       | `true`ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)
semVerLevel | URL    | chaîne  | Non       | Une chaîne de version SemVer 2.0.0 

Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.

Le `semVerLevel` paramètre de requête permet de participer à des packages de SemVer 2.0.0. Si ce paramètre de requête est exclu, seules les versions SemVer 1.0.0 seront retournées. Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et SemVer 2.0.0 versions seront retournées. Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.

### <a name="response"></a>Réponse

La réponse est un document JSON qui contient toutes les versions de package de l’ID de package fourni, le filtrage par les paramètres de requête donnée.

L’objet JSON racine a la propriété suivante :

Name      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
Données      | Tableau de chaînes | oui      | Les versions de package correspondance à la demande

Les versions de package dans le `data` tableau peut contenir des métadonnées de génération SemVer 2.0.0 (par exemple, `1.0.0+metadata`) si le `semVerLevel=2.0.0` a été fourni dans la chaîne de requête.

### <a name="sample-request"></a>Exemple de demande

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
