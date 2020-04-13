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
# <a name="consuming-packages-from-authenticated-feeds"></a>Consommer des paquets à partir d’aliments authentifiés

En plus de la nuget.org [alimentation publique](https://api.nuget.org/v3/index.json), les clients NuGet ont la possibilité d’interagir avec les flux de fichiers et les flux http privés.


Pour authentifier avec des flux http privés, les 2 approches sont :

* Ajouter les informations d’identification dans le [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Authentifier à l’aide d’un des nombreux modèles d’extéabilité selon le client utilisé.

## <a name="nuget-clients-authentication-extensibility"></a>L’extéabilité de l’authentification des clients de NuGet

Pour les différents clients NuGet, le fournisseur privé d’aliments est lui-même responsable de l’authentification.
Tous les clients de NuGet ont des méthodes d’exténuabilité pour soutenir cela. Il s’agit soit d’une extension Visual Studio ou d’un plugin qui peut communiquer avec NuGet pour récupérer les informations d’identification.

### <a name="visual-studio"></a>Visual Studio

Dans Visual Studio, NuGet expose une interface que les fournisseurs d’aliments peuvent implémenter et fournir à leurs clients. Pour plus de détails, veuillez consulter la documentation sur la [façon de créer un fournisseur d’informations d’identification Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio

Il existe un fournisseur d’informations d’identification intégré à Visual Studio pour prendre en charge Azure DevOps.


Les fournisseurs d’informations d’identification plug-in disponibles comprennent :

* [MyGet Credential Provider pour Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Lorsque `nuget.exe` les informations d’identification doivent être authentiques avec un flux, elles les recherchent de la manière suivante :

1. Recherchez les `NuGet.config` informations d’identification dans les fichiers.
1. Utilisez les fournisseurs d’informations d’identification rechargeables V2
1. Utilisez les fournisseurs d’informations d’identification rechargeableS V1
1. NuGet invite ensuite l’utilisateur pour les informations d’identification sur la ligne de commande.

#### <a name="nugetexe-and-v2-credential-providers"></a>fournisseurs d’informations d’identification nuget.exe et V2

Dans `4.8` la version NuGet a défini un nouveau mécanisme de plugin d’authentification, par la suite appelé fournisseurs d’identification V2.
Pour l’installation et la découverte de ces fournisseurs, se référer à [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>fournisseurs d’informations d’identification nuget.exe et V1

Dans `3.3` la version NuGet introduit la première version de plugins d’authentification.
Pour l’installation et la découverte de ces fournisseurs se réfèrent à [nuget.exe fournisseurs d’informations d’identification](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Fournisseurs d’informations d’identification disponibles pour nuget.exe

* [Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider) Azure DevOps V2 Credential Providers or Azure Artifacts Credential Provider Azure DevOps V2 Credential Providers or Azure Artifacts Credential Provider Azure

Avec Visual Studio 2017 version 15.9 et plus tard, le fournisseur d’informations Azure DevOps est regroupé dans Visual Studio.
Si `nuget.exe` l’on utilise MSBuild à partir de cet outil Visual Studio spécifique, alors le plugin sera découvert automatiquement.

### <a name="dotnetexe"></a>dotnet.exe

Lorsque `dotnet.exe` les informations d’identification doivent être authentiques avec un flux, elles les recherchent de la manière suivante :

1. Recherchez les `NuGet.config` informations d’identification dans les fichiers.
1. Utilisez les fournisseurs d’informations d’identification rechargeables V2

Par `dotnet.exe` défaut n’est pas interactif, vous `--interactive` pourriez donc avoir besoin de passer un drapeau pour obtenir l’outil à bloquer pour l’authentification.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe et fournisseurs d’identification V2

En `2.2.100` version du SDK, NuGet a défini un mécanisme de plugin d’authentification qui fonctionne chez tous les clients.
Pour l’installation et la découverte de ces fournisseurs, se référer à [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Fournisseurs d’informations d’identification disponibles pour dotnet.exe

* [Fournisseur d’informations d’identification Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Lorsque `MSBuild.exe` les informations d’identification doivent être authentiques avec un flux, elles les recherchent de la manière suivante :

1. Rechercher les informations `NuGet.config` d’identification dans les fichiers
1. Utilisez les fournisseurs d’informations d’identification rechargeables V2

Par `MSBuild.exe` défaut n’est pas interactif, `/p:NuGetInteractive=true` de sorte que vous pourriez avoir besoin de définir la propriété pour obtenir l’outil à bloquer pour l’authentification.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Fournisseurs d’informations d’identification MSBuild.exe et V2

Dans Visual Studio 2019 Update 9, NuGet a défini un mécanisme de plugin d’authentification qui fonctionne chez tous les clients.
Pour l’installation et la découverte de ces fournisseurs, se référer à [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Fournisseurs d’informations d’identification disponibles pour MSBuild.exe

* [Fournisseur d’informations d’identification Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Avec Visual Studio 2017 Update 9 et plus tard, le fournisseur d’informations Azure DevOps est regroupé dans Visual Studio. Aucune étape supplémentaire n’est nécessaire.
