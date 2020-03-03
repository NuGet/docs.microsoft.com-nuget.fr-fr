---
title: Utilisation de packages à partir de flux authentifiés
description: Consommation de packages à partir de flux authentifiés dans tous les scénarios client NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231790"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="e0a29-103">Utilisation de packages à partir de flux authentifiés</span><span class="sxs-lookup"><span data-stu-id="e0a29-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="e0a29-104">En plus du [flux public](https://api.nuget.org/v3/index.json)NuGet.org, les clients NuGet ont la possibilité d’interagir avec les flux de fichiers et les flux http privés.</span><span class="sxs-lookup"><span data-stu-id="e0a29-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="e0a29-105">Pour s’authentifier avec des flux http privés, les deux approches sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0a29-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="e0a29-106">Ajouter des informations d’identification dans [NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="e0a29-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="e0a29-107">Authentifiez-vous à l’aide de l’un des nombreux modèles d’extensibilité en fonction du client utilisé.</span><span class="sxs-lookup"><span data-stu-id="e0a29-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="e0a29-108">Extensibilité des authentifications des clients NuGet</span><span class="sxs-lookup"><span data-stu-id="e0a29-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="e0a29-109">Pour les différents clients NuGet, le fournisseur de flux privé lui-même est responsable de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="e0a29-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="e0a29-110">Tous les clients NuGet ont des méthodes d’extensibilité pour prendre en charge cette méthode.</span><span class="sxs-lookup"><span data-stu-id="e0a29-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="e0a29-111">Il s’agit soit d’une extension de Visual Studio, soit d’un plug-in capable de communiquer avec NuGet pour récupérer les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e0a29-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="e0a29-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0a29-112">Visual Studio</span></span>

<span data-ttu-id="e0a29-113">Dans Visual Studio, NuGet expose une interface que les fournisseurs de flux peuvent implémenter et fournir à leurs clients.</span><span class="sxs-lookup"><span data-stu-id="e0a29-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="e0a29-114">Pour plus d’informations, consultez la documentation sur la [création d’un fournisseur d’informations d’identification Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="e0a29-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="e0a29-115">Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0a29-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="e0a29-116">Un fournisseur d’informations d’identification est intégré à Visual Studio pour prendre en charge Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="e0a29-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="e0a29-117">Les fournisseurs d’informations d’identification de plug-in disponibles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="e0a29-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="e0a29-118">Fournisseur d’informations d’identification MyGet pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0a29-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="e0a29-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e0a29-119">nuget.exe</span></span>

<span data-ttu-id="e0a29-120">Lorsque `nuget.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il les recherche de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="e0a29-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="e0a29-121">Recherchez les informations d’identification dans `NuGet.config` fichiers.</span><span class="sxs-lookup"><span data-stu-id="e0a29-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="e0a29-122">Utiliser des fournisseurs d’informations d’identification de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="e0a29-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="e0a29-123">Utiliser des fournisseurs d’informations d’identification de plug-in v1</span><span class="sxs-lookup"><span data-stu-id="e0a29-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="e0a29-124">NuGet invite ensuite l’utilisateur à fournir des informations d’identification sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="e0a29-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="e0a29-125">fournisseurs d’informations d’identification NuGet. exe et v2</span><span class="sxs-lookup"><span data-stu-id="e0a29-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="e0a29-126">Dans la version `4.8` NuGet définissait un nouveau mécanisme de plug-in d’authentification, ci-après appelés fournisseurs d’informations d’identification v2.</span><span class="sxs-lookup"><span data-stu-id="e0a29-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="e0a29-127">Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [plug-ins NuGet inter-plateformes](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="e0a29-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="e0a29-128">fournisseurs d’informations d’identification NuGet. exe et v1</span><span class="sxs-lookup"><span data-stu-id="e0a29-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="e0a29-129">Dans la version `3.3` NuGet a introduit la première version des plug-ins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e0a29-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="e0a29-130">Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [fournisseurs d’informations d’identification NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="e0a29-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="e0a29-131">Fournisseurs d’informations d’identification disponibles pour NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="e0a29-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="e0a29-132">[Fournisseurs d’informations d’identification Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou [Azure artifacts fournisseur d’informations d’identification](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="e0a29-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="e0a29-133">Avec Visual Studio 2017 version 15,9 et versions ultérieures, le fournisseur d’informations d’identification Azure DevOps est regroupé dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0a29-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="e0a29-134">Si `nuget.exe` utilise MSBuild à partir de cet ensemble d’outils Visual Studio spécifique, le plug-in est découvert automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e0a29-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="e0a29-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="e0a29-135">dotnet.exe</span></span>

<span data-ttu-id="e0a29-136">Lorsque `dotnet.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il les recherche de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="e0a29-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="e0a29-137">Recherchez les informations d’identification dans `NuGet.config` fichiers.</span><span class="sxs-lookup"><span data-stu-id="e0a29-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="e0a29-138">Utiliser des fournisseurs d’informations d’identification de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="e0a29-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="e0a29-139">Par défaut `dotnet.exe` n’est pas interactif, vous devrez peut-être passer un indicateur `--interactive` pour que l’outil soit bloqué pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="e0a29-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="e0a29-140">fournisseurs d’informations d’identification dotnet. exe et v2</span><span class="sxs-lookup"><span data-stu-id="e0a29-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="e0a29-141">Dans `2.2.100` de version du kit de développement logiciel (SDK), NuGet a défini un mécanisme de plug-in d’authentification qui fonctionne sur tous les clients.</span><span class="sxs-lookup"><span data-stu-id="e0a29-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="e0a29-142">Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [plug-ins NuGet inter-plateformes](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="e0a29-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="e0a29-143">Fournisseurs d’informations d’identification disponibles pour dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="e0a29-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="e0a29-144">Fournisseur d’informations d’identification Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="e0a29-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="e0a29-145">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="e0a29-145">MSBuild.exe</span></span>

<span data-ttu-id="e0a29-146">Lorsque `MSBuild.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il les recherche de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="e0a29-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="e0a29-147">Rechercher les informations d’identification dans les fichiers `NuGet.config`</span><span class="sxs-lookup"><span data-stu-id="e0a29-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="e0a29-148">Utiliser des fournisseurs d’informations d’identification de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="e0a29-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="e0a29-149">Par défaut `MSBuild.exe` n’est pas interactif, vous devrez peut-être définir la propriété `/p:NuGetInteractive=true` pour que l’outil soit bloqué pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="e0a29-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="e0a29-150">Fournisseurs d’informations d’identification MSBuild. exe et v2</span><span class="sxs-lookup"><span data-stu-id="e0a29-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="e0a29-151">Dans Visual Studio 2019 Update 9, NuGet a défini un mécanisme de plug-in d’authentification qui fonctionne sur tous les clients.</span><span class="sxs-lookup"><span data-stu-id="e0a29-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="e0a29-152">Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [plug-ins NuGet inter-plateformes](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="e0a29-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="e0a29-153">Fournisseurs d’informations d’identification disponibles pour MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="e0a29-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="e0a29-154">Fournisseur d’informations d’identification Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="e0a29-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="e0a29-155">Avec Visual Studio 2017 Update 9 et versions ultérieures, le fournisseur d’informations d’identification Azure DevOps est regroupé dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0a29-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="e0a29-156">Aucune étape supplémentaire n’est requise.</span><span class="sxs-lookup"><span data-stu-id="e0a29-156">No additional steps are required.</span></span>
