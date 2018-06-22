---
title: Protocoles NuGet.org
description: Les protocoles nuget.org en constante évolution pour interagir avec les clients NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822576"
---
# <a name="nugetorg-protocols"></a>protocoles NuGet.org

Pour interagir avec nuget.org, les clients doivent suivre certains protocoles. Étant donné que ces protocoles conservent en constante évolution, les clients doivent identifier la version du protocole qu’ils utilisent lors de l’appel d’API de nuget.org spécifique. Cela permet de nuget.org apporter des modifications d’une manière sans rupture pour les anciens clients.

> [!Note]
> Les API décrites dans cette page sont spécifiques à nuget.org et n’est pas garantie pour d’autres implémentations de serveur NuGet présenter ces API. 

Pour plus d’informations sur l’API NuGet implémentés largement dans l’écosystème de NuGet, consultez le [présentation de l’API](overview.md).

Cette rubrique répertorie les différents protocoles en tant qu’et lorsque leur présence.

## <a name="nuget-protocol-version-410"></a>Version du protocole NuGet 4.1.0

Le 4.1.0 protocole spécifie l’utilisation de clés de portée vérifier pour interagir avec les services autres que nuget.org, pour valider un package avec un compte de nuget.org. Notez que le `4.1.0` version nombre est une chaîne opaque mais se produit pour coïncider avec la première version du client NuGet officiel pris en charge ce protocole.

Validation garantit que les clés API créés par l’utilisateur sont utilisées uniquement avec nuget.org, et que cette vérification ou la validation à partir d’un service tiers est gérée via un usage des clés de vérifier l’étendue. Ces clés de vérifier l’étendue peuvent être utilisées pour valider que le package appartient à un utilisateur spécifique (compte) sur nuget.org.

### <a name="client-requirement"></a>Spécification du client

Les clients doivent passer de l’en-tête suivant lorsqu’ils effectuent des appels d’API à **push** packages nuget.org :

    X-NuGet-Protocol-Version: 4.1.0

Notez que le `X-NuGet-Client-Version` en-tête a une sémantique similaire, mais elle est réservé à utiliser par le client NuGet officiels. Les clients tiers doivent utiliser le `X-NuGet-Protocol-Version` en-tête et valeur.

Le **push** protocole lui-même est décrit dans la documentation relative à la [ `PackagePublish` ressources](package-publish-resource.md).

Si un client interagit avec les services externes et des besoins pour vérifier si un package appartient à un utilisateur spécifique (compte), il doit utiliser le protocole suivant et utiliser les clés de l’étendue de la vérification et pas les clés de l’API de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API pour demander une clé de vérification étendue

Cette API est utilisée pour obtenir une clé de l’étendue de la vérification d’un auteur nuget.org valider un package détenu par ce dernier.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’identidier de package pour lequel la clé de portée Vérifiez est demandée
VERSION        | URL    | chaîne | Non       | La version du package
NuGet-X-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Réponse

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API pour vérifier la clé de portée Vérifiez

Cette API est utilisée pour valider une clé de vérifier la portée pour le package détenu par l’auteur nuget.org.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Paramètres de la demande

Name           | Vers l'avant     | Type   | Obligatoire | Notes
-------------  | ------ | ------ | -------- | -----
Id             | URL    | chaîne | oui      | L’identificateur de package pour lequel la clé de portée Vérifiez est demandée
VERSION        | URL    | chaîne | Non       | La version du package
NuGet-X-ApiKey | Header | chaîne | oui      | Par exemple, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Cette clé de portée API Vérifiez expire dans une journée ou à la première utilisation, selon ce qui se produit en premier.

#### <a name="response"></a>Réponse

Code d’état | Signification
----------- | -------
200         | La clé API est valide
403         | La clé API est non valide ou non autorisé à distribuer sur le package
404         | Le package référencé par `ID` et `VERSION` (facultatif) n’existe pas
