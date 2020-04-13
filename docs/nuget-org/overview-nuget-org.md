---
title: Vue d’ensemble de NuGet.org
description: Vue d’ensemble de NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427014"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="4444c-103">Vue d’ensemble de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4444c-103">Overview of NuGet.org</span></span>

<span data-ttu-id="4444c-104">NuGet.org est un hôte public qui héberge les packages NuGet utilisés par des millions de développeurs .NET et .NET Core chaque jour.</span><span class="sxs-lookup"><span data-stu-id="4444c-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="4444c-105">Rôle de NuGet.org dans l’écosystème NuGet</span><span class="sxs-lookup"><span data-stu-id="4444c-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="4444c-106">Dans son rôle d’hôte public, NuGet.org elle-même maintient le dépôt central de plus de 100.000 paquets uniques à [nuget.org](https://www.nuget.org). NuGet.org n’est pas le seul hôte possible pour les forfaits.</span><span class="sxs-lookup"><span data-stu-id="4444c-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="4444c-107">La technologie NuGet vous permet également d’héberger des packages à titre privé dans le cloud (par exemple sur Azure DevOps), sur un réseau privé ou tout simplement sur votre système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="4444c-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="4444c-108">Si vous êtes intéressé par un autre hôte ou une autre option d’hébergement, consultez [Hébergement de vos propres flux NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4444c-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="4444c-109">NuGet.org, comme tous les autres hôtes de packages NuGet, sert de point de connexion entre les *créateurs* et les *consommateurs* de packages.</span><span class="sxs-lookup"><span data-stu-id="4444c-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="4444c-110">Les créateurs génèrent des packages NuGet utiles et les publient.</span><span class="sxs-lookup"><span data-stu-id="4444c-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="4444c-111">Les consommateurs recherchent des packages pratiques et compatibles sur les hôtes accessibles, les téléchargent et incluent ces packages dans leurs projets.</span><span class="sxs-lookup"><span data-stu-id="4444c-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="4444c-112">Une fois installés dans un projet, les API des packages sont disponibles pour le reste du code du projet.</span><span class="sxs-lookup"><span data-stu-id="4444c-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relation entre les créateurs de packages, les hôtes de packages et les consommateurs de packages](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="4444c-114">Comptes</span><span class="sxs-lookup"><span data-stu-id="4444c-114">Accounts</span></span>

<span data-ttu-id="4444c-115">Pour publier des packages sur NuGet.org, vous créez d’abord un [compte individuel (utilisateur)](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="4444c-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="4444c-116">Ce compte devient votre identité sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4444c-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="4444c-117">NuGet.org vous permet également de créer un [compte d’organisation](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="4444c-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="4444c-118">Un compte d’organisation comprend un ou plusieurs comptes individuels comme membres.</span><span class="sxs-lookup"><span data-stu-id="4444c-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="4444c-119">Ces derniers peuvent gérer un ensemble de packages tout en conservant une identité unique pour appropriation.</span><span class="sxs-lookup"><span data-stu-id="4444c-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="4444c-120">Votre compte individuel vous permet d’être membre de plusieurs organisations.</span><span class="sxs-lookup"><span data-stu-id="4444c-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="4444c-121">Un package peut appartenir à un compte d’organisation ou à un compte individuel.</span><span class="sxs-lookup"><span data-stu-id="4444c-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="4444c-122">Pour les consommateurs de packages, il n’y a aucune différence entre un compte individuel et le compte d’organisation : tous deux sont présentés comme les propriétaires (`owners`) des packages.</span><span class="sxs-lookup"><span data-stu-id="4444c-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="4444c-123">Clés API</span><span class="sxs-lookup"><span data-stu-id="4444c-123">API keys</span></span>

<span data-ttu-id="4444c-124">Maintenant que vous disposez d’un package NuGet (fichier *.nupkg*) à publier, publiez-le sur NuGet.org à l’aide de l’interface CLI nuget.exe ou dotnet.exe, avec une [clé API](scoped-api-keys.md) acquise sur NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4444c-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="4444c-125">Quand vous [publiez un package](../create-packages/creating-a-package.md), incluez la valeur de la clé API dans la commande CLI.</span><span class="sxs-lookup"><span data-stu-id="4444c-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="4444c-126">Préfixes d’ID</span><span class="sxs-lookup"><span data-stu-id="4444c-126">ID prefixes</span></span>

<span data-ttu-id="4444c-127">Quand vous publiez des packages, vous pouvez réserver et protéger votre identité en [réservant des préfixes d’ID](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="4444c-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="4444c-128">Durant l’installation d’un package, les consommateurs reçoivent des informations supplémentaires indiquant que les propriétés d’identification du package qu’ils consomment ne sont pas trompeuses.</span><span class="sxs-lookup"><span data-stu-id="4444c-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="4444c-129">Point de terminaison d’API pour NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4444c-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="4444c-130">Pour utiliser NuGet.org comme dépôt de packages avec les clients NuGet, vous devez utiliser le point de terminaison d’API V3 suivant :</span><span class="sxs-lookup"><span data-stu-id="4444c-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="4444c-131">Les clients plus âgés peuvent toujours utiliser le protocole V2 pour atteindre NuGet.org. Toutefois, veuillez noter que les clients de NuGet 3.0 ou plus tard auront un service plus lent et moins fiable en utilisant le protocole V2 :</span><span class="sxs-lookup"><span data-stu-id="4444c-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="4444c-132">`https://www.nuget.org/api/v2` (**Le protocole V2 est déprécié !**)</span><span class="sxs-lookup"><span data-stu-id="4444c-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
