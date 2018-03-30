---
title: Notes de publication de NuGet 4.4 RTM | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notes de publication de NuGet 4.4 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
keywords: notes de publication de NuGet 4.4 RTM, correctifs de bogues, problèmes connus, fonctionnalités ajoutées, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6c122dc3d9b576a2ea5f094746a830e5fab5637e
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-44-rtm-release-notes"></a>Notes de publication de NuGet 4.4 RTM

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.4 RTM.

## <a name="known-issues"></a>Problèmes connus

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problèmes liés à .NET Standard 2.0 avec .NET Framework & NuGet 

.NET Standard et ses outils ont été conçus de façon à ce que les projets qui ciblent le .NET Framework 4.6.1 puissent consommer les projets et les packages NuGet ciblant .NET Standard 2.0 ou antérieur. [Ce document](https://github.com/dotnet/standard/issues/481) récapitule les problèmes liés à ce scénario et propose des solutions de contournement que vous pouvez déployer avec les outils actuellement disponibles.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Un package dans un projet .NET Core qui contient un assembly avec une signature non valide peut déclencher une boucle de restauration infinie

#### <a name="issue"></a>Problème

Parfois, quand vous utilisez un package qui contient un assembly avec une signature non valide ou quand la version du package est définie avec le symbole « DateTime », la restauration automatique du package s’exécute dans une boucle infinie (dotnet/project-system#1457).

#### <a name="workaround"></a>Solution de contournement

Il n’existe aucune solution de contournement pour l’instant.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problèmes résolus dans NuGet 4.4 RTM

[Notes de publication de NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) : répertorie tous les problèmes résolus dans NuGet 4.3 RTM

### <a name="features"></a>Fonctionnalités

- Prise en charge du chargement de solution allégé dans les scénarios d’interface utilisateur de Gestionnaire de package NuGet et PMC - [#5180](https://github.com/NuGet/Home/issues/5180)

- La cible de pack msbuild doit avoir un raccordement public pour l’exécution des cibles utilisateur avant elle-même - [#5143](https://github.com/NuGet/Home/issues/5143)

- Fonctionnalité : Ajout du commutateur dependencyVersion à nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 doit mapper à .NET Standard 2.0 pour NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Prise en charge du SKU Visual Studio Build Tools avec msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Pendant la restauration, générer une erreur si la prise en charge de .NET 4.6.1 pour .NET 2.0 Standard est nécessaire mais pas installée - [#5325](https://github.com/NuGet/Home/issues/5325)

- Interface utilisateur de client de réservation de préfixe d’ID de package - [#5572](https://github.com/NuGet/Home/issues/5572)

- Remise de composants nuget localisés pour prendre en charge la localisation de dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Bogues

- Différentes casses de chemin de projet peuvent entraîner la perte de PackageReferences par la restauration - [#5855](https://github.com/NuGet/Home/issues/5855)

- Déplacement des codes d’erreur avec numéros d’avertissement vers la plage d’erreurs - [#5824](https://github.com/NuGet/Home/issues/5824)

- Erreur trompeuse quand la version de .NET Standard n’est pas connue pour être compatible avec le framework cible - [#5818](https://github.com/NuGet/Home/issues/5818)

- Fichiers texte avec licences prêtant à confusion - [#5776](https://github.com/NuGet/Home/issues/5776)

- En-têtes de licence manquants dans les modèles tests EndToEnd - [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config restore affiche les erreurs comme NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe install doit avoir DisableParallelProcessing sur mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe install désactive incorrectement la mise en cache - [#5737](https://github.com/NuGet/Home/issues/5737)

- Visual Studio : l’exécution de la commande restore pour packages.config quand la restauration est désactivée provoque l’affichage d’un message incorrect - [#5718](https://github.com/NuGet/Home/issues/5718)

- Visual Studio : l’exécution de la commande restore quand la restauration est désactivée provoque l’affichage d’un message prêtant à confusion : [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask échoue quand les métadonnées de version sont manquantes - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet add package peut effacer les lignes vides d’un csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Les noms de sources des paramètres d’informations d’identification dans NuGet.Config respectent la casse - [#5695](https://github.com/NuGet/Home/issues/5695)

- L’activation de GeneratePackageOnBuild a supprimé tout mon historique des packages - [#5676](https://github.com/NuGet/Home/issues/5676)

- Restauration ne restaure pas les packages mono.cecil ou semver, mais tous les autres packages sont restaurés. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Erreurs et avertissements - erreur incorrecte quand une source n’est pas disponible.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [Cohérence de conception] Le texte d’état d’installation de NuGet ne semble pas correct actuellement sur le thème sombre. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Mise à jour des packages lors des mises à jour/installations de solution pour tous les projets - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet pack se comporte différemment pour TargetFramework et TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Les DLL incluses dans le dossier Tools génèrent des avertissements - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel consomme trop de mémoire pour les opérations de chaîne - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux retourne la valeur true pour OSX - [#4648](https://github.com/NuGet/Home/issues/4648)

- « dotnet pack » place nuspec sous obj au lieu d’obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- NuGet : mise à niveau de package extrêmement lente - [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS non synchronisé avec la restauration avec les solutions plus grandes pour lesquelles la restauration de solution allégée (LSL) n’est pas activée - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pack avec version fournie ignore les métadonnées (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Le package d’installation NuGet.exe (3 +) avec numéro de version et indicateur ExcludeVersion n’effectue pas la mise à jour du package vers une version plus récente [#2405](https://github.com/NuGet/Home/issues/2405)

- La restauration Project.json doit émettre un avertissement quand des packages de niveau supérieur enfreignent des contraintes - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile ne définit pas la configuration personnalisée sur la commande install - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe install n’honore pas le commutateur « -DisableParallelProcessing » - [#1556](https://github.com/NuGet/Home/issues/1556)

- Sources désactivées encore utilisées par DotNet.exe ou msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Corriger les blocages dans un scénario LSL - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCR

- Prise en charge du framework cible avec nuget.exe install - [#5736](https://github.com/NuGet/Home/issues/5736)

- Ajout de différentes chaînes UserAgent de tâche msbuild (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName doit être virtuel - [#5700](https://github.com/NuGet/Home/issues/5700)

- [Cohérence de conception] Message prêtant à confusion lors de l’ajout d’un package NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Avertissements et erreurs] NoWarn n’est pas transmis de manière transitive à travers les références P2P - [#5501](https://github.com/NuGet/Home/issues/5501)

- Chargement de solution allégé : noyau commun pour l’interface utilisateur du Gestionnaire de package, PMC et les IV - [#5057](https://github.com/NuGet/Home/issues/5057)

- Chargement de solution allégé : Prise en charge - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Ajouter la prise en charge de la cible MSBuild de pré-restauration déclenchée par Visual Studio - [#4781](https://github.com/NuGet/Home/issues/4781)

- Ajouter une cible publique à NuGet.targets qui peut être référencée à l’aide de BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- La cible Pack ne peut pas créer correctement de contentFiles avec des actions de génération - [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do bloque les threads de pool de threads - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Documentation pour les indicateurs DependencyVersion et Framework de la commande Install - [#5858](https://github.com/NuGet/Home/issues/5858)

- Mise à jour de la documentation sur les avertissements et erreurs NuGet - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Liens vers les problèmes GitHub corrigés dans RTM 4.4

[Liste des problèmes 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Liste des problèmes 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Liste des problèmes 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
