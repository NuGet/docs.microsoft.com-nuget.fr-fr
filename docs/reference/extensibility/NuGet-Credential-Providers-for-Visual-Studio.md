---
title: Fournisseurs d’informations d’identification NuGet pour Visual Studio
description: Fournisseurs d’informations d’identification NuGet s’authentifier avec des flux en implémentant l’interface IVsCredentialProvider dans une extension Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547952"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>L’authentification de flux dans Visual Studio avec les fournisseurs d’informations d’identification NuGet

L’Extension NuGet Visual Studio 3.6 et + prend en charge les fournisseurs d’informations d’identification, qui permettent de NuGet travailler avec les flux authentifiés.
Après avoir installé un fournisseur d’informations d’identification NuGet pour Visual Studio, l’extension NuGet Visual Studio va automatiquement acquérir et actualiser les informations d’identification pour les flux authentifiés en fonction des besoins.

Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

En commençant par 4.8 + NuGet dans Visual Studio prend en charge les nouvelles inter-plateformes authentification plug-ins également, mais ils ne sont pas l’approche recommandée pour des raisons de performances.

> [!Note]
> Fournisseurs d’informations d’identification NuGet pour Visual Studio doit être installés comme une extension de Visual Studio standard et nécessitera [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) ou version ultérieure.
>
> Fournisseurs d’informations d’identification NuGet pour Visual Studio fonctionnent uniquement dans Visual Studio (pas dans la restauration de dotnet ou nuget.exe). Pour les fournisseurs d’informations d’identification avec nuget.exe, consultez [nuget.exe fournisseurs d’informations d’identification](nuget-exe-Credential-providers.md).
> Pour les informations d’identification fournisseurs dans dotnet et msbuild consultez [NuGet entre les plug-ins de la plateforme](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio

Il existe un fournisseur d’informations d’identification intégré à l’extension de Visual Studio NuGet pour prendre en charge de Visual Studio Team Services.

L’Extension NuGet Visual Studio utilise un interne `VsCredentialProviderImporter` qui analyse également pour les fournisseurs de plug-in informations d’identification. Ces fournisseurs d’informations d’identification de plug-in doivent être détectables en tant qu’une exportation MEF de type `IVsCredentialProvider`.

Fournisseurs d’informations d’identification de plug-in disponibles sont les suivantes :

- [Fournisseur d’informations d’identification MyGet pour Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Création d’un fournisseur d’informations d’identification NuGet pour Visual Studio

L’Extension NuGet Visual Studio 3.6 et + implémente un CredentialService interne qui est utilisée pour obtenir des informations d’identification. Le CredentialService a une liste de fournisseurs d’informations d’identification intégrés et plug-in. Chaque fournisseur est testé séquentiellement jusqu'à ce que les informations d’identification sont acquis.

Pendant l’acquisition d’informations d’identification, le service d’informations d’identification va tenter de fournisseurs d’informations d’identification dans l’ordre suivant, l’arrêt dès que les informations d’identification sont acquis :

1. Informations d’identification seront extraites à partir des fichiers de configuration NuGet (à l’aide intégrée `SettingsCredentialProvider`).
1. Si la source du package se trouve sur Visual Studio Team Services, le `VisualStudioAccountProvider` sera utilisé.
1. Tous les autres fournisseurs d’informations d’identification Visual Studio plug-in seront tentées de manière séquentielle.
1. Essayez d’utiliser tous les NuGet entre les fournisseurs d’informations d’identification de plateforme séquentiellement.
1. Si aucune information d’identification n’ont été acquis, l’utilisateur demandera les informations d’identification à l’aide d’une boîte de dialogue de l’authentification de base standard.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implémentation IVsCredentialProvider.GetCredentialsAsync

Pour créer un fournisseur d’informations d’identification NuGet pour Visual Studio, créez une Extension Visual Studio qui expose une publique exportation MEF qui implémente le `IVsCredentialProvider` tapez, adhère aux principes énoncés ci-dessous.

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

Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Chaque fournisseur d’informations d’identification NuGet pour Visual Studio doit :

1. Déterminer si elle peut fournir des informations d’identification pour l’URI cible avant de lancer l’acquisition des informations d’identification. Si le fournisseur ne peut pas fournir les informations d’identification pour la source ciblée, elle doit retourner `null`.
1. Si le fournisseur gère les demandes pour l’URI cible, mais ne peut pas fournir les informations d’identification, une exception doit être levée.

Un fournisseur d’informations d’identification NuGet personnalisé pour Visual Studio doit implémenter le `IVsCredentialProvider` interface disponible dans le [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Paramètre d’entrée |Description|
| ----------------|-----------|
| Uri de l’URI | L’Uri de source de package pour lequel les informations d’identification sont demandées.|
| IWebProxy proxy | Proxy Web à utiliser lors de la communication sur le réseau. Null s’il n’existe aucune authentification de proxy configurée. |
| bool isProxyRequest | True si cette demande est pour obtenir des informations d’identification de l’authentification de proxy. Si l’implémentation n’est pas valide pour l’acquisition des informations d’identification de proxy, null doit être retourné. |
| bool isRetry | True si les informations d’identification ont été précédemment demandées pour cet Uri, mais les informations d’identification fournies ne permettait pas d’accès autorisé. |
| bool non interactive | Si la valeur est true, le fournisseur d’informations d’identification doit supprimer toutes les invites utilisateur et utilisez à la place des valeurs par défaut. |
| CancellationToken cancellationToken | Ce jeton d’annulation doit être vérifié pour déterminer si les informations d’identification demandeur d’opération a été annulée. |

**Valeur de retour**: un objet informations d’identification qui implémente le [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
