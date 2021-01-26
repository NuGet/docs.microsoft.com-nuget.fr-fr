---
title: Contenu du package, API NuGet
description: L’adresse de base du package est une interface simple permettant d’extraire le package lui-même.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773940"
---
# <a name="package-content"></a>Contenu des packages

Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (fichier. nupkg) à l’aide de l’API V3. La ressource utilisée pour récupérer le contenu du package est la `PackageBaseAddress` ressource trouvée dans l' [index de service](service-index.md). Cette ressource permet également la détection de toutes les versions d’un package, répertoriées ou désactivées.

Cette ressource est communément appelée « adresse de base du package » ou « conteneur plat ».

## <a name="versioning"></a>Contrôle de version

La `@type` valeur suivante est utilisée :

Valeur @type              | Notes
------------------------ | -----
PackageBaseAddress/3.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la valeur de ressource mentionnée ci-dessus `@type` . Dans le document suivant, l’URL de base de l’espace réservé `{@id}` sera utilisée.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource d’inscription prennent en charge les méthodes HTTP `GET` et `HEAD` .

## <a name="enumerate-package-versions"></a>Énumérer les versions du package

Si le client connaît un ID de package et souhaite découvrir quelles versions de package la source du package a disponibles, le client peut construire une URL prévisible pour énumérer toutes les versions du package. Cette liste est censée être une « liste de répertoires » pour l’API de contenu de package mentionnée ci-dessous.

> [!Note]
> Cette liste contient à la fois les versions de packages listées et désinscrites.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom     | Dans     | Type    | Obligatoire | Notes
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | Oui      | ID de package, en minuscules

La `LOWER_ID` valeur est l’ID de package souhaité en minuscules à l’aide des règles implémentées par. Méthode du réseau [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

### <a name="response"></a>response

Si la source du package n’a pas de version de l’ID de package fourni, un code d’État 404 est retourné.

Si la source du package a une ou plusieurs versions, un code d’état 200 est retourné. Le corps de la réponse est un objet JSON avec la propriété suivante :

Nom     | Type             | Obligatoire | Notes
-------- | ---------------- | -------- | -----
versions | tableau de chaînes | Oui      | Les versions disponibles

Les chaînes du `versions` tableau sont toutes des [chaînes de version NuGet, normalisées](../concepts/package-versioning.md#normalized-version-numbers)et en minuscules. Les chaînes de version ne contiennent pas de métadonnées de build SemVer 2.0.0.

L’objectif est que les chaînes de version trouvées dans ce tableau peuvent être utilisées textuellement pour les `LOWER_VERSION` jetons trouvés dans les points de terminaison suivants.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Télécharger le contenu du package (. nupkg)

Si le client connaît un ID de package et une version et qu’il souhaite télécharger le contenu du package, il n’a besoin que de créer l’URL suivante :

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom          | Dans     | Type   | Obligatoire | Notes
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | Oui      | ID de package, minuscules
LOWER_VERSION | URL    | string | Oui      | Version du package, normalisée et en minuscules

`LOWER_ID`Et `LOWER_VERSION` sont en minuscules à l’aide des règles implémentées par. Du réseau[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
.

`LOWER_VERSION`Est la version de package souhaitée normalisée à l’aide des [règles de normalisation](../concepts/package-versioning.md#normalized-version-numbers)de la version de NuGet. Cela signifie que les métadonnées de build autorisées par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.

### <a name="response-body"></a>Response body

Si le package existe sur la source du package, un code d’état 200 est retourné. Le corps de la réponse sera le contenu du package lui-même.

Si le package n’existe pas sur la source du package, un code d’État 404 est retourné.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Exemple de réponse

Flux binaire qui est le. nupkg pour Newtonsoft.Jssur la version 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Télécharger le manifeste du package (. NuSpec)

Si le client connaît un ID de package et une version et qu’il souhaite télécharger le manifeste du package, il n’a besoin que de créer l’URL suivante :

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom          | Dans     | Type   | Obligatoire | Notes
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | Oui      | ID de package, minuscules
LOWER_VERSION | URL    | string | Oui      | Version du package, normalisée et en minuscules

`LOWER_ID`Et `LOWER_VERSION` sont en minuscules à l’aide des règles implémentées par. Méthode du réseau [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

`LOWER_VERSION`Est la version de package souhaitée normalisée à l’aide des [règles de normalisation](../concepts/package-versioning.md#normalized-version-numbers)de la version de NuGet. Cela signifie que les métadonnées de build autorisées par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.

### <a name="response-body"></a>Response body

Si le package existe sur la source du package, un code d’état 200 est retourné. Le corps de la réponse sera le manifeste du package, qui est le. NuSpec contenu dans le fichier. nupkg correspondant. Le fichier. NuSpec est un document XML.

Si le package n’existe pas sur la source du package, un code d’État 404 est retourné.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Exemple de réponse

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
