---
title: Migration du format package.config au format PackageReference
description: Détails sur la migration d'un projet du format de gestion package.config vers le format PackageReference dans le cadre de la prise en charge par NuGet 4.0+ et VS2017 et .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428890"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrer de packages.config vers PackageReference

Visual Studio 2017 15.7 ou version ultérieure prend en charge la migration d'un projet du format de gestion [packages.config](../reference/packages-config.md) vers le format [PackageReference](../consume-packages/Package-References-in-Project-Files.md).

## <a name="benefits-of-using-packagereference"></a>Avantages de l’utilisation de PackageReference

* **Gérer toutes les dépendances de projet en un seul endroit**: Tout comme `PackageReference` le projet de références de projet et les références d’assemblage, les références de paquets NuGet (à l’aide du nœud) sont gérées directement dans les fichiers de projet plutôt que d’utiliser un fichier packages.config séparé.
* **Vue épurée des dépendances de haut niveau**: Contrairement à packages.config, PackageReference ne répertorie que les paquets NuGet que vous avez directement installés dans le projet. Ainsi, l'interface utilisateur de NuGet Package Manager et le fichier projet ne sont pas encombrés de dépendances de niveau inférieur.
* **Améliorations des performances**: Lors de l’utilisation de PackageReference, les paquets sont maintenus dans le dossier global *(comme* décrit sur [la gestion des paquets globaux et des dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) plutôt que dans un `packages` dossier dans la solution. En conséquence, PackageReference est plus rapide et consomme moins d'espace disque.
* **Contrôle fin des dépendances et du flux**de contenu : L’utilisation des fonctionnalités existantes de MSBuild vous permet de [référencer sous condition un package NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) et de choisir des références de paquets par cadre cible, configuration, plate-forme ou autres pivots.
* **PackageReference est en cours de développement actif**: Voir les [numéros packageReference sur GitHub](https://aka.ms/nuget-pr-improvements). packages.config n’est plus en cours de développement.

### <a name="limitations"></a>Limites

* NuGet PackageReference n'est pas disponible dans Visual Studio 2015 et versions antérieures. Les projets migrés ne peuvent être ouverts que dans Visual Studio 2017 et versions ultérieures.
* La migration n’est actuellement pas possible pour les projets C++ et ASP.NET.
* Certains packages peuvent ne pas être entièrement compatibles avec PackageReference. Pour plus d’informations, voir la section [Problèmes de compatibilité des packages](#package-compatibility-issues).

En outre, il ya quelques différences dans la façon dont PackageReferences fonctionnent par rapport à packages.config. Par exemple - [les versions de mise à niveau contraignantes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) ne sont pas supprétées par PackageReference, mais ajoutent la prise en charge pour [les versions flottantes](../consume-packages/package-references-in-project-files.md#floating-versions).

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

## <a name="migration-steps"></a>Étapes de la migration

> [!Note]
> Avant le début de la migration, Visual Studio crée une sauvegarde du projet pour vous permettre de [retourner au format packages.config](#how-to-roll-back-to-packagesconfig) si nécessaire.

1. Ouvrez une solution contenant un projet en utilisant `packages.config`.

1. Dans **Explorateur de solutions**, cliquez avec le bouton droit de la souris sur le nœud **Références** ou sur le fichier `packages.config`, puis sélectionnez **Migrer packages.config vers PackageReference**.

1. Le migrateur analyse les références des packages NuGet du projet et tente de les classer dans la catégorie des **dépendances de niveau supérieur** (packages NuGet que vous avez installés directement) et des **dépendances transitoires** (packages qui ont été installés en tant que dépendances de packages de niveau supérieur).

   > [!Note]
   > PackageReference prend en charge la restauration des packages transitifs et résout les dépendances de manière dynamique, ce qui signifie que les dépendances transitives n'ont pas à être installées explicitement.

1. (Facultatif) Vous pouvez traiter un package NuGet classé comme une dépendance transitive en tant que dépendance de niveau supérieur en sélectionnant l'option **Top-Level** (niveau supérieur) pour ce package. Cette option est automatiquement définie pour les packages contenant des ressources qui ne s'exécutent pas de manière transitoire (celles des dossiers `build`, `buildCrossTargeting`, `contentFiles` ou `analyzers`) et celles marquées comme des dépendances de développement (`developmentDependency = "true"`).

1. Vérifiez les éventuels [problèmes de compatibilité des packages](#package-compatibility-issues).

1. Sélectionnez **OK** pour commencer la migration.

1. À la fin de la migration, Visual Studio fournit un rapport indiquant un chemin d'accès à la sauvegarde, la liste des packages installés (dépendances de niveau supérieur), une liste des packages référencés comme dépendances transitives, et une liste des problèmes de compatibilité identifiés au début de la migration. Le rapport est enregistré dans le dossier de sauvegarde.

1. Vérifiez la génération et l’exécution de la solution. Si vous rencontrez des problèmes, [signalez-les sur GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Revenir à packages.config

1. Fermez le projet migré.

1. Copiez le fichier projet et `packages.config` de la sauvegarde (généralement `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) dans le dossier du projet. Supprimez le dossier obj s'il existe dans le répertoire racine du projet.

1. Ouvrez le projet.

1. Ouvrez la Console du Gestionnaire de package à partir de la commande de menu **Outils > Gestionnaire de package NuGet > Console du Gestionnaire de package**.

1. Exécutez la commande suivante dans la console :

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Créer un package après la migration

Une fois la migration terminée, nous vous recommandons d'ajouter une référence au package nuget [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack), puis d'utiliser [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) pour créer le package. Bien que certains scénarios vous permettent d’utiliser `dotnet.exe pack` au lieu de `msbuild -t:pack`, cette méthode n'est pas recommandée.

## <a name="package-compatibility-issues"></a>Problèmes de compatibilité des packages

Certains aspects autrefois pris en charge dans packages.config ne le sont plus dans PackageReference. Le migrateur analyse et détecte ces problèmes. Tout package présentant un ou plusieurs des problèmes suivants risque de ne pas se comporter comme prévu après la migration.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Les scripts « install.ps1 » sont ignorés lorsque le package est installé après la migration

| | |
| --- | --- |
| **Description** | Avec PackageReference, les scripts PowerShell install.ps1 et uninstall.ps1 ne sont pas exécutés pendant l'installation ou la désinstallation d'un package. |
| **Impact potentiel** | Les packages qui dépendent de ces scripts pour configurer certains comportements dans le projet de destination peuvent ne pas fonctionner comme prévu. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Les ressources « content » sont ignorées lorsque le package est installé après la migration

| | |
| --- | --- |
| **Description** | Les ressources du dossier `content` d'un package ne sont pas prises en charge par PackageReference et sont ignorées. PackageReference ajoute la prise en charge de `contentFiles` pour permettre une meilleure prise en charge transitive et le partage de contenu.  |
| **Impact potentiel** | les ressources dans `content` ne sont pas copiées dans le projet et le code de projet qui dépend de la présence de ces ressources nécessite une refactorisation.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Les transformations XDT ne sont pas appliquées lorsque le package est installé après la mise à niveau

| | |
| --- | --- |
| **Description** | Les transformations XDT ne sont pas prises en charge avec PackageReference et les fichiers `.xdt` sont ignorés lors de l'installation ou de la désinstallation d'un package.   |
| **Impact potentiel** | les transformations XDT ne sont appliquées à aucun fichier XML du projet, le plus souvent, `web.config.install.xdt` et `web.config.uninstall.xdt`, ce qui signifie que le fichier ` web.config` du projet n'est pas mis à jour lorsque le package est installé ou désinstallé. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Les assemblys à la racine de la bibliothèque sont ignorés lorsque le package est installé après la migration

| | |
| --- | --- |
| **Description** | Avec PackageReference, les assemblys présents à la racine du dossier `lib` sans sous-dossier spécifique au framework cible sont ignorés. NuGet recherche un sous-dossier correspondant au moniker de framework cible (TFM) pour le framework cible du projet, puis installe les assemblys correspondants dans le projet. |
| **Impact potentiel** | Les packages sans sous-dossier correspondant au moniker de framework cible (TFM) pour le framework cible du projet peuvent ne pas se comporter comme prévu après la transition, ou l'installation peut échouer pendant la migration |

## <a name="found-an-issue-report-it"></a>Vous avez rencontré un problème ? Signalez-le !

Si vous rencontrez un problème avec l'expérience de migration, veuillez [signaler ce problème sur le référentiel NuGet GitHub](https://github.com/NuGet/Home/issues/).
