---
title: Recherche, API NuGet
description: Le service de recherche permet aux clients de requête pour les packages par mot clé et pour filtrer les résultats sur certains champs de package.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d462b289c39c2dd1418304dabcad47d0d4217f82
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426734"
---
# <a name="search"></a>Rechercher

Il est possible de rechercher des packages disponibles sur une source de package à l’aide de l’API V3. La ressource utilisée pour la recherche est la `SearchQueryService` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur@type                   | Notes
----------------------------- | -----
SearchQueryService            | La version initiale
SearchQueryService/3.0.0-beta | Alias de `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias de `SearchQueryService`

## <a name="base-url"></a>URL de base

L’URL de base pour l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge de la ressource d’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="search-for-packages"></a>Rechercher des packages

L’API de recherche permet à un client à la requête pour une page de packages correspondant à une requête de recherche spécifié. L’interprétation de la requête de recherche (par exemple, la création de jetons pour les termes de recherche) est déterminée par l’implémentation du serveur, mais il est courant général que la requête de recherche est utilisée pour la correspondance des ID de package, les titres, descriptions et balises. Autres champs de métadonnées de package peuvent également être considérés.

Un package retirée de la liste ne doit jamais apparaître dans les résultats de la recherche.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Vers l'avant     | Type    | Obligatoire | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Non       | Les termes de recherche à utiliser pour les packages de filtre
skip        | URL    | entiers | Non       | Le nombre de résultats à ignorer, pour la pagination
Take        | URL    | entiers | Non       | Le nombre de résultats à retourner pour la pagination
version préliminaire  | URL    | boolean | Non       | `true` ou `false` déterminer s’il faut inclure [packages de préversion](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Non       | Une chaîne de version SemVer 1.0.0 

La requête de recherche `q` est analysé d’une manière qui est définie par l’implémentation du serveur. NuGet.org prend en charge le filtrage de base sur un [divers champs](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si aucun `q` n’est fourni, tous les packages doivent être retournées dans les limites imposées par skip et take. Ainsi, l’onglet « Browse » dans l’expérience NuGet Visual Studio.

Le `skip` paramètre valeur par défaut est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, packages de préversion sont exclus.

Le `semVerLevel` paramètre de requête permet de participer à la [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, uniquement les packages avec les versions compatibles de SemVer 1.0.0 seront retournés (avec le [le contrôle de version NuGet standard](../reference/package-versioning.md) mises en garde, tels que les chaînes de version avec 4 éléments entier).
Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et packages compatibles SemVer 2.0.0 seront retournés. Consultez le [prise en charge de SemVer 2.0.0 pour nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.

### <a name="response"></a>Réponse

La réponse est document JSON contenant jusqu'à `take` résultats de la recherche. Résultats de la recherche sont regroupés par ID de package.

L’objet JSON racine a les propriétés suivantes :

Nom      | Type             | Obligatoire | Notes
--------- | ---------------- | -------- | -----
totalHits | entiers          | oui      | Le nombre total de correspondances, en ignorant `skip` et `take`
Données      | tableau d’objets | oui      | Les résultats de recherche correspondant à la demande

### <a name="search-result"></a>Résultat de la recherche

Chaque élément dans le `data` tableau est un objet JSON composé d’un groupe de versions de package partage le même ID de package.
L’objet a les propriétés suivantes :

Nom           | Type                       | Obligatoire | Notes
-------------- | -------------------------- | -------- | -----
ID             | string                     | oui      | L’ID du package de mise en correspondance
version        | string                     | oui      | La chaîne de version SemVer 2.0.0 complète du package (peut contenir des métadonnées de build)
Description    | string                     | Non       | 
versions       | tableau d’objets           | oui      | Toutes les versions de la mise en correspondance le `prerelease` paramètre
authors        | chaîne ou tableau de chaînes | Non       | 
iconUrl        | string                     | Non       | 
licenseUrl     | string                     | Non       | 
owners         | chaîne ou tableau de chaînes | Non       | 
projectUrl     | string                     | Non       | 
inscription   | string                     | Non       | L’URL absolue à associé [index de l’inscription](registration-base-url-resource.md#registration-index)
résumé        | string                     | Non       | 
étiquettes           | chaîne ou tableau de chaînes | Non       | 
titre          | string                     | Non       | 
totalDownloads | entiers                    | Non       | Cette valeur peut être déduite par la somme des téléchargements dans le `versions` tableau
vérifié       | boolean                    | Non       | Une valeur JSON booléenne indiquant si le package est [vérifié](../nuget-org/id-prefix-reservation.md)

Sur nuget.org, un package vérifié est celui qui a un ID de package correspondant à un préfixe d’identificateur réservé et détenues par un des propriétaires du préfixe réservé. Pour plus d’informations, consultez le [documentation sur la réservation du préfixe ID](../reference/id-prefix-reservation.md).

Les métadonnées contenues dans l’objet de résultat de recherche sont effectuée à partir de la dernière version de package. Chaque élément dans le `versions` tableau est un objet JSON avec les propriétés suivantes :

Nom      | Type    | Obligatoire | Notes
--------- | ------- | -------- | -----
@id       | string  | oui      | L’URL absolue à associé [feuille d’inscription](registration-base-url-resource.md#registration-leaf)
version   | string  | oui      | La chaîne de version SemVer 2.0.0 complète du package (peut contenir des métadonnées de build)
Téléchargements | entiers | oui      | Le nombre de téléchargements pour cette version de package spécifique

### <a name="sample-request"></a>Exemple de demande

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [search-result.json](./_data/search-result.json)]
