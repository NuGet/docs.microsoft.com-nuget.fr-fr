---
title: Notes de publication de NuGet 5,10
description: Notes de publication de NuGet 5,10, y compris les nouvelles fonctionnalités, les correctifs de bogues et DCR.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356538"
---
# <a name="nuget-510-release-notes"></a>Notes de publication de NuGet 5,10

Véhicules de distribution NuGet :

| Version de NuGet | Disponible dans la version Visual Studio | Disponible dans les SDK .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16,10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installé avec Visual Studio 2019 avec une charge de travail .net Core
  
> [!NOTE]
> Visual Studio 16,10, MSBuild 16,10 et .NET 5.0.300 + requièrent NuGet.exe 5,10 ou version ultérieure.

## <a name="summary-whats-new-in-510"></a>Résumé : nouveautés de 5,10

* Signature : implémentation de la commande des signataires approuvés dotnet- [#8053](https://github.com/NuGet/Home/issues/8053)

* Désactivation de la validation par défaut sur Linux, mais activée par défaut sur Windows- [#10713](https://github.com/NuGet/Home/issues/10713)

* Ajouter une variable ENV pour la vérification de la signature du package sur .NET 5 + Linux/MAC- [#10742](https://github.com/NuGet/Home/issues/10742)

* Améliorer les performances de l’installation de nouveaux packages pour les solutions de grande taille- [#10166](https://github.com/NuGet/Home/issues/10166)

* Ajoutez le type de projet `nfproj` à la liste de supportedProjectExtensions pour l’interface CLI NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problèmes résolus dans cette version

* Supprimer l' <requireLicenseAcceptance> élément lors de l’empaquetage d’un projet- [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] l’avertissement de préversion doit s’afficher dans dotnet CLI- [#10226](https://github.com/NuGet/Home/issues/10226)

* Mettez à jour les jetons de couleur d’arrière-plan et de premier plan de PMUI sur CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608)

* [Coccinelle des bogues] Erreur « opération annulée par l’utilisateur » afficher dans la fenêtre de Liste d’erreurs lors du basculement rapide entre les onglets dans l’interface utilisateur PM- [#10671](https://github.com/NuGet/Home/issues/10671)

* Interface utilisateur PM : améliorer les performances d’installation des packages au niveau de la solution- [#10210](https://github.com/NuGet/Home/issues/10210)

* Remplacez GetService par GetServiceAsync Everywhere dans NuGet. clients- [#3784](https://github.com/NuGet/Home/issues/3784)

* Problème de performances de NuGet.exe Pack avec `..` chemin d’accès relatif- [#5016](https://github.com/NuGet/Home/issues/5016)

* Les performances de « Pack NuGet » diminuent avec des niveaux plus élevés dans les chemins source- [#5706](https://github.com/NuGet/Home/issues/5706)

* NuGet n’est pas une erreur lors de l’empaquetage de NuSpec avec des fichiers dupliqués. - [#6941](https://github.com/NuGet/Home/issues/6941)

* Pack NuGet « le DateTimeOffset spécifié ne peut pas être converti en horodatage de fichier zip »- [#7001](https://github.com/NuGet/Home/issues/7001)

* Les horodateurs du fichier de package compressé sont déplacés par le fuseau horaire- [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 doit contenir plus d’informations actionnables- [#7696](https://github.com/NuGet/Home/issues/7696)

* [Coccinelle des bogues] [Échec du test] Le fichier de verrouillage vide/incorrect ne doit pas être mis à jour lors de l’exécution de’dotnet restore--use-Lock-file--Locked-Mode'- [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange permet l’analyse de plages logiquement incorrectes- [#9145](https://github.com/NuGet/Home/issues/9145)

* L’interface utilisateur PM ne peut pas afficher la couleur d’arrière-plan différenciable entre les sources de package sélectionnées et survolées- [#9538](https://github.com/NuGet/Home/issues/9538)

* La case à cocher permettant de sélectionner les projets à installer n’est pas lue par le lecteur d’écran- [#9578](https://github.com/NuGet/Home/issues/9578)

* La sélection par défaut de la liste déroulante des versions du volet d’informations doit être installée/LatestStable sur les onglets installés/mises à jour- [#9887](https://github.com/NuGet/Home/issues/9887)

* Supprimer le compte de solution pour certains kits de développement logiciel (SDK) .net 5 TargetPlatformMoniker de ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet NuGet Verify est trop calme [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange ne peut pas analyser les plages à un chiffre- [#10342](https://github.com/NuGet/Home/issues/10342)

* VS solution Manager lève une exception null pour le débogage- [#10352](https://github.com/NuGet/Home/issues/10352)

* Déplacer les messages d’exception CLI vers des fichiers de ressources de chaîne- [#10392](https://github.com/NuGet/Home/issues/10392)

* Supprimer le code mort (TabItemButtonAutomationPeer)- [#10435](https://github.com/NuGet/Home/issues/10435)

* Le menu contextuel de mise à jour doit défiler jusqu’au premier élément sélectionné- [#10498](https://github.com/NuGet/Home/issues/10498)

* Les détails de la solution PMUI ont un chevauchement de barres horizontales [#10533](https://github.com/NuGet/Home/issues/10533)

* Signature : les détails de la signature principale ne sont pas affichés lorsque le certificat a expiré et l’horodateur non fiable- [#10535](https://github.com/NuGet/Home/issues/10535)

* L’absence d’une source activée empêche l’interface utilisateur PM d’apparaître- [#10541](https://github.com/NuGet/Home/issues/10541)

* Les métadonnées du package (détails, dépréciation) ne sont parfois pas extraites de nuget.org dans CodeSpaces- [#10549](https://github.com/NuGet/Home/issues/10549)

* L’initialisation de PMUI échoue avec une exception pendant la session de débogage [#10559](https://github.com/NuGet/Home/issues/10559)

* la restauration NuGet entraîne l’échec de la vérification de l’intégrité du package sur le système Big endian- [#10567](https://github.com/NuGet/Home/issues/10567)

* FormatException est levée à la place de PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM-problèmes d’accès concurrentiel dans l’algorithme de parcours du graphique- [#10598](https://github.com/NuGet/Home/issues/10598)

* Ajouter des données de télémétrie de la version PowerShell de PMC- [#10609](https://github.com/NuGet/Home/issues/10609)

* Améliorer les performances de tri NuGetVersion- [#10611](https://github.com/NuGet/Home/issues/10611)

* L’ajout de signataires approuvés a des arguments incohérents- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0 : le basculement des onglets dans le gestionnaire de package NuGet de « mises à jour » vers « installé » ne met pas à jour le frame. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Supprimer le « v » du numéro de version dans PMUI- [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService. GetInstalledPackagesAsync lève une exception avant de recevoir la désignation du système de projet CPS- [#10681](https://github.com/NuGet/Home/issues/10681)

* Les icônes incorporées entraînent l’accès refusé à la source « Microsoft Visual Studio les packages hors connexion » dans l’onglet Parcourir- [#10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService. GetInstalledPackagesAsync lève une exception lorsque MSBuildProjectExtensionsPath n’est pas défini- [#10739](https://github.com/NuGet/Home/issues/10739)

* « dotnet NuGet Remove source nuget.org » ne fonctionne pas la première fois- [#10745](https://github.com/NuGet/Home/issues/10745)

* NuGet bloque un thread ThreadPool dans une méthode Async en effectuant un appel synchrone au thread d’interface utilisateur [#10775](https://github.com/NuGet/Home/issues/10775)

* Outils-options de >-> chaîne du gestionnaire de package NuGet est tronquée- [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` est du code mort et nuit aux performances [#10790](https://github.com/NuGet/Home/issues/10790)

* Utiliser l’icône incorporée dans les packages du SDK NuGet- [#10795](https://github.com/NuGet/Home/issues/10795)

* Mettre à jour la liste de licences SPDX- [#10806](https://github.com/NuGet/Home/issues/10806)

**[Liste de tous les problèmes résolus dans cette version-5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Liste des validations dans cette version-5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Contributions de la communauté

Merci à tous les contributeurs qui ont aidé à rendre cette version de NuGet extraordinaire !

|Qui|Tirage|Problèmes|
|----|----|----|
[Louis-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange ne peut pas analyser les plages à un chiffre- [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. client build.sh est rompu [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. client build.sh est rompu [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Les performances de « Pack NuGet » diminuent avec des niveaux plus élevés dans les chemins source- [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Problème de performances de NuGet.exe Pack avec.. chemin d’accès relatif- [#5016](https://github.com/NuGet/Home/issues/5016)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM-problèmes d’accès concurrentiel dans l’algorithme de parcours du graphique- [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Ajoutez le type de projet nfproj à la liste des supportedProjectExtensions pour l’interface CLI NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Commentaires

Vos commentaires sont très importants pour nous.  En cas de problème avec cette version, consultez nos [problèmes GitHub](https://github.com/NuGet/Home/issues) et la [communauté de développeurs Visual Studio](https://developercommunity.visualstudio.com/) pour les problèmes existants.  Pour les nouveaux problèmes dans NuGet, signalez un [problème GitHub](https://github.com/NuGet/Home/issues/new).
Pour les problèmes généraux d’expérience NuGet, faites-le nous savoir par le biais de l’option [signaler un problème](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) trouvée dans votre IDE favori sous **aide > signaler un problème**.
