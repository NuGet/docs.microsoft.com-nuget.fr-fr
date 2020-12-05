---
title: Packages Push Symbol, API NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Le service de publication permet aux clients de publier de nouveaux packages de symboles.
keywords: Package de symboles push de l’API NuGet
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738875"
---
# <a name="push-symbol-packages"></a>Envoyer des packages de symboles

Il est possible d’envoyer des packages de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API NuGet v3.
Ces opérations sont basées sur la `SymbolPackagePublish` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

La `@type` valeur suivante est utilisée :

Valeur @type                 | Notes
--------------------        | -----
SymbolPackagePublish/4.9.0  | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `SymbolPackagePublish/4.9.0` ressource dans l’index de [service](service-index.md)de la source du package. Pour la documentation ci-dessous, l’URL de NuGet. org est utilisée. Considérez `https://www.nuget.org/api/v2/symbolpackage` comme un espace réservé pour la `@id` valeur trouvée dans l’index de service.

## <a name="http-methods"></a>Méthodes HTTP

La `PUT` méthode http est prise en charge par cette ressource. 

## <a name="push-a-symbol-package"></a>Envoyer un package de symboles

nuget.org prend en charge l’envoi d’un nouveau format de packages de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) à l’aide de l’API suivante. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Les packages de symboles avec le même ID et la même version peuvent être envoyés plusieurs fois. Un package de symboles sera rejeté dans les cas suivants.
- Un package ayant le même ID et la même version n’existe pas.
- Un package de symboles avec le même ID et la même version a fait l’objet d’un push, mais n’est pas encore publié.
- Le package de symboles ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) n’est pas valide (consultez [contraintes de package de symboles](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Paramètres de la demande

Nom           | Dans     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | En-tête | string | Oui      | Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`

La clé API est une chaîne opaque obtenue à partir de la source du package par l’utilisateur et configurée dans le client. Aucun format de chaîne particulier n’est mandaté, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.

### <a name="request-body"></a>Corps de la demande

Le corps de la demande pour la notification push de symbole est le même que le corps de la demande d’une demande push de package (voir [push et suppression de packages](package-publish-resource.md)). 

### <a name="response"></a>response

Code d’état | Signification
----------- | -------
201         | Le package de symboles a été correctement poussé.
400         | Le package de symboles fourni n’est pas valide.
401         | L’utilisateur n’est pas autorisé à effectuer cette action.
404         | Un package correspondant avec l’ID et la version fournis n’existe pas.
409         | Un package de symboles avec l’ID et la version fournis a été envoyé, mais il n’est pas encore disponible.
413         | Le package est trop volumineux.

