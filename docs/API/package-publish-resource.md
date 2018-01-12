---
title: Push et supprimer, NuGet API | Documents Microsoft
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Le service de publication autorise les clients à publier les nouveaux packages et de retrait de la liste ou de supprimer des packages existants."
keywords: "Package NuGet API push supprimer le package NuGet API, API NuGet package, le package de téléchargement NuGet API retirer de la liste, créer des package NuGet API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a>Push et supprimer

Il est possible de transmettre, supprimer (ou retirer de la liste, en fonction de l’implémentation du serveur) et la remise des packages à l’aide de l’API de V3 NuGet. Ces opérations sont en fonction de la `PackagePublish` ressource trouvée dans le [index service](service-index.md).

## <a name="versioning"></a>Gestion de version

Les éléments suivants `@type` valeur est utilisée :

Valeur @type          | Notes
-------------------- | -----
PackagePublish/2.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans la source de package [index service](service-index.md). Pour obtenir la documentation ci-dessous, nuget.org URL est utilisé. Envisagez de `https://www.nuget.org/api/v2/package` comme espace réservé pour le `@id` valeur trouvée dans l’index de service.

Notez que cette URL pointe vers le même emplacement que le point de terminaison de push V2 hérité, car le protocole est le même.

## <a name="http-methods"></a>Méthodes HTTP

Le `PUT`, `POST` et `DELETE` méthodes HTTP sont pris en charge par cette ressource. Pour les méthodes qui sont pris en charge sur chaque point de terminaison, voir ci-dessous.

## <a name="push-a-package"></a>Un package de push

> [!Note]
> NuGet.org a [exigences supplémentaires](NuGet-Protocols.md) pour interagir avec le point de terminaison par émission de données.

NuGet.org prend en charge l’exécution d’un push des nouveaux packages à l’aide de l’API suivante. Si le package avec l’ID et la version fourni existe déjà, nuget.org rejette le push. Autres sources de package peuvent prendre en charge le remplacement d’un package existant.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
NuGet-X-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

La clé API est une chaîne opaque obtenu à partir de la source du package par l’utilisateur et configuré dans le client. Aucun format de chaîne particulière n’est autorisé, mais la longueur de la clé d’API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.

### <a name="request-body"></a>Corps de la requête

Le corps de la demande doit être placée sous la forme suivante :

#### <a name="multipart-form-data"></a>Données de formulaire en plusieurs parties

L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande est les octets bruts de le .nupkg lancé. Les éléments suivants dans le corps en plusieurs parties sont ignorés. Le nom de fichier ou de tous les autres en-têtes des éléments en plusieurs parties sont ignorés.

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
201, 202    | Le package a été envoyée avec succès
400         | Le package fourni n’est pas valide
409         | Un package avec l’ID et la version fourni existe déjà

Les implémentations de serveur varient selon le code d’état de réussite retournés lorsqu’un package est envoyé avec succès.

## <a name="delete-a-package"></a>Supprimer un package

NuGet.org interprète la demande de suppression de package comme un « retirer de la liste ». Cela signifie que le package est toujours disponible pour les utilisateurs existants du package, mais le package ne s’affiche plus dans les résultats de la recherche ou dans l’interface web. Pour plus d’informations sur cette pratique, consultez la [supprimé les Packages](../policies/deleting-packages.md) stratégie. Autres implémentations de serveur sont libres d’interpréter ce signal comme une suppression définitive, la suppression réversible ou retirer de la liste. Par exemple, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur de prise en charge uniquement l’ancienne API V2) prend en charge gère cette requête comme un unlist ou une suppression définitive basé sur une option de configuration.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’ID du package à supprimer
VERSION        | URL    | chaîne | oui      | La version du package à supprimer
NuGet-X-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
204         | Le package a été supprimé.
404         | Aucun package avec le paramètre `ID` et `VERSION` existe

## <a name="relist-a-package"></a>Remettre un package

Si un package n’est pas spécifié, il est possible de rendre ce package à nouveau visible dans les résultats de recherche à l’aide du point de terminaison « remise ». Ce point de terminaison a la même forme que le [supprimer (retirer de la liste) point de terminaison](#delete-a-package) , mais utilise le `POST` méthode HTTP au lieu du `DELETE` (méthode).

Si le package est déjà répertorié, la demande réussit toujours.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’ID du package de remise
VERSION        | URL    | chaîne | oui      | La version du package à remettre en vente
NuGet-X-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
200         | Le package est maintenant répertorié.
404         | Aucun package avec le paramètre `ID` et `VERSION` existe
