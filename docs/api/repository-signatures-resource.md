---
title: Les Signatures de référentiel, l’API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La ressource de signatures de référentiel permet aux clients de sources de package annoncer leur référentiel fonctionnalités de signature.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59509020"
---
# <a name="repository-signatures"></a>Signatures de dépôt

Si une source de package prend en charge l’ajout des signatures de référentiel pour les packages publiés, il est possible pour un client déterminer la signature des certificats qui sont utilisés par la source du package. Cette ressource permet aux clients de détecter si un référentiel signé le package a été falsifié ou dispose d’un certificat de signature inattendu.

La ressource utilisée pour récupérer ces informations de signature du référentiel est la `RepositorySignatures` ressource trouvée dans le [index de service](service-index.md).

## <a name="versioning"></a>Gestion de version

Ce qui suit `@type` valeur est utilisée :

Valeur@type                 | Notes
-------------------------- | -----
RepositorySignatures/4.7.0 | La version initiale
RepositorySignatures/4.9.0 | Prise en charge par les clients NuGet v4.9 +
RepositorySignatures/5.0.0 | Autorise l’activation `allRepositorySigned`. Prise en charge par les clients NuGet v5.0 +

## <a name="base-url"></a>URL de base

L’URL de point d’entrée pour les API suivantes est la valeur de la `@id` propriété associée à la ressource susmentionnée `@type` valeur. Cette rubrique utilise l’URL de l’espace réservé `{@id}`.

Notez que contrairement à d’autres ressources, le `{@id}` URL est nécessaire pour être pris en charge via le protocole HTTPS.

## <a name="http-methods"></a>Méthodes HTTP

Toutes les URL figurant dans les méthodes de prise en charge uniquement le protocole HTTP de référentiel signatures ressource `GET` et `HEAD`.

## <a name="repository-signatures-index"></a>Index de signatures du référentiel

L’index de signatures de référentiel contient deux informations :

1. S’il faut ou non tous les packages se trouvent sur la source sont référentiel signée par cette source de package.
1. La liste des certificats utilisés par la source du package pour signer les packages.

La plupart des cas, la liste des certificats uniquement jamais est ajoutée à. Nouveaux certificats étaient être ajoutés à la liste lorsque le certificat de signature précédent a expiré et la source du package a besoin commencer à utiliser un certificat de signature. Si un certificat est supprimé de la liste, ce qui signifie que toutes les signatures de package créés avec le certificat de signature supprimé doivent plus être considérés comme valides par le client. Dans ce cas, la signature du package (mais pas nécessairement le package) n’est pas valide. Une stratégie du client peut-être autoriser l’installation du package comme étant non signés.

Dans le cas de la révocation de certificats (par exemple, clé compromise), la source du package est prévue pour signer à nouveau tous les packages signés par le certificat en question. En outre, la source du package doit supprimer le certificat en question à partir de la liste de certificats de signature.

La requête suivante extrait l’index de signatures de référentiel.

    GET {@id}

L’index de signature de référentiel est un document JSON qui contient un objet avec les propriétés suivantes :

Nom                | Type             | Obligatoire | Notes
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | oui      | Doit être `false` sur les ressources 4.7.0 et 4.9.0
signingCertificates | tableau d’objets | oui      | 

Le `allRepositorySigned` valeur booléenne est définie sur false si la source du package a certains packages ayant aucune signature de référentiel. Si la valeur booléenne est définie sur true, tous les packages disponibles sur la source doit avoir une signature de référentiel produite par un des certificats de signature mentionnés dans `signingCertificates`.

> [!Warning]
> Le `allRepositorySigned` booléenne doit avoir la valeur false sur les ressources 4.7.0 et 4.9.0. NuGet v4.7 v4.8, v4.9 les clients et ne peut pas installer les packages à partir de sources qui ont `allRepositorySigned` défini sur true.

Il doit y avoir un ou plusieurs certificats de signature dans le `signingCertificates` tableau si le `allRepositorySigned` valeur booléenne est définie sur true. Si le tableau est vide et `allRepositorySigned` est définie sur true, tous les packages à partir de la source doivent être considéré comme non valides, même si une stratégie de client peut autorise toujours la consommation de packages. Chaque élément de ce tableau est un objet JSON avec les propriétés suivantes.

Nom         | Type   | Obligatoire | Notes
------------ | ------ | -------- | -----
contentUrl   | string | oui      | URL absolue pour le certificat public encodé DER
empreintes digitales | object | oui      |
subject      | string | oui      | Le nom unique du sujet du certificat
issuer       | string | oui      | Le nom unique de l’émetteur du certificat
notBefore    | string | oui      | L’horodatage de début de période de validité du certificat
notAfter     | string | oui      | L’horodatage de fin de période de validité du certificat

Notez que le `contentUrl` est nécessaire pour être pris en charge via le protocole HTTPS. Cette URL n’a aucun modèle d’URL spécifique et doit être découverts dynamiquement à l’aide de ce document d’index de signatures référentiel. 

Toutes les propriétés de cet objet (outre `contentUrl`) doit être dérivé du certificat, consultez `contentUrl`.
Ces propriétés dérivables sont fournies pour des raisons pratiques afin de réduire les allers-retours.

Le `fingerprints` objet a les propriétés suivantes :

Nom                   | Type   | Obligatoire | Notes
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | oui      | L’empreinte SHA-256

Le nom de clé `2.16.840.1.101.3.4.2.1` est l’OID de l’algorithme de hachage SHA-256.

Toutes les valeurs de hachage doivent être représentations sous forme de chaîne en minuscules, codé en hexadécimal du résumé de hachage.

### <a name="sample-request"></a>Exemple de demande

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Exemple de réponse

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
