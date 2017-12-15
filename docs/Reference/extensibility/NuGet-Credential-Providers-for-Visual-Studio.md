---
title: "Fournisseurs d’informations d’identification de NuGet pour Visual Studio | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "Fournisseurs d’informations d’identification de NuGet auprès de flux en implémentant l’interface IVsCredentialProvider dans une extension Visual Studio."
keywords: "Fournisseurs d’informations d’identification de NuGet, auprès de l’alimentation, auprès de la galerie, extension de visual studio NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>L’authentification des flux avec des fournisseurs d’informations d’identification de NuGet dans Visual Studio

L’Extension NuGet Visual Studio 3.6 et + prend en charge les fournisseurs d’informations d’identification, qui permettent de NuGet travailler avec des flux authentifiés.
Après avoir installé un fournisseur d’informations d’identification de NuGet pour Visual Studio, l’extension NuGet Visual Studio va automatiquement acquérir et actualiser les informations d’identification pour un flux authentifié en tant que nécessaire.

Vous trouverez un exemple d’implémentation dans [l’exemple VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Fournisseurs d’informations d’identification de NuGet pour Visual Studio doit être installés comme une extension de Visual Studio standard et nécessitera [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (actuellement en version préliminaire) ou version ultérieure.
>
> Fournisseurs d’informations d’identification de NuGet pour Visual Studio fonctionnent uniquement dans Visual Studio (et non dans dotnet restauration ou nuget.exe). Pour les fournisseurs d’informations d’identification avec nuget.exe, consultez [nuget.exe fournisseurs d’informations d’identification](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio

Il existe un fournisseur d’informations d’identification intégré de l’extension Visual Studio NuGet pour prendre en charge de Visual Studio Team Services.

L’Extension NuGet Visual Studio utilise interne `VsCredentialProviderImporter` qui analyse également pour les fournisseurs d’informations d’identification du plug-in. Ces fournisseurs d’informations d’identification du plug-in doivent être détectables comme une exportation MEF de type `IVsCredentialProvider`.

Fournisseurs d’informations d’identification du plug-in disponibles sont les suivantes :

- [Fournisseur d’informations d’identification MyGet pour Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Création d’un fournisseur d’informations d’identification de NuGet pour Visual Studio

L’Extension NuGet Visual Studio 3.6 et + implémente un CredentialService interne qui est utilisée pour acquérir des informations d’identification. Le CredentialService a une liste de fournisseurs d’informations d’identification intégrés et plug-in. Chaque fournisseur est testé séquentiellement jusqu'à ce que les informations d’identification sont acquis.

Pendant l’acquisition d’informations d’identification, le service d’informations d’identification va essayer de fournisseurs d’informations d’identification dans l’ordre suivant, l’arrêt dès que les informations d’identification sont acquis :

1. Informations d’identification seront extraites à partir des fichiers de configuration NuGet (à l’aide de la fonction intégrée `SettingsCredentialProvider`).
1. Si la source du package est sur Visual Studio Team Services, le `VisualStudioAccountProvider` sera utilisé.
1. Tous les autres fournisseurs d’informations d’identification du plug-in sont testés séquentiellement.
1. Si aucune information d’identification n’ont été acquis, l’utilisateur sera invité pour les informations d’identification à l’aide d’une boîte de dialogue de l’authentification de base standard.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implémentation de IVsCredentialProvider.GetCredentialsAsync

Pour créer un fournisseur d’informations d’identification de NuGet pour Visual Studio, créez une Extension Visual Studio qui expose une implémentation d’exportation MEF publique le `IVsCredentialProvider` tapez et adhère aux principes décrites ci-dessous.

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

Chaque fournisseur d’informations d’identification de NuGet pour Visual Studio doit :

1. Déterminer si elle peut fournir des informations d’identification pour l’URI cible avant de lancer l’acquisition des informations d’identification. Si le fournisseur ne peut pas fournir les informations d’identification pour la source ciblée, elle doit retourner `null`.
1. Si le fournisseur gère les demandes pour l’URI cible, mais ne peut pas fournir les informations d’identification, une exception doit être levée.

Un fournisseur d’informations d’identification NuGet personnalisé pour Visual Studio doit implémenter la `IVsCredentialProvider` interface disponible dans le [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Paramètre d’entrée |Description|
| ----------------|-----------|
| Uri de l’URI | L’Uri de source de package pour lequel les informations d’identification sont demandées.|
| IWebProxy proxy | Proxy Web à utiliser lors de la communication sur le réseau. Null s’il n’existe aucune authentification proxy configurée. |
| bool isProxyRequest | True si cette demande est pour obtenir des informations d’identification de l’authentification proxy. Si l’implémentation n’est pas valide pour l’acquisition d’informations d’identification de proxy, null doit être retourné. |
| bool isRetry | True si les informations d’identification ont été précédemment demandées pour cet Uri, mais les informations d’identification fournies ne permettait pas autorisé à accéder. |
| bool non interactif | Si la valeur est true, le fournisseur d’informations d’identification doit supprimer toutes les invites utilisateur et utilisez à la place des valeurs par défaut. |
| CancellationToken cancellationToken | Ce jeton d’annulation doit être vérifié pour déterminer si les informations d’identification demande à l’opération a été annulée. |
  
**Valeur de retour**: un objet informations d’identification qui implémente le [ `System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).
