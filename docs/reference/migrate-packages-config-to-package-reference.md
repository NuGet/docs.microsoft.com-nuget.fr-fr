---
title: Migration de package.config vers les formats PackageReference
description: Pour plus d’informations sur la façon de migrer un projet à partir du format de gestion package.config vers PackageReference pris en charge par NuGet 4.0 + et Visual Studio 2017 et .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 05a82e48c7083a19c50a05fa1df74ebfff8030d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546684"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrer à partir de packages.config vers PackageReference

Visual Studio 2017 Version 15.7 et ultérieures prend en charge la migration d’un projet à partir de la [packages.config](./packages-config.md) format de gestion pour le [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.

## <a name="benefits-of-using-packagereference"></a>Avantages de l’utilisation de PackageReference

* **Gérer toutes les dépendances de projet au même endroit**: tout comme les références entre projets et références d’assembly, le package NuGet fait référence (à l’aide de la `PackageReference` nœud) sont gérés directement dans les fichiers de projet, plutôt que d’utiliser un distinct fichier packages.config.
* **Vue ne soit pas encombré de dépendances de niveau supérieur**: contrairement à packages.config, PackageReference répertorie uniquement les packages NuGet que vous avez installé directement dans le projet. Par conséquent, le Gestionnaire de Package NuGet UI et le fichier projet ne sont pas encombrés de dépendances de bas niveau.
* **Améliorations des performances**: Si vous utilisez PackageReference, les packages sont conservés dans le *global-packages* dossier (tel que décrit sur [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) plutôt que dans un `packages` dossier au sein de la solution. Par conséquent, PackageReference s’exécute plus rapidement et consomme moins d’espace disque.
* **Un meilleur contrôle sur les dépendances et les flux de contenu**: à l’aide des fonctionnalités existantes de MSBuild vous permet de [référencer conditionnellement un package NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) et choisir des références de package par le framework cible, configuration, plateforme, ou autres tableaux croisés dynamiques.
* **PackageReference est en cours de développement**: consultez [PackageReference émet sur GitHub](https://aka.ms/nuget-pr-improvements). packages.config n’est plus en cours de développement.

### <a name="limitations"></a>Limitations

* NuGet PackageReference n’est pas disponible dans Visual Studio 2015 et versions antérieures. Les projets migrés peuvent être ouverts que dans Visual Studio 2017.
* Migration n’est pas actuellement disponible pour les projets C++ et ASP.NET.
* Certains packages ne sont peut-être pas entièrement compatibles avec PackageReference. Pour plus d’informations, consultez [les problèmes de compatibilité du package](#package-compatibility-issues).

### <a name="known-issues"></a>Problèmes connus

1. L’option `Migrate packages.config to PackageReference...` n’est pas disponible dans le menu contextuel 

#### <a name="issue"></a>Problème 
 
À la première ouverture d’un projet, il peut arriver que NuGet ne s’initialise pas tant qu’aucune opération NuGet n’a été réalisée. Dans ce cas, l’option de migration ne s’affiche pas dans le menu contextuel sur `packages.config` ou `References`. 

#### <a name="workaround"></a>Solution de contournement 

Effectuez l’une des actions NuGet suivantes : 
* Ouvrez l’interface utilisateur du Gestionnaire de package : cliquez avec le bouton droit sur `References` et sélectionnez `Manage NuGet Packages...`. 
* Ouvrez la console du Gestionnaire de package : dans `Tools > NuGet Package Manager`, sélectionnez `Package Manager Console`. 
* Exécutez la restauration NuGet : cliquez avec le bouton droit sur le nœud de la solution dans l’Explorateur de solutions, puis sélectionnez `Restore NuGet Packages`. 
* Générez le projet qui déclenche également la restauration NuGet. 

L’option de migration devrait apparaître. Notez qu’elle n’est pas prise en charge et ne s’affiche pas pour les types de projets ASP.NET et C++. 

## <a name="migration-steps"></a>Étapes de migration

> [!Note]
> Avant de commencer la migration, Visual Studio crée une sauvegarde du projet afin que vous puissiez [restaurer packages.config](#how-to-roll-back-to-packagesconfig) si nécessaire.

1. Ouvrez une solution contenant le projet à l’aide `packages.config`.

1. Dans **l’Explorateur de solutions**, avec le bouton droit sur le **références** nœud ou le `packages.config` fichier et sélectionnez **migrer packages.config vers PackageReference...** .

1. L’utilitaire de migration analyse les références de package NuGet du projet et tente de les classer dans **dépendances de niveau supérieur** (packages NuGet que vous avez installé directement) et **dépendances transitives** (les packages qui ont été installés en tant que dépendances de packages de niveau supérieur.)

   > [!Note]
   > PackageReference prend en charge de la restauration de package transitives et résout les dépendances de façon dynamique, ce qui signifie que les dépendances transitives ne doivent pas être installés de manière explicite.

1. (Facultatif) Vous pouvez choisir de traiter un package NuGet classé comme une dépendance transitive comme une dépendance de niveau supérieur en sélectionnant le **niveau supérieur** option pour le package. Cette option est définie automatiquement pour les packages contenant des ressources qui ne sont pas acheminées de manière transitive (ceux de la `build`, `buildCrossTargeting`, `contentFiles`, ou `analyzers` dossiers) et ceux marqués comme une dépendance de développement (`developmentDependency = "true"`).

1. Passez en revue les [les problèmes de compatibilité du package](#package-compatibility-issues).

1. Sélectionnez **OK** pour commencer la migration.

1. À la fin de la migration, Visual Studio fournit un rapport avec un chemin d’accès à la sauvegarde, la liste des packages installés (dépendances de niveau supérieur), une liste des packages référencés en tant que dépendances transitives et une liste de problèmes de compatibilité identifiés au début de migration. Le rapport est enregistré dans le dossier de sauvegarde.

1. Vérifiez que la solution génère et s’exécute. Si vous rencontrez des problèmes, [signaler un problème sur GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Comment revenir à packages.config

1. Fermez le projet migré.

1. Copiez le fichier de projet et `packages.config` à partir de la sauvegarde (généralement `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) au dossier du projet. Supprimer le dossier obj, s’il existe dans le répertoire racine du projet.

1. Ouvrez le projet.

1. Ouvrez la Console du Gestionnaire de Package à l’aide de la **Outils > Gestionnaire de Package NuGet > Console du Gestionnaire de Package** commande de menu.

1. Dans la Console, exécutez la commande suivante :

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problèmes de compatibilité de package

Certains aspects qui étaient pris en charge dans packages.config ne sont pas pris en charge dans PackageReference. L’utilitaire de migration analyse et détecte ces problèmes. N’importe quel package qui comporte un ou plusieurs des problèmes suivants peuvent ne pas fonctionner comme prévu après la migration.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>scripts de « Install.ps1 » sont ignorés lorsque le package est installé après la migration

| | |
| --- | --- |
| **Description** | Avec PackageReference, des scripts PowerShell Install.ps1 et uninstall.ps1 ne sont pas exécutées pendant l’installation ou désinstallation d’un package. |
| **Impact potentiel** | Les packages qui dépendent de ces scripts pour configurer un comportement dans le projet de destination ne peuvent pas fonctionner comme prévu. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>ressources de « content » ne sont pas disponibles lorsque le package est installé après la migration

| | |
| --- | --- |
| **Description** | Ressources dans d’un package `content` dossier ne sont pas pris en charge avec PackageReference et sont ignorés. PackageReference ajoute la prise en charge de `contentFiles` pour avoir une meilleure prise en charge transitive et contenu partagé.  |
| **Impact potentiel** | Ressources dans `content` ne sont pas copiés dans le projet et le projet de code qui dépend de la présence de ces ressources nécessite de refactorisation.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Les transformations XDT ne sont pas appliquées lorsque le package est installé après la mise à niveau

| | |
| --- | --- |
| **Description** | Les transformations XDT ne sont pas pris en charge avec PackageReference et `.xdt` fichiers sont ignorés lors de l’installation ou désinstallation d’un package.   |
| **Impact potentiel** | Les transformations XDT ne sont pas appliquées à tous les fichiers projet XML, le plus souvent, `web.config.install.xdt` et `web.config.uninstall.xdt`, ce qui signifie que le projet` web.config` fichier n’est pas mis à jour lorsque le package est installé ou désinstallé. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblys à la racine de lib sont ignorés lorsque le package est installé après la migration

| | |
| --- | --- |
| **Description** | Avec PackageReference, assemblys présentent à la racine de `lib` dossier sans un target framework sous-dossier spécifique sont ignorés. NuGet recherche un sous-dossier correspondant le moniker du framework cible (TFM) correspondant à la version du projet cible et installe les assemblys correspondants dans le projet. |
| **Impact potentiel** | Les packages qui n’ont pas un sous-dossier correspondant le moniker du framework cible (TFM) correspondant à la version du projet cible ne peuvent pas se comporter comme prévu après la transition et Échec de l’installation lors de la migration |

## <a name="found-an-issue-report-it"></a>Rencontré un problème ? Signalez-le !

Si vous rencontrez un problème lors de la migration, veuillez [signaler un problème sur le dépôt NuGet GitHub](https://github.com/NuGet/Home/issues/).
