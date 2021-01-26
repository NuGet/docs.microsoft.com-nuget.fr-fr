---
title: Protocoles nuget.org
description: Les protocoles nuget.org en constante évolution pour interagir avec les clients NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773974"
---
# <a name="nugetorg-protocols"></a>Protocoles nuget.org

Pour interagir avec nuget.org, les clients doivent suivre certains protocoles. Étant donné que ces protocoles continuent d’évoluer, les clients doivent identifier la version de protocole qu’ils utilisent lors de l’appel d’API nuget.org spécifiques. Cela permet à nuget.org d’introduire des modifications de manière non-critique pour les anciens clients.

> [!Note]
> Les API documentées dans cette page sont spécifiques à nuget.org et il n’est pas prévu que d’autres implémentations de serveur NuGet introduisent ces API. 

Pour plus d’informations sur l’API NuGet implémentée globalement sur l’écosystème NuGet, consultez la [vue d’ensemble](overview.md)de l’API.

Cette rubrique répertorie les différents protocoles tels qu’ils existent et à quel moment.

## <a name="nuget-protocol-version-410"></a>Version du protocole NuGet 4.1.0

Le protocole 4.1.0 spécifie l’utilisation des clés de la portée de vérification pour interagir avec des services autres que nuget.org, pour valider un package par rapport à un compte nuget.org. Notez que le `4.1.0` numéro de version est une chaîne opaque, mais qu’il coïncide avec la première version du client officiel NuGet qui prenait en charge ce protocole.

La validation garantit que les clés d’API créées par l’utilisateur sont utilisées uniquement avec nuget.org, et que d’autres vérifications ou validations à partir d’un service tiers sont gérées par le biais de clés de la portée de vérification à usage unique. Ces clés de l’étendue de vérification peuvent être utilisées pour valider le fait que le package appartient à un utilisateur particulier (compte) sur nuget.org.

### <a name="client-requirement"></a>Configuration requise du client

Les clients doivent passer l’en-tête suivant lorsqu’ils effectuent des appels d’API vers des packages **Push** vers NuGet.org :

```
X-NuGet-Protocol-Version: 4.1.0
```

Notez que l' `X-NuGet-Client-Version` en-tête a une sémantique similaire, mais qu’il est réservé pour être utilisé uniquement par le client NuGet officiel. Les clients tiers doivent utiliser l' `X-NuGet-Protocol-Version` en-tête et la valeur.

Le protocole **Push** lui-même est décrit dans la documentation de la [ `PackagePublish` ressource](package-publish-resource.md).

Si un client interagit avec des services externes et doit vérifier si un package appartient à un utilisateur particulier (compte), il doit utiliser le protocole suivant et utiliser les clés de la portée de vérification et non les clés API de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API pour demander une clé de la portée de la vérification

Cette API est utilisée pour obtenir une clé de la portée de la vérification pour un auteur nuget.org afin de valider un package qui lui appartient.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Paramètres de la demande

Nom           | Dans     | Type   | Obligatoire | Notes
-------------- | ------ | ------ | -------- | -----
id             | URL    | string | Oui      | Identidier de package pour lequel la clé de vérification de la portée est demandée
VERSION        | URL    | string | non       | Version du package
X-NuGet-ApiKey | En-tête | string | Oui      | Par exemple : `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>response

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API pour vérifier la clé de l’étendue

Cette API est utilisée pour valider une clé de la portée de vérification pour le package détenu par l’auteur nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Paramètres de la demande

Nom           | Dans     | Type   | Obligatoire | Notes
-------------  | ------ | ------ | -------- | -----
id             | URL    | string | Oui      | Identificateur du package pour lequel la clé de vérification de la portée est demandée.
VERSION        | URL    | string | non       | Version du package
X-NuGet-ApiKey | En-tête | string | Oui      | Par exemple : `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Cette clé de l’API de la portée de vérification expire dans l’heure d’un jour ou lors de la première utilisation, selon ce qui se produit en premier.

#### <a name="response"></a>response

Code d’état | Signification
----------- | -------
200         | La clé API est valide
403         | La clé API n’est pas valide ou n’est pas autorisée à effectuer une transmission de type push sur le package
404         | Le package référencé par `ID` et `VERSION` (facultatif) n’existe pas
