---
title: Métadonnées de package, API NuGet
description: L’URL de base d’inscription du package autorise l’extraction des métadonnées sur les packages.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488315"
---
# <a name="package-metadata"></a>Métadonnées de package

Il est possible d’extraire des métadonnées sur les packages disponibles sur une source de package à l’aide de l’API NuGet v3. Ces métadonnées peuvent être extraites à `RegistrationsBaseUrl` l’aide de la ressource trouvée dans l' [index de service](service-index.md).

La collection des documents trouvés sous `RegistrationsBaseUrl` est souvent appelée «inscriptions» ou «objets BLOB d’inscription». L’ensemble de documents sous un seul `RegistrationsBaseUrl` est appelé «Hive d’inscription». Une ruche d’inscription contient toutes les métadonnées relatives à chaque package disponible sur une source de package.

## <a name="versioning"></a>Gestion de version

Les valeurs `@type` suivantes sont utilisées:

Valeur@type                     | Notes
------------------------------- | -----
RegistrationsBaseUrl            | La version initiale
RegistrationsBaseUrl/3.0.0-beta | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Réponses gzippé
RegistrationsBaseUrl/3.6.0      | Comprend des packages SemVer 2.0.0

Il s’agit de trois ruches d’inscription distinctes disponibles pour différentes versions du client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Ces inscriptions ne sont pas compressées (ce qui signifie `Content-Encoding: identity`qu’elles utilisent un implicite). Les packages SemVer 2.0.0 sont **exclus** de cette ruche.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Ces inscriptions sont compressées `Content-Encoding: gzip`à l’aide de. Les packages SemVer 2.0.0 sont **exclus** de cette ruche.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Ces inscriptions sont compressées `Content-Encoding: gzip`à l’aide de. Les packages SemVer 2.0.0 sont **inclus** dans cette ruche.
Pour plus d’informations sur SemVer 2.0.0, consultez [prise en charge de SemVer 2.0.0 pour NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de `@id` la propriété associée aux valeurs de `@type` ressource mentionnées ci-dessus. Dans le document suivant, l’URL `{@id}` de base de l’espace réservé sera utilisée.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource d’inscription prennent en `GET` charge `HEAD`les méthodes http et.

## <a name="registration-index"></a>Index d’inscription

Les groupes de ressources d’inscription regroupent les métadonnées par ID de package. Il n’est pas possible d’obtenir des données sur plus d’un ID de package à la fois. Cette ressource n’offre aucun moyen de découvrir des ID de package. Au lieu de cela, le client est supposé connaître déjà l’ID de package souhaité. Les métadonnées disponibles sur chaque version de package varient en fonction de l’implémentation du serveur. Les objets BLOB d’inscription de package ont la structure hiérarchique suivante:

- **Index**: point d’entrée pour les métadonnées du package, partagé par tous les packages sur une source avec le même ID de package.
- **Page**: regroupement des versions de package. Le nombre de versions de packages dans une page est défini par l’implémentation du serveur.
- **Feuille**: document spécifique à une version de package unique.

L’URL de l’index d’inscription est prévisible et peut être déterminée par le client en fonction d’un ID de package et `@id` de la valeur de la ressource d’inscription de l’index de service. Les URL des pages d’inscription et des feuilles sont découvertes en inspectant l’index d’inscription.

### <a name="registration-pages-and-leaves"></a>Pages d’inscription et feuilles

Bien qu’il ne soit pas strictement nécessaire pour une implémentation de serveur de stocker les feuilles d’inscription dans des documents de page d’inscription distincts, il est recommandé de conserver la mémoire côté client. Au lieu d’incorporer toutes les feuilles d’inscription dans l’index ou de stocker immédiatement les feuilles dans les documents, il est recommandé que l’implémentation du serveur définisse une méthode heuristique pour choisir entre les deux approches en fonction du nombre de versions de packages ou taille cumulée des feuilles des packages.

Le stockage de toutes les versions de package (feuilles) dans l’index d’inscription économise le nombre de requêtes HTTP nécessaires à l’extraction des métadonnées de package, mais signifie qu’un document plus volumineux doit être téléchargé et que davantage de mémoire cliente doit être allouée. En revanche, si l’implémentation de serveur stocke immédiatement l’inscription dans des documents de page distincts, le client doit effectuer davantage de requêtes HTTP pour obtenir les informations dont il a besoin.

La méthode heuristique utilisée par nuget.org est la suivante: s’il existe 128 versions ou plus d’un package, scindez les feuilles de sortie en pages de taille 64. S’il y a moins de 128 versions, toutes les feuilles sont insérées dans l’index d’inscription.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Paramètres de la demande

Nom     | Dans     | Type    | Obligatoire | Notes
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | oui      | ID de package, en minuscules

La `LOWER_ID` valeur est l’ID de package souhaité en minuscules à l’aide des règles implémentées par. Méthode du [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) réseau.

### <a name="response"></a>response

La réponse est un document JSON qui a un objet racine avec les propriétés suivantes:

Nom  | Type             | Obligatoire | Notes
----- | ---------------- | -------- | -----
count | integer          | oui      | Nombre de pages d’inscription dans l’index
contenus | Tableau d’objets | oui      | Tableau des pages d’inscription

Chaque élément du tableau de `items` l’objet index est un objet JSON représentant une page d’inscription.

#### <a name="registration-page-object"></a>Objet de page d’inscription

L’objet de page d’inscription trouvé dans l’index d’inscription a les propriétés suivantes:

Nom   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | string           | oui      | URL de la page d’inscription
count  | integer          | oui      | Nombre d’inscriptions laissées dans la page
contenus  | Tableau d’objets | Non       | Le tableau de l’inscription quitte et leurs métadonnées associées
lower  | string           | oui      | La version SemVer 2.0.0 la plus basse dans la page (inclusive)
parent | string           | Non       | URL de l’index d’inscription
upper  | string           | oui      | Version SemVer 2.0.0 la plus élevée dans la page (inclusive)

Les `lower` limites `upper` et de l’objet page sont utiles lorsque les métadonnées pour une version de page spécifique sont nécessaires.
Ces limites peuvent être utilisées pour extraire la seule page d’inscription nécessaire. Les chaînes de version adhèrent aux [règles de version de NuGet](../concepts/package-versioning.md). Les chaînes de version sont normalisées et n’incluent pas de métadonnées de Build. Comme pour toutes les versions de l’écosystème NuGet, la comparaison des chaînes de version est implémentée à l’aide des [règles de précédence des versions de SemVer 2.0.0](http://semver.org/spec/v2.0.0.html#spec-item-11).

La `parent` propriété n’apparaît que si l’objet de la page d' `items` inscription possède la propriété.

Si la `items` propriété n’est pas présente dans l’objet de la page d’inscription, l' `@id` URL spécifiée dans le doit être utilisée pour récupérer les métadonnées sur les différentes versions du package. Le `items` tableau est parfois exclu de l’objet page en tant qu’optimisation. Si le nombre de versions d’un ID de package unique est très élevé, le document d’index d’inscription sera volumineux et gaspiller à traiter pour un client qui s’intéresse uniquement à une version spécifique ou à une petite plage de versions.

Notez que si la `items` propriété est présente, la `@id` propriété n’a pas besoin d’être utilisée, car toutes les données de la page sont déjà inline dans la `items` propriété.

Chaque élément du tableau de `items` l’objet page est un objet JSON qui représente une feuille d’inscription et ses métadonnées associées.

#### <a name="registration-leaf-object-in-a-page"></a>Objet feuille d’inscription dans une page

L’objet feuille d’inscription trouvé dans une page d’inscription a les propriétés suivantes:

Nom           | Type   | Obligatoire | Notes
-------------- | ------ | -------- | -----
@id            | string | oui      | URL de la feuille d’inscription
catalogEntry   | objet | oui      | Entrée de catalogue contenant les métadonnées du package
packageContent | string | oui      | URL du contenu du package (. nupkg)

Chaque objet feuille d’inscription représente des données associées à une version de package unique.

#### <a name="catalog-entry"></a>Entrée de catalogue

La `catalogEntry` propriété de l’objet feuille d’inscription a les propriétés suivantes:

Nom                     | Type                       | Obligatoire | Notes
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | oui      | URL du document utilisé pour produire cet objet
authors                  | chaîne ou tableau de chaînes | Non       | 
dependencyGroups         | Tableau d’objets           | Non       | Dépendances du package, regroupées par version cible du .NET Framework
désapprobation              | objet                     | Non       | Désapprobation associée au package
description              | string                     | Non       | 
iconUrl                  | string                     | Non       | 
id                       | string                     | oui      | ID du package
licenseUrl               | string                     | Non       |
licenseExpression        | string                     | Non       | 
liste                   | booléenne                    | Non       | Doit être considéré comme indiqué s’il est absent
minClientVersion         | string                     | Non       | 
projectUrl               | string                     | Non       | 
publié                | string                     | Non       | Chaîne contenant un horodateur ISO 8601 de la publication du package
requireLicenseAcceptance | booléenne                    | Non       | 
résumé                  | string                     | Non       | 
balises                     | chaîne ou tableau de chaînes  | Non       | 
title                    | string                     | Non       | 
version                  | string                     | oui      | Chaîne de version complète après la normalisation

La propriété `version` de package est la chaîne de version complète après la normalisation. Cela signifie que les données de build SemVer 2.0.0 peuvent être incluses ici.

La `dependencyGroups` propriété est un tableau d’objets représentant les dépendances du package, regroupées par version cible du .NET Framework. Si le package n’a pas de dépendances, `dependencyGroups` si la propriété est manquante, un tableau vide ou si la `dependencies` propriété de tous les groupes est vide ou manquante.

La valeur de la `licenseExpression` propriété est conforme à la syntaxe de l' [expression de licence NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Groupe de dépendances du package

Chaque objet de groupe de dépendances a les propriétés suivantes:

Nom            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
targetFramework | string           | Non       | Framework cible auquel ces dépendances sont applicables
dépendances    | Tableau d’objets | Non       |

La `targetFramework` chaîne utilise le format implémenté par la bibliothèque .net NuGet [. frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)de NuGet. Si aucun `targetFramework` n’est spécifié, le groupe de dépendances s’applique à tous les frameworks cibles.

La `dependencies` propriété est un tableau d’objets, chacun représentant une dépendance du package actuel.

#### <a name="package-dependency"></a>Dépendance de package

Chaque dépendance de package a les propriétés suivantes:

Name         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
id           | string | oui      | ID de la dépendance du package
range        | objet | Non       | Plage de [versions](../concepts/package-versioning.md#version-ranges-and-wildcards) autorisée de la dépendance
inscription | string | Non       | URL de l’index d’inscription pour cette dépendance

Si la `range` propriété est exclue ou est une chaîne vide, le client doit avoir comme valeur `(, )`par défaut la plage de versions. Autrement dit, toute version de la dépendance est autorisée.

#### <a name="package-deprecation"></a>Désapprobation du package

Chaque désapprobation de package a les propriétés suivantes:

Nom             | Type             | Obligatoire | Notes
---------------- | ---------------- | -------- | -----
principales          | Tableau de chaînes | oui      | Raisons pour lesquelles le package a été déconseillé
message          | string           | Non       | Détails supplémentaires sur cette désapprobation
alternatePackage | objet           | Non       | Dépendance de package à utiliser à la place

La `reasons` propriété doit contenir au moins une chaîne et ne doit contenir que des chaînes du tableau suivant:

Reason       | Description             
------------ | -----------
Hérité       | Le package n’est plus conservé
CriticalBugs | Le package contient des bogues qui le rendent inapproprié pour une utilisation
Autre        | Le package est déconseillé en raison d’une raison qui ne figure pas dans cette liste

Si la `reasons` propriété contient des chaînes qui ne proviennent pas de l’ensemble connu, elles doivent être ignorées. Les chaînes ne sont pas sensibles à la casse `legacy` . elles doivent donc être traitées `Legacy`de la même façon que. Il n’existe aucune restriction de classement sur le tableau, de sorte que les chaînes peuvent être organisées dans n’importe quel ordre arbitraire. En outre, si la propriété contient uniquement des chaînes qui ne proviennent pas de l’ensemble connu, elle doit être traitée comme si elle contenait uniquement la chaîne «other».

### <a name="sample-request"></a>Exemple de requête

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Dans ce cas particulier, la page d’inscription de l’index d’inscription est inline et aucune demande supplémentaire n’est nécessaire pour récupérer les métadonnées sur les versions de package individuelles.

## <a name="registration-page"></a>Page Inscription

La page d’inscription contient des feuilles d’inscription. L’URL permettant de récupérer une page d’inscription est déterminée `@id` par la propriété dans l' [objet de page d’inscription](#registration-page-object) mentionné ci-dessus.

Lorsque le `items` tableau n’est pas fourni dans l’index d’inscription, une requête HTTP d' `@id` extraction de la valeur retourne un document JSON qui a un objet comme racine. L’objet a les propriétés suivantes:

Nom   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | string           | oui      | URL de la page d’inscription
count  | integer          | oui      | Nombre d’inscriptions laissées dans la page
contenus  | Tableau d’objets | oui      | Le tableau de l’inscription quitte et leurs métadonnées associées
lower  | string           | oui      | La version SemVer 2.0.0 la plus basse dans la page (inclusive)
parent | string           | oui      | URL de l’index d’inscription
upper  | string           | oui      | Version SemVer 2.0.0 la plus élevée dans la page (inclusive)

La forme des objets feuilles d’inscription est identique à celle de l’index d’inscription [ci-dessus](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Exemple de requête

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Feuille d’inscription

La feuille d’inscription contient des informations sur un ID de package et une version spécifiques. Les métadonnées relatives à la version spécifique peuvent ne pas être disponibles dans ce document. Les métadonnées du package doivent être extraites de l' [index d’inscription](#registration-index) ou de la [page d’inscription](#registration-page) (qui est découverte à l’aide de l’index d’inscription).

L’URL permettant d’extraire une feuille d’inscription est obtenue `@id` à partir de la propriété d’un objet feuille d’inscription dans une page d’index ou d’inscription.

La feuille d’inscription est un document JSON avec un objet racine avec les propriétés suivantes:

Nom           | Type    | Obligatoire | Notes
-------------- | ------- | -------- | -----
@id            | string  | oui      | URL de la feuille d’inscription
catalogEntry   | string  | Non       | URL de l’entrée de catalogue qui a produit ces feuilles
liste         | booléenne | Non       | Doit être considéré comme indiqué s’il est absent
packageContent | string  | Non       | URL du contenu du package (. nupkg)
publié      | string  | Non       | Chaîne contenant un horodateur ISO 8601 de la publication du package
inscription   | string  | Non       | URL de l’index d’inscription

> [!Note]
> Sur NuGet.org, la `published` valeur est définie sur année 1900 lorsque le package est non répertorié.

### <a name="sample-request"></a>Exemple de requête

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
