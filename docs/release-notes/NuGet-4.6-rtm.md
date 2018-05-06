---
title: Notes de publication de NuGet 4.6 RTM
description: Notes de publication de NuGet 4.6.0, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: d8fc374167e5c7f601c41887c4844854d0177ccb
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-46-rtm-release-notes"></a>Notes de publication de NuGet 4.6 RTM

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Résumé : Nouveautés de cette version release
* Nous avons ajouté la prise en charge de la [signature de packages](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package).  
* Visual Studio 2017 et nuget.exe vérifient maintenant l’intégrité des packages avant d’installer et de restaurer des [packages signés](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference).
* Nous avons amélioré les performances des restaurations successives.

## <a name="known-issues"></a>Problèmes connus
### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problèmes liés à .NET Standard 2.0 avec .NET Framework & NuGet 

.NET Standard et ses outils ont été conçus de façon à ce que les projets qui ciblent le .NET Framework 4.6.1 puissent consommer les projets et les packages NuGet ciblant .NET Standard 2.0 ou antérieur. [Ce document](https://github.com/dotnet/standard/issues/481) récapitule les problèmes liés à ce scénario et propose des solutions de contournement que vous pouvez déployer avec les outils actuellement disponibles.

## <a name="top-issues-fixed-in-this-release"></a>Principaux problèmes résolus dans cette version

**Résolution des problèmes de performance**
* Aucun fichier de ressource n’est écrit en l’absence de changements - [#6491](https://github.com/NuGet/Home/issues/6491)
* La restauration provoque des évaluations supplémentaires de MSBuild quand le TFM des projets enfants ne correspond pas à celui du projet parent - [#6311](https://github.com/NuGet/Home/issues/6311)
* Amélioration des performances de la restauration NoOp grâce à l’optimisation de la création de spécifications pour les graphiques de dépendance - [#6252](https://github.com/NuGet/Home/issues/6252)

**Bogues**
* L’envoi (push) au dossier local laisse nupkg verrouillé - [#6325](https://github.com/NuGet/Home/issues/6325)
* Plusieurs problèmes liés à l’implémentation du plug-in NuGet - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang : suppression de l’appel de service de requête à partir de l’initialisation MEF dans VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Erreur de signalement de l’exception pour une tâche de téléchargement de package annulée - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe remplace « + » par « %2 » dans le nom de l’assembly - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 n’ouvre pas la page d’aide adéquate pour l’interface utilisateur et la console PM - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet écrit des chemins absolus dans les fichiers projet dans des circonstances particulières - [#5888](https://github.com/NuGet/Home/issues/5888)
* Régression du correctif 4.3 : les espaces réservés $product$ et $AssemblyGuid$ ne sont pas remplacés dans contentfile par transformation - [#5880](https://github.com/NuGet/Home/issues/5880)
* Blocage de dotnet restore avec plusieurs sources - [#5817](https://github.com/NuGet/Home/issues/5817)
* Le pack doit réévaluer les versions de projet pour permettre la gestion des versions git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Amélioration des erreurs difficiles à comprendre au moment de l’installation d’un package incompatible - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard nécessite une option pour installer des packages en tant que PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Les fichiers props remis par package sont ignorés quand MSBuild.exe est exécuté en dehors d’une invite de commandes développeur - [#4530](https://github.com/NuGet/Home/issues/4530)
* Correction d’un message d’erreur de mauvaise qualité dans le cadre du référencement d’une bibliothèque .NET Standard qui n’est pas applicable au projet - [#4423](https://github.com/NuGet/Home/issues/4423)
* Aide limitée en cas d’échec de dotnet add package pour le profil portable de ciblage de packages- [#4349](https://github.com/NuGet/Home/issues/4349)
* Suffixe de la version du pack dotnet absente de ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Erreurs de build et blocage de VS avec le modèle .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)
* Impossible de charger l’index de service pour la source https :* - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list : allversions ne fonctionne pas - [#3441](https://github.com/NuGet/Home/issues/3441)
* Message d’erreur de résolution de dépendance trompeur - [#2984](https://github.com/NuGet/Home/issues/2984)
* La restauration de nuget.exe ne produit pas les fichiers .props et .targets pour .msbuildproj (régression dans la mise à niveau v3.3.0-3.4.4) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Délai de l’interface utilisateur durant la mise à jour d’un package NuGet avec un fichier XAML ouvert - [#2878](https://github.com/NuGet/Home/issues/2878)
* Échec du projet de site web à partir d’IIS avec des caractères non autorisés dans le chemin - [#2798](https://github.com/NuGet/Home/issues/2798)
* Blocage de nuget add sur CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Échec de la restauration avec packagesavemode -nupkg pour json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Le filtre du Gestionnaire de package n’est pas disponible dans la fenêtre de sortie de VS pour la commande restore[#2704](https://github.com/NuGet/Home/issues/2704)


[Liste de tous les problèmes résolus dans cette version](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
