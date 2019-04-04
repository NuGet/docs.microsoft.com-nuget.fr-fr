---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921557"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Raisonnement

Avec l’introduction de la [licence expressions](nuspec.md#license), une exigence émergé pour avoir un service fiable qui fournit un texte de référence pour les identificateurs de licence individuelle, les identificateurs d’exception ou les expressions de licence.
Une condition supplémentaire pour ce service est de disposer d’un schéma URL stable, qui n’est pas exposée à lier la table rot, afin que nous pouvons l’utiliser en toute sécurité pour assurer la compatibilité descendante pour les clients plus anciens.

Licenses.NuGet.org remplira ce rôle. NuGet.org utilise pour fournir la référence de texte de licence pour les packages qui spécifient leur licence à l’aide d’une expression de la licence. `nuget pack` ou l’emballage avec d’autres [outils clients](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) définir le [ `licenseUrl` ](nuspec.md#licenseurl) élément pour pointer vers licenses.nuget.org pour des raisons de compatibilité avec les anciens clients qui ne prennent en charge le `license` élément.

## <a name="protocol"></a>Protocole

Aucune réponse lisible par machine Licenses.NuGet.org est ne destinée à être affichée par des personnes dans leur navigateur, est fournis.
Le protocole HTTPS doit être utilisé et les demandes sont censés être construite dans une certaine manière. Il prend uniquement en charge `GET` demandes.
Il accepte les expressions de licence ou d’identificateurs d’exception de licence en tant qu’entrée d’une manière spécifiée ci-dessous. Notez, que tous les éléments des expressions de licence respectent la casse, et par conséquent, toutes les entrées à licenses.nuget.org respecte la casse également.

### <a name="license-expressions"></a>Expressions de licence

#### <a name="request"></a>Demande

Expressions de licence (y compris les cas triviales lors de l’expression se compose d’une seule licence) doivent être [encodé en URL](https://tools.ietf.org/html/rfc3986#section-2.1) et utilisé comme un chemin d’accès à la demande pour licenses.nuget.org.

| Expression de la licence | URL à utiliser |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL 2.0-uniquement avec FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Le service prend en charge uniquement les identificateurs de licence et les identificateurs d’exception de licence qui sont acceptées par nuget.org. Toutes les expressions de licence qui contiennent des identificateurs de licence non pris en charge ou des identificateurs d’exception de licence ou qui n’est pas conforme à la syntaxe d’expression de licence sont considérés comme non valides.

#### <a name="response"></a>Réponse

Licenses.NuGet.org répond aux requêtes contenant des expressions de licence valide avec un code d’état HTTP 200 et une page web contenant une description de l’expression de la licence :

* Si fourni licence expression contient un identificateur de licence unique une page web est retourné qui contient ce texte de référence de licence ;
* s’il est fourni expression de la licence est une expression de la licence composite, une page web est retourné qui contient l’expression de licence avec des liens vers la licence individuelle ou licence exception références.

Toutes les demandes qui contiennent un résultat d’expression de licence non valide dans une réponse HTTP 404.

### <a name="license-exceptions"></a>Exceptions de licence

#### <a name="request"></a>Demande

Identificateurs d’exception de licence doivent être utilisé comme un chemin d’accès à la demande pour licenses.nuget.org et encodé en URL. Uniquement un identificateur d’exception de la licence unique peut être fourni dans une demande unique. Aucun des caractères supplémentaires en plus de l’identificateur d’exception licence n’être présents dans la partie chemin d’accès de l’URL.

| Identificateur d’exception de licence | URL à utiliser |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Réponse

Licenses.NuGet.org répond à une demande avec un identificateur d’exception connus licence avec une réponse HTTP 200 et une page web contenant le texte de référence pour l’exception de licence spécifié.

Toute demande contenant un identificateur d’exception non prise en charge de licence entraîne une réponse HTTP 404.