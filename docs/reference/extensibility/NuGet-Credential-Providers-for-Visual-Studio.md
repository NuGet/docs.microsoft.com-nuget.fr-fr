---
title: Fournisseurs d’informations d’identification NuGet pour Visual Studio
description: Fournisseurs d’informations d’identification NuGet s’authentifier avec des flux en implémentant l’interface IVsCredentialProvider dans une extension Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793901"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="7784b-103">L’authentification de flux dans Visual Studio avec les fournisseurs d’informations d’identification NuGet</span><span class="sxs-lookup"><span data-stu-id="7784b-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="7784b-104">L’Extension NuGet Visual Studio 3.6 et + prend en charge les fournisseurs d’informations d’identification, qui permettent de NuGet travailler avec les flux authentifiés.</span><span class="sxs-lookup"><span data-stu-id="7784b-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="7784b-105">Après avoir installé un fournisseur d’informations d’identification NuGet pour Visual Studio, l’extension NuGet Visual Studio va automatiquement acquérir et actualiser les informations d’identification pour les flux authentifiés en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="7784b-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="7784b-106">Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="7784b-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="7784b-107">En commençant par 4.8 + NuGet dans Visual Studio prend en charge les nouvelles inter-plateformes authentification plug-ins également, mais ils ne sont pas l’approche recommandée pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="7784b-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="7784b-108">Fournisseurs d’informations d’identification NuGet pour Visual Studio doit être installés comme une extension de Visual Studio standard et nécessitera [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7784b-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="7784b-109">Fournisseurs d’informations d’identification NuGet pour Visual Studio fonctionnent uniquement dans Visual Studio (pas dans la restauration de dotnet ou nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="7784b-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="7784b-110">Pour les fournisseurs d’informations d’identification avec nuget.exe, consultez [nuget.exe fournisseurs d’informations d’identification](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="7784b-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="7784b-111">Pour les informations d’identification fournisseurs dans dotnet et msbuild consultez [NuGet entre les plug-ins de la plateforme](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="7784b-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="7784b-112">Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7784b-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="7784b-113">Il existe un fournisseur d’informations d’identification intégré à l’extension de Visual Studio NuGet pour prendre en charge de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7784b-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="7784b-114">L’Extension NuGet Visual Studio utilise un interne `VsCredentialProviderImporter` qui analyse également pour les fournisseurs de plug-in informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7784b-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="7784b-115">Ces fournisseurs d’informations d’identification de plug-in doivent être détectables en tant qu’une exportation MEF de type `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="7784b-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="7784b-116">Fournisseurs d’informations d’identification de plug-in disponibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7784b-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="7784b-117">Fournisseur d’informations d’identification MyGet pour Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7784b-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="7784b-118">Création d’un fournisseur d’informations d’identification NuGet pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7784b-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="7784b-119">L’Extension NuGet Visual Studio 3.6 et + implémente un CredentialService interne qui est utilisée pour obtenir des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7784b-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="7784b-120">Le CredentialService a une liste de fournisseurs d’informations d’identification intégrés et plug-in.</span><span class="sxs-lookup"><span data-stu-id="7784b-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="7784b-121">Chaque fournisseur est testé séquentiellement jusqu'à ce que les informations d’identification sont acquis.</span><span class="sxs-lookup"><span data-stu-id="7784b-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="7784b-122">Pendant l’acquisition d’informations d’identification, le service d’informations d’identification va tenter de fournisseurs d’informations d’identification dans l’ordre suivant, l’arrêt dès que les informations d’identification sont acquis :</span><span class="sxs-lookup"><span data-stu-id="7784b-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="7784b-123">Informations d’identification seront extraites à partir des fichiers de configuration NuGet (à l’aide intégrée `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="7784b-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="7784b-124">Si la source du package se trouve sur Visual Studio Team Services, le `VisualStudioAccountProvider` sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="7784b-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="7784b-125">Tous les autres fournisseurs d’informations d’identification Visual Studio plug-in seront tentées de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="7784b-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="7784b-126">Essayez d’utiliser tous les NuGet entre les fournisseurs d’informations d’identification de plateforme séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="7784b-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="7784b-127">Si aucune information d’identification n’ont été acquis, l’utilisateur demandera les informations d’identification à l’aide d’une boîte de dialogue de l’authentification de base standard.</span><span class="sxs-lookup"><span data-stu-id="7784b-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="7784b-128">Implémentation IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="7784b-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="7784b-129">Pour créer un fournisseur d’informations d’identification NuGet pour Visual Studio, créez une Extension Visual Studio qui expose une publique exportation MEF qui implémente le `IVsCredentialProvider` tapez, adhère aux principes énoncés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7784b-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="7784b-130">Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="7784b-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="7784b-131">Chaque fournisseur d’informations d’identification NuGet pour Visual Studio doit :</span><span class="sxs-lookup"><span data-stu-id="7784b-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="7784b-132">Déterminer si elle peut fournir des informations d’identification pour l’URI cible avant de lancer l’acquisition des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7784b-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="7784b-133">Si le fournisseur ne peut pas fournir les informations d’identification pour la source ciblée, elle doit retourner `null`.</span><span class="sxs-lookup"><span data-stu-id="7784b-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="7784b-134">Si le fournisseur gère les demandes pour l’URI cible, mais ne peut pas fournir les informations d’identification, une exception doit être levée.</span><span class="sxs-lookup"><span data-stu-id="7784b-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="7784b-135">Un fournisseur d’informations d’identification NuGet personnalisé pour Visual Studio doit implémenter le `IVsCredentialProvider` interface disponible dans le [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="7784b-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="7784b-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="7784b-136">GetCredentialAsync</span></span>

| <span data-ttu-id="7784b-137">Paramètre d’entrée</span><span class="sxs-lookup"><span data-stu-id="7784b-137">Input Parameter</span></span> |<span data-ttu-id="7784b-138">Description</span><span class="sxs-lookup"><span data-stu-id="7784b-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="7784b-139">Uri de l’URI</span><span class="sxs-lookup"><span data-stu-id="7784b-139">Uri uri</span></span> | <span data-ttu-id="7784b-140">L’Uri de source de package pour lequel les informations d’identification sont demandées.</span><span class="sxs-lookup"><span data-stu-id="7784b-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="7784b-141">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="7784b-141">IWebProxy proxy</span></span> | <span data-ttu-id="7784b-142">Proxy Web à utiliser lors de la communication sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="7784b-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="7784b-143">Null s’il n’existe aucune authentification de proxy configurée.</span><span class="sxs-lookup"><span data-stu-id="7784b-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="7784b-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="7784b-144">bool isProxyRequest</span></span> | <span data-ttu-id="7784b-145">True si cette demande est pour obtenir des informations d’identification de l’authentification de proxy.</span><span class="sxs-lookup"><span data-stu-id="7784b-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="7784b-146">Si l’implémentation n’est pas valide pour l’acquisition des informations d’identification de proxy, null doit être retourné.</span><span class="sxs-lookup"><span data-stu-id="7784b-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="7784b-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="7784b-147">bool isRetry</span></span> | <span data-ttu-id="7784b-148">True si les informations d’identification ont été précédemment demandées pour cet Uri, mais les informations d’identification fournies ne permettait pas d’accès autorisé.</span><span class="sxs-lookup"><span data-stu-id="7784b-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="7784b-149">bool non interactive</span><span class="sxs-lookup"><span data-stu-id="7784b-149">bool nonInteractive</span></span> | <span data-ttu-id="7784b-150">Si la valeur est true, le fournisseur d’informations d’identification doit supprimer toutes les invites utilisateur et utilisez à la place des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="7784b-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="7784b-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="7784b-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="7784b-152">Ce jeton d’annulation doit être vérifié pour déterminer si les informations d’identification demandeur d’opération a été annulée.</span><span class="sxs-lookup"><span data-stu-id="7784b-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="7784b-153">**Valeur de retour**: un objet informations d’identification qui implémente le [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="7784b-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
