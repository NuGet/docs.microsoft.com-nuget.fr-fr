---
title: Signatures de référentiel, API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La ressource de signatures de référentiels permet aux sources de package de clients d’annoncer leurs fonctionnalités de signature de référentiel.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775331"
---
# <a name="repository-signatures"></a>Signatures de dépôt

Si une source de package prend en charge l’ajout de signatures de référentiel aux packages publiés, un client peut déterminer les certificats de signature utilisés par la source du package. Cette ressource permet aux clients de détecter si un package signé de référentiel a été falsifié ou s’il dispose d’un certificat de signature inattendu.

La ressource utilisée pour récupérer ces informations de signature de référentiel est la `RepositorySignatures` ressource trouvée dans l' [index de service](service-index.md).

## <a name="versioning"></a>Contrôle de version

La `@type` valeur suivante est utilisée :

Valeur @type                | Notes
-------------------------- | -----
RepositorySignatures/4.7.0 | La version initiale
RepositorySignatures/4.9.0 | Pris en charge par les clients NuGet v 4.9 +
RepositorySignatures/5.0.0 | Autorise l’activation de `allRepositorySigned` . Pris en charge par les clients NuGet v 5.0 +

## <a name="base-url"></a>URL de base

L’URL du point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la valeur de ressource mentionnée ci-dessus `@type` . Cette rubrique utilise l’URL de l’espace réservé `{@id}` .

Notez que, contrairement à d’autres ressources, l' `{@id}` URL doit être fournie via HTTPS.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL trouvées dans la ressource de signatures de référentiel prennent uniquement en charge les méthodes HTTP `GET` et `HEAD` .

## <a name="repository-signatures-index"></a>Index des signatures de référentiel

L’index des signatures de référentiel contient deux informations :

1. Indique si tous les packages trouvés sur la source sont des référentiels signés par cette source de package.
1. Liste des certificats utilisés par la source du package pour signer des packages.

Dans la plupart des cas, la liste des certificats n’est jamais ajoutée à. De nouveaux certificats sont ajoutés à la liste lorsque le certificat de signature précédent a expiré et que la source du package doit commencer à utiliser un nouveau certificat de signature. Si un certificat est supprimé de la liste, cela signifie que toutes les signatures de package créées avec le certificat de signature supprimé ne doivent plus être considérées comme valides par le client. Dans ce cas, la signature du package (mais pas nécessairement le package) n’est pas valide. Une stratégie client peut autoriser l’installation du package en tant que non signé.

Dans le cas de la révocation de certificat (par exemple, la compromission d’une clé), la source du package est censée signer à nouveau tous les packages signés par le certificat affecté. En outre, la source du package doit supprimer le certificat affecté de la liste des certificats de signature.

La requête suivante extrait l’index des signatures de référentiel.

```
GET {@id}
```

L’index de signature du référentiel est un document JSON qui contient un objet avec les propriétés suivantes :

Nom                | Type             | Obligatoire | Notes
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | Oui      | Doit se trouver `false` sur les ressources 4.7.0 et 4.9.0
signingCertificates | tableau d’objets | Oui      | 

La valeur `allRepositorySigned` booléenne est définie sur false si la source du package contient des packages qui n’ont pas de signature de référentiel. Si la valeur booléenne est définie sur true, tous les packages disponibles sur la source doivent avoir une signature de référentiel produite par l’un des certificats de signature mentionnés dans `signingCertificates` .

> [!Warning]
> La valeur `allRepositorySigned` booléenne doit être false sur les ressources 4.7.0 et 4.9.0. Les clients NuGet v 4.7, v 4.8 et v 4.9 ne peuvent pas installer de packages à partir de sources dont la propriété a la valeur `allRepositorySigned` true.

Il doit y avoir un ou plusieurs certificats de signature dans le `signingCertificates` tableau si le `allRepositorySigned` booléen a la valeur true. Si le tableau est vide et `allRepositorySigned` a la valeur true, tous les packages de la source doivent être considérés comme non valides, bien qu’une stratégie client puisse toujours autoriser la consommation de packages. Chaque élément de ce tableau est un objet JSON avec les propriétés suivantes.

Nom         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
contentUrl   | string | Oui      | URL absolue du certificat public encodé DER
empreintes digitales | objet | Oui      |
subject      | string | Oui      | Nom unique du sujet du certificat
émetteur       | string | Oui      | Nom unique de l’émetteur du certificat
notBefore    | string | Oui      | Horodateur de début de la période de validité du certificat
notAfter     | string | Oui      | Horodateur de fin de la période de validité du certificat

Notez que doit `contentUrl` être servi via HTTPS. Cette URL n’a pas de modèle d’URL spécifique et doit être détectée de manière dynamique à l’aide de ce document d’index de signatures de référentiel. 

Toutes les propriétés de cet objet (à part de `contentUrl` ) doivent être extraites du certificat trouvé à l’adresse `contentUrl` .
Ces propriétés de l’agent sont fournies à titre de commodité pour réduire les allers-retours.

L’objet `fingerprints` dispose des propriétés suivantes :

Nom                   | Type   | Obligatoire | Notes
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | Oui      | L’empreinte SHA-256

Le nom `2.16.840.1.101.3.4.2.1` de clé est l’OID de l’algorithme de hachage SHA-256.

Toutes les valeurs de hachage doivent être des représentations sous forme de chaîne en minuscules et encodées en hex du condensé de hachage.

### <a name="sample-request"></a>Exemple de requête

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
