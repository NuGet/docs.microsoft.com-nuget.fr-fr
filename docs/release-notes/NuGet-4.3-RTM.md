---
title: Notes de publication de NuGet 4.3 RTM
description: Notes de publication de NuGet 4.4 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496589"
---
# <a name="nuget-43-release-notes"></a>Notes de publication de NuGet 4.3

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.3 RTM, qui ajoute la prise en charge de nouveaux scénarios tels que .NET Standard 2.0/.NET Core 2.0, contient de nombreux correctifs de qualité et améliore les performances. Cette version offre également plusieurs améliorations comme la prise en charge de la Gestion sémantique de version 2.0.0, l’intégration MSBuild des avertissements et erreurs NuGet, et bien plus encore.

## <a name="summary-whats-new-in-430"></a>Résumé: Quoi de neuf en 4.3.0

## <a name="summary-whats-new-in-431"></a>Résumé: Quoi de neuf en 4.3.1

* Correctif de sécurité : Les autorisations sur les fichiers créés à l’intérieur de l’adresse suivante [: les #7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)
* Correctif de sécurité: Les fichiers à l’intérieur des NUPKGs peuvent avoir un chemin relatif au-dessus de l’annuaire NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problèmes connus

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>La restauration NuGet peut dans certains cas traiter des sources de packages désactivées comme étant activées

#### <a name="issue"></a>Problème

Les techniques des lignes de commande de restauration suivantes traitent les sources de packages désactivées comme étant activées. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (concerne le dotnet.exe fourni avec Visual Studio ou la version livrée avec le SDK NetCore 2.0.0)

#### <a name="workaround"></a>Solution de contournement

1. Utilisez Visual Studio (2017 15.3 ou ultérieur) ou NuGet.exe (v4.3.0 ou ultérieur)
1. Supprimez votre source désactivée, puis continuez à utiliser msbuild ou dotnet.exe.
1. Pour votre solution, vous pouvez utiliser « Clear » dans NuGet.config puis définir les sources nécessaires pour cette solution.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Lors de l’utilisation de la Console du Gestionnaire de Package, la touche « Entrée » peut ne pas fonctionner

#### <a name="issue"></a>Problème

Parfois, la touche Entrée ne fonctionne pas dans la Console du Gestionnaire de Package. Si cela se produit, vérifiez l’évolution du correctif et spécifiez les éventuelles informations supplémentaires utiles dans les étapes de reproduction du problème. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solution de contournement

Redémarrez Visual Studio et ouvrez la console de gestion des packages avant d’ouvrir la solution. Vous pouvez aussi tenter de supprimer le `project.lock.json` et de réeffectuer la restauration.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Impossible d’afficher, d’ajouter ou de mettre à jour DotNetCLITools à l’aide du Gestionnaire de package NuGet

#### <a name="issue"></a>Problème

Le Gestionnaire de package NuGet ne s’affiche pas et n’autorise pas l’ajout/mise à jour de DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solution de contournement

Vous devez modifier manuellement DotNetCLIToolReferences dans votre fichier projet.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes

#### <a name="issue"></a>Problème

Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes dans Visual Studio. Cela se produit quand vous utilisez PackageReferences comme format de gestionnaire de package. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solution de contournement

Effectuez une restauration manuelle.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problèmes résolus dans NuGet 4.3 RTM

[Notes de publication de NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md) : répertorie tous les problèmes résolus dans NuGet 4.0 RTM

### <a name="features"></a>Fonctionnalités

- Amélioration des performances de restauration NuGet - Implémentation de NoOp plus intelligent pour les restaurations sur la ligne de commande et VS - [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0 : l’interface de ligne de commande VS/Dotnet doit commencer à utiliser les fonctionnalités existantes de NuGet : dossiers de secours - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0 : Permet aux utilisateurs d’ignorer des avertissements de restauration spécifiques (ou de les promouvoir en erreur) - [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0 : assemblys CLI localisés - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0 : inscription de tous les avertissements/erreurs dans le fichier de ressources (notamment PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Activation de la prise en charge TFM : NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Réduction du nombre de projets NuGet.Core et NuGet.Client (et donc de DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Ajout de la possibilité de marquer des avertissements nuget comme des erreurs - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Bogues

- msbuild /t:pack échoue avec l’erreur Le paramètre « DevelopmentDependency » n’est pas pris en charge par la tâche « PackTask » - [#5584](https://github.com/NuGet/Home/issues/5584)

- La structure de répertoires des fichiers de contenu est aplatie si vous n’ajoutez pas de séparateur de répertoire Windows à la fin de PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)

- Les projets netcore ne prennent pas en charge le paramétrage en tant que developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage chargé de façon synchrone, ce qui bloquait le thread d’interface utilisateur et provoquait un interblocage de VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore restore (et par conséquent msbuild /t:restore) ignore les projets avec une dépendance de projet de solution explicite [#4578](https://github.com/NuGet/Home/issues/4578)

- Si votre solution a des références de projet qui référencent le même projet avec une casse différente, la restauration risque de ne pas fonctionner. Cela affecte également les chemins relatifs différents sans différence de casse - [#4574](https://github.com/NuGet/Home/issues/4574)

- Les fichiers exécutables restaurés à partir de packages NuGet ne sont plus exécutables avec .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe avale les détails d’exception lors de l’analyse du fichier de solution - [#4411](https://github.com/NuGet/Home/issues/4411)

- Le pack place les fichiers de contenu à un emplacement incorrect si ContentTargetFolders contient un chemin qui se termine par « / » sur Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

- Impossible de restaurer un DotNetCliToolReference pour un package d’outils qui cible netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

- L’interface de ligne de commande de mise à jour de NuGet laisse l’ancienne condition de version de package dans le fichier de projet (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- Lecture de DotnetCliToolTargetFramework à partir de la nomination CPS - [#5397](https://github.com/NuGet/Home/issues/5397)

- La vérification TPMinV doit fonctionner pour les applications UWP de style pj - [#4763](https://github.com/NuGet/Home/issues/4763)

- Amélioration de la description de l’interface utilisateur pour les packages AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet restore sélectionne des ressources de compilation à partir de la section de runtime. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Placement des diagnostics de dépendances dans le fichier de verrouillage - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Liens vers les problèmes GitHub corrigés dans RTM 4.3

[Liste des questions](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
