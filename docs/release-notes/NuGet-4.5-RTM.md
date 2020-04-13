---
title: Notes de publication de NuGet 4.5 RTM
description: Notes de publication pour NuGet 4.5 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496583"
---
# <a name="nuget-45-release-notes"></a>Notes de publication de NuGet 4.5

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="summary-whats-new-in-450"></a>Résumé: Quoi de neuf en 4.5.0

## <a name="summary-whats-new-in-452"></a>Résumé: Quoi de neuf en 4.5.2

* Correctif de sécurité : Les autorisations sur les fichiers créés à l’intérieur de l’adresse suivante [: les #7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-453"></a>Résumé: Quoi de neuf en 4.5.3

* Correctif de sécurité: Les fichiers à l’intérieur des NUPKGs peuvent avoir un chemin relatif au-dessus de l’annuaire NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problèmes connus

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problèmes liés à .NET Standard 2.0 avec .NET Framework & NuGet 

.NET Standard et ses outils ont été conçus de façon à ce que les projets qui ciblent le .NET Framework 4.6.1 puissent consommer les projets et les packages NuGet ciblant .NET Standard 2.0 ou antérieur. [Ce document](https://github.com/dotnet/standard/issues/481) récapitule les problèmes liés à ce scénario et propose des solutions de contournement que vous pouvez déployer avec les outils actuellement disponibles.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Un package dans un projet .NET Core qui contient un assembly avec une signature non valide peut déclencher une boucle de restauration infinie

#### <a name="issue"></a>Problème

De temps en temps, lorsque vous utilisez un paquet qui contient un assemblage avec une signature invalide ou lorsque la version du paquet est définie avec 'DateTime' ticker, il provoque le paquet auto-restauration pour fonctionner dans un dotnet boucle infinie [/ projet-système 1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Solution de contournement

Il n’existe aucune solution de contournement pour l’instant.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problèmes résolus dans NuGet 4.5 RTM

Pour plus d’informations sur les problèmes résolus dans NuGet 4.4 RTM, consultez les [Notes de publication de NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md). 

### <a name="features"></a>Fonctionnalités

- Désactiver l’envoi (push) automatique du package de symboles - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Bogues

- [Régression] dans 15.5p1 : Portable0.0 est ignoré - [#6105](https://github.com/NuGet/Home/issues/6105)
- Les ressources des packages sont manquantes après restauration - [#5995](https://github.com/NuGet/Home/issues/5995)
- Les fournisseurs d’informations d’identification de plug-in ne fonctionnent pas avec les URI contenant des espaces - [#5982](https://github.com/NuGet/Home/issues/5982)
- Si la restauration de package a échoué, l’erreur devrait s’imprimer en sortie, même si le niveau de détail minimal est activé - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - dotnetcore restore au niveau de la solution ne suit pas ProjectReference avec ReferenceOutputAssembly false provoquant des échecs de génération aléatoires - [#5490](https://github.com/NuGet/Home/issues/5490)
- La saisie semi-automatique dans PMC fonctionne correctement avec les méthodes d’objet - [#4800](https://github.com/NuGet/Home/issues/4800)
- La restauration de nuget.exe échoue avec l’ensemble d’outils de Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)
- Performances - l’instanciation de pmc est coûteuse dans vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Lenteur d’obtention des informations de dépendances en cas de lenteur de la connexion - [#4089](https://github.com/NuGet/Home/issues/4089)
- uninstall-package w/ -RemoveDependencies échoue si plusieurs packages partagent une dépendance commune - [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalisation de NuGet.Core.nupkg pour la publication - [#3581](https://github.com/NuGet/Home/issues/3581)
- Le pack NuGet résout un ID de dépendance à partir du nom de répertoire quand -IncludeProjectReferences est utilisé pour csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- L’initialiseur de type pour « NuGet.ProxyCache » a levé une exception - [#3144](https://github.com/NuGet/Home/issues/3144)
- Problème de performances de nuget restore avec kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- L’interface utilisateur du client n’affiche ni erreur ni avertissement quand la recherche est en avance par rapport aux objets blob d’inscription - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -Updates génère une requête incorrecte - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Liens vers les problèmes GitHub corrigés dans RTM 4.5

[Liste des problèmes](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
