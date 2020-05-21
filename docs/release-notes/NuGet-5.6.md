---
title: Notes de publication de NuGet 5,6
description: Notes de publication de NuGet 5,6, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727820"
---
# <a name="nuget-56-release-notes"></a>Notes de publication de NuGet 5,6

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio| Disponible dans les SDK .NET|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installé avec Visual Studio 2019 avec une charge de travail .NET Core

## <a name="summary-whats-new-in-56"></a>Résumé : nouveautés de 5,6

* Prendre en charge les packages de version préliminaire avec des versions flottantes. `Version="*-*"`, `Version="1.*-*"` et sont similaires aux versions les plus récentes, y compris les versions préliminaires, au sein de la plage spécifiée- [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**Corrigé**

* `nuget push *.nupkg`échoue quand snupkg n’existe pas- [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack, et plusieurs autres chemins de code, ne dépendent pas des paramètres régionaux. Utilisez RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Perf : la spécification DG pour les scénarios de projet non chargés ne doit pas être écrite dans les restaurations de l’aperçu- [#8793](https://github.com/NuGet/Home/issues/8793)

* Restauration : améliorer les performances en mettant en cache la spécification du graphique de dépendances de solution- [#9201](https://github.com/NuGet/Home/issues/9201)

* L’interface utilisateur PM ne fonctionne pas pour les projets de style SDK après l’installation d’un package avec la console PM- [#9203](https://github.com/NuGet/Home/issues/9203)

* L’icône incorporée ne peut pas être affichée dans l’interface utilisateur PM avec un flux de package local-en fonction de/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict () doit retourner false s’il ne parvient pas à analyser- [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`aide pour `-source` , doit suggérer l’utilisation du nom de la source, et non l’URL source- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`crée un nom de source de package par défaut incorrect- [#9277](https://github.com/NuGet/Home/issues/9277)

* Le lecteur d’écran n’annonce pas la « recherche... » message lors du changement d’onglets- [#9307](https://github.com/NuGet/Home/issues/9307)

* Accessibilité : la couleur du rectangle n’est pas accessible dans les onglets de l’interface utilisateur PM dans le thème sombre- [#9336](https://github.com/NuGet/Home/issues/9336)

* échec de la restauration de NuGet. exe 5,5 avec MSBuild 14 ou sous- [#9458](https://github.com/NuGet/Home/issues/9458)

* Ne pas journaliser les durées en millisecondes des messages de restauration- [#8977](https://github.com/NuGet/Home/issues/8977)

* Rendre IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)

* Le choix de la version MSBuild fonctionne mal sur certaines cultures non anglaises- [#9322](https://github.com/NuGet/Home/issues/9322)

* La valeur par défaut du format est manquante sur `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf : RestoreOperationLogger a une affinité de thread inutile- [#9288](https://github.com/NuGet/Home/issues/9288)

* Création automatisée de documents pour les `dotnet nuget` commandes- [#9146](https://github.com/NuGet/Home/issues/9146)

* Le niveau de détail par défaut ne doit pas signaler la restauration NOOP de chaque projet- [#8792](https://github.com/NuGet/Home/issues/8792)

* Paramètre de prise en charge `-DependencyVersion` pour `NuGet.exe update` , similaire à la commande d’installation [#7694](https://github.com/NuGet/Home/issues/7694)


**DCR**

* Ajouter la prise en charge initiale de .net 5.0 Target Framework- [#9584](https://github.com/NuGet/Home/issues/9584)

* Triez les packages par ID sous l’onglet mises à jour de l’interface utilisateur PM- [#9278](https://github.com/NuGet/Home/issues/9278)


**[Liste de tous les problèmes résolus dans cette version-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
