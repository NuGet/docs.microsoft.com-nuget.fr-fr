---
title: Notes de publication de NuGet 5,8
description: Notes de publication de NuGet 5,8, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 550971d77ed4b15129fdc58fef95e0cceda8d8d1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776170"
---
# <a name="nuget-58-release-notes"></a>Notes de publication de NuGet 5,8

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio | Disponible dans les SDK .NET |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Version 16.8.4 de Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> installé avec Visual Studio 2019 avec une charge de travail .net Core
  
> [!NOTE]
> Visual Studio 16,8, MSBuild 16,8 et .NET 5,0 requièrent NuGet.exe 5,8 ou version ultérieure.


## <a name="summary-whats-new-in-58"></a>Résumé : nouveautés de 5,8
🎉 **il s’agit de la première version pour offrir une prise en charge complète de la création et de la restauration des packages NuGet ciblant .net 5,0** 🎉

* Accélérer l’extraction de nupkg à l’aide de mmap/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807)

* Afficher les détails de la vulnérabilité du package dans le volet Détails du package de l’interface utilisateur du gestionnaire de package- [#9850](https://github.com/NuGet/Home/issues/9850)

* Vérifier les packages NuGet signés avec le nouveau [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) [#8051](https://github.com/NuGet/Home/issues/8051) de commande

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) prend en charge `--prerelease` l’option pour ajouter la version la plus récente d’un package, y compris les versions préliminaires- [#4699](https://github.com/NuGet/Home/issues/4699)

* Rechercher des packages dans l’interface CLI avec la [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) commande- [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) la commande prend en charge l' `--verbosity` option- [#9600](https://github.com/NuGet/Home/issues/9600)

* Activer l’optimisation de la restauration rapide des No-Op pour les projets PackageReference de type csproj dans Visual Studio- [#9565](https://github.com/NuGet/Home/issues/9565)

* Les opérations de l’interface utilisateur du gestionnaire de package au niveau de la solution, telles que les installations de packages et les mises à jour, sont jusqu’à 10 fois plus rapides [#6010](https://github.com/NuGet/Home/issues/6010)

* Plusieurs autres améliorations des performances de NuGet dans Visual Studio : [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984) [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

**DCR**

* .NET 5,0 TFM : règles de précédence de l’infrastructure- [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet ne doit pas déduire la version de plateforme en points lors de l’analyse de TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842)

* Utilisez TargetFrameworkMoniker & TargetPlatformMoniker pour déduire les frameworks au lieu d’utiliser les propriétés individuelles TFI, TFV, TPI, TPV, [#9895](https://github.com/NuGet/Home/issues/9895)

* Mise à jour `GetReferenceNearestTargetFrameworkTask()` pour prendre en charge les frameworks cibles avec des plateformes (telles que .net 5.0-Windows)- [#9894](https://github.com/NuGet/Home/issues/9894)

* API .NET 5,0 Visual Studio- [#9650](https://github.com/NuGet/Home/issues/9650)

* Interface utilisateur du gestionnaire de package : les opérations de consolidation ou de mise à jour des packages ne doivent pas être bloquées en raison d’erreurs (rétrogradation de package, etc.)- [#9224](https://github.com/NuGet/Home/issues/9224)

* Les fonctionnalités NuGet doivent s’allumer pour les projets qui ont la capacité ; « PackageReferences »- [#9957](https://github.com/NuGet/Home/issues/9957)

* Supprimer No-Op restaurer des messages dans Visual Studio- [#6384](https://github.com/NuGet/Home/issues/6384)

**Corrigé**

* Le constructeur OutputWindowTextWriter ne doit pas être appelé sur un thread d’arrière-plan [#9764](https://github.com/NuGet/Home/issues/9764)

* Restaurer les packages signés sur des processeurs Big endian- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger ne doit pas appeler les méthodes affinité dans les constructeurs MEF- [#9591](https://github.com/NuGet/Home/issues/9591)

* Bogue dans NuGet. CommandLine. Console `PrintJustified()` , méthode- [#9737](https://github.com/NuGet/Home/issues/9737)

* Fuite de mémoire de l’interface utilisateur du gestionnaire de package lorsque les métadonnées du package sont récupérées [#9757](https://github.com/NuGet/Home/issues/9757) par le garbage collector en raison d’une liaison erronée

* Fermeture Aucun avertissement n’est affiché dans Liste d’erreurs lors de l’installation d’un package signé avec packages.config format dans l’interface utilisateur du gestionnaire de package- [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat ne doit pas avoir d’API publiques- [#9821](https://github.com/NuGet/Home/issues/9821)

* Réduire la contention des ressources au moment du chargement de la solution provoqué par le blocage d’un thread de pool de threads avec `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* Dans la restauration à partir de la ligne de commande, avec des projets multi-ciblés, NuGet doit lire les informations relatives à l’infrastructure cible à partir de la build interne- [#9869](https://github.com/NuGet/Home/issues/9869)

* Lire le graphique d’identificateur de Runtime via l’élément TargetFrameworkInformation- [#9874](https://github.com/NuGet/Home/issues/9874)

* La restauration de graphiques statiques est incohérente en ce qui concerne la propriété CrossTargeting par rapport à Visual Studio et à la restauration d’évaluation MSBuild régulière- [#9881](https://github.com/NuGet/Home/issues/9881)

* Dans la restauration de graphiques statiques, avec des projets multi-ciblés, NuGet doit lire les informations relatives à l’infrastructure cible à partir de la build interne. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Autoriser `net5.0-platform` le chargement et la restauration des projets dans Visual Studio [#9863](https://github.com/NuGet/Home/issues/9863)

* Afficher la version résolue dans l’interface utilisateur du gestionnaire de package- [#9826](https://github.com/NuGet/Home/issues/9826)

* Interface utilisateur du gestionnaire de package : Explorateur de solutions n’indique pas toutes les dépendances de package NuGet- [#9898](https://github.com/NuGet/Home/issues/9898)

* Mettre à jour la liste de licences SPDX- [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 plante après l’ouverture gérer les packages NuGet : l’icône provoque une exception non gérée dans l’image Conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging. extraction a besoin de ILMerge pour exclure Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* La compression avec ContinuePackingAfterGeneratingNuspec = false ne doit pas échouer en l’absence d’erreurs- [#9786](https://github.com/NuGet/Home/issues/9786)

* Interface utilisateur du gestionnaire de package : les icônes n’inversent pas correctement les couleurs- [#10017](https://github.com/NuGet/Home/issues/10017)

* Nombre de projets incorrects pour les projets No-Op et à jour à la restauration- [#10026](https://github.com/NuGet/Home/issues/10026)

* L’utilisation `/p:RestoreUseStaticGraphEvaluation=true` des résultats dans la valeur ne peut pas être null- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` utilise par erreur l’alias pour les projets de bibliothèque WPF- [#10020](https://github.com/NuGet/Home/issues/10020)

* Interface utilisateur du gestionnaire de package : NullReferenceException lorsque la validation de signature échoue- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces : n’utilisez pas `object` de type pour les valeurs de métadonnées de projet- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces : l’enregistrement des sources de package dans les options outils remplace les informations d’identification- [#9711](https://github.com/NuGet/Home/issues/9711)


**[Liste de tous les problèmes résolus dans cette version-5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Liste des problèmes dans cette version-5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Contributions de la communauté

Merci à tous les contributeurs qui ont aidé à rendre cette version de NuGet extraordinaire !

|Qui|Tirage|Problèmes|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Faute de frappe dans le message d’erreur. « administrateur » au lieu de « Administrator »- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Description du Pack NuGet avec des rapports de AssemblyInformationalVersion non valides»- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` ne prend pas en compte les propriétés Branch et Commit- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Cliquez sur code nu dans Visual Studio liste d’erreurs fenêtre doit accéder à https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Utilisez « https:// » lors de l’ajout d’une nouvelle source de package via les options Visual Studio- [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problème de performances sur mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Ajoutez un TypeConverter pour la classe SemanticVersion- [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Résumé : nouveautés de 5.8.1

* packages.config package.lock.jssur utilise une version cible du .NET Framework incorrecte dans 5,8- [#10257](https://github.com/NuGet/Home/issues/10257)

* 5,8 + 16,8 ne peut pas résoudre les dépendances de projet transitives lors de la combinaison de PackageReference et de packages.config- [#10326](https://github.com/NuGet/Home/issues/10326)

**[Liste de tous les problèmes résolus dans cette version-5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Liste des validations dans cette version-5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Commentaires

Vos commentaires sont très importants pour nous.  En cas de problème avec cette version, consultez nos [problèmes GitHub](https://github.com/NuGet/Home/issues) et la [communauté de développeurs Visual Studio](https://developercommunity.visualstudio.com/) pour les problèmes existants.  Pour les nouveaux problèmes dans NuGet, signalez un [problème GitHub](https://github.com/NuGet/Home/issues/new).
Pour les problèmes généraux d’expérience NuGet, faites-le nous savoir par le biais de l’option [signaler un problème](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) trouvée dans votre IDE favori sous **aide > signaler un problème**.