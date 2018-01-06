---
title: "Package NuGet API métadonnées | Documents Microsoft"
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
ms.assetid: 96b07019-c2e1-4f40-9290-f65ad71af3b1
description: "L’URL de base de l’inscription de package permet de récupérer les métadonnées à propos des packages."
keywords: "Métadonnées de package NuGet API, l’inscription NuGet API, les API NuGet packages non listées"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1aabe6ae5c661e12b2639700813946e7a9a58b24
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="package-metadata"></a>Métadonnées du package

Il est possible de récupérer les métadonnées sur les packages disponibles sur une source de package à l’aide de l’API de V3 NuGet. Ces métadonnées peuvent être extraites à l’aide de la `RegistrationsBaseUrl` ressource trouvée dans le [index service](service-index.md).

La collection des documents situés sous `RegistrationsBaseUrl` sont souvent appelés « inscriptions » ou « objets BLOB de l’inscription ». L’ensemble de documents sous un seul `RegistrationsBaseUrl` est appelé une « ruche de l’inscription ». Une ruche de l’enregistrement contient toutes les métadonnées relatives à chaque package disponible sur une source de package.

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` les valeurs sont utilisées :

Valeur @type                     | Notes
------------------------------- | -----
RegistrationsBaseUrl            | La version initiale
RegistrationsBaseUrl/3.0.0-beta | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Réponses Gzippé
RegistrationsBaseUrl/3.6.0      | Inclut les packages SemVer 2.0.0

Cela représente trois ruches distinctes d’enregistrement disponibles pour les différentes versions de client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Ces enregistrements ne sont pas compressés (c'est-à-dire qu’ils utilisent un implicite `Content-Encoding: identity`). Les packages SemVer 2.0.0 sont **exclus** à partir de cette ruche.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Ces enregistrements sont compressées à l’aide `Content-Encoding: gzip`. Les packages SemVer 2.0.0 sont **exclus** à partir de cette ruche.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Ces enregistrements sont compressées à l’aide `Content-Encoding: gzip`. Les packages SemVer 2.0.0 sont **inclus** de cette ruche.
Pour plus d’informations sur SemVer 2.0.0, consultez [prise en charge SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeurs. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="registration-index"></a>Index de l’enregistrement

Les groupes de ressources de l’inscription du package métadonnées par ID de package. Il n’est pas possible d’obtenir des données sur plusieurs ID de package à la fois. Cette ressource ne fournit aucun moyen de détecter l’ID de package. Au lieu de cela, le client est censé connaissez l’ID de package de votre choix. Les métadonnées disponibles sur chaque version de package varient par l’implémentation de serveur. Les objets BLOB d’inscription de package ont la structure hiérarchique suivante :

- **Index**: le point d’entrée pour les métadonnées de package partagé par tous les packages sur une source avec le même ID de package.
- **Page**: regroupement des versions de package. Le nombre de versions de package dans une page est défini par l’implémentation du serveur.
- **Feuille**: un document spécifique à une version de package unique.

L’URL de l’index de l’enregistrement est prévisible et peut être déterminé par le client étant donné un ID de package et de la ressource d’inscription `@id` la valeur de l’index de service. Les URL pour les pages d’inscription et les feuilles sont détectés en examinant l’index de l’enregistrement.

### <a name="registration-pages-and-leaves"></a>Feuilles et pages d’inscription

Bien qu’il ne soit pas strictement requis pour une implémentation de serveur stocker les feuilles de l’inscription dans des documents de page d’inscription distinctes, il est recommandé d’économiser la mémoire du côté client. Au lieu d’incorporation (inlining) de tous les laisse de l’inscription dans l’index ou immédiatement le stockage laisse dans les documents de la page, il est recommandé que l’implémentation du serveur définir certains éléments de recherche pour choisir entre les deux approches en fonction du nombre de versions de package ou quitte la taille cumulée de package.

Le stockage de toutes les versions de package (feuilles) dans les sauvegardes d’index d’enregistrement sur le nombre de requêtes HTTP nécessaire pour extraire les métadonnées du package mais signifie qu’un document plus volumineux doit être téléchargé et davantage de mémoire de client doit être allouée. En revanche, si l’implémentation du serveur stocke immédiatement laisse de l’inscription dans les documents d’une page distincte, le client doit effectuer davantage de requêtes HTTP pour obtenir les informations dont il a besoin.

L’heuristique nuget.org utilise est comme suit : s’il existe 128 ou de plusieurs versions d’un package, scinder le laisse en pages de taille de 64. S’il existe moins de 128 versions, inline tous les laisse dans l’index de l’enregistrement.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Paramètres de la demande

Name     | Vers l'avant     | Type    | Obligatoire | Notes
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | chaîne  | oui      | L’ID de package, minuscule

Le `LOWER_ID` valeur est l’ID de package souhaité minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).

### <a name="response"></a>Réponse

La réponse est un document JSON qui possède un objet racine avec les propriétés suivantes :

Name  | Type             | Obligatoire | Notes
----- | ---------------- | -------- | -----
count | entiers          | oui      | Le nombre de pages d’inscription dans l’index
Éléments | Tableau d’objets | oui      | Le tableau des pages d’inscription

Chaque élément dans l’objet index `items` tableau est un objet JSON qui représente une page d’inscription.

#### <a name="registration-page-object"></a>Objet de page d’inscription

L’objet de page d’inscription dans l’index de l’enregistrement a les propriétés suivantes :

Name   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | chaîne           | oui      | L’URL vers la page d’inscription
count  | entiers          | oui      | Le numéro d’enregistrement laisse dans la page
Éléments  | Tableau d’objets | Non       | Le tableau de feuilles de l’inscription et leurs métadonnées associées
Inférieure  | chaîne           | oui      | La version la plus basse SemVer 2.0.0 dans la page (incluse)
Parent | chaîne           | Non       | L’URL à l’index de l’enregistrement
supérieur  | chaîne           | oui      | La version la plus récente SemVer 2.0.0 dans la page (incluse)

Le `lower` et `upper` limites de l’objet de la page sont utiles lorsque les métadonnées pour une version de la page spécifique sont nécessaire.
Ces limites peuvent être utilisés pour extraire la page d’inscription uniquement si nécessaire. Les chaînes de version est conforme aux [les règles de version de NuGet](../reference/package-versioning.md). Les chaînes de version sont normalisés et n’incluent pas de métadonnées de la build. Comme avec toutes les versions de l’écosystème de NuGet, la comparaison de chaînes de version est implémentée à l’aide de [SemVer 2.0.0's les règles de priorité de version](http://semver.org/spec/v2.0.0.html#spec-item-11).

Le `parent` propriété apparaît uniquement si l’objet de la page d’inscription a le `items` propriété.

Si le `items` propriété n’est pas présente dans l’objet de la page d’inscription, l’URL spécifiée dans le `@id` doit être utilisé pour extraire des métadonnées sur les versions de package individuels. Le `items` tableau est parfois exclu de l’objet page en guise d’optimisation. Si le nombre de versions d’un ID de package unique est très volumineux, le document d’index d’enregistrement sera massive et perte de temps de processus pour un client uniquement attentive à une version spécifique ou d’une petite plage de versions.

Notez que si le `items` propriété n’est présente, la `@id` propriété ne doive pas être utilisée, car toutes les données de la page est déjà inline dans le `items` propriété.

Chaque élément dans l’objet page `items` tableau est un objet JSON qui représente une feuille de l’inscription et il a des métadonnées associées.

#### <a name="registration-leaf-object-in-a-page"></a>Objet de feuille de l’enregistrement dans une page

L’objet de feuille de l’inscription trouvé dans une page d’inscription a les propriétés suivantes :

Name           | Type   | Obligatoire | Notes
-------------- | ------ | -------- | -----
@id            | chaîne | oui      | L’URL de la feuille de l’inscription
catalogEntry   | object | oui      | L’entrée du catalogue contenant les métadonnées de package
packageContent | chaîne | oui      | L’URL pour le contenu du package (.nupkg)

Chaque objet de feuille d’enregistrement représente les données associées à une version de package unique.

#### <a name="catalog-entry"></a>Entrée de catalogue

Le `catalogEntry` propriété de l’objet de feuille de l’enregistrement a les propriétés suivantes :

Name                     | Type                       | Obligatoire | Notes
------------------------ | -------------------------- | -------- | -----
@id                      | chaîne                     | oui      | L’URL du document utilisé pour produire cet objet
authors                  | chaîne ou tableau de chaînes | Non       | 
dependencyGroups         | Tableau d’objets           | Non       | L’URL pour le contenu du package (.nupkg)
Description              | chaîne                     | Non       | 
iconUrl                  | chaîne                     | Non       | 
ID                       | chaîne                     | oui      | L’ID du package
licenseUrl               | chaîne                     | Non       | 
liste                   | boolean                    | Non       | Doit être considéré comme répertoriée si elle est absente
minClientVersion         | chaîne                     | Non       | 
projectUrl               | chaîne                     | Non       | 
publié                | chaîne                     | Non       | Une chaîne contenant un horodatage ISO 8601 de lorsque le package a été publié.
requireLicenseAcceptance | boolean                    | Non       | 
résumé                  | chaîne                     | Non       | 
étiquettes                     | chaîne ou tableau de chaînes  | Non       | 
titre                    | chaîne                     | Non       | 
version                  | chaîne                     | oui      | La version du package

Le `dependencyGroups` propriété est un tableau d’objets représentant les dépendances du package, regroupés par le framework cible. Si le package ne possède pas de dépendances, le `dependencyGroups` manquant dans la propriété, un tableau vide, ou le `dependencies` propriété de tous les groupes est vide ou manquant.

#### <a name="package-dependency-group"></a>Groupe de packages de dépendance

Chaque objet de dépendance de groupe a les propriétés suivantes :

Name            | Type             | Obligatoire | Notes
--------------- | ---------------- | -------- | -----
targetFramework | chaîne           | Non       | La cible de .NET framework ces dépendances sont applicables à
dépendances    | Tableau d’objets | Non       |

Le `targetFramework` chaîne utilise le format implémenté par la bibliothèque de .NET de NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Si aucun `targetFramework` est spécifié, le groupe de dépendance s’applique à toutes les infrastructures de cible.

Le `dependencies` propriété est un tableau d’objets, représentant chacune une dépendance de package du package en cours.

#### <a name="package-dependency"></a>Dépendance de package

Chaque dépendance de package a les propriétés suivantes :

Name         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
ID           | chaîne | oui      | L’ID de la dépendance de package
range        | object | Non       | Autorisées [la plage de versions](../reference/package-versioning.md#version-ranges-and-wildcards) de la dépendance
inscription | chaîne | Non       | L’URL à l’index de l’enregistrement de cette dépendance

Si le `range` propriété est exclue ou une chaîne vide, le client doit utiliser par défaut pour la plage de versions `(, )`. Autrement dit, n’importe quelle version de la dépendance est autorisée.

### <a name="sample-request"></a>Exemple de demande

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>Exemple de réponse 

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Dans ce cas particulier, l’index de l’enregistrement a la page d’inscription inline donc aucune demande supplémentaire n’est nécessaire pour extraire les métadonnées sur les versions de package individuels.

## <a name="registration-page"></a>Page d’inscription

La page d’inscription contient des feuilles de l’inscription. L’URL pour extraire une page d’inscription est déterminée par le `@id` propriété dans le [objet de page d’inscription](#registration-page-object) mentionnés ci-dessus.

Lorsque le `items` tableau n’est pas fourni dans l’index de l’enregistrement, d’une demande HTTP GET de la `@id` valeur retournera un document JSON qui dispose d’un objet en tant que racine. L’objet a les propriétés suivantes :

Name   | Type             | Obligatoire | Notes
------ | ---------------- | -------- | -----
@id    | chaîne           | oui      | L’URL vers la page d’inscription
count  | entiers          | oui      | Le numéro d’enregistrement laisse dans la page
Éléments  | Tableau d’objets | oui      | Le tableau de feuilles de l’inscription et leurs métadonnées associées
Inférieure  | chaîne           | oui      | La version la plus basse SemVer 2.0.0 dans la page (incluse)
Parent | chaîne           | oui      | L’URL à l’index de l’enregistrement
supérieur  | chaîne           | oui      | La version la plus récente SemVer 2.0.0 dans la page (incluse)

La forme des objets de feuille de l’inscription est le même que dans l’index de l’enregistrement [ci-dessus](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Exemple de demande

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Feuille de l’inscription

La feuille de l’enregistrement contient des informations sur un ID de package spécifique et une version. Les métadonnées relatives à la version spécifique n’est peut-être pas disponible dans ce document. Les métadonnées du package doivent être extraites depuis la [index de l’enregistrement](#registration-index) ou [page d’inscription](#registration-page) (qui est découvert à l’aide de l’index de l’enregistrement).

L’URL pour extraire d’une feuille de l’enregistrement est obtenu à partir de la `@id` propriété d’un objet de feuille de l’enregistrement dans un index de l’enregistrement ou de la page d’inscription.

La feuille de l’enregistrement est un document JSON avec un objet racine avec les propriétés suivantes :

Name           | Type    | Obligatoire | Notes
-------------- | ------- | -------- | -----
@id            | chaîne  | oui      | L’URL de la feuille de l’inscription
catalogEntry   | chaîne  | Non       | L’URL à l’entrée de catalogue qui a produit ces feuille
liste         | boolean | Non       | Doit être considéré comme répertoriée si elle est absente
packageContent | chaîne  | Non       | L’URL pour le contenu du package (.nupkg)
publié      | chaîne  | Non       | Une chaîne contenant un horodatage ISO 8601 de lorsque le package a été publié.
inscription   | chaîne  | Non       | L’URL à l’index de l’enregistrement

> [!Note]
> Sur nuget.org, le `published` a la valeur année 1900 lorsque le package n’est pas spécifié.

### <a name="sample-request"></a>Exemple de demande

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
