---
title: Index de service, API NuGet
description: L’index de service est le point d’entrée de l’API HTTP de NuGet et énumère les fonctionnalités du serveur.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324719"
---
# <a name="service-index"></a>Index de service

L’index de service est un document JSON qui est le point d’entrée pour une source de package NuGet et permet une implémentation de client découvrir les fonctionnalités de la source du package. L’index de service est un objet JSON avec deux propriétés requises : `version` (la version de schéma de l’index de service) et `resources` (les points de terminaison ou les capacités de la source du package).

index de service de NuGet.org se trouve dans `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Gestion de version

Le `version` valeur est une chaîne de version analysable SemVer 2.0.0 qui indique la version du schéma de l’index de service. L’API impose que la chaîne de version a un numéro de version principale de `3`. Quand des modifications sans rupture sont apportées au schéma d’index de service, version mineure de la chaîne de version sera augmentée.

Chaque ressource dans l’index de service est gérée indépendamment de la version de schéma d’index service.

La version de schéma actuelle est `3.0.0`. Le `3.0.0` version est fonctionnellement équivalente à l’ancien `3.0.0-beta.1` version mais il est préférable qu’il communique plus clairement le schéma stable, défini.

## <a name="http-methods"></a>Méthodes HTTP

L’index de service est accessible à l’aide de méthodes HTTP `GET` et `HEAD`.

## <a name="resources"></a>Ressources

Le `resources` propriété contient un ensemble de ressources pris en charge par cette source de package.

### <a name="resource"></a>Ressource

Une ressource est un objet dans le `resources` tableau. Il représente une fonctionnalité avec contrôle de version d’une source de package. Une ressource a les propriétés suivantes :

Name          | Type   | Obligatoire | Notes
------------- | ------ | -------- | -----
@id           | chaîne | oui      | L’URL de la ressource
@type         | chaîne | oui      | Constante de chaîne représentant le type de ressource
commentaire       | chaîne | Non       | Description explicite de la ressource

Le `@id` est une URL qui doit être absolu et doit avoir le schéma HTTP ou HTTPS.

Le `@type` est utilisé pour identifier le protocole spécifique à utiliser lors de l’interaction avec les ressources. Le type de la ressource est une chaîne opaque, mais est généralement au format :

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Les clients sont censés coder en dur le `@type` valeurs qu’ils comprennent et les consulter dans l’index de service d’une source de package. Exactement `@type` valeurs utilisés aujourd'hui sont énumérées sur les documents de référence de ressource individuelle répertoriées dans le [vue d’ensemble de l’API](overview.md#resources-and-schema).

Pour des raisons de cette documentation, la documentation sur les différentes ressources est essentiellement regroupée par le `{RESOURCE_NAME}` trouvé dans l’index de service qui est analogue à un regroupement par scénario. 

Il n’est pas nécessaire que chaque ressource a une valeur unique `@id` ou `@type`. C’est à l’implémentation de client pour déterminer quelle ressource préférez plutôt qu’un autre. Une implémentation possible est que les ressources d’identiques ou compatibles `@type` peut être utilisé de manière alternée en cas d’erreur de serveur ou d’échec de connexion.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [service-index.json](./_data/service-index.json)]
