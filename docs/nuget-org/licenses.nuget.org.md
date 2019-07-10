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
# <a name="licensesnugetorg"></a><span data-ttu-id="e62ad-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="e62ad-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="e62ad-103">Raisonnement</span><span class="sxs-lookup"><span data-stu-id="e62ad-103">Rationale</span></span>

<span data-ttu-id="e62ad-104">Avec l’introduction des [expressions de licence](../reference/nuspec.md#license), il est devenu indispensable de disposer d’un service fiable fournissant un texte de référence pour les identificateurs de licence individuels, les identificateurs d’exception ou les expressions de licence.</span><span class="sxs-lookup"><span data-stu-id="e62ad-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="e62ad-105">Ce service doit également avoir un schéma d’URL stable non sujet aux liens rompus, ce qui nous permet de l’utiliser de manière sécurisée pour fournir une compatibilité descendante aux anciens clients.</span><span class="sxs-lookup"><span data-stu-id="e62ad-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="e62ad-106">Licenses.nuget.org remplit ce rôle.</span><span class="sxs-lookup"><span data-stu-id="e62ad-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="e62ad-107">Nuget.org l’utilise pour fournir la référence au texte de licence pour les packages qui spécifient leur licence à l’aide d’une expression de licence.</span><span class="sxs-lookup"><span data-stu-id="e62ad-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="e62ad-108">L’utilisation de `nuget pack` ou la création d’un package avec d’autres [outils clients](../install-nuget-client-tools.md) définit l’élément [`licenseUrl`](../reference/nuspec.md#licenseurl) pour qu’il pointe vers license.nuget.org afin de fournir une compatibilité ascendante avec les anciens clients ne prenant pas en charge l’élément `license`.</span><span class="sxs-lookup"><span data-stu-id="e62ad-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="e62ad-109">Protocole</span><span class="sxs-lookup"><span data-stu-id="e62ad-109">Protocol</span></span>

<span data-ttu-id="e62ad-110">Licenses.nuget.org est destiné à être visualisé par les utilisateurs dans leur navigateur. Aucune réponse lisible par machine n’est fournie.</span><span class="sxs-lookup"><span data-stu-id="e62ad-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="e62ad-111">Le protocole HTTPS doit être utilisé et les demandes sont censées être construites d’une certaine manière.</span><span class="sxs-lookup"><span data-stu-id="e62ad-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="e62ad-112">Seules les demandes `GET` sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="e62ad-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="e62ad-113">Il accepte les expressions de licence et les identificateurs d’exception de licence en entrée de la manière spécifiée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e62ad-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="e62ad-114">Notez que tous les éléments des expressions de licence sont sensibles à la casse. Toute entrée dans le fichier licences.nuget.org l’est donc également.</span><span class="sxs-lookup"><span data-stu-id="e62ad-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="e62ad-115">Expressions de licence</span><span class="sxs-lookup"><span data-stu-id="e62ad-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="e62ad-116">Requête</span><span class="sxs-lookup"><span data-stu-id="e62ad-116">Request</span></span>

<span data-ttu-id="e62ad-117">Les expressions de licence (y compris les cas triviaux où l’expression se compose d’une seule licence) doivent être [encodées dans une URL](https://tools.ietf.org/html/rfc3986#section-2.1) et utilisées comme chemin dans la demande à licences.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e62ad-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="e62ad-118">Expression de licence</span><span class="sxs-lookup"><span data-stu-id="e62ad-118">License expression</span></span> | <span data-ttu-id="e62ad-119">URL à utiliser</span><span class="sxs-lookup"><span data-stu-id="e62ad-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="e62ad-120">MIT</span><span class="sxs-lookup"><span data-stu-id="e62ad-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="e62ad-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="e62ad-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="e62ad-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="e62ad-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="e62ad-123">Le service prend en charge uniquement les identificateurs de licence et d’exception de licence acceptés par nuget.org. Toutes les expressions de licence contenant des identificateurs de licence ou d’exception de licence non pris en charge ou non conformes à la syntaxe d’expression de licence sont considérées comme non valides.</span><span class="sxs-lookup"><span data-stu-id="e62ad-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="e62ad-124">Réponse</span><span class="sxs-lookup"><span data-stu-id="e62ad-124">Response</span></span>

<span data-ttu-id="e62ad-125">Licenses.nuget.org répond aux demandes contenant des expressions de licence valides avec un code d’état HTTP 200 et une page web contenant une description de l’expression de licence :</span><span class="sxs-lookup"><span data-stu-id="e62ad-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="e62ad-126">si l’expression de licence fournie contient un identificateur de licence unique, une page web contenant ce texte de référence de licence est retournée ;</span><span class="sxs-lookup"><span data-stu-id="e62ad-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="e62ad-127">si l’expression de licence fournie est une expression de licence composite, une page web contenant l’expression de licence avec des liens vers des références à une licence ou une exception de licence est retournée.</span><span class="sxs-lookup"><span data-stu-id="e62ad-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="e62ad-128">Toute demande contenant une expression de licence non valide entraîne une réponse HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="e62ad-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="e62ad-129">Exceptions de licence</span><span class="sxs-lookup"><span data-stu-id="e62ad-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="e62ad-130">Requête</span><span class="sxs-lookup"><span data-stu-id="e62ad-130">Request</span></span>

<span data-ttu-id="e62ad-131">Les identificateurs d’exception de licence doivent être codés dans une URL et utilisés comme chemin dans la demande à licences.nuget.org. Un seul identificateur d’exception de licence peut être fourni dans une même demande.</span><span class="sxs-lookup"><span data-stu-id="e62ad-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="e62ad-132">Aucun caractère supplémentaire à part l’identificateur d’exception de licence ne peut être présent dans la partie chemin de l’URL.</span><span class="sxs-lookup"><span data-stu-id="e62ad-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="e62ad-133">Identificateur d’exception de licence</span><span class="sxs-lookup"><span data-stu-id="e62ad-133">License exception identifier</span></span> | <span data-ttu-id="e62ad-134">URL à utiliser</span><span class="sxs-lookup"><span data-stu-id="e62ad-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="e62ad-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="e62ad-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="e62ad-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="e62ad-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="e62ad-137">Réponse</span><span class="sxs-lookup"><span data-stu-id="e62ad-137">Response</span></span>

<span data-ttu-id="e62ad-138">Licenses.nuget.org répond à une demande contenant un identificateur d’exception de licence connu avec une réponse HTTP 200 et une page web contenant le texte de référence pour l’exception de licence spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e62ad-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="e62ad-139">Toute demande contenant un identificateur d’exception de licence non pris en charge entraîne une réponse HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="e62ad-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>