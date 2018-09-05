---
title: Push et supprimer des API NuGet
description: Le service de publication permet aux clients publier les nouveaux packages et de retirer de la liste ou de supprimer des packages existants.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547519"
---
# <a name="push-and-delete"></a>Push et supprimer

Il est possible d’envoyer, supprimer (ou retirer de la liste, selon l’implémentation de serveur) et les remettre dans la liste des packages à l’aide de l’API V3 de NuGet. Ces opérations sont basées issu de la `PackagePublish` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Ce qui suit `@type` valeur est utilisée :

Valeur @type          | Notes
-------------------- | -----
PackagePublish/2.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans la source de package [index de service](service-index.md). Pour obtenir la documentation ci-dessous, les URL de nuget.org est utilisé. Envisagez `https://www.nuget.org/api/v2/package` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.

Notez que cette URL pointe vers le même emplacement que le point de terminaison push V2 héritée, étant donné que le protocole est le même.

## <a name="http-methods"></a>Méthodes HTTP

Le `PUT`, `POST` et `DELETE` méthodes HTTP sont pris en charge par cette ressource. Pour les méthodes sont prises en charge sur chaque point de terminaison, voir ci-dessous.

## <a name="push-a-package"></a>Push d’un package

> [!Note]
> NuGet.org a [des exigences supplémentaires](NuGet-Protocols.md) permettant d’interagir avec le point de terminaison push.

NuGet.org prend en charge l’exécution de type push des nouveaux packages à l’aide de l’API suivante. Si le package avec l’ID et la version fournie existe déjà, nuget.org rejette la notification push. Autres sources de package peuvent prendre en charge le remplacement d’un package existant.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client. Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.

### <a name="request-body"></a>Corps de la requête

Le corps de la demande doit être placée sous la forme suivante :

#### <a name="multipart-form-data"></a>Données de formulaire en plusieurs parties

L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande est les octets bruts du fichier .nupkg poussé. Les éléments suivants dans le corps en plusieurs parties sont ignorés. Le nom de fichier ou de tous les autres en-têtes des éléments en plusieurs parties sont ignorés.

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
201, 202    | Le package a été correctement envoyé.
400         | Le package fourni n’est pas valide
409         | Un package avec l’ID et la version fournie existe déjà

Les implémentations serveur varient sur le code d’état de réussite retourné lorsqu’un package est envoyé avec succès.

## <a name="delete-a-package"></a>Supprimer un package

NuGet.org interprète la demande de suppression de package comme un « retirer de la liste ». Cela signifie que le package est toujours disponible pour les consommateurs existants du package, mais le package n’apparaît plus dans les résultats de recherche ou dans l’interface web. Pour plus d’informations sur cette pratique, consultez le [Packages supprimés](../policies/deleting-packages.md) stratégie. Autres implémentations de serveur sont libres d’interpréter ce signal comme une suppression de disque dur, de suppression réversible ou de retirer de la liste. Par exemple, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur uniquement prise en charge de l’ancienne API V2) prend en charge la gestion de cette demande comme une suppression de la liste ou une suppression dure basée sur une option de configuration.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’ID du package à supprimer
VERSION        | URL    | chaîne | oui      | La version du package à supprimer
X-NuGet-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
204         | Le package a été supprimé
404         | Aucun package avec l’argument `ID` et `VERSION` existe

## <a name="relist-a-package"></a>Remettre dans la liste d’un package

Si un package n’est pas répertorié, il est possible de rendre ce package une fois encore visible dans les résultats de recherche à l’aide du point de terminaison « remise ». Ce point de terminaison a la même forme que la [supprimer (retirer de la liste) point de terminaison](#delete-a-package) , mais utilise le `POST` méthode HTTP au lieu du `DELETE` (méthode).

Si le package est déjà répertorié, la demande réussit toujours.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’ID du package à remettre dans la liste
VERSION        | URL    | chaîne | oui      | La version du package à remettre dans la liste
X-NuGet-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
200         | Le package est maintenant répertorié.
404         | Aucun package avec l’argument `ID` et `VERSION` existe
