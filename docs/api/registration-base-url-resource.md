---
title: Métadonnées de package, API NuGet
description: L’URL de base d’inscription du package autorise l’extraction des métadonnées sur les packages.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230879"
---
# <a name="package-metadata"></a>Métadonnées de package

Il est possible d’extraire des métadonnées sur les packages disponibles sur une source de package à l’aide de l’API NuGet v3. Ces métadonnées peuvent être extraites à l’aide de la ressource `RegistrationsBaseUrl` trouvée dans l' [index de service](service-index.md).

La collection des documents trouvés sous `RegistrationsBaseUrl` sont souvent appelées « inscriptions » ou « objets BLOB d’inscription ». L’ensemble de documents sous un `RegistrationsBaseUrl` unique est appelé « Hive d’inscription ». Une ruche d’inscription contient toutes les métadonnées relatives à chaque package disponible sur une source de package.

## <a name="versioning"></a>Contrôle de version

Les valeurs de `@type` suivantes sont utilisées :

Valeur @type                     | Notes
------------------------------- | -----
RegistrationsBaseUrl            | La version initiale
RegistrationsBaseUrl/3.0.0-beta | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Réponses gzippé
RegistrationsBaseUrl/3.6.0      | Comprend des packages SemVer 2.0.0

Il s’agit de trois ruches d’inscription distinctes disponibles pour différentes versions du client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Ces inscriptions ne sont pas compressées (ce qui signifie qu’elles utilisent un `Content-Encoding: identity`implicite). Les packages SemVer 2.0.0 sont **exclus** de cette ruche.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Ces inscriptions sont compressées à l’aide de `Content-Encoding: gzip`. Les packages SemVer 2.0.0 sont **exclus** de cette ruche.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Ces inscriptions sont compressées à l’aide de `Content-Encoding: gzip`. Les packages SemVer 2.0.0 sont **inclus** dans cette ruche.
Pour plus d’informations sur SemVer 2.0.0, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la propriété `@id` associée aux valeurs de `@type` de ressources mentionnées ci-dessus. Dans le document suivant, l’URL de base de l’espace réservé `{@id}` sera utilisée.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource d’inscription prennent en charge les méthodes HTTP `GET` et `HEAD`.

## <a name="registration-index"></a>Index d’inscription

Les groupes de ressources d’inscription regroupent les métadonnées par ID de package. Il n’est pas possible d’obtenir des données sur plus d’un ID de package à la fois. Cette ressource n’offre aucun moyen de découvrir des ID de package. Au lieu de cela, le client est supposé connaître déjà l’ID de package souhaité. Les métadonnées disponibles sur chaque version de package varient en fonction de l’implémentation du serveur. Les objets BLOB d’inscription de package ont la structure hiérarchique suivante :

- **Index**: point d’entrée pour les métadonnées du package, partagé par tous les packages sur une source avec le même ID de package.
- **Page**: regroupement des versions de package. Le nombre de versions de packages dans une page est défini par l’implémentation du serveur.
- **Feuille**: document spécifique à une version de package unique.

L’URL de l’index d’inscription est prévisible et peut être déterminée par le client en fonction d’un ID de package et de la valeur `@id` de la ressource d’inscription à partir de l’index de service. Les URL des pages d’inscription et des feuilles sont découvertes en inspectant l’index d’inscription.

### <a name="registration-pages-and-leaves"></a>Pages d’inscription et feuilles

Bien qu’il ne soit pas strictement nécessaire pour une implémentation de serveur de stocker les feuilles d’inscription dans des documents de page d’inscription distincts, il est recommandé de conserver la mémoire côté client. Au lieu d’incorporer toutes les feuilles d’inscription dans l’index ou de stocker immédiatement les feuilles dans les documents, il est recommandé que l’implémentation du serveur définisse une méthode heuristique pour choisir entre les deux approches en fonction du nombre de versions de packages ou taille cumulée des feuilles des packages.

Le stockage de toutes les versions de package (feuilles) dans l’index d’inscription économise le nombre de requêtes HTTP nécessaires à l’extraction des métadonnées de package, mais signifie qu’un document plus volumineux doit être téléchargé et que davantage de mémoire cliente doit être allouée. En revanche, si l’implémentation de serveur stocke immédiatement l’inscription dans des documents de page distincts, le client doit effectuer davantage de requêtes HTTP pour obtenir les informations dont il a besoin.

La méthode heuristique utilisée par nuget.org est la suivante : s’il existe 128 versions ou plus d’un package, scindez les feuilles de sortie en pages de taille 64. S’il y a moins de 128 versions, toutes les feuilles sont insérées dans l’index d’inscription. Notez que cela signifie que les packages avec des versions 65 à 127 auront deux pages dans l’index, mais les deux pages seront Inline.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Paramètres de la demande

Name     | Dans     | Type    | Obligatoire | Notes
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | Oui      | ID de package, en minuscules

La valeur `LOWER_ID` est l’ID de package souhaité en minuscules à l’aide des règles implémentées par. Méthode du [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) du réseau.

### <a name="response"></a>response

La réponse est un document JSON qui a un objet racine avec les propriétés suivantes :

Name  | Type             | Obligatoire | Notes
----- | ---------------- | -------- | -----
count | entier          | Oui      | Nombre de pages d’inscription dans l’index
items | tableau d’objets | Oui      | Tableau des pages d’inscription

Chaque élément du tableau `items` de l’objet index est un objet JSON représentant une page d’inscription.

#### <a name="registration-page-object"></a>Objet de page d’inscription

L’objet de page d’inscription trouvé dans l’index d’inscription a les propriétés suivantes :

Name   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | string           | Oui      | URL de la page d’inscription
count  | entier          | Oui      | Nombre d’inscriptions laissées dans la page
items  | tableau d’objets | non       | Le tableau de l’inscription quitte et leurs métadonnées associées
lower  | string           | Oui      | La version SemVer 2.0.0 la plus basse dans la page (inclusive)
parent | string           | non       | URL de l’index d’inscription
upper  | string           | Oui      | Version SemVer 2.0.0 la plus élevée dans la page (inclusive)

Les limites `lower` et `upper` de l’objet page sont utiles lorsque les métadonnées pour une version de page spécifique sont nécessaires.
Ces limites peuvent être utilisées pour extraire la seule page d’inscription nécessaire. Les chaînes de version adhèrent aux [règles de version de NuGet](../concepts/package-versioning.md). Les chaînes de version sont normalisées et n’incluent pas de métadonnées de Build. Comme pour toutes les versions de l’écosystème NuGet, la comparaison des chaînes de version est implémentée à l’aide des [règles de précédence des versions de SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

La propriété `parent` s’affiche uniquement si l’objet de la page d’inscription a la propriété `items`.

Si la propriété `items` n’est pas présente dans l’objet de la page d’inscription, l’URL spécifiée dans le `@id` doit être utilisée pour récupérer les métadonnées sur les différentes versions du package. Le tableau `items` est parfois exclu de l’objet page en tant qu’optimisation. Si le nombre de versions d’un ID de package unique est très élevé, le document d’index d’inscription sera volumineux et gaspiller à traiter pour un client qui s’intéresse uniquement à une version spécifique ou à une petite plage de versions.

Notez que si la propriété `items` est présente, la propriété `@id` ne doit pas être utilisée, car toutes les données de la page sont déjà inline dans la propriété `items`.

Chaque élément du tableau de `items` de l’objet page est un objet JSON qui représente une feuille d’inscription et ses métadonnées associées.

#### <a name="registration-leaf-object-in-a-page"></a>Objet feuille d’inscription dans une page

L’objet feuille d’inscription trouvé dans une page d’inscription a les propriétés suivantes :

Name           | Type   | Obligatoire | Notes
-------------- | ------ | -------- | -----
@id            | string | Oui      | URL de la feuille d’inscription
catalogEntry   | object | Oui      | Entrée de catalogue contenant les métadonnées du package
packageContent | string | Oui      | URL du contenu du package (. nupkg)

Chaque objet feuille d’inscription représente des données associées à une version de package unique.

#### <a name="catalog-entry"></a>Entrée de catalogue

La propriété `catalogEntry` dans l’objet feuille d’inscription a les propriétés suivantes :

Name                     | Type                       | Obligatoire | Notes
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | Oui      | URL du document utilisé pour produire cet objet
authors                  | chaîne ou tableau de chaînes | non       | 
dependencyGroups         | tableau d’objets           | non       | Dépendances du package, regroupées par version cible du .NET Framework
désapprobation              | object                     | non       | Désapprobation associée au package
description              | string                     | non       | 
iconUrl                  | string                     | non       | 
id                       | string                     | Oui      | ID du package
licenseUrl               | string                     | non       |
licenseExpression        | string                     | non       | 
répertoriés                   | boolean                    | non       | Doit être considéré comme indiqué s’il est absent
minClientVersion         | string                     | non       | 
projectUrl               | string                     | non       | 
published                | string                     | non       | Chaîne contenant un horodateur ISO 8601 de la publication du package
requireLicenseAcceptance | boolean                    | non       | 
summary                  | string                     | non       | 
tags                     | chaîne ou tableau de chaînes  | non       | 
title                    | string                     | non       | 
version                  | string                     | Oui      | Chaîne de version complète après la normalisation

La propriété `version` du package est la chaîne de version complète après la normalisation. Cela signifie que les données de build SemVer 2.0.0 peuvent être incluses ici.

La propriété `dependencyGroups` est un tableau d’objets représentant les dépendances du package, regroupées par version cible du .NET Framework. Si le package n’a pas de dépendances, la propriété `dependencyGroups` est manquante, un tableau vide ou la propriété `dependencies` de tous les groupes est vide ou manquante.

La valeur de la propriété `licenseExpression` est conforme à la syntaxe de l' [expression de licence NuGet](../reference/nuspec.md#license).

> [!Note]
> Sur nuget.org, la valeur `published` est définie sur l’année 1900 lorsque le package est non répertorié.

#### <a name="package-dependency-group"></a>Groupe de dépendances du package

Chaque objet de groupe de dépendances a les propriétés suivantes :

Name            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
targetFramework | string           | non       | Framework cible auquel ces dépendances sont applicables
dependencies    | tableau d’objets | non       |

La chaîne de `targetFramework` utilise le format implémenté par la bibliothèque .NET NuGet [. frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)de NuGet. Si aucun `targetFramework` n’est spécifié, le groupe de dépendances s’applique à tous les frameworks cibles.

La propriété `dependencies` est un tableau d’objets, chacun représentant une dépendance du package actuel.

#### <a name="package-dependency"></a>Dépendance de package

Chaque dépendance de package a les propriétés suivantes :

Name         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
id           | string | Oui      | ID de la dépendance du package
range        | object | non       | Plage de [versions](../concepts/package-versioning.md#version-ranges) autorisée de la dépendance
inscription | string | non       | URL de l’index d’inscription pour cette dépendance

Si la propriété `range` est exclue ou est une chaîne vide, le client doit avoir comme valeur par défaut la plage de versions `(, )`. Autrement dit, toute version de la dépendance est autorisée. La valeur de `*` n’est pas autorisée pour la propriété `range`.

#### <a name="package-deprecation"></a>Désapprobation du package

Chaque désapprobation de package a les propriétés suivantes :

Name             | Type             | Obligatoire | Notes
---------------- | ---------------- | -------- | -----
principales          | tableau de chaînes | Oui      | Raisons pour lesquelles le package a été déconseillé
message          | string           | non       | Détails supplémentaires sur cette désapprobation
alternatePackage | object           | non       | Autre package à utiliser à la place

La propriété `reasons` doit contenir au moins une chaîne et ne doit contenir que des chaînes du tableau suivant :

Motif       | Description             
------------ | -----------
Ancien       | Le package n’est plus conservé
CriticalBugs | Le package contient des bogues qui le rendent inapproprié pour une utilisation
Autres        | Le package est déconseillé en raison d’une raison qui ne figure pas dans cette liste

Si la propriété `reasons` contient des chaînes qui ne proviennent pas de l’ensemble connu, elles doivent être ignorées. Les chaînes ne respectent pas la casse, `legacy` doit donc être traitée de la même façon que `Legacy`. Il n’existe aucune restriction de classement sur le tableau, de sorte que les chaînes peuvent être organisées dans n’importe quel ordre arbitraire. En outre, si la propriété contient uniquement des chaînes qui ne proviennent pas de l’ensemble connu, elle doit être traitée comme si elle contenait uniquement la chaîne « other ».

#### <a name="alternate-package"></a>Autre package

L’objet de package de remplacement possède les propriétés suivantes :

Name         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
id           | string | Oui      | ID de l’autre package
range        | object | non       | Plage de [versions](../concepts/package-versioning.md#version-ranges)autorisée ou `*` si une version est autorisée

### <a name="sample-request"></a>Exemple de requête

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Dans ce cas particulier, la page d’inscription de l’index d’inscription est inline et aucune demande supplémentaire n’est nécessaire pour récupérer les métadonnées sur les versions de package individuelles.

## <a name="registration-page"></a>Page Inscription

La page d’inscription contient des feuilles d’inscription. L’URL permettant de récupérer une page d’inscription est déterminée par la propriété `@id` dans l' [objet de page d’inscription](#registration-page-object) mentionné ci-dessus. L’URL n’est pas censée être prévisible et doit toujours être détectée au moyen du document d’index.

> [!Warning]
> Sur nuget.org, l’URL du document de page d’inscription contient de manière cofortuite les limites inférieure et supérieure de la page. Toutefois, cette hypothèse ne doit jamais être effectuée par un client, car les implémentations de serveur sont libres de modifier la forme de l’URL tant que le document d’index a un lien valide.

Lorsque le tableau de `items` n’est pas fourni dans l’index d’inscription, une requête HTTP d’extraction de la valeur `@id` retourne un document JSON qui a un objet comme racine. L'objet a les propriétés suivantes :

Name   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | string           | Oui      | URL de la page d’inscription
count  | entier          | Oui      | Nombre d’inscriptions laissées dans la page
items  | tableau d’objets | Oui      | Le tableau de l’inscription quitte et leurs métadonnées associées
lower  | string           | Oui      | La version SemVer 2.0.0 la plus basse dans la page (inclusive)
parent | string           | Oui      | URL de l’index d’inscription
upper  | string           | Oui      | Version SemVer 2.0.0 la plus élevée dans la page (inclusive)

La forme des objets feuilles d’inscription est identique à celle de l’index d’inscription [ci-dessus](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Exemple de requête

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Feuille d’inscription

La feuille d’inscription contient des informations sur un ID de package et une version spécifiques. Les métadonnées relatives à la version spécifique peuvent ne pas être disponibles dans ce document. Les métadonnées du package doivent être extraites de l' [index d’inscription](#registration-index) ou de la [page d’inscription](#registration-page) (qui est découverte à l’aide de l’index d’inscription).

L’URL permettant d’extraire une feuille d’inscription est obtenue à partir de la propriété `@id` d’un objet feuille d’inscription dans une page d’index ou d’inscription. Comme avec le document de la page. l’URL n’est pas censée être prévisible et doit toujours être détectée au moyen de l’objet de page d’inscription.

> [!Warning]
> Sur nuget.org, l’URL du document feuille d’inscription contient par ailleurs la version du package. Toutefois, cette hypothèse ne doit jamais être effectuée par un client, car les implémentations de serveur sont libres de modifier la forme de l’URL tant que le document parent a un lien valide. 

La feuille d’inscription est un document JSON avec un objet racine avec les propriétés suivantes :

Name           | Type    | Obligatoire | Notes
-------------- | ------- | -------- | -----
@id            | string  | Oui      | URL de la feuille d’inscription
catalogEntry   | string  | non       | URL de l’entrée de catalogue qui a produit ces feuilles
répertoriés         | boolean | non       | Doit être considéré comme indiqué s’il est absent
packageContent | string  | non       | URL du contenu du package (. nupkg)
published      | string  | non       | Chaîne contenant un horodateur ISO 8601 de la publication du package
inscription   | string  | non       | URL de l’index d’inscription

> [!Note]
> Sur nuget.org, la valeur `published` est définie sur l’année 1900 lorsque le package est non répertorié.

### <a name="sample-request"></a>Exemple de requête

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
