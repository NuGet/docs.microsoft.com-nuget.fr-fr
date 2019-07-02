---
title: Métadonnées du package, NuGet API
description: L’URL de base de l’inscription de package permet de récupérer les métadonnées à propos des packages.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0b35e2bbdde63f7f7a5298bd035c180389cd345d
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496497"
---
# <a name="package-metadata"></a>Métadonnées de package

Il est possible d’extraire des métadonnées sur les packages disponibles sur une source de package à l’aide de l’API V3 de NuGet. Ces métadonnées peuvent être extraites à l’aide de la `RegistrationsBaseUrl` ressource trouvée dans le [index de service](service-index.md).

La collection de documents trouvés sous `RegistrationsBaseUrl` sont souvent appelés « inscriptions » ou « objets BLOB d’inscription ». L’ensemble de documents dans un seul `RegistrationsBaseUrl` est appelé une « ruche de l’inscription ». Une ruche de l’enregistrement contient toutes les métadonnées relatives à chaque package disponible sur une source de package.

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur@type                     | Notes
------------------------------- | -----
RegistrationsBaseUrl            | La version initiale
RegistrationsBaseUrl/3.0.0-beta | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Réponses Gzippé
RegistrationsBaseUrl/3.6.0      | Inclut les packages de SemVer 2.0.0

Cela représente trois ruches distinctes d’enregistrement disponibles pour les différentes versions de client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Ces enregistrements ne sont pas compressés (ce qui signifie qu’ils utilisent un implicite `Content-Encoding: identity`). Packages de SemVer 2.0.0 sont **exclus** à partir de cette ruche.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Ces inscriptions sont compressées à l’aide `Content-Encoding: gzip`. Packages de SemVer 2.0.0 sont **exclus** à partir de cette ruche.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Ces inscriptions sont compressées à l’aide `Content-Encoding: gzip`. Packages de SemVer 2.0.0 sont **inclus** dans cette ruche.
Pour plus d’informations sur SemVer 2.0.0, consultez [prise en charge de SemVer 2.0.0 pour nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeurs. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge de la ressource d’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="registration-index"></a>Index de l’inscription

Les groupes de ressources de l’inscription du package métadonnées par ID de package. Il n’est pas possible d’obtenir des données relatives à plusieurs ID de package à la fois. Cette ressource ne fournit aucun moyen de découvrir les ID de package. Au lieu de cela, le client est censé pour déjà connaître l’ID de package souhaité. Les métadonnées disponibles sur chaque version du package varient par implémentation de serveur. Les objets BLOB d’inscription de package ont la structure hiérarchique suivante :

- **Index**: le point d’entrée pour les métadonnées du package, partagées par tous les packages sur une source avec le même ID de package.
- **Page**: un regroupement de versions de package. Le nombre de versions de package dans une page est défini par l’implémentation du serveur.
- **Feuille**: un document spécifique à une version de package unique.

L’URL de l’index de l’inscription est prévisible et peut être déterminé par le client étant donné un ID de package et de la ressource d’inscription `@id` valeur à partir de l’index de service. Les URL pour les pages d’inscription et les feuilles sont détectés en examinant l’index de l’inscription.

### <a name="registration-pages-and-leaves"></a>/ / Niveaux feuilles et les pages d’inscription

Bien qu’il ne soit pas strictement requis pour une implémentation de serveur stocker les feuilles de l’inscription dans les documents de page d’inscription distinctes, il est fortement recommandé de conserver de la mémoire du côté client. Au lieu d’incorporant tous les laisse de l’inscription dans l’index ou le stockage immédiatement les laisse dans les documents de la page, il est recommandé que l’implémentation du serveur définir certains éléments de recherche pour choisir entre les deux approches en fonction du nombre de versions de package ou taille cumulée de package quitte.

Stockage de toutes les versions de package (feuilles) dans les sauvegardes d’index d’enregistrement sur le nombre de requêtes HTTP nécessaire pour extraire les métadonnées du package mais signifie qu’un document plus grand doit être téléchargé et davantage de mémoire de client doit être alloué. En revanche, si l’implémentation du serveur stocke immédiatement laisse de l’inscription dans les documents de page distincte, le client doit effectuer davantage de demandes HTTP pour obtenir les informations dont il a besoin.

L’heuristique nuget.org utilise est comme suit : s’il existe 128 ou de plusieurs versions d’un package, diviser le laisse en pages de taille de 64. S’il existe moins de 128 versions, inline tous les laisse dans l’index de l’inscription.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Paramètres de la demande

Nom     | Vers l'avant     | Type    | Obligatoire | Notes
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | oui      | L’ID de package, minuscule

Le `LOWER_ID` valeur est l’ID de package souhaité minuscule en utilisant les règles implémentées par. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).

### <a name="response"></a>Réponse

La réponse est un document JSON qui a un objet racine avec les propriétés suivantes :

Nom  | Type             | Obligatoire | Notes
----- | ---------------- | -------- | -----
count | entiers          | oui      | Le nombre de pages d’inscription dans l’index
éléments | tableau d’objets | oui      | Le tableau de pages d’inscription

Chaque élément dans l’objet index `items` tableau est un objet JSON qui représente une page d’inscription.

#### <a name="registration-page-object"></a>Objet de page d’inscription

L’objet de page d’inscription trouvé dans l’index de l’enregistrement a les propriétés suivantes :

Nom   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | string           | oui      | L’URL vers la page d’inscription
count  | entiers          | oui      | Le numéro d’inscription laisse dans la page
éléments  | tableau d’objets | Non       | Le tableau des feuilles de l’inscription et leurs métadonnées associer
inférieur  | string           | oui      | La version SemVer 2.0.0 plus bas dans la page (incluse)
parent | string           | Non       | L’URL à l’index de l’inscription
supérieur  | string           | oui      | La version la plus récente de SemVer 2.0.0 dans la page (incluse)

Le `lower` et `upper` limites de l’objet de page sont utiles lorsque les métadonnées pour une version spécifique de page sont nécessaire.
Ces limites peuvent être utilisés pour extraire la page d’inscription uniquement nécessitée. Respectent les chaînes de version [les règles de version de NuGet](../reference/package-versioning.md). Les chaînes de version sont normalisées et n’incluent pas de métadonnées de build. Comme avec toutes les versions de l’écosystème NuGet, comparaison de chaînes de version est implémenté à l’aide de [règles de priorité de version SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

Le `parent` propriété apparaît uniquement si l’objet de la page d’inscription a le `items` propriété.

Si le `items` propriété n’est pas présente dans l’objet de la page d’inscription, l’URL spécifiée dans le `@id` doit être utilisé pour extraire les métadonnées sur les versions de package individuel. Le `items` tableau est parfois exclu de l’objet de page en guise d’optimisation. Si le nombre de versions d’un ID de package unique est très volumineux, le document d’index d’enregistrement sera massive et perte de temps de processus pour un client qui le concernent uniquement une version spécifique ou d’une petite plage de versions.

Notez que si le `items` propriété n’est présente, la `@id` propriété pas nécessaire d’utiliser, dans la mesure où toutes les données de la page est déjà incluse dans le `items` propriété.

Chaque élément dans l’objet page `items` tableau est un objet JSON qui représente une feuille d’inscription et les métadonnées associées.

#### <a name="registration-leaf-object-in-a-page"></a>Objet de feuille d’inscription dans une page

L’objet de feuille de l’inscription trouvé dans une page d’inscription a les propriétés suivantes :

Nom           | Type   | Obligatoire | Notes
-------------- | ------ | -------- | -----
@id            | string | oui      | L’URL à la feuille d’inscription
catalogEntry   | object | oui      | L’entrée de catalogue qui contient les métadonnées du package
packageContent | string | oui      | L’URL pour le contenu du package (fichier .nupkg)

Chaque objet de feuille de l’inscription représente les données associées à une version de package unique.

#### <a name="catalog-entry"></a>Entrée de catalogue

Le `catalogEntry` propriété de l’objet de feuille de l’enregistrement a les propriétés suivantes :

Nom                     | Type                       | Obligatoire | Notes
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | oui      | L’URL utilisée pour produire cet objet de document
authors                  | chaîne ou tableau de chaînes | Non       | 
dependencyGroups         | tableau d’objets           | Non       | Les dépendances du package, regroupées par le framework cible
Dépréciation              | object                     | Non       | La désapprobation associée au package
Description              | string                     | Non       | 
iconUrl                  | string                     | Non       | 
ID                       | string                     | oui      | L’ID du package
licenseUrl               | string                     | Non       |
licenseExpression        | string                     | Non       | 
liste                   | boolean                    | Non       | Doit être considérée comme répertoriée s’il est absent
minClientVersion         | string                     | Non       | 
projectUrl               | string                     | Non       | 
Publié                | string                     | Non       | Chaîne contenant un horodatage ISO8601 de quand le package a été publié
requireLicenseAcceptance | boolean                    | Non       | 
résumé                  | string                     | Non       | 
étiquettes                     | chaîne ou tableau de chaînes  | Non       | 
titre                    | string                     | Non       | 
version                  | string                     | oui      | La chaîne de version complète après normalisation

Le package `version` propriété est la chaîne de version complète après la normalisation. Cela signifie que les données de build de SemVer 2.0.0 peuvent être incluses ici.

Le `dependencyGroups` propriété est un tableau d’objets représentant les dépendances du package, regroupées par le framework cible. Si le package n’a aucune dépendance, le `dependencyGroups` manquant dans la propriété, un tableau vide, ou le `dependencies` propriété de tous les groupes est vide ou manquant.

La valeur de la `licenseExpression` propriété respecte [syntaxe d’expression de licence NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Groupe de dépendances de package

Chaque objet de dépendance de groupe a les propriétés suivantes :

Nom            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
targetFramework | string           | Non       | Le framework cible que ces dépendances sont applicables à
dépendances    | tableau d’objets | Non       |

Le `targetFramework` chaîne utilise le format implémenté par la bibliothèque de .NET de NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Si aucun `targetFramework` est spécifié, le groupe de dépendance s’applique à toutes les infrastructures cibles.

Le `dependencies` propriété est un tableau d’objets, représentant chacun une dépendance de package du package actuel.

#### <a name="package-dependency"></a>Dépendance de package

Chaque dépendance de package a les propriétés suivantes :

Nom         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
ID           | string | oui      | L’ID de la dépendance de package
range        | object | Non       | Autorisées [plage de versions](../reference/package-versioning.md#version-ranges-and-wildcards) de la dépendance
inscription | string | Non       | L’URL à l’index de l’inscription de cette dépendance

Si le `range` propriété est exclue ou une chaîne vide, le client doit utiliser par défaut la plage de versions `(, )`. Autrement dit, n’importe quelle version de la dépendance est autorisée.

#### <a name="package-deprecation"></a>Désapprobation de package

Désapprobation de chaque package a les propriétés suivantes :

Nom             | Type             | Obligatoire | Notes
---------------- | ---------------- | -------- | -----
raisons          | tableau de chaînes | oui      | Les raisons pourquoi le package a été déconseillé
message          | string           | Non       | Les détails supplémentaires sur cette utilisation déconseillée
alternatePackage | object           | Non       | La dépendance de package qui doit être utilisée à la place

Le `reasons` propriété doit contenir au moins une chaîne et doit contenir seulement des chaînes dans le tableau suivant :

Raison       | Description             
------------ | -----------
Hérité       | Le package n’est pas conservé
CriticalBugs | Le package comporte des bogues qui le rendent inapproprié pour l’utilisation
Autre        | Le package est déconseillé en raison d’une raison pas sur cette liste

Si le `reasons` propriété contient des chaînes qui ne sont pas à partir de l’ensemble connu, ils doivent être ignorés. Les chaînes respectent la casse, de sorte que `legacy` doit être traité comme `Legacy`. Il n’existe aucune restriction de classement dans le groupe, afin des chaînes peuvent être organisés dans n’importe quel ordre arbitraire. En outre, si la propriété contient uniquement les chaînes qui ne sont pas à partir de l’ensemble connu, il doit être traité comme s’il ne contenait la chaîne « Autre ».

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Dans ce cas particulier, l’index de l’inscription a la page d’inscription inline sans demandes supplémentaires sont nécessaires pour extraire les métadonnées sur les versions de package individuel.

## <a name="registration-page"></a>Page d’inscription

La page d’inscription contient des feuilles de l’inscription. L’URL pour récupérer une page d’inscription est déterminé par le `@id` propriété dans le [objet de page d’inscription](#registration-page-object) mentionné ci-dessus.

Lorsque le `items` tableau n’est pas fourni dans l’index de l’inscription, une requête HTTP GET de la `@id` valeur retournera un document JSON qui a un objet en tant que sa racine. L’objet a les propriétés suivantes :

Nom   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | string           | oui      | L’URL vers la page d’inscription
count  | entiers          | oui      | Le numéro d’inscription laisse dans la page
éléments  | tableau d’objets | oui      | Le tableau des feuilles de l’inscription et leurs métadonnées associer
inférieur  | string           | oui      | La version SemVer 2.0.0 plus bas dans la page (incluse)
parent | string           | oui      | L’URL à l’index de l’inscription
supérieur  | string           | oui      | La version la plus récente de SemVer 2.0.0 dans la page (incluse)

La forme des objets de feuille d’inscription est le même que dans l’index de l’inscription [ci-dessus](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Feuille de l’inscription

La feuille d’inscription contient des informations sur un ID de package spécifique et une version. Les métadonnées relatives à la version spécifique n’est peut-être pas disponibles dans ce document. Métadonnées du package doivent être extraites depuis la [index de l’inscription](#registration-index) ou [page d’inscription](#registration-page) (qui est découvert à l’aide de l’index de l’inscription).

L’URL pour récupérer une feuille d’inscription est obtenu à partir de la `@id` propriété d’un objet de feuille de l’inscription dans un index de l’inscription ou de la page d’inscription.

La feuille d’inscription est un document JSON avec un objet racine avec les propriétés suivantes :

Nom           | Type    | Obligatoire | Notes
-------------- | ------- | -------- | -----
@id            | string  | oui      | L’URL à la feuille d’inscription
catalogEntry   | string  | Non       | L’URL à l’entrée de catalogue qui a produit ces feuille
liste         | boolean | Non       | Doit être considérée comme répertoriée s’il est absent
packageContent | string  | Non       | L’URL pour le contenu du package (fichier .nupkg)
Publié      | string  | Non       | Chaîne contenant un horodatage ISO8601 de quand le package a été publié
inscription   | string  | Non       | L’URL à l’index de l’inscription

> [!Note]
> Sur nuget.org, le `published` a la valeur année 1900 lorsque le package n’est pas répertorié.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
