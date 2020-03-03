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
# <a name="consuming-packages-from-authenticated-feeds"></a>Utilisation de packages à partir de flux authentifiés

En plus du [flux public](https://api.nuget.org/v3/index.json)NuGet.org, les clients NuGet ont la possibilité d’interagir avec les flux de fichiers et les flux http privés.


Pour s’authentifier avec des flux http privés, les deux approches sont les suivantes :

* Ajouter des informations d’identification dans [NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)
* Authentifiez-vous à l’aide de l’un des nombreux modèles d’extensibilité en fonction du client utilisé.

## <a name="nuget-clients-authentication-extensibility"></a>Extensibilité des authentifications des clients NuGet

Pour les différents clients NuGet, le fournisseur de flux privé lui-même est responsable de l’authentification.
Tous les clients NuGet ont des méthodes d’extensibilité pour prendre en charge cette méthode. Il s’agit soit d’une extension de Visual Studio, soit d’un plug-in capable de communiquer avec NuGet pour récupérer les informations d’identification.

### <a name="visual-studio"></a>Visual Studio

Dans Visual Studio, NuGet expose une interface que les fournisseurs de flux peuvent implémenter et fournir à leurs clients. Pour plus d’informations, consultez la documentation sur la [création d’un fournisseur d’informations d’identification Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Fournisseurs d’informations d’identification NuGet disponibles pour Visual Studio

Un fournisseur d’informations d’identification est intégré à Visual Studio pour prendre en charge Azure DevOps.


Les fournisseurs d’informations d’identification de plug-in disponibles sont les suivants :

* [Fournisseur d’informations d’identification MyGet pour Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Lorsque `nuget.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il les recherche de la manière suivante :

1. Recherchez les informations d’identification dans `NuGet.config` fichiers.
1. Utiliser des fournisseurs d’informations d’identification de plug-in v2
1. Utiliser des fournisseurs d’informations d’identification de plug-in v1
1. NuGet invite ensuite l’utilisateur à fournir des informations d’identification sur la ligne de commande.

#### <a name="nugetexe-and-v2-credential-providers"></a>fournisseurs d’informations d’identification NuGet. exe et v2

Dans la version `4.8` NuGet définissait un nouveau mécanisme de plug-in d’authentification, ci-après appelés fournisseurs d’informations d’identification v2.
Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [plug-ins NuGet inter-plateformes](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>fournisseurs d’informations d’identification NuGet. exe et v1

Dans la version `3.3` NuGet a introduit la première version des plug-ins d’authentification.
Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [fournisseurs d’informations d’identification NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Fournisseurs d’informations d’identification disponibles pour NuGet. exe

* [Fournisseurs d’informations d’identification Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou [Azure artifacts fournisseur d’informations d’identification](https://github.com/microsoft/artifacts-credprovider)

Avec Visual Studio 2017 version 15,9 et versions ultérieures, le fournisseur d’informations d’identification Azure DevOps est regroupé dans Visual Studio.
Si `nuget.exe` utilise MSBuild à partir de cet ensemble d’outils Visual Studio spécifique, le plug-in est découvert automatiquement.

### <a name="dotnetexe"></a>dotnet.exe

Lorsque `dotnet.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il les recherche de la manière suivante :

1. Recherchez les informations d’identification dans `NuGet.config` fichiers.
1. Utiliser des fournisseurs d’informations d’identification de plug-in v2

Par défaut `dotnet.exe` n’est pas interactif, vous devrez peut-être passer un indicateur `--interactive` pour que l’outil soit bloqué pour l’authentification.

#### <a name="dotnetexe-and-v2-credential-providers"></a>fournisseurs d’informations d’identification dotnet. exe et v2

Dans `2.2.100` de version du kit de développement logiciel (SDK), NuGet a défini un mécanisme de plug-in d’authentification qui fonctionne sur tous les clients.
Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [plug-ins NuGet inter-plateformes](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Fournisseurs d’informations d’identification disponibles pour dotnet. exe

* [Fournisseur d’informations d’identification Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild. exe

Lorsque `MSBuild.exe` a besoin d’informations d’identification pour s’authentifier avec un flux, il les recherche de la manière suivante :

1. Rechercher les informations d’identification dans les fichiers `NuGet.config`
1. Utiliser des fournisseurs d’informations d’identification de plug-in v2

Par défaut `MSBuild.exe` n’est pas interactif, vous devrez peut-être définir la propriété `/p:NuGetInteractive=true` pour que l’outil soit bloqué pour l’authentification.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Fournisseurs d’informations d’identification MSBuild. exe et v2

Dans Visual Studio 2019 Update 9, NuGet a défini un mécanisme de plug-in d’authentification qui fonctionne sur tous les clients.
Pour l’installation et la découverte de ces fournisseurs, reportez-vous aux [plug-ins NuGet inter-plateformes](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Fournisseurs d’informations d’identification disponibles pour MSBuild. exe

* [Fournisseur d’informations d’identification Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Avec Visual Studio 2017 Update 9 et versions ultérieures, le fournisseur d’informations d’identification Azure DevOps est regroupé dans Visual Studio. Aucune étape supplémentaire n’est requise.
