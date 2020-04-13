---
title: Notes de publication de la version NuGet 4.0 RC
description: Notes de publication pour NuGet 4.0 RTM, avec notamment les problèmes connus, les correctifs de bogues, les fonctionnalités ajoutées et les DCR.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496604"
---
# <a name="nuget-40-rtm-release-notes"></a>Notes de publication de NuGet 4.0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) est fourni avec NuGet 4.0, qui ajoute la prise en charge de .NET Core, intègre un ensemble de correctifs de qualité et améliore les performances. Cette version offre aussi plusieurs améliorations telles que la prise en charge de PackageReference, des commandes NuGet comme cibles MSBuild, la restauration des packages en arrière-plan, et bien plus encore.

## <a name="known-issues"></a>Problèmes connus

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>La restauration NuGet peut échouer quand plusieurs projets référencent un autre projet dans une solution

#### <a name="issue"></a>Problème

La restauration NuGet peut ne pas fonctionner si, dans une solution, vous avez des références de projet au projet même avec une casse différente ou avec différents chemins relatifs. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Solution de contournement

Corrigez les casses ou les chemins relatifs pour qu’ils soient identiques pour toutes les références de projet.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Lors de l’utilisation de la Console du Gestionnaire de Package, la touche « Entrée » peut ne pas fonctionner

#### <a name="issue"></a>Problème

Parfois, la touche Entrée ne fonctionne pas dans la Console du Gestionnaire de Package. Si cela se produit, vérifiez l’évolution du correctif et spécifiez les éventuelles informations supplémentaires utiles dans les étapes de reproduction du problème. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solution de contournement

Redémarrez Visual Studio et ouvrez la console de gestion des packages avant d’ouvrir la solution. Vous pouvez aussi tenter de supprimer le `project.lock.json` et de réeffectuer la restauration.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Dans les projets .NET Core, vous pouvez vous retrouver avec une boucle de restauration infinie quand vous utilisez un package qui contient un assembly avec une signature non valide

#### <a name="issue"></a>Problème

Parfois, quand vous utilisez un package qui contient un assembly avec une signature non valide, ou quand la version du package est définie avec 'DateTime', la restauration automatique de package s’exécute dans une boucle infinie. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Solution de contournement

Il n’existe aucune solution de contournement pour l’instant.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Impossible d’afficher, d’ajouter ou de mettre à jour DotNetCLITools à l’aide du Gestionnaire de package NuGet

#### <a name="issue"></a>Problème

Le Gestionnaire de package NuGet ne s’affiche pas et n’autorise pas l’ajout/mise à jour de DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solution de contournement

Vous devez modifier manuellement DotNetCLIToolReferences dans votre fichier projet.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>La restauration NuGet échoue quand vous définissez la propriété PackageId pour des projets

#### <a name="issue"></a>Problème

Pour les projets .NET Core, la restauration NuGet dans Visual Studio ne respecte pas la propriété PackageId des projets. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Solution de contournement

Exécutez la restauration à l’aide de la ligne de commande.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Quand votre projet n’a pas de dossier « obj », la restauration du package peut échouer

#### <a name="issue"></a>Problème

Visual Studio ne parvient pas à restaurer PackageReferences quand le dossier « obj » a été supprimé. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Solution de contournement

Créez manuellement le dossier « obj » ; la restauration devrait alors fonctionner.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>La mise à jour manuelle des packages à l’aide de Update-Package dans la console peut échouer

#### <a name="issue"></a>Problème

L’utilisation manuelle d’Update-Package dans la console ne fonctionne qu’une seule fois pour les projets PackageReferences qui viennent d’être convertis. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Solution de contournement

Il n’existe aucune solution de contournement pour l’instant.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes

#### <a name="issue"></a>Problème

Le reciblage de la version du framework cible peut générer des informations Intellisense incomplètes dans Visual Studio. Cela se produit quand vous utilisez PackageReferences comme format de gestionnaire de package. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solution de contournement

Effectuez une restauration manuelle.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>msbuild /t:restore échoue quand un projet ciblant .NET461 référence un autre projet ciblant .NETStandard

#### <a name="issue"></a>Problème

msbuild /t:restore échoue quand un projet basé sur PackageReference ciblant .NET461 référence un autre projet basé sur PackageReference ciblant .NETStandard.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Solution de contournement

Il n’existe aucune solution de contournement pour l’instant.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problèmes résolus dans NuGet 4.0 RTM

[Notes de publication de NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) : répertorie tous les problèmes résolus dans NuGet 4.0 RC

### <a name="features"></a>Fonctionnalités

- Localiser les chaînes dans NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

- NuGet force le chargement des projets d’application web en mode LSL - [#4258](https://github.com/NuGet/Home/issues/4258)

- Prise en charge d’AutoReferenced PackageReference pour bloquer les changements de version dans l’interface utilisateur pour les packages à « sdk installé » - [#4044](https://github.com/NuGet/Home/issues/4044)

- Communiquer correctement PackageSpec.Version pour toutes les dépendances de projet (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- Prise en charge de la suppression des références dans `.csproj` à partir de la ligne de commande - [#4101](https://github.com/NuGet/Home/issues/4101)

- Prise en charge de la restauration pour les projets PackageReference (normaux et xplat) et le chargement de solution allégé - [#4003](https://github.com/NuGet/Home/issues/4003)

- Prise en charge de l’ajout des références dans `.csproj` à partir de la ligne de commande - [#3751](https://github.com/NuGet/Home/issues/3751)

- Prise en charge de la restauration NuGet pour le chargement de solution allégé pour `packages.config` ou `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)

- Prise en charge de contentFiles dans le fichier de cibles généré nuget - [#3683](https://github.com/NuGet/Home/issues/3683)

- Établir un Mono CI pour la validation nuget.exe sur Mac à l’aide de MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

- Déplacer NuGet hors des dépendances v2 NuGet.Core - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Bogues

- La restauration NuGet dans Visual Studio ne respecte pas la propriété PackageId des projets - [#4586](https://github.com/NuGet/Home/issues/4586)

- Erreur NuGet ProjectSystemCache lors de l’ajout d’un package dans un package vsix - [#4545](https://github.com/NuGet/Home/issues/4545)

- Le pack lève une exception si IncludeSource est utilisé dans un projet avec plusieurs TFM - [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 se bloque lors de l’utilisation de la mise à jour à partir de la gestion de package à l’échelle de la solution - [#4474](https://github.com/NuGet/Home/issues/4474)

- Impossible de désinstaller un package nouvellement installé - [#4435](https://github.com/NuGet/Home/issues/4435)

- Lors de la migration vers PackageRef, les solutions hybrides ont un comportement de restauration étrange - [#4433](https://github.com/NuGet/Home/issues/4433)

- La génération peu après le démarrage d’une opération NuGet (installation, mise à jour, restauration) peut provoquer le blocage de VS - [#4420](https://github.com/NuGet/Home/issues/4420)

- Blocage de l’interface utilisateur : interblocage lors de l’initialisation de NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- La commande add package doit ajouter la version en tant qu’attribut au lieu d’élément - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln -- échoue quand des configurations dans SLN provoquent la présence de projets en double (mais avec des configurations différentes) dans le graphe de restauration - [#4316](https://github.com/NuGet/Home/issues/4316)

- Packages de contenu uniquement - [#3668](https://github.com/NuGet/Home/issues/3668)

- Par défaut, ignorer l’option de sélection du format de package - [#4468](https://github.com/NuGet/Home/issues/4468)

- Performances : Le projet CreateUAP_CSharp_VS.01.1.Create a diminué Duration_TotalElapsedTime de 3 153,570 ms (149,1 %). Ligne de base 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Performances : La solution ManagedLangs_CS_DDRIT.0300.Rebuild a diminué Duration_TotalElapsedTime de 1,5 seconde. Ligne de base de 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- La nomination échoue dans les projets multi-TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Performances : La solution WebForms_DDRIT.1200.Close a diminué VM_ImagesInMemory_Total_devenv de 3,000 (0,5 %). Ligne de base 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - Avertissements de pack lors du ciblage de netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException lors de la tentative d’ajout d’un package NuGet à une application web ASP.NET Core vide - [#4391](https://github.com/NuGet/Home/issues/4391)

- Le pack s’exécute trop souvent -- dotnet
  - Échec de dotnetcore pack avec l’erreur : Il existe une dépendance circulaire dans le graphique de dépendance cible qui implique la cible « Pack » - [#4381](https://github.com/NuGet/Home/issues/4381)

- Le pack s’exécute trop souvent -- La génération de package NuGet n’inclut pas toutes les configurations - [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException : ajout de nuget avec packageref dans le projet C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Accessibilité : Le narrateur n’effectue pas la narration de la case à cocher pour sélectionner les projets dans lesquels installer le package- [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 ne parvient pas toujours à se connecter aux flux VSO/VSTS - Bogue VS 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles envoie la sortie vers un emplacement incorrect si PackagePath spécifie « contentFiles » comme chemin - [#4348](https://github.com/NuGet/Home/issues/4348)

- La cible de pack ajoute la propriété PackageVersion avec VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

- La spécification du chemin du package ne fonctionne pas avec dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet génère un ensemble d’avertissements à propos des importations en double pendant la restauration - [#4304](https://github.com/NuGet/Home/issues/4304)

- Le choix de la boîte de dialogue « Format du Gestionnaire de Package NuGet » semble incorrect dans le thème sombre - [#4300](https://github.com/NuGet/Home/issues/4300)

- Blocage de Visual Studio lors de la restauration de la build - [#4298](https://github.com/NuGet/Home/issues/4298)

- Interblocages de Visual Studio si vous ajoutez TFM dans targetframeworks, enregistrez, puis générez. 10 % du temps - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack ne génère pas de message de réussite en cas d’empaquetage correct d’un projet - [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask échoue car System.IO.Compression 4.1 est introuvable - [#4290](https://github.com/NuGet/Home/issues/4290)

- Le pack s’exécute trop souvent -- PackTask échoue souvent avec un conflit d’accès aux fichiers - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet ouvre la fenêtre de sortie pendant la restauration en arrière-plan - [#4274](https://github.com/NuGet/Home/issues/4274)

- Éliminer ServiceProvider en tant que modèle de codage dangereux (susceptible de provoquer des blocages) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Performances/blocage de l’interface utilisateur - Améliorer les lectures DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)

- Interblocage de Visual Studio si vous essayez de fermer un projet avant la fin de la restauration NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

- Problèmes liés à PackTask et à l’empaquetage `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Impossible de résoudre les packages nuget sur un nouveau projet (nécessité de redémarrer visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] La liste déroulante « Version » qui affiche les versions de package disponibles a du mal à rester synchronisée avec le package nuGet sélectionné... - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client doit utiliser CPS JoinableTaskFactory lors de l’interaction avec CPS pour éviter les interblocages - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 ne décompresse pas `.targets` à partir du package - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore pack ne prend pas en charge le titre dans `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package génère une boîte de dialogue d’erreur dans VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)

- La mise à jour d’un package pour un projet .net core semble ne pas fonctionner, car l’interface utilisateur n’obtient pas la mise à jour CPS à partir de la nomination. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Améliorer l’avertissement de référence non résolue - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore pack - ProjectReference perd les informations de version - [#3953](https://github.com/NuGet/Home/issues/3953)

- Création d’application UWP - régressions de durée totale écoulée pour la création de projet et la régénération - [#3873](https://github.com/NuGet/Home/issues/3873)

- Un message de fin de restauration s’affiche même après une erreur pendant la restauration. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Republier Nuget.CommandLine 3.4.4 sur Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Lors de la migration, le projet change de `project.json` à `.csproj` --- la restauration échoue - [#4297](https://github.com/NuGet/Home/issues/4297)

- Échec de restauration en cas de projet de test xunit nouvellement créé - [#4296](https://github.com/NuGet/Home/issues/4296)

- Les projets Core peuvent se bloquer, verrouiller l’interface utilisateur à l’ouverture - [#4269](https://github.com/NuGet/Home/issues/4269)

- Corriger le fichier de cibles pour les tâches de génération - [#4267](https://github.com/NuGet/Home/issues/4267)

- La liste d’erreurs contient une erreur après la génération d’une solution qui décharge le projet référencé - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057 : L’objet « _GenerateRestoreGraphProjectEntry » cible n’existe pas dans le projet. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback : l’interface utilisateur du gestionnaire nuget pour la solution se bloque quand vous sélectionnez tous les projets - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath échoue quand il y a une barre oblique de fin - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback : NuGet restore génère plusieurs avertissements de référence de projet pour un projet LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)

- Le pack de `.csproj` n’inclut pas l’attribut minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll fournie est signée avec retard dans VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback : Échec de restauration d’un projet VS 2015 généré avec CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback : Des erreurs de restauration peuvent masquer des messages d’erreur plus complets que la build pourrait donner - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Une erreur s’est produite lors de la restauration des packages NuGet pour le projet de site web : la valeur ne peut pas être null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- La migration lève « Exception de référence d’objet » dans NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore pack doit empaqueter les outils avec les versions par rapport auxquelles le package a été créé - [#4063](https://github.com/NuGet/Home/issues/4063)

- Une nouvelle restauration en arrière-plan écrit des millisecondes dans la barre d’état alors que la restauration prend plusieurs secondes - [#4036](https://github.com/NuGet/Home/issues/4036)

- Faute de frappe lors d’un échec de résolution de toutes les références de projet - [#4018](https://github.com/NuGet/Home/issues/4018)

- Activer les flux de travail PCM dans les scénarios de référence de package - [#4016](https://github.com/NuGet/Home/issues/4016)

- Packages installés introuvables dans l’interface utilisateur du Gestionnaire de package - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - dotnetcore pack échoue quand PackagePath est vide - [#3993](https://github.com/NuGet/Home/issues/3993)

- La tâche de restauration échoue dans un scénario à plusieurs utilisateurs - [#3897](https://github.com/NuGet/Home/issues/3897)

- Impossible de modifier le type de contenu lors de l’empaquetage à l’aide de la tâche NuGet Pack - [#3895](https://github.com/NuGet/Home/issues/3895)

- La copie par défaut de ContentFiles est incorrecte pour MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

- La restauration de package d’installation enregistre deux fois le message de restauration de packages - [#3785](https://github.com/NuGet/Home/issues/3785)

- Supprimer Guardrails - La restauration de la section « runtimes » doit s’appliquer uniquement au projet actif - [#3768](https://github.com/NuGet/Home/issues/3768)

- La tâche Pack place les fichiers de contenu à la fois dans « content/ » et dans « contentFiles/ » - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 effectue un fractionnement de balise supplémentaire - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore pack : L’empaquetage d’un projet avec des références de package génère un avertissement d’importation en double - [#3665](https://github.com/NuGet/Home/issues/3665)

- La journalisation de restauration dans Visual Studio ne s’affiche pas toujours - [#3633](https://github.com/NuGet/Home/issues/3633)

- Le texte d’aide de nuget locals mentionnait encore le cache des packages - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 associe PackageReferences à TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- NuGet récupère une version inattendue de MSBuild dans VS « 15 » Preview 4 dev. invite de commandes - [#3408](https://github.com/NuGet/Home/issues/3408)

- Écrire des cibles/fichiers de propriétés lors de l’échec de restauration - [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet pendant la restauration ne respecte pas les mêmes shims de compatibilité que MSBuild lors de l’exécution dans l’invite de commandes de Visual Studio 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

- Réactiver PackFromProjectWithDevelopmentDependencySet pour VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Fusionner des problèmes avec NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

- Intégrer 4.0.0.2067 dans les dépôts CLI et SDK pour livrer avec RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

- Blocage de Visual Studio quand vous créez une application de console Core, fermez la solution, ouvrez la solution puis fermez la solution - [#4008](https://github.com/NuGet/Home/issues/4008)

- Blocage lors de l’ouverture de projet contre d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Corriger le message d’aide/documentation dotnet/nuget.exe locals - [#3919](https://github.com/NuGet/Home/issues/3919)

- Inspecter PackTask à la recherche des problèmes avec les espaces blancs de début ou de fin - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore pack empaquette à partir d’obj et non bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore pack semble toujours définir la version de ProjectReference sur 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - dotnetcore pack échoue avec les références de projet et <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException dans ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- Supprimer les espaces blancs des propriétés MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

- Consolider les deux événements de projets déclenchés lors du chargement du projet - [#3759](https://github.com/NuGet/Home/issues/3759)

- Les bibliothèques P2P dans le fichier `project.assets.json` ont une version incorrecte - [#3748](https://github.com/NuGet/Home/issues/3748)

- Blocage de la restauration car un flux ne répond pas et un package est indisponible - [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe pourrait se bloquer en cas de sortie d’erreur MSBuild volumineuse - [#3572](https://github.com/NuGet/Home/issues/3572)

- La restauration au moment de la génération pour Blend échoue la première fois, réussit la deuxième fois (scénario VS corrigé) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- migrer vsix de v2 vsix vers v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet devrait avoir un mécanisme permettant d’obtenir le chemin du fichier de verrouillage dans MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Ajouter des ressources de build au contrôle de compatibilité TFM et au fichier de ressources - [#3296](https://github.com/NuGet/Home/issues/3296)

- Définir un nouveau « Pack » ProjectCapability dans les cibles Pack pour l’activation des fonctionnalités liées au package - [#4146](https://github.com/NuGet/Home/issues/4146)

- Exécuter le pack en tant que cible post-build sous réserve de propriété MSBuild « GeneratePackageOnBuild » - [#4145](https://github.com/NuGet/Home/issues/4145)

- Utiliser la propriété NuGet RestoreProjectStyle pour créer un projet NuGet spécifique - [#4134](https://github.com/NuGet/Home/issues/4134)

- Adapter la restauration pour changement de références de projet transitives - [#4076](https://github.com/NuGet/Home/issues/4076)

- Ajouter des propriétés NuGet dans le fichier cible pour les projets non UWP - [#4030](https://github.com/NuGet/Home/issues/4030)

- Prise en charge UWP TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)

- Communiquer les métadonnées de référence de projet au système de projet NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)

- Ajouter une interface utilisateur pour le mode d’empaquetage - [#3921](https://github.com/NuGet/Home/issues/3921)

- `.csproj` hérité a besoin de NugetTargetMoniker et RuntimeIdentifiers définis dans le projet/les cibles - [#3854](https://github.com/NuGet/Home/issues/3854)

- L’installation de package peut chevaucher la restauration automatique - [#3836](https://github.com/NuGet/Home/issues/3836)

- Le menu contextuel QueryStatus ne se produit pas quand VSPackage n’est pas chargé - [#3835](https://github.com/NuGet/Home/issues/3835)

- La restauration de solution et la restauration de build continuent à afficher des boîtes de dialogue - [#3789](https://github.com/NuGet/Home/issues/3789)

- Isoler la version VSSDK dans la build de solution NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Liens vers les problèmes GitHub corrigés dans la version RTM
[Liste des problèmes 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Liste des problèmes 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Liste des problèmes 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Liste des problèmes 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Liste des problèmes 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
