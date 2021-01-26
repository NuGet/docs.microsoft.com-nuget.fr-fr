---
title: Index de service, API NuGet
description: L’index de service est le point d’entrée de l’API HTTP NuGet et énumère les fonctionnalités du serveur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775357"
---
# <a name="service-index"></a>Index de service

L’index de service est un document JSON qui est le point d’entrée d’une source de package NuGet et permet à une implémentation cliente de découvrir les fonctionnalités de la source du package. L’index de service est un objet JSON avec deux propriétés obligatoires : `version` (la version de schéma de l’index de service) et `resources`  (les points de terminaison ou les fonctionnalités de la source du package).

l’index de service de NuGet. org se trouve à l’emplacement `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Contrôle de version

La `version` valeur est une chaîne de version analysable SemVer 2.0.0 qui indique la version de schéma de l’index de service. L’API impose que la chaîne de version ait un numéro de version principale de `3` . À mesure que des modifications sans rupture sont apportées au schéma d’index de service, la version mineure de la chaîne de version est augmentée.

Chaque ressource de l’index de service est gérée indépendamment de la version du schéma d’index de service.

La version du schéma actuel est `3.0.0` . La `3.0.0` version est fonctionnellement équivalente à l’ancienne `3.0.0-beta.1` version, mais elle doit être préférée, car elle communique plus clairement le schéma stable et défini.

## <a name="http-methods"></a>Méthodes HTTP

L’index de service est accessible à l’aide des méthodes HTTP `GET` et `HEAD` .

## <a name="resources"></a>Ressources

La `resources` propriété contient un tableau de ressources prises en charge par cette source de package.

### <a name="resource"></a>Ressource

Une ressource est un objet dans le `resources` tableau. Il représente une fonctionnalité avec version d’une source de package. Une ressource a les propriétés suivantes :

Nom          | Type   | Obligatoire | Notes
------------- | ------ | -------- | -----
@id           | string | Oui      | URL de la ressource
@type         | string | Oui      | Constante de chaîne représentant le type de ressource
comment       | string | non       | Description lisible par l’utilisateur de la ressource

`@id`Est une URL qui doit être absolue et doit avoir le schéma http ou HTTPS.

`@type`Est utilisé pour identifier le protocole spécifique à utiliser lors de l’interaction avec la ressource. Le type de la ressource est une chaîne opaque mais a généralement le format :

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

Les clients sont censés coder en dur les `@type` valeurs qu’ils comprennent et les Rechercher dans l’index de service d’une source de package. Les valeurs exactes `@type` utilisées aujourd’hui sont énumérées sur les documents de référence de ressource individuels répertoriés dans la [vue d’ensemble](overview.md#resources-and-schema)de l’API.

Dans le cadre de cette documentation, la documentation sur les différentes ressources sera essentiellement regroupée par le `{RESOURCE_NAME}` trouvé dans l’index de service, ce qui est analogue au regroupement par scénario. 

Il n’est pas obligatoire que chaque ressource dispose d’un ou d’un unique `@id` `@type` . C’est à l’implémentation cliente de déterminer la ressource à préférer à une autre. Une implémentation possible est que les ressources de même ou compatibles `@type` peuvent être utilisées en mode tourniquet (Round Robin) en cas d’échec de connexion ou d’erreur de serveur.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [service-index.json](./_data/service-index.json)]
