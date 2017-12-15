---
title: Recherche, NuGet API | Documents Microsoft
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
ms.assetid: 11ca2092-67dc-41a9-a7af-afe610d8febb
description: "Le service de recherche permet aux clients pour rechercher les packages par mot clé et de résultats du filtrage sur certains champs de package."
keywords: "API de recherche NuGet, NuGet découvrir les packages, les API pour les packages NuGet de requête, les API pour parcourir les packages NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 8b37c1bfb66290de49641a8b6197cb83cd35318a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="search"></a>Rechercher

Il est possible de rechercher des packages disponibles sur une source de package à l’aide de l’API V3. La ressource utilisée pour la recherche est la `SearchQueryService` ressource trouvée dans le [index service](service-index.md).

## <a name="versioning"></a>Versioning

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur @type                   | Remarques
----------------------------- | -----
SearchQueryService            | La version initiale
SearchQueryService/3.0.0-beta | Alias de`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias de`SearchQueryService`

## <a name="base-url"></a>URL de base

L’URL de base pour l’API suivante est la valeur de la `@id` propriété associée à un de la ressource susmentionnée `@type` valeurs. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="search-for-packages"></a>Recherche des packages

L’API de recherche permet à un client à une requête pour une page de packages correspondant à une requête de recherche spécifié. L’interprétation de la requête de recherche (par exemple, la création de jetons pour les termes de recherche) est déterminée par l’implémentation du serveur mais les attentes générales que la requête de recherche est utilisée pour la correspondance d’ID de package, les titres, les descriptions et les balises. Autres champs de métadonnées de package peuvent également être considéré comme.

Un package non listé doit n’apparaissent jamais dans les résultats de la recherche.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom        | Vers l'avant     | Type    | Obligatoire | Remarques
----------- | ------ | ------- | -------- | -----
q           | URL    | chaîne  | Non       | Les termes de recherche à utiliser pour les packages de filtre
skip        | URL    | entiers | Non       | Le nombre de résultats à ignorer, pour la pagination
prendre        | URL    | entiers | Non       | Le nombre de résultats à retourner pour la pagination
version préliminaire  | URL    | boolean | Non       | `true`ou `false` déterminant s’il faut inclure [préliminaires des packages](../create-packages/prerelease-packages.md)
semVerLevel | URL    | chaîne  | Non       | Une chaîne de version SemVer 1.0.0 

La requête de recherche `q` est analysé de manière définie par l’implémentation du serveur. NuGet.org prend en charge le filtrage de base sur un [divers champs](../consume-packages/finding-and-choosing-packages.md#search-syntax). Si aucun `q` n’est fourni, tous les packages doivent être retournés dans les limites imposées par skip et take. Ainsi, l’onglet « Parcourir » dans l’expérience de NuGet Visual Studio.

Le `skip` paramètre valeur par défaut est 0.

Le `take` paramètre doit être un entier supérieur à zéro. L’implémentation du serveur peut imposer une valeur maximale.

Si `prerelease` n’est pas fourni, les packages en version préliminaire sont exclus.

Le `semVerLevel` paramètre de requête permet de choisir de [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Si ce paramètre de requête est exclu, seuls les packages avec les versions compatibles de SemVer 1.0.0 seront retournés (avec la [version standard de NuGet](../reference/package-versioning.md) avertissements, telles que des chaînes de version avec 4 parties entier).
Si `semVerLevel=2.0.0` est fourni, SemVer 1.0.0 et les packages compatibles SemVer 2.0.0 seront retournés. Consultez le [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) pour plus d’informations.

### <a name="response"></a>Réponse

La réponse est document JSON contenant jusqu'à `take` résultats de la recherche. Résultats de la recherche sont regroupés par ID de package.

L’objet JSON racine a les propriétés suivantes :

Nom      | Type             | Obligatoire | Remarques
--------- | ---------------- | -------- | -----
total des accès | entiers          | oui      | Le nombre total de correspondances, ignorant `skip` et`take`
Données      | Tableau d’objets | oui      | Les résultats de recherche correspondant à la demande

### <a name="search-result"></a>résultat de recherche

Chaque élément dans le `data` tableau est un objet JSON composé d’un groupe de versions de package partage le même ID de package.
L’objet a les propriétés suivantes :

Nom           | Type                       | Obligatoire | Remarques
-------------- | -------------------------- | -------- | -----
ID             | chaîne                     | oui      | L’ID du package de mise en correspondance
version        | chaîne                     | oui      | La chaîne de version SemVer 2.0.0 complet du package (peut contenir des métadonnées de la build)
Description    | chaîne                     | Non       | 
versions       | Tableau d’objets           | oui      | Toutes les versions de la mise en correspondance le `prerelease` paramètre
authors        | chaîne ou tableau de chaînes | Non       | 
iconUrl        | chaîne                     | Non       | 
licenseUrl     | chaîne                     | Non       | 
owners         | chaîne ou tableau de chaînes | Non       | 
projectUrl     | chaîne                     | Non       | 
inscription   | chaîne                     | Non       | L’URL absolue à le [les index d’enregistrement](registration-base-url-resource.md#registration-index)
résumé        | chaîne                     | Non       | 
étiquettes           | chaîne ou tableau de chaînes | Non       | 
titre          | chaîne                     | Non       | 
totalDownloads | entiers                    | Non       | Cette valeur peut être déduite par la somme des téléchargements dans le `versions` tableau
Vérifié       | boolean                    | Non       | Un booléen JSON qui indique si le package est [vérifié](../reference/id-prefix-reservation.md)

Sur nuget.org, un package vérifié est celui qui a un ID de lot correspondant à un préfixe d’identificateur réservé et détenues par l’un des propriétaires de l’espace de noms. Pour plus d’informations, consultez la [plus d’informations sur la réservation du préfixe ID](../reference/id-prefix-reservation.md).

Les métadonnées contenues dans l’objet de résultat de recherche sont effectuée à partir de la dernière version du package. Chaque élément dans le `versions` tableau est un objet JSON avec les propriétés suivantes :

Nom      | Type    | Obligatoire | Remarques
--------- | ------- | -------- | -----
@id       | chaîne  | oui      | L’URL absolue à le [feuille de l’inscription](registration-base-url-resource.md#registration-leaf)
version   | chaîne  | oui      | La chaîne de version SemVer 2.0.0 complet du package (peut contenir des métadonnées de la build)
Téléchargements | entiers | oui      | Le nombre de téléchargements pour cette version de package spécifique

### <a name="sample-request"></a>Exemple de demande

```
GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [search-result.json](./_data/search-result.json)]
