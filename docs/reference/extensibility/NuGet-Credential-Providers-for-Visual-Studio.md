---
title: Fournisseurs d’informations d’identification NuGet pour Visual Studio
description: Les fournisseurs d’informations d’identification NuGet s’authentifient avec des flux en implémentant l’interface IVsCredentialProvider dans une extension Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384427"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="d42fb-103">Authentification de flux dans Visual Studio avec des fournisseurs d’informations d’identification NuGet</span><span class="sxs-lookup"><span data-stu-id="d42fb-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="d42fb-104">L’extension Visual Studio NuGet 3.6 + prend en charge les fournisseurs d’informations d’identification, ce qui permet à NuGet de fonctionner avec les flux authentifiés.</span><span class="sxs-lookup"><span data-stu-id="d42fb-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="d42fb-105">Après l’installation d’un fournisseur d’informations d’identification NuGet pour Visual Studio, l’extension NuGet Visual Studio acquière et actualise automatiquement les informations d’identification pour les flux authentifiés si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d42fb-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="d42fb-106">Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="d42fb-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="d42fb-107">À compter de la section 4.8 + NuGet dans Visual Studio prend également en charge les nouveaux plug-ins d’authentification multiplateforme, mais ce n’est pas l’approche recommandée pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="d42fb-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="d42fb-108">Les fournisseurs d’informations d’identification NuGet pour Visual Studio doivent être installés en tant qu’extension Visual Studio standard et nécessitent [Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d42fb-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="d42fb-109">Les fournisseurs d’informations d’identification NuGet pour Visual Studio fonctionnent uniquement dans Visual Studio (pas dans dotnet restore ou NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="d42fb-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="d42fb-110">Pour obtenir des fournisseurs d’informations d’identification avec NuGet. exe, consultez [fournisseurs d’informations d’identification NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="d42fb-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="d42fb-111">Pour les fournisseurs d’informations d’identification dans dotnet et MSBuild, consultez [plug-ins inter-plateforme NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="d42fb-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="d42fb-112">Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d42fb-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="d42fb-113">Un fournisseur d’informations d’identification est intégré à l’extension NuGet de Visual Studio pour prendre en charge Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="d42fb-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="d42fb-114">L’extension Visual Studio NuGet utilise une interne `VsCredentialProviderImporter` qui recherche également les fournisseurs d’informations d’identification de plug-in.</span><span class="sxs-lookup"><span data-stu-id="d42fb-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="d42fb-115">Ces fournisseurs d’informations d’identification de plug-in doivent être détectables comme une exportation `IVsCredentialProvider`MEF de type.</span><span class="sxs-lookup"><span data-stu-id="d42fb-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="d42fb-116">Les fournisseurs d’informations d’identification de plug-in disponibles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d42fb-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="d42fb-117">Fournisseur d’informations d’identification MyGet pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d42fb-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="d42fb-118">Création d’un fournisseur d’informations d’identification NuGet pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d42fb-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="d42fb-119">L’extension Visual Studio NuGet 3.6 + implémente un CredentialService interne qui est utilisé pour obtenir les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d42fb-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="d42fb-120">Le CredentialService contient une liste de fournisseurs d’informations d’identification intégrés et de plug-in.</span><span class="sxs-lookup"><span data-stu-id="d42fb-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="d42fb-121">Chaque fournisseur est essayé séquentiellement jusqu’à ce que les informations d’identification soient acquises.</span><span class="sxs-lookup"><span data-stu-id="d42fb-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="d42fb-122">Lors de l’acquisition des informations d’identification, le service d’informations d’identification essaiera les fournisseurs d’informations d’identification dans l’ordre suivant, en arrêtant dès que les informations d’identification sont acquises :</span><span class="sxs-lookup"><span data-stu-id="d42fb-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="d42fb-123">Les informations d’identification sont extraites à partir des fichiers de configuration NuGet (à `SettingsCredentialProvider`l’aide de l’intégré).</span><span class="sxs-lookup"><span data-stu-id="d42fb-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="d42fb-124">Si la source du package se trouve sur Visual Studio Team Services `VisualStudioAccountProvider` , sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="d42fb-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="d42fb-125">Tous les autres fournisseurs d’informations d’identification Visual Studio du plug-in seront essayés séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="d42fb-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="d42fb-126">Essayez d’utiliser tous les fournisseurs d’informations d’identification inter-plateforme NuGet de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="d42fb-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="d42fb-127">Si aucune information d’identification n’a encore été acquise, l’utilisateur est invité à fournir des informations d’identification à l’aide d’une boîte de dialogue d’authentification de base standard.</span><span class="sxs-lookup"><span data-stu-id="d42fb-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="d42fb-128">Implémentation de IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="d42fb-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="d42fb-129">Pour créer un fournisseur d’informations d’identification NuGet pour Visual Studio, créez une extension Visual Studio qui expose une exportation MEF `IVsCredentialProvider` publique qui implémente le type et qui adhère aux principes énoncés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d42fb-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="d42fb-130">Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="d42fb-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="d42fb-131">Chaque fournisseur d’informations d’identification NuGet pour Visual Studio doit :</span><span class="sxs-lookup"><span data-stu-id="d42fb-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="d42fb-132">Déterminez si elle peut fournir des informations d’identification pour l’URI ciblé avant de lancer l’acquisition des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d42fb-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="d42fb-133">Si le fournisseur ne peut pas fournir d’informations d’identification pour la source ciblée `null`, il doit retourner.</span><span class="sxs-lookup"><span data-stu-id="d42fb-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="d42fb-134">Si le fournisseur gère les demandes pour l’URI ciblé, mais ne peut pas fournir d’informations d’identification, une exception doit être levée.</span><span class="sxs-lookup"><span data-stu-id="d42fb-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="d42fb-135">Un fournisseur d’informations d’identification NuGet personnalisé pour Visual Studio `IVsCredentialProvider` doit implémenter l’interface disponible dans le [package NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="d42fb-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="d42fb-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="d42fb-136">GetCredentialAsync</span></span>

| <span data-ttu-id="d42fb-137">Paramètre d’entrée</span><span class="sxs-lookup"><span data-stu-id="d42fb-137">Input Parameter</span></span> |<span data-ttu-id="d42fb-138">Description</span><span class="sxs-lookup"><span data-stu-id="d42fb-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="d42fb-139">URI de l’URI</span><span class="sxs-lookup"><span data-stu-id="d42fb-139">Uri uri</span></span> | <span data-ttu-id="d42fb-140">URI source du package pour lequel les informations d’identification sont demandées.</span><span class="sxs-lookup"><span data-stu-id="d42fb-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="d42fb-141">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="d42fb-141">IWebProxy proxy</span></span> | <span data-ttu-id="d42fb-142">Proxy Web à utiliser lors de la communication sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="d42fb-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="d42fb-143">NULL si aucune authentification du proxy n’est configurée.</span><span class="sxs-lookup"><span data-stu-id="d42fb-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="d42fb-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="d42fb-144">bool isProxyRequest</span></span> | <span data-ttu-id="d42fb-145">True si cette demande doit obtenir les informations d’identification de l’authentification du proxy.</span><span class="sxs-lookup"><span data-stu-id="d42fb-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="d42fb-146">Si l’implémentation n’est pas valide pour l’acquisition des informations d’identification du proxy, la valeur null doit être retournée.</span><span class="sxs-lookup"><span data-stu-id="d42fb-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="d42fb-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="d42fb-147">bool isRetry</span></span> | <span data-ttu-id="d42fb-148">True si les informations d’identification ont été précédemment demandées pour cet URI, mais que les informations d’identification fournies n’autorisent pas l’accès autorisé.</span><span class="sxs-lookup"><span data-stu-id="d42fb-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="d42fb-149">bool non interactif</span><span class="sxs-lookup"><span data-stu-id="d42fb-149">bool nonInteractive</span></span> | <span data-ttu-id="d42fb-150">Si la valeur est true, le fournisseur d’informations d’identification doit supprimer toutes les invites utilisateur et utiliser les valeurs par défaut à la place.</span><span class="sxs-lookup"><span data-stu-id="d42fb-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="d42fb-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="d42fb-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="d42fb-152">Ce jeton d’annulation doit être vérifié pour déterminer si l’opération qui demande des informations d’identification a été annulée.</span><span class="sxs-lookup"><span data-stu-id="d42fb-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="d42fb-153">**Valeur de retour**: Objet d’informations d’identification implémentant l' [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="d42fb-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
