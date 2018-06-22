---
title: Contenu du package NuGet API
description: L’adresse de base du package est une interface simple pour extraire le package lui-même.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819175"
---
# <a name="package-content"></a>Contenu du package

Il est possible de générer une URL pour extraire le contenu d’un package arbitraire (le fichier .nupkg) à l’aide de l’API V3. La ressource utilisée pour extraire le contenu du package est le `PackageBaseAddress` ressource trouvée dans le [index service](service-index.md). Cette ressource permet également la découverte de toutes les versions d’un package répertorié ou non listées.

Cette ressource est communément soit « package adresse de base » ou « conteneur plat ».

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` valeur est utilisée :

Valeur @type              | Notes
------------------------ | -----
PackageBaseAddress/3.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur. Dans le document suivant, les URL de base de l’espace réservé `{@id}` sera utilisé.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvés dans la prise en charge des ressources de l’inscription, les méthodes HTTP `GET` et `HEAD`.

## <a name="enumerate-package-versions"></a>Énumérer des versions de package

Si le client connaît un ID de package et souhaite découvrir qui package versions du package source disponible, le client peut construire une URL prévisible pour énumérer toutes les versions de package. Cette liste doit être une « liste de répertoires » pour l’API de contenu de package indiqué ci-dessous.

> [!Note]
> Cette liste contient les deux versions de package répertoriés et non répertoriés.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Paramètres de la demande

Name     | Vers l'avant     | Type    | Obligatoire | Notes
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | chaîne  | oui      | L’ID de package, en minuscules

Le `LOWER_ID` valeur est l’ID de package souhaité minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).

### <a name="response"></a>Réponse

Si la source du package n’a aucune version de l’ID de package fourni, un code de 404 état est retourné.

Si la source du package a une ou plusieurs versions, un code de 200 état est retourné. Le corps de réponse est un objet JSON avec la propriété suivante :

Name     | Type             | Obligatoire | Notes
-------- | ---------------- | -------- | -----
versions | Tableau de chaînes | oui      | Le package ID disponibles

Les chaînes dans le `versions` tableau toutes les minuscules, [normalisée des chaînes de version de NuGet](../reference/package-versioning.md#normalized-version-numbers). Les chaînes de version ne contiennent pas toutes les métadonnées de la build SemVer 2.0.0.

L’objectif est que les chaînes de version trouvées dans ce tableau peuvent être utilisés textuellement pour le `LOWER_VERSION` jetons situés dans les points de terminaison suivants.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Télécharger le contenu du package (.nupkg)

Si le client connaît un ID de package et la version et souhaite télécharger le contenu du package, ils doivent uniquement construire l’URL suivante :

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Paramètres de la demande

Name          | Vers l'avant     | Type   | Obligatoire | Notes
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | chaîne | oui      | L’ID de package, en minuscules
LOWER_VERSION | URL    | chaîne | oui      | La version du package, normalisé et minuscule

Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).

Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers). Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.

### <a name="response-body"></a>Corps de réponse

Si le package existe sur la source du package, un code de 200 état est retourné. Le corps de réponse sera le contenu du package lui-même.

Si le package n’existe pas sur la source du package, un code de 404 état est retourné.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Exemple de réponse

Le flux binaire qui est la .nupkg pour Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Télécharger le manifeste du package (.nuspec)

Si le client connaît un ID de package et la version et souhaite télécharger le manifeste du package, ils doivent uniquement construire l’URL suivante :

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Paramètres de la demande

Name          | Vers l'avant     | Type    | Obligatoire | Notes
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | chaîne  | oui      | L’ID de package, en minuscules
LOWER_VERSION | URL    | entiers | oui      | La version du package, normalisé et minuscule

Les deux `LOWER_ID` et `LOWER_VERSION` sont minuscule à l’aide des règles implémentées par. De NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (méthode).

Le `LOWER_VERSION` est la version du package souhaitée normalisée par rapport à l’aide de la version de NuGet [règles de normalisation](../reference/package-versioning.md#normalized-version-numbers). Cela signifie que les métadonnées de build qui sont autorisée par la spécification SemVer 2.0.0 doivent être exclues dans ce cas.

### <a name="response-body"></a>Corps de réponse

Si le package existe sur la source du package, un code de 200 état est retourné. Le corps de réponse sera le manifeste du package, qui est le .nuspec contenus dans le .nupkg correspondant. Le .nuspec est un document XML.

Si le package n’existe pas sur la source du package, un code de 404 état est retourné.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Exemple de réponse

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
