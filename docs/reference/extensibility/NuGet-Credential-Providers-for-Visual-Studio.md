---
title: Fournisseurs d’informations d’identification NuGet pour Visual Studio
description: Les fournisseurs d’informations d’identification NuGet s’authentifient avec des flux en implémentant l’interface IVsCredentialProvider dans une extension Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859094"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Authentification de flux dans Visual Studio avec des fournisseurs d’informations d’identification NuGet

L’extension Visual Studio NuGet 3.6 + prend en charge les fournisseurs d’informations d’identification, ce qui permet à NuGet de fonctionner avec les flux authentifiés.
Après l’installation d’un fournisseur d’informations d’identification NuGet pour Visual Studio, l’extension NuGet Visual Studio acquière et actualise automatiquement les informations d’identification pour les flux authentifiés si nécessaire.

Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).

Dans Visual Studio, NuGet utilise un interne `VsCredentialProviderImporter` qui recherche également les fournisseurs d’informations d’identification de plug-in. Ces fournisseurs d’informations d’identification de plug-in doivent être détectables comme une exportation MEF de type `IVsCredentialProvider` .

À compter de la section 4.8 + NuGet dans Visual Studio prend également en charge les nouveaux plug-ins d’authentification multiplateforme, mais ce n’est pas l’approche recommandée pour des raisons de performances.

> [!Note]
> Les fournisseurs d’informations d’identification NuGet pour Visual Studio doivent être installés en tant qu’extension Visual Studio standard et nécessitent [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) ou version ultérieure.
>
> Les fournisseurs d’informations d’identification NuGet pour Visual Studio fonctionnent uniquement dans Visual Studio (pas dans dotnet restore ou nuget.exe). Pour les fournisseurs d’informations d’identification avec nuget.exe, consultez [nuget.exe des fournisseurs d’informations d’identification](nuget-exe-Credential-providers.md).
> Pour les fournisseurs d’informations d’identification dans dotnet et MSBuild, consultez [plug-ins inter-plateforme NuGet](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Création d’un fournisseur d’informations d’identification NuGet pour Visual Studio

L’extension Visual Studio NuGet 3.6 + implémente un CredentialService interne qui est utilisé pour obtenir les informations d’identification. Le CredentialService contient une liste de fournisseurs d’informations d’identification intégrés et de plug-in. Chaque fournisseur est essayé séquentiellement jusqu’à ce que les informations d’identification soient acquises.

Lors de l’acquisition des informations d’identification, le service d’informations d’identification essaiera les fournisseurs d’informations d’identification dans l’ordre suivant, en arrêtant dès que les informations d’identification sont acquises :

1. Les informations d’identification sont extraites à partir des fichiers de configuration NuGet (à l’aide de l’intégré `SettingsCredentialProvider` ).
1. Si la source du package se trouve sur Visual Studio Team Services, `VisualStudioAccountProvider` sera utilisé.
1. Tous les autres fournisseurs d’informations d’identification Visual Studio du plug-in seront essayés séquentiellement.
1. Essayez d’utiliser tous les fournisseurs d’informations d’identification inter-plateforme NuGet de manière séquentielle.
1. Si aucune information d’identification n’a encore été acquise, l’utilisateur est invité à fournir des informations d’identification à l’aide d’une boîte de dialogue d’authentification de base standard.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implémentation de IVsCredentialProvider. GetCredentialsAsync

Pour créer un fournisseur d’informations d’identification NuGet pour Visual Studio, créez une extension Visual Studio qui expose une exportation MEF publique qui implémente le `IVsCredentialProvider` type et qui adhère aux principes énoncés ci-dessous.

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

Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).

Chaque fournisseur d’informations d’identification NuGet pour Visual Studio doit :

1. Déterminez si elle peut fournir des informations d’identification pour l’URI ciblé avant de lancer l’acquisition des informations d’identification. Si le fournisseur ne peut pas fournir d’informations d’identification pour la source ciblée, il doit retourner `null` .
1. Si le fournisseur gère les demandes pour l’URI ciblé, mais ne peut pas fournir d’informations d’identification, une exception doit être levée.

Un fournisseur d’informations d’identification NuGet personnalisé pour Visual Studio doit implémenter l' `IVsCredentialProvider` interface disponible dans le [package NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Paramètre d’entrée |Description|
| ----------------|-----------|
| URI de l’URI | URI source du package pour lequel les informations d’identification sont demandées.|
| Proxy IWebProxy | Proxy Web à utiliser lors de la communication sur le réseau. NULL si aucune authentification du proxy n’est configurée. |
| bool isProxyRequest | True si cette demande doit obtenir les informations d’identification de l’authentification du proxy. Si l’implémentation n’est pas valide pour l’acquisition des informations d’identification du proxy, la valeur null doit être retournée. |
| bool isRetry | True si les informations d’identification ont été précédemment demandées pour cet URI, mais que les informations d’identification fournies n’autorisent pas l’accès autorisé. |
| bool non interactif | Si la valeur est true, le fournisseur d’informations d’identification doit supprimer toutes les invites utilisateur et utiliser les valeurs par défaut à la place. |
| CancellationToken cancellationToken | Ce jeton d’annulation doit être vérifié pour déterminer si l’opération qui demande des informations d’identification a été annulée. |

**Valeur de retour**: objet d’informations d’identification implémentant l' [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials).
