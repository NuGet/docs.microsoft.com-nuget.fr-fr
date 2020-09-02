---
title: Notes de publication de NuGet 5,7
description: Notes de publication de NuGet 5,7, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364167"
---
# <a name="nuget-57-release-notes"></a>Notes de publication de NuGet 5,7

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio | Disponible dans les SDK .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> installé avec Visual Studio 2019 avec une charge de travail .net Core

## <a name="summary-whats-new-in-57"></a>Résumé : nouveautés de 5,7

### <a name="features-added-in-this-release"></a>Fonctionnalités ajoutées dans cette version

* Ajout de la prise en charge des alias extern pour les références de package NuGet- [#4989](https://github.com/NuGet/Home/issues/4989)

* Le basculement entre les onglets installé et mis à jour est plus rapide en leur permettant de partager une source de données et de réduire la [#8294](https://github.com/NuGet/Home/issues/8294) de resfreshing

* Rendre la restauration plus rapide-accélérer les évaluations en appelant les API Graph statiques MSBuild (dotnet.exe)- [#9644](https://github.com/NuGet/Home/issues/9644)

* Ajout de la restauration partielle de Visual Studio pour les projets PackageReference (no-op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* L’interface utilisateur du gestionnaire de package Visual Studio se bloque moins souvent lors de la recherche de sources de package incorrectes qui retournent plus que le nombre demandé de résultats par requête HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Ajout de l’intégration des informations de PackageVersion pour les projets de style non-SDK dans VS Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Ajout de la prise en charge de nuget.exe mise à jour `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Ajout de la prise en charge de plusieurs fichiers de configuration dans le répertoire%APPDATA%\NuGet- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths prend désormais en compte les packages source NuGet [#9431](https://github.com/NuGet/Home/issues/9431)

* Ajout de l’API d’extensibilité INuGetProjectService. GetInstalledPackagesAsync- [#9702](https://github.com/NuGet/Home/issues/9702)

* Ajout de l’API d’interopérabilité pour énumérer les dossiers de secours sans nécessiter de [#9395](https://github.com/NuGet/Home/issues/9395) de solution/projet

* Ajout `latest` de l’option pour `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Corrigé**

* Dans une restauration dotnet CLI, lors du lancement des plug-ins d’informations d’identification, essayez l’interface CLI dotnet sur le chemin d’accès système si la `DOTNET_HOST_PATH`  variable d’environnement n’est pas définie. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spécification génère une balise de Copyright avec un texte codé en dur de Copyright yyyy au lieu de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe lève une exception’authors required’pendant que le pack d’un csproj ignore les espaces réservés et les attributs AssemblyInfo si le nom de l’assembly est modifié- [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage est réutilisé plusieurs fois, ce qui n’est pas pris en charge avec SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. Indexing 5.6.0 Preview 3 et versions ultérieures utilisent un jeton de clé publique différent- [#9481](https://github.com/NuGet/Home/issues/9481)

* Honorer TreatWarningsAsErrors pendant la création du package NuGet- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Mise à niveau des packages paraparasites pour plusieurs projets P2P- [#9549](https://github.com/NuGet/Home/issues/9549)

* L’onglet « Parcourir » n’est pas aligné à gauche avec la zone de recherche- [#9559](https://github.com/NuGet/Home/issues/9559)

* La version installée n’est pas cohérente avec l’icône incorporée dans l’interface utilisateur PM au niveau de la solution pour un ID de package avec plusieurs versions installées- [#9321](https://github.com/NuGet/Home/issues/9321)

* Fuite : PartCreationPolicy (CreationPolicy. non Shared) NuGet. SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Évitez de lire le fichier de ressources en cours de restauration sans opération- [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. Protocol ne prend pas en charge l’obtention du nombre de téléchargements d’une version à partir de Search- [#9086](https://github.com/NuGet/Home/issues/9086)

* Améliorez les performances de la mémoire de PackageMetadataResourceV3 en réduisant les dépendances JObject- [#9719](https://github.com/NuGet/Home/issues/9719)

**Concevoir des demandes de modification :**

* Suppression de l' `<owners>` élément lorsqu’il est redondant- [#5134](https://github.com/NuGet/Home/issues/5134)

* Consigner les IntervalTrackers en tant qu’événements ETW- [#9593](https://github.com/NuGet/Home/issues/9593)

* Ajout d’un message d’information sur la restauration pour informer les utilisateurs CPVM que la fonctionnalité est en version préliminaire- [#9340](https://github.com/NuGet/Home/issues/9340)

* Remplir Explorateur de solutions dépendances transitives de package/projet à partir du fichier de ressources- [#9580](https://github.com/NuGet/Home/issues/9580)

* L’onglet packages installés ne doit pas paginer la liste des packages- [#6995](https://github.com/NuGet/Home/issues/6995)

**[Liste de tous les problèmes résolus dans cette version-5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Contributions de la communauté

Merci à tous les contributeurs qui ont aidé à rendre cette version de NuGet extraordinaire !

|Qui|Tirage|Problèmes|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. Protocol ne prend pas en charge l’obtention du nombre de téléchargements d’une version à partir de Search- [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage est réutilisé plusieurs fois, ce qui n’est pas pris en charge avec SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Suppression de l' `<owners>` élément lorsqu’il est redondant- [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet ne peut pas restaurer à partir de sources HTTPs qui requièrent des certificats clients- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Ce que Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim à la prochaine épreuve- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spécification génère une balise de Copyright avec un texte codé en dur de Copyright yyyy au lieu de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (Olivier-Spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Dans une restauration dotnet CLI, lors du lancement des plug-ins d’informations d’identification, essayez l’interface CLI dotnet sur le chemin d’accès système si la `DOTNET_HOST_PATH`  variable d’environnement n’est pas définie. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Ajout `latest` de l’option pour `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
