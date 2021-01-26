---
title: tools.jspour la découverte de versions nuget.exe
description: Le point de terminaison pour
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773817"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="cbc6c-103">tools.jspour la découverte de versions nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cbc6c-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="cbc6c-104">Aujourd’hui, il existe plusieurs façons d’obtenir la dernière version de nuget.exe sur votre machine de manière scriptable.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="cbc6c-105">Par exemple, vous pouvez télécharger et extraire le [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package à partir de NuGet.org. Cela a une certaine complexité, car elle nécessite que vous disposiez déjà d' nuget.exe (pour `nuget.exe install` ), ou vous devez décompresser le fichier. nupkg à l’aide d’un outil de décompression de base et rechercher le binaire à l’intérieur de.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="cbc6c-106">Si vous avez déjà nuget.exe, vous pouvez également utiliser `nuget.exe update -self` , mais cela nécessite également une copie existante de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="cbc6c-107">Cette approche vous permet également de vous mettre à jour vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="cbc6c-108">Elle n’autorise pas l’utilisation d’une version spécifique.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="cbc6c-109">Le `tools.json` point de terminaison est disponible pour résoudre le problème d’amorçage et pour vous permettre de contrôler la version de nuget.exe que vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="cbc6c-110">Il peut être utilisé dans des environnements CI/CD ou dans des scripts personnalisés pour détecter et télécharger une version finale de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="cbc6c-111">Le `tools.json` point de terminaison peut être extrait à l’aide d’une requête HTTP non authentifiée (par exemple, `Invoke-WebRequest` dans PowerShell ou `wget` ).</span><span class="sxs-lookup"><span data-stu-id="cbc6c-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="cbc6c-112">Elle peut être analysée à l’aide d’un désérialiseur JSON et les URL de téléchargement ultérieures nuget.exe peuvent également être extraites à l’aide de requêtes HTTP non authentifiées.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="cbc6c-113">Le point de terminaison peut être extrait à l’aide de la `GET` méthode :</span><span class="sxs-lookup"><span data-stu-id="cbc6c-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="cbc6c-114">Le [schéma JSON](https://json-schema.org/) du point de terminaison est disponible ici :</span><span class="sxs-lookup"><span data-stu-id="cbc6c-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="cbc6c-115">response</span><span class="sxs-lookup"><span data-stu-id="cbc6c-115">Response</span></span>

<span data-ttu-id="cbc6c-116">La réponse est un document JSON contenant toutes les versions disponibles de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="cbc6c-117">L’objet JSON racine a la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="cbc6c-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="cbc6c-118">Nom</span><span class="sxs-lookup"><span data-stu-id="cbc6c-118">Name</span></span>      | <span data-ttu-id="cbc6c-119">Type</span><span class="sxs-lookup"><span data-stu-id="cbc6c-119">Type</span></span>             | <span data-ttu-id="cbc6c-120">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="cbc6c-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="cbc6c-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cbc6c-121">nuget.exe</span></span> | <span data-ttu-id="cbc6c-122">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="cbc6c-122">array of objects</span></span> | <span data-ttu-id="cbc6c-123">Oui</span><span class="sxs-lookup"><span data-stu-id="cbc6c-123">yes</span></span>

<span data-ttu-id="cbc6c-124">Chaque objet du `nuget.exe` tableau a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbc6c-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="cbc6c-125">Nom</span><span class="sxs-lookup"><span data-stu-id="cbc6c-125">Name</span></span>     | <span data-ttu-id="cbc6c-126">Type</span><span class="sxs-lookup"><span data-stu-id="cbc6c-126">Type</span></span>   | <span data-ttu-id="cbc6c-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="cbc6c-127">Required</span></span> | <span data-ttu-id="cbc6c-128">Notes</span><span class="sxs-lookup"><span data-stu-id="cbc6c-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="cbc6c-129">version</span><span class="sxs-lookup"><span data-stu-id="cbc6c-129">version</span></span>  | <span data-ttu-id="cbc6c-130">string</span><span class="sxs-lookup"><span data-stu-id="cbc6c-130">string</span></span> | <span data-ttu-id="cbc6c-131">Oui</span><span class="sxs-lookup"><span data-stu-id="cbc6c-131">yes</span></span>      | <span data-ttu-id="cbc6c-132">Chaîne SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cbc6c-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="cbc6c-133">url</span><span class="sxs-lookup"><span data-stu-id="cbc6c-133">url</span></span>      | <span data-ttu-id="cbc6c-134">string</span><span class="sxs-lookup"><span data-stu-id="cbc6c-134">string</span></span> | <span data-ttu-id="cbc6c-135">Oui</span><span class="sxs-lookup"><span data-stu-id="cbc6c-135">yes</span></span>      | <span data-ttu-id="cbc6c-136">Une URL absolue pour le téléchargement de cette version de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cbc6c-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="cbc6c-137">étape</span><span class="sxs-lookup"><span data-stu-id="cbc6c-137">stage</span></span>    | <span data-ttu-id="cbc6c-138">string</span><span class="sxs-lookup"><span data-stu-id="cbc6c-138">string</span></span> | <span data-ttu-id="cbc6c-139">Oui</span><span class="sxs-lookup"><span data-stu-id="cbc6c-139">yes</span></span>      | <span data-ttu-id="cbc6c-140">Chaîne d’énumération</span><span class="sxs-lookup"><span data-stu-id="cbc6c-140">An enum string</span></span>
<span data-ttu-id="cbc6c-141">Téléchargé</span><span class="sxs-lookup"><span data-stu-id="cbc6c-141">uploaded</span></span> | <span data-ttu-id="cbc6c-142">string</span><span class="sxs-lookup"><span data-stu-id="cbc6c-142">string</span></span> | <span data-ttu-id="cbc6c-143">Oui</span><span class="sxs-lookup"><span data-stu-id="cbc6c-143">yes</span></span>      | <span data-ttu-id="cbc6c-144">Horodatage ISO 8601 approximatif de la date de mise à disposition de la version</span><span class="sxs-lookup"><span data-stu-id="cbc6c-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="cbc6c-145">Les éléments du tableau sont triés dans l’ordre décroissant, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="cbc6c-146">Cette garantie est destinée à réduire la charge d’un client qui est intéressé par le numéro de version le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="cbc6c-147">Toutefois, cela signifie que la liste n’est pas triée dans l’ordre chronologique.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="cbc6c-148">Par exemple, si une version principale inférieure est gérée à une date ultérieure à une version majeure supérieure, cette version en service n’apparaît pas en haut de la liste.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="cbc6c-149">Si vous souhaitez que la version la plus récente soit libérée par *horodateur*, il vous suffit de trier le tableau par la `uploaded` chaîne.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="cbc6c-150">Cela fonctionne parce que l' `uploaded` horodatage est au format [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) qui peut être trié par ordre chronologique à l’aide d’un tri lexicographique (par exemple, un tri de chaîne simple).</span><span class="sxs-lookup"><span data-stu-id="cbc6c-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="cbc6c-151">La `stage` propriété indique le degré de vérification de cette version de l’outil.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="cbc6c-152">Étape</span><span class="sxs-lookup"><span data-stu-id="cbc6c-152">Stage</span></span>              | <span data-ttu-id="cbc6c-153">Signification</span><span class="sxs-lookup"><span data-stu-id="cbc6c-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="cbc6c-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="cbc6c-154">EarlyAccessPreview</span></span> | <span data-ttu-id="cbc6c-155">Pas encore visible sur la [page Web de téléchargement](https://www.nuget.org/downloads) et doit être validé par les partenaires</span><span class="sxs-lookup"><span data-stu-id="cbc6c-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="cbc6c-156">Final</span><span class="sxs-lookup"><span data-stu-id="cbc6c-156">Released</span></span>           | <span data-ttu-id="cbc6c-157">Disponible sur le site de téléchargement, mais n’est pas encore recommandée pour une consommation étendue</span><span class="sxs-lookup"><span data-stu-id="cbc6c-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="cbc6c-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="cbc6c-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="cbc6c-159">Disponible sur le site de téléchargement et est recommandé pour la consommation</span><span class="sxs-lookup"><span data-stu-id="cbc6c-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="cbc6c-160">Une approche simple pour disposer de la version la plus récente recommandée consiste à prendre la première version de la liste qui a la `stage` valeur `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="cbc6c-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="cbc6c-161">Cela fonctionne parce que les versions sont triées dans l’ordre SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="cbc6c-162">Le `NuGet.CommandLine` package sur NuGet.org est généralement uniquement mis à jour avec des `ReleasedAndBlessed` versions.</span><span class="sxs-lookup"><span data-stu-id="cbc6c-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cbc6c-163">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="cbc6c-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="cbc6c-164">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="cbc6c-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
