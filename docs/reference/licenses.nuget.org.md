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
# <a name="licensesnugetorg"></a><span data-ttu-id="5d259-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="5d259-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="5d259-103">Raisonnement</span><span class="sxs-lookup"><span data-stu-id="5d259-103">Rationale</span></span>

<span data-ttu-id="5d259-104">Avec l’introduction de la [licence expressions](nuspec.md#license), une exigence émergé pour avoir un service fiable qui fournit un texte de référence pour les identificateurs de licence individuelle, les identificateurs d’exception ou les expressions de licence.</span><span class="sxs-lookup"><span data-stu-id="5d259-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="5d259-105">Une condition supplémentaire pour ce service est de disposer d’un schéma URL stable, qui n’est pas exposée à lier la table rot, afin que nous pouvons l’utiliser en toute sécurité pour assurer la compatibilité descendante pour les clients plus anciens.</span><span class="sxs-lookup"><span data-stu-id="5d259-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="5d259-106">Licenses.NuGet.org remplira ce rôle.</span><span class="sxs-lookup"><span data-stu-id="5d259-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="5d259-107">NuGet.org utilise pour fournir la référence de texte de licence pour les packages qui spécifient leur licence à l’aide d’une expression de la licence.</span><span class="sxs-lookup"><span data-stu-id="5d259-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> `nuget pack` <span data-ttu-id="5d259-108">ou l’emballage avec d’autres [outils clients](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) définir le [ `licenseUrl` ](nuspec.md#licenseurl) élément pour pointer vers licenses.nuget.org pour des raisons de compatibilité avec les anciens clients qui ne prennent en charge le `license` élément.</span><span class="sxs-lookup"><span data-stu-id="5d259-108">or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="5d259-109">Protocole</span><span class="sxs-lookup"><span data-stu-id="5d259-109">Protocol</span></span>

<span data-ttu-id="5d259-110">Aucune réponse lisible par machine Licenses.NuGet.org est ne destinée à être affichée par des personnes dans leur navigateur, est fournis.</span><span class="sxs-lookup"><span data-stu-id="5d259-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="5d259-111">Le protocole HTTPS doit être utilisé et les demandes sont censés être construite dans une certaine manière.</span><span class="sxs-lookup"><span data-stu-id="5d259-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="5d259-112">Il prend uniquement en charge `GET` demandes.</span><span class="sxs-lookup"><span data-stu-id="5d259-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="5d259-113">Il accepte les expressions de licence ou d’identificateurs d’exception de licence en tant qu’entrée d’une manière spécifiée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5d259-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="5d259-114">Notez, que tous les éléments des expressions de licence respectent la casse, et par conséquent, toutes les entrées à licenses.nuget.org respecte la casse également.</span><span class="sxs-lookup"><span data-stu-id="5d259-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="5d259-115">Expressions de licence</span><span class="sxs-lookup"><span data-stu-id="5d259-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="5d259-116">Demande</span><span class="sxs-lookup"><span data-stu-id="5d259-116">Request</span></span>

<span data-ttu-id="5d259-117">Expressions de licence (y compris les cas triviales lors de l’expression se compose d’une seule licence) doivent être [encodé en URL](https://tools.ietf.org/html/rfc3986#section-2.1) et utilisé comme un chemin d’accès à la demande pour licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5d259-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="5d259-118">Expression de la licence</span><span class="sxs-lookup"><span data-stu-id="5d259-118">License expression</span></span> | <span data-ttu-id="5d259-119">URL à utiliser</span><span class="sxs-lookup"><span data-stu-id="5d259-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="5d259-120">MIT</span><span class="sxs-lookup"><span data-stu-id="5d259-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="5d259-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="5d259-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="5d259-122">(LGPL 2.0-uniquement avec FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="5d259-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="5d259-123">Le service prend en charge uniquement les identificateurs de licence et les identificateurs d’exception de licence qui sont acceptées par nuget.org. Toutes les expressions de licence qui contiennent des identificateurs de licence non pris en charge ou des identificateurs d’exception de licence ou qui n’est pas conforme à la syntaxe d’expression de licence sont considérés comme non valides.</span><span class="sxs-lookup"><span data-stu-id="5d259-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="5d259-124">Réponse</span><span class="sxs-lookup"><span data-stu-id="5d259-124">Response</span></span>

<span data-ttu-id="5d259-125">Licenses.NuGet.org répond aux requêtes contenant des expressions de licence valide avec un code d’état HTTP 200 et une page web contenant une description de l’expression de la licence :</span><span class="sxs-lookup"><span data-stu-id="5d259-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="5d259-126">Si fourni licence expression contient un identificateur de licence unique une page web est retourné qui contient ce texte de référence de licence ;</span><span class="sxs-lookup"><span data-stu-id="5d259-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="5d259-127">s’il est fourni expression de la licence est une expression de la licence composite, une page web est retourné qui contient l’expression de licence avec des liens vers la licence individuelle ou licence exception références.</span><span class="sxs-lookup"><span data-stu-id="5d259-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="5d259-128">Toutes les demandes qui contiennent un résultat d’expression de licence non valide dans une réponse HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="5d259-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="5d259-129">Exceptions de licence</span><span class="sxs-lookup"><span data-stu-id="5d259-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="5d259-130">Demande</span><span class="sxs-lookup"><span data-stu-id="5d259-130">Request</span></span>

<span data-ttu-id="5d259-131">Identificateurs d’exception de licence doivent être utilisé comme un chemin d’accès à la demande pour licenses.nuget.org et encodé en URL. Uniquement un identificateur d’exception de la licence unique peut être fourni dans une demande unique.</span><span class="sxs-lookup"><span data-stu-id="5d259-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="5d259-132">Aucun des caractères supplémentaires en plus de l’identificateur d’exception licence n’être présents dans la partie chemin d’accès de l’URL.</span><span class="sxs-lookup"><span data-stu-id="5d259-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="5d259-133">Identificateur d’exception de licence</span><span class="sxs-lookup"><span data-stu-id="5d259-133">License exception identifier</span></span> | <span data-ttu-id="5d259-134">URL à utiliser</span><span class="sxs-lookup"><span data-stu-id="5d259-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="5d259-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="5d259-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="5d259-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="5d259-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="5d259-137">Réponse</span><span class="sxs-lookup"><span data-stu-id="5d259-137">Response</span></span>

<span data-ttu-id="5d259-138">Licenses.NuGet.org répond à une demande avec un identificateur d’exception connus licence avec une réponse HTTP 200 et une page web contenant le texte de référence pour l’exception de licence spécifié.</span><span class="sxs-lookup"><span data-stu-id="5d259-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="5d259-139">Toute demande contenant un identificateur d’exception non prise en charge de licence entraîne une réponse HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="5d259-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>