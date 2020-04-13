---
title: Consommer des paquets à partir d’aliments authentifiés
description: Consommer des paquets à partir d’aliments authentifiés dans tous les scénarios des clients NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231790"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="77d60-103">Consommer des paquets à partir d’aliments authentifiés</span><span class="sxs-lookup"><span data-stu-id="77d60-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="77d60-104">En plus de la nuget.org [alimentation publique](https://api.nuget.org/v3/index.json), les clients NuGet ont la possibilité d’interagir avec les flux de fichiers et les flux http privés.</span><span class="sxs-lookup"><span data-stu-id="77d60-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="77d60-105">Pour authentifier avec des flux http privés, les 2 approches sont :</span><span class="sxs-lookup"><span data-stu-id="77d60-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="77d60-106">Ajouter les informations d’identification dans le [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="77d60-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="77d60-107">Authentifier à l’aide d’un des nombreux modèles d’extéabilité selon le client utilisé.</span><span class="sxs-lookup"><span data-stu-id="77d60-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="77d60-108">L’extéabilité de l’authentification des clients de NuGet</span><span class="sxs-lookup"><span data-stu-id="77d60-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="77d60-109">Pour les différents clients NuGet, le fournisseur privé d’aliments est lui-même responsable de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="77d60-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="77d60-110">Tous les clients de NuGet ont des méthodes d’exténuabilité pour soutenir cela.</span><span class="sxs-lookup"><span data-stu-id="77d60-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="77d60-111">Il s’agit soit d’une extension Visual Studio ou d’un plugin qui peut communiquer avec NuGet pour récupérer les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="77d60-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="77d60-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77d60-112">Visual Studio</span></span>

<span data-ttu-id="77d60-113">Dans Visual Studio, NuGet expose une interface que les fournisseurs d’aliments peuvent implémenter et fournir à leurs clients.</span><span class="sxs-lookup"><span data-stu-id="77d60-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="77d60-114">Pour plus de détails, veuillez consulter la documentation sur la [façon de créer un fournisseur d’informations d’identification Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="77d60-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="77d60-115">Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77d60-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="77d60-116">Il existe un fournisseur d’informations d’identification intégré à Visual Studio pour prendre en charge Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="77d60-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="77d60-117">Les fournisseurs d’informations d’identification plug-in disponibles comprennent :</span><span class="sxs-lookup"><span data-stu-id="77d60-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="77d60-118">MyGet Credential Provider pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77d60-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="77d60-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="77d60-119">nuget.exe</span></span>

<span data-ttu-id="77d60-120">Lorsque `nuget.exe` les informations d’identification doivent être authentiques avec un flux, elles les recherchent de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="77d60-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="77d60-121">Recherchez les `NuGet.config` informations d’identification dans les fichiers.</span><span class="sxs-lookup"><span data-stu-id="77d60-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="77d60-122">Utilisez les fournisseurs d’informations d’identification rechargeables V2</span><span class="sxs-lookup"><span data-stu-id="77d60-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="77d60-123">Utilisez les fournisseurs d’informations d’identification rechargeableS V1</span><span class="sxs-lookup"><span data-stu-id="77d60-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="77d60-124">NuGet invite ensuite l’utilisateur pour les informations d’identification sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="77d60-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="77d60-125">fournisseurs d’informations d’identification nuget.exe et V2</span><span class="sxs-lookup"><span data-stu-id="77d60-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="77d60-126">Dans `4.8` la version NuGet a défini un nouveau mécanisme de plugin d’authentification, par la suite appelé fournisseurs d’identification V2.</span><span class="sxs-lookup"><span data-stu-id="77d60-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="77d60-127">Pour l’installation et la découverte de ces fournisseurs, se référer à [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="77d60-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="77d60-128">fournisseurs d’informations d’identification nuget.exe et V1</span><span class="sxs-lookup"><span data-stu-id="77d60-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="77d60-129">Dans `3.3` la version NuGet introduit la première version de plugins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="77d60-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="77d60-130">Pour l’installation et la découverte de ces fournisseurs se réfèrent à [nuget.exe fournisseurs d’informations d’identification](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="77d60-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="77d60-131">Fournisseurs d’informations d’identification disponibles pour nuget.exe</span><span class="sxs-lookup"><span data-stu-id="77d60-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="77d60-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider) Azure DevOps V2 Credential Providers or Azure Artifacts Credential Provider Azure DevOps V2 Credential Providers or Azure Artifacts Credential Provider Azure</span><span class="sxs-lookup"><span data-stu-id="77d60-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="77d60-133">Avec Visual Studio 2017 version 15.9 et plus tard, le fournisseur d’informations Azure DevOps est regroupé dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77d60-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="77d60-134">Si `nuget.exe` l’on utilise MSBuild à partir de cet outil Visual Studio spécifique, alors le plugin sera découvert automatiquement.</span><span class="sxs-lookup"><span data-stu-id="77d60-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="77d60-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="77d60-135">dotnet.exe</span></span>

<span data-ttu-id="77d60-136">Lorsque `dotnet.exe` les informations d’identification doivent être authentiques avec un flux, elles les recherchent de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="77d60-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="77d60-137">Recherchez les `NuGet.config` informations d’identification dans les fichiers.</span><span class="sxs-lookup"><span data-stu-id="77d60-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="77d60-138">Utilisez les fournisseurs d’informations d’identification rechargeables V2</span><span class="sxs-lookup"><span data-stu-id="77d60-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="77d60-139">Par `dotnet.exe` défaut n’est pas interactif, vous `--interactive` pourriez donc avoir besoin de passer un drapeau pour obtenir l’outil à bloquer pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="77d60-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="77d60-140">dotnet.exe et fournisseurs d’identification V2</span><span class="sxs-lookup"><span data-stu-id="77d60-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="77d60-141">En `2.2.100` version du SDK, NuGet a défini un mécanisme de plugin d’authentification qui fonctionne chez tous les clients.</span><span class="sxs-lookup"><span data-stu-id="77d60-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="77d60-142">Pour l’installation et la découverte de ces fournisseurs, se référer à [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="77d60-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="77d60-143">Fournisseurs d’informations d’identification disponibles pour dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="77d60-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="77d60-144">Fournisseur d’informations d’identification Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="77d60-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="77d60-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="77d60-145">MSBuild.exe</span></span>

<span data-ttu-id="77d60-146">Lorsque `MSBuild.exe` les informations d’identification doivent être authentiques avec un flux, elles les recherchent de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="77d60-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="77d60-147">Rechercher les informations `NuGet.config` d’identification dans les fichiers</span><span class="sxs-lookup"><span data-stu-id="77d60-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="77d60-148">Utilisez les fournisseurs d’informations d’identification rechargeables V2</span><span class="sxs-lookup"><span data-stu-id="77d60-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="77d60-149">Par `MSBuild.exe` défaut n’est pas interactif, `/p:NuGetInteractive=true` de sorte que vous pourriez avoir besoin de définir la propriété pour obtenir l’outil à bloquer pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="77d60-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="77d60-150">Fournisseurs d’informations d’identification MSBuild.exe et V2</span><span class="sxs-lookup"><span data-stu-id="77d60-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="77d60-151">Dans Visual Studio 2019 Update 9, NuGet a défini un mécanisme de plugin d’authentification qui fonctionne chez tous les clients.</span><span class="sxs-lookup"><span data-stu-id="77d60-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="77d60-152">Pour l’installation et la découverte de ces fournisseurs, se référer à [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="77d60-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="77d60-153">Fournisseurs d’informations d’identification disponibles pour MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="77d60-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="77d60-154">Fournisseur d’informations d’identification Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="77d60-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="77d60-155">Avec Visual Studio 2017 Update 9 et plus tard, le fournisseur d’informations Azure DevOps est regroupé dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77d60-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="77d60-156">Aucune étape supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="77d60-156">No additional steps are required.</span></span>
