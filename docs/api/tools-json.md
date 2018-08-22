---
title: Tools.JSON de détection des versions de nuget.exe
description: Le point de terminaison
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2018
ms.locfileid: "40247957"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="cb776-103">Tools.JSON de détection des versions de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cb776-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="cb776-104">Aujourd'hui, il existe plusieurs façons d’obtenir la dernière version de nuget.exe sur votre ordinateur de manière scriptable.</span><span class="sxs-lookup"><span data-stu-id="cb776-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="cb776-105">Par exemple, vous pouvez télécharger et extraire le [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) package à partir de nuget.org. Cela a une certaine complexité car elle requiert soit que vous avez déjà nuget.exe (pour `nuget.exe install`) ou vous devez décompresser le fichier .nupkg à l’aide d’un outil de décompression de base et de trouver le binaire à l’intérieur.</span><span class="sxs-lookup"><span data-stu-id="cb776-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="cb776-106">Si vous avez déjà nuget.exe, vous pouvez également utiliser `nuget.exe update -self`, mais cela nécessite également avoir une copie existante de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="cb776-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="cb776-107">Cette approche met également à jour vous vers la dernière version.</span><span class="sxs-lookup"><span data-stu-id="cb776-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="cb776-108">Il n’autorise pas l’utilisation d’une version spécifique.</span><span class="sxs-lookup"><span data-stu-id="cb776-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="cb776-109">Le `tools.json` point de terminaison est disponible pour les deux résoudre le problème de démarrage et à laisser le contrôle de la version de nuget.exe que vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="cb776-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="cb776-110">Cela peut servir dans des environnements CI/CD ou dans des scripts personnalisés pour détecter et de télécharger n’importe quelle version publiée de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="cb776-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="cb776-111">Le `tools.json` point de terminaison peut être extraites à l’aide d’une requête HTTP non authentifiée (par exemple, `Invoke-WebRequest` dans PowerShell ou `wget`).</span><span class="sxs-lookup"><span data-stu-id="cb776-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="cb776-112">Il peut être analysée à l’aide d’un désérialiseur JSON et télécharger nuget.exe suivantes de qu'url peuvent également être extraites à l’aide non authentifiée de requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="cb776-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="cb776-113">Le point de terminaison peut être extraites à l’aide de la `GET` méthode :</span><span class="sxs-lookup"><span data-stu-id="cb776-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="cb776-114">Le [schéma JSON](http://json-schema.org/) pour le point de terminaison est disponible ici :</span><span class="sxs-lookup"><span data-stu-id="cb776-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="cb776-115">Réponse</span><span class="sxs-lookup"><span data-stu-id="cb776-115">Response</span></span>

<span data-ttu-id="cb776-116">La réponse est un document JSON contenant toutes les versions disponibles de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="cb776-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="cb776-117">L’objet JSON racine a la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="cb776-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="cb776-118">Name</span><span class="sxs-lookup"><span data-stu-id="cb776-118">Name</span></span>      | <span data-ttu-id="cb776-119">Type</span><span class="sxs-lookup"><span data-stu-id="cb776-119">Type</span></span>             | <span data-ttu-id="cb776-120">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="cb776-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="cb776-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cb776-121">nuget.exe</span></span> | <span data-ttu-id="cb776-122">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="cb776-122">array of objects</span></span> | <span data-ttu-id="cb776-123">oui</span><span class="sxs-lookup"><span data-stu-id="cb776-123">yes</span></span>

<span data-ttu-id="cb776-124">Chaque objet dans le `nuget.exe` tableau présente les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb776-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="cb776-125">Name</span><span class="sxs-lookup"><span data-stu-id="cb776-125">Name</span></span>     | <span data-ttu-id="cb776-126">Type</span><span class="sxs-lookup"><span data-stu-id="cb776-126">Type</span></span>   | <span data-ttu-id="cb776-127">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="cb776-127">Required</span></span> | <span data-ttu-id="cb776-128">Notes</span><span class="sxs-lookup"><span data-stu-id="cb776-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="cb776-129">version</span><span class="sxs-lookup"><span data-stu-id="cb776-129">version</span></span>  | <span data-ttu-id="cb776-130">chaîne</span><span class="sxs-lookup"><span data-stu-id="cb776-130">string</span></span> | <span data-ttu-id="cb776-131">oui</span><span class="sxs-lookup"><span data-stu-id="cb776-131">yes</span></span>      | <span data-ttu-id="cb776-132">Une chaîne de SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cb776-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="cb776-133">url</span><span class="sxs-lookup"><span data-stu-id="cb776-133">url</span></span>      | <span data-ttu-id="cb776-134">chaîne</span><span class="sxs-lookup"><span data-stu-id="cb776-134">string</span></span> | <span data-ttu-id="cb776-135">oui</span><span class="sxs-lookup"><span data-stu-id="cb776-135">yes</span></span>      | <span data-ttu-id="cb776-136">Une URL absolue pour le téléchargement de cette version de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cb776-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="cb776-137">Étape</span><span class="sxs-lookup"><span data-stu-id="cb776-137">stage</span></span>    | <span data-ttu-id="cb776-138">chaîne</span><span class="sxs-lookup"><span data-stu-id="cb776-138">string</span></span> | <span data-ttu-id="cb776-139">oui</span><span class="sxs-lookup"><span data-stu-id="cb776-139">yes</span></span>      | <span data-ttu-id="cb776-140">Une chaîne d’enum</span><span class="sxs-lookup"><span data-stu-id="cb776-140">An enum string</span></span>
<span data-ttu-id="cb776-141">téléchargé</span><span class="sxs-lookup"><span data-stu-id="cb776-141">uploaded</span></span> | <span data-ttu-id="cb776-142">chaîne</span><span class="sxs-lookup"><span data-stu-id="cb776-142">string</span></span> | <span data-ttu-id="cb776-143">oui</span><span class="sxs-lookup"><span data-stu-id="cb776-143">yes</span></span>      | <span data-ttu-id="cb776-144">Un horodatage approximatif de lorsque la version mise à disposition</span><span class="sxs-lookup"><span data-stu-id="cb776-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="cb776-145">Les éléments dans le tableau doit être triées, SemVer 2.0.0 par ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="cb776-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="cb776-146">Cette garantie est destinée à alléger le fardeau sur un client recherche de la dernière version.</span><span class="sxs-lookup"><span data-stu-id="cb776-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="cb776-147">Le `stage` propriété indique le mode vettect cette version de l’outil.</span><span class="sxs-lookup"><span data-stu-id="cb776-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="cb776-148">Étape</span><span class="sxs-lookup"><span data-stu-id="cb776-148">Stage</span></span>              | <span data-ttu-id="cb776-149">Signification</span><span class="sxs-lookup"><span data-stu-id="cb776-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="cb776-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="cb776-150">EarlyAccessPreview</span></span> | <span data-ttu-id="cb776-151">Pas encore visible sur le [web page de téléchargement](https://www.nuget.org/downloads) et doivent être validés par les partenaires</span><span class="sxs-lookup"><span data-stu-id="cb776-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="cb776-152">Final</span><span class="sxs-lookup"><span data-stu-id="cb776-152">Released</span></span>           | <span data-ttu-id="cb776-153">Disponible sur le site de téléchargement, mais n’est pas encore recommandé pour la consommation généralisée</span><span class="sxs-lookup"><span data-stu-id="cb776-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="cb776-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="cb776-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="cb776-155">Disponible sur le site de téléchargement et est recommandée pour la consommation</span><span class="sxs-lookup"><span data-stu-id="cb776-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="cb776-156">Une approche simple pour avoir la dernière version, la version recommandée est à prendre la première version dans la liste qui possède le `stage` valeur `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="cb776-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="cb776-157">Le `NuGet.CommandLine` package sur nuget.org est généralement uniquement mis à jour avec `ReleasedAndBlessed` versions.</span><span class="sxs-lookup"><span data-stu-id="cb776-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cb776-158">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="cb776-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="cb776-159">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="cb776-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
