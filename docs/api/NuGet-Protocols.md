---
title: Protocoles NuGet.org
description: Les protocoles nuget.org en constante évolution pour interagir avec les clients NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547271"
---
# <a name="nugetorg-protocols"></a>protocoles NuGet.org

Pour interagir avec nuget.org, les clients doivent suivre certains protocoles. Étant donné que ces protocoles conservent en constante évolution, les clients doivent identifier la version du protocole qu’ils utilisent lors de l’appel d’API de nuget.org spécifique. Cela permet de nuget.org d’introduire des modifications d’une manière sans rupture pour les anciens clients.

> [!Note]
> Les API documentées dans cette page sont spécifiques à nuget.org et n’est pas garantie pour d’autres implémentations de serveur NuGet d’introduire ces API. 

Pour plus d’informations sur l’API NuGet implémenté largement au sein de l’écosystème NuGet, consultez le [vue d’ensemble de l’API](overview.md).

Cette rubrique répertorie les différents protocoles en tant qu’et quand ils proviennent de l’existence.

## <a name="nuget-protocol-version-410"></a>Version du protocole NuGet 4.1.0

Le 4.1.0 protocole spécifie l’utilisation de clés de portée vérifier pour interagir avec les services autres que nuget.org, pour valider un package par rapport à un compte nuget.org. Notez que le `4.1.0` version nombre est une chaîne opaque mais qu’il coïncide avec la première version du client NuGet officiel pris en charge ce protocole.

La validation garantit que les clés API créés par l’utilisateur sont utilisées uniquement auprès de nuget.org, et cette vérification ou la validation à partir d’un service tiers est gérée via un usage des clés de vérifier de portée. Ces clés de vérifier de portée peuvent être utilisées pour valider que le package appartient à un utilisateur particulier (compte) sur nuget.org.

### <a name="client-requirement"></a>Exigence du client

Les clients sont requises pour transmettre l’en-tête suivant lorsqu’ils effectuent des appels d’API vers **push** packages sur nuget.org :

    X-NuGet-Protocol-Version: 4.1.0

Notez que le `X-NuGet-Client-Version` en-tête a une sémantique similaire, mais elle est réservé uniquement à être utilisé par le client NuGet officiel. Les clients tiers doivent utiliser le `X-NuGet-Protocol-Version` en-tête et valeur.

Le **push** protocole lui-même est décrit dans la documentation pour le [ `PackagePublish` ressources](package-publish-resource.md).

Si un client interagit avec les services externes et des besoins pour vérifier si un package appartient à un utilisateur particulier (compte), il doit utiliser le protocole suivant et utiliser les clés de l’étendue de vérifier et pas les clés de l’API à partir de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API pour demander une clé de l’étendue de la vérification

Cette API est utilisée pour obtenir une clé de l’étendue de la vérification d’un auteur de nuget.org valider un package détenu par ce dernier.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’identidier de package pour lequel la touche d’étendue de vérification est demandée
VERSION        | URL    | chaîne | Non       | La version du package
X-NuGet-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Réponse

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API pour vérifier la touche d’étendue de vérification

Cette API est utilisée pour valider une clé de vérifier de portée pour le package détenu par l’auteur de nuget.org.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------  | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’identificateur de package pour lequel la touche d’étendue de vérification est demandée
VERSION        | URL    | chaîne | Non       | La version du package
X-NuGet-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Cette touche étendue API de vérification expire dans une journée ou à la première utilisation, selon ce qui se produit en premier.

#### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
200         | La clé API est valide
403         | La clé API est non valide ou non autorisé à envoyer sur le package
404         | Le package référencé par `ID` et `VERSION` (facultatif) n’existe pas
