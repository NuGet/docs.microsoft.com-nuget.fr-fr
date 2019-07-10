---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427114"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Raisonnement

Avec l’introduction des [expressions de licence](../reference/nuspec.md#license), il est devenu indispensable de disposer d’un service fiable fournissant un texte de référence pour les identificateurs de licence individuels, les identificateurs d’exception ou les expressions de licence.
Ce service doit également avoir un schéma d’URL stable non sujet aux liens rompus, ce qui nous permet de l’utiliser de manière sécurisée pour fournir une compatibilité descendante aux anciens clients.

Licenses.nuget.org remplit ce rôle. Nuget.org l’utilise pour fournir la référence au texte de licence pour les packages qui spécifient leur licence à l’aide d’une expression de licence. L’utilisation de `nuget pack` ou la création d’un package avec d’autres [outils clients](../install-nuget-client-tools.md) définit l’élément [`licenseUrl`](../reference/nuspec.md#licenseurl) pour qu’il pointe vers license.nuget.org afin de fournir une compatibilité ascendante avec les anciens clients ne prenant pas en charge l’élément `license`.

## <a name="protocol"></a>Protocole

Licenses.nuget.org est destiné à être visualisé par les utilisateurs dans leur navigateur. Aucune réponse lisible par machine n’est fournie.
Le protocole HTTPS doit être utilisé et les demandes sont censées être construites d’une certaine manière. Seules les demandes `GET` sont prises en charge.
Il accepte les expressions de licence et les identificateurs d’exception de licence en entrée de la manière spécifiée ci-dessous. Notez que tous les éléments des expressions de licence sont sensibles à la casse. Toute entrée dans le fichier licences.nuget.org l’est donc également.

### <a name="license-expressions"></a>Expressions de licence

#### <a name="request"></a>Requête

Les expressions de licence (y compris les cas triviaux où l’expression se compose d’une seule licence) doivent être [encodées dans une URL](https://tools.ietf.org/html/rfc3986#section-2.1) et utilisées comme chemin dans la demande à licences.nuget.org.

| Expression de licence | URL à utiliser |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Le service prend en charge uniquement les identificateurs de licence et d’exception de licence acceptés par nuget.org. Toutes les expressions de licence contenant des identificateurs de licence ou d’exception de licence non pris en charge ou non conformes à la syntaxe d’expression de licence sont considérées comme non valides.

#### <a name="response"></a>Réponse

Licenses.nuget.org répond aux demandes contenant des expressions de licence valides avec un code d’état HTTP 200 et une page web contenant une description de l’expression de licence :

* si l’expression de licence fournie contient un identificateur de licence unique, une page web contenant ce texte de référence de licence est retournée ;
* si l’expression de licence fournie est une expression de licence composite, une page web contenant l’expression de licence avec des liens vers des références à une licence ou une exception de licence est retournée.

Toute demande contenant une expression de licence non valide entraîne une réponse HTTP 404.

### <a name="license-exceptions"></a>Exceptions de licence

#### <a name="request"></a>Requête

Les identificateurs d’exception de licence doivent être codés dans une URL et utilisés comme chemin dans la demande à licences.nuget.org. Un seul identificateur d’exception de licence peut être fourni dans une même demande. Aucun caractère supplémentaire à part l’identificateur d’exception de licence ne peut être présent dans la partie chemin de l’URL.

| Identificateur d’exception de licence | URL à utiliser |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Réponse

Licenses.nuget.org répond à une demande contenant un identificateur d’exception de licence connu avec une réponse HTTP 200 et une page web contenant le texte de référence pour l’exception de licence spécifiée.

Toute demande contenant un identificateur d’exception de licence non pris en charge entraîne une réponse HTTP 404.