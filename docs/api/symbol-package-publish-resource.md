---
title: Envoyez des Packages de symboles, API NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Le service de publication permet aux clients de publier de nouveaux packages de symboles.
keywords: Package de symboles NuGet API push
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580412"
---
# <a name="push-symbol-packages"></a>Packages de symboles de push

Il est possible de packages de symboles push ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API V3 de NuGet.
Ces opérations sont basées issu de la `SymbolPackagePublish` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Ce qui suit `@type` valeur est utilisée :

Valeur@type                  | Notes
--------------------        | -----
SymbolPackagePublish/4.9.0  | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `SymbolPackagePublish/4.9.0` ressource dans la source de package [index de service](service-index.md). Pour obtenir la documentation ci-dessous, les URL de nuget.org est utilisé. Envisagez `https://www.nuget.org/api/v2/symbolpackage` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.

## <a name="http-methods"></a>Méthodes HTTP

Le `PUT` méthode HTTP est pris en charge par cette ressource. 

## <a name="push-a-symbol-package"></a>Envoyer un package de symboles

NuGet.org prend en charge l’exécution de type push nouveau format de packages de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API suivante. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Les packages de symboles avec le même ID et la version peuvent être soumis plusieurs fois. Un package de symboles est rejeté dans les cas suivants.
- Un package avec le même ID et la version n’existe pas.
- Un package de symboles avec le même ID et la version a été envoyé, mais n’est pas encore publié.
- Le package de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) n’est pas valide (consultez [contraintes de package de symboles](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client. Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.

### <a name="request-body"></a>Corps de la requête

Le corps de demande pour le push de symbole est identique à celle dont le corps d’une demande de push de package (consultez [push de package et de supprimer](package-publish-resource.md)). 

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
201         | Le package de symboles a été correctement envoyé.
400         | Le package de symboles fourni n’est pas valide.
401         | L’utilisateur n’est pas autorisé à effectuer cette action.
404         | Un package avec l’ID et la version fournie correspondant n’existe pas.
409         | Un package de symboles avec l’ID et la version fournie a été envoyé, mais il n'est pas encore disponible.
413         | Le package est trop volumineux.

