---
title: Push et Delete, API NuGet
description: Le service de publication permet aux clients de publier de nouveaux packages et de retirer ou de supprimer des packages existants.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773923"
---
# <a name="push-and-delete"></a>Push et Delete

Il est possible d’effectuer un push, une suppression (ou une annulation de liste, selon l’implémentation du serveur) et de relister les packages à l’aide de l’API NuGet v3. Ces opérations sont basées sur la `PackagePublish` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Contrôle de version

La `@type` valeur suivante est utilisée :

Valeur @type          | Notes
-------------------- | -----
PackagePublish/2.0.0 | La version initiale

## <a name="base-url"></a>URL de base

L’URL de base pour les API suivantes est la valeur de la `@id` propriété de la `PackagePublish/2.0.0` ressource dans l’index de [service](service-index.md)de la source du package. Pour la documentation ci-dessous, l’URL de NuGet. org est utilisée. Considérez `https://www.nuget.org/api/v2/package` comme un espace réservé pour la `@id` valeur trouvée dans l’index de service.

Notez que cette URL pointe vers le même emplacement que le point de terminaison v2 Push hérité puisque le protocole est le même.

## <a name="http-methods"></a>Méthodes HTTP

Les `PUT` `POST` `DELETE` méthodes http et sont prises en charge par cette ressource. Pour connaître les méthodes prises en charge sur chaque point de terminaison, voir ci-dessous.

## <a name="push-a-package"></a>Envoyer (push) un package

> [!Note]
> nuget.org a des [exigences supplémentaires](NuGet-Protocols.md) pour interagir avec le point de terminaison push.

nuget.org prend en charge le push de nouveaux packages à l’aide de l’API suivante. Si le package avec l’ID et la version fournis existe déjà, nuget.org rejette l’opération push. D’autres sources de package peuvent prendre en charge le remplacement d’un package existant.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom           | Dans     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | En-tête | string | Oui      | Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`

La clé API est une chaîne opaque obtenue à partir de la source du package par l’utilisateur et configurée dans le client. Aucun format de chaîne particulier n’est mandaté, mais la longueur de la clé API ne doit pas dépasser une taille raisonnable pour les valeurs d’en-tête HTTP.

### <a name="request-body"></a>Corps de la demande

Le corps de la demande doit se présenter sous la forme suivante :

#### <a name="multipart-form-data"></a>Données de formulaire en plusieurs parties

L’en-tête de demande `Content-Type` est `multipart/form-data` et le premier élément dans le corps de la demande correspond aux octets bruts du. nupkg faisant l’objet d’un push. Les éléments suivants dans le corps en plusieurs parties sont ignorés. Le nom de fichier ou tout autre en-tête des éléments en plusieurs parties est ignoré.

### <a name="response"></a>response

Code d’état | Signification
----------- | -------
201, 202    | Le package a bien fait l’objet d’un push
400         | Le package fourni n’est pas valide
409         | Un package avec l’ID et la version fournis existe déjà

Les implémentations de serveur varient en fonction du code d’état de réussite renvoyé lorsqu’un package est correctement envoyé.

## <a name="delete-a-package"></a>Supprimer un package

nuget.org interprète la demande de suppression du package comme une « annulation de la liste ». Cela signifie que le package est toujours disponible pour les consommateurs existants du package, mais le package n’apparaît plus dans les résultats de la recherche ou dans l’interface Web. Pour plus d’informations sur cette pratique, consultez la stratégie [packages supprimés](../nuget-org/policies/deleting-packages.md) . D’autres implémentations de serveur sont gratuites pour interpréter ce signal comme une suppression définitive, une suppression réversible ou une suppression de liste. Par exemple, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (une implémentation de serveur qui prend uniquement en charge l’ancienne API v2) prend en charge la gestion de cette demande sous la forme d’une suppression de liste ou d’une suppression forcée basée sur une option de configuration.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom           | Dans     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
id             | URL    | string | Oui      | ID du package à supprimer
VERSION        | URL    | string | Oui      | Version du package à supprimer
X-NuGet-ApiKey | En-tête | string | Oui      | Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>response

Code d’état | Signification
----------- | -------
204         | Le package a été supprimé
404         | Aucun package avec le fourni `ID` et n' `VERSION` existe

## <a name="relist-a-package"></a>Remettre en vente un package

Si un package n’est pas répertorié, il est possible de le rendre à nouveau visible dans les résultats de la recherche à l’aide du point de terminaison « Relist ». Ce point de terminaison a la même forme que le [point de terminaison de suppression (Unlist)](#delete-a-package) , mais utilise la `POST` méthode http à la place de la `DELETE` méthode.

Si le package est déjà listé, la demande est toujours réussie.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Paramètres de la demande

Nom           | Dans     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
id             | URL    | string | Oui      | ID du package à remettre en liste
VERSION        | URL    | string | Oui      | Version du package à remettre en vente
X-NuGet-ApiKey | En-tête | string | Oui      | Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>response

Code d’état | Signification
----------- | -------
200         | Le package est maintenant listé
404         | Aucun package avec le fourni `ID` et n' `VERSION` existe
