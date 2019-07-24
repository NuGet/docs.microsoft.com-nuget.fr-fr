---
title: Migration de package. config vers les formats PackageReference
description: Détails sur la migration d’un projet à partir du format de gestion package. config vers PackageReference, comme pris en charge par NuGet 4.0 + et VS2017 et .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433288"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrer de packages. config vers PackageReference

Visual Studio 2017 version 15,7 et les versions ultérieures prennent en charge la migration d’un projet à partir du format de gestion [packages. config](./packages-config.md) vers le format [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Avantages de l’utilisation de PackageReference

* **Gérer toutes les dépendances de projet à un seul emplacement**: Tout comme les références de projet à projet et les références d’assembly, les `PackageReference` références de package NuGet (à l’aide du nœud) sont gérées directement dans les fichiers projet plutôt que d’utiliser un fichier Packages. config distinct.
* **Affichage des dépendances de niveau supérieur non encombré**: Contrairement à packages. config, PackageReference répertorie uniquement les packages NuGet que vous avez installés directement dans le projet. Par conséquent, l’interface utilisateur du gestionnaire de package NuGet et le fichier projet ne sont pas encombrés par des dépendances de niveau inférieure.
* **Améliorations des performances**: Lorsque vous utilisez PackageReference, les packages sont conservés dans le dossier *Global-packages* (comme décrit dans [gestion des dossiers de packages globaux et](../consume-packages/managing-the-global-packages-and-cache-folders.md) de `packages` cache plutôt que dans un dossier dans la solution. Par conséquent, PackageReference fonctionne plus rapidement et consomme moins d’espace disque.
* **Contrôle précis sur les dépendances et le workflow de contenu**: L’utilisation des fonctionnalités existantes de MSBuild vous permet de référencer de manière [conditionnelle un package NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) et de choisir des références de package par Framework cible, configuration, plate-forme ou d’autres tableaux croisés dynamiques.
* **PackageReference est en cours de développement actif**: Consultez [problèmes PackageReference sur GitHub](https://aka.ms/nuget-pr-improvements). Packages. config n’est plus en cours de développement actif.

### <a name="limitations"></a>Limites

* NuGet PackageReference n’est pas disponible dans Visual Studio 2015 et versions antérieures. Les projets migrés ne peuvent être ouverts que dans Visual Studio 2017 et versions ultérieures.
* La migration n’est actuellement pas possible pour les projets C++ et ASP.NET.
* Certains Packages peuvent ne pas être entièrement compatibles avec PackageReference. Pour plus d’informations, consultez [problèmes de compatibilité des packages](#package-compatibility-issues).

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
> Avant le début de la migration, Visual Studio crée une sauvegarde du projet pour vous permettre de revenir [à packages. config](#how-to-roll-back-to-packagesconfig) si nécessaire.

1. Ouvrez une solution contenant un projet `packages.config`à l’aide de.

1. Dans **Explorateur de solutions**, cliquez avec le bouton droit  sur le nœud Références `packages.config` ou le fichier, puis sélectionnez **migrer packages. config vers PackageReference...** .

1. L’utilitaire de migration analyse les références de package NuGet du projet et tente de les classer dans des dépendances de **niveau supérieur** (packages NuGet que vous avez installées directement) et des **dépendances transitives** (les packages qui ont été installés en tant que dépendances des packages de niveau supérieur).

   > [!Note]
   > PackageReference prend en charge la restauration transitive des packages et résout les dépendances de manière dynamique, ce qui signifie que les dépendances transitives n’ont pas besoin d’être installées de manière explicite.

1. Facultatif Vous pouvez choisir de traiter un package NuGet classé comme une dépendance transitive en tant que dépendance de niveau supérieur en sélectionnant l’option de **niveau supérieur** pour le package. Cette option est automatiquement définie pour les packages contenant des ressources qui ne circulent pas de manière `build`transitive `contentFiles`(celles `analyzers` des dossiers, `buildCrossTargeting`, ou) et celles marquées`developmentDependency = "true"`comme dépendance de développement ().

1. Examinez les éventuels [problèmes de compatibilité des packages](#package-compatibility-issues).

1. Sélectionnez **OK** pour commencer la migration.

1. À la fin de la migration, Visual Studio fournit un rapport avec un chemin d’accès à la sauvegarde, la liste des packages installés (dépendances de niveau supérieur), une liste de packages référencés en tant que dépendances transitives et une liste des problèmes de compatibilité identifiés au début de passage. Le rapport est enregistré dans le dossier de sauvegarde.

1. Vérifiez que la solution est générée et exécutée. Si vous rencontrez des problèmes, [envoyez un problème sur GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Comment revenir à packages. config

1. Fermez le projet migré.

1. Copiez le fichier projet `packages.config` et à partir de la `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`sauvegarde (en général) dans le dossier du projet. Supprimez le dossier obj s’il existe dans le répertoire racine du projet.

1. Ouvrez le projet.

1. Ouvrez la console du gestionnaire de package à l’aide des **outils > gestionnaire de package NuGet >** commande de menu de la console du gestionnaire de package.

1. Exécutez la commande suivante dans la console:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Créer un package après la migration

Une fois la migration terminée, nous vous recommandons d’ajouter une référence au package NuGet [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) , puis d’utiliser [msbuild-t:Pack](../reference/msbuild-targets.md#pack-target) pour créer le package. Toutefois, dans certains scénarios, vous `dotnet.exe pack` pouvez utiliser `msbuild -t:pack`au lieu de, mais ce n’est pas recommandé.

## <a name="package-compatibility-issues"></a>Problèmes de compatibilité des packages

Certains aspects pris en charge dans les packages. config ne sont pas pris en charge dans PackageReference. L’outil de migration analyse et détecte de tels problèmes. Tout package ayant un ou plusieurs des problèmes suivants peut ne pas se comporter comme prévu après la migration.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>les scripts «install. ps1» sont ignorés lors de l’installation du package après la migration

| | |
| --- | --- |
| **Description** | Avec PackageReference, les scripts PowerShell install. ps1 et uninstall. ps1 ne sont pas exécutés lors de l’installation ou de la désinstallation d’un package. |
| **Impact potentiel** | Les packages qui dépendent de ces scripts pour configurer un comportement dans le projet de destination peuvent ne pas fonctionner comme prévu. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>les ressources «contenu» ne sont pas disponibles lors de l’installation du package après la migration

| | |
| --- | --- |
| **Description** | Les ressources dans le dossier `content` d’un package ne sont pas prises en charge avec PackageReference et sont ignorées. PackageReference ajoute la prise `contentFiles` en charge de à pour offrir un meilleur support transitif et du contenu partagé.  |
| **Impact potentiel** | Les éléments `content` multimédias de ne sont pas copiés dans le projet et le code de projet qui dépend de la présence de ces ressources requiert une refactorisation.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Les transformations XDT ne sont pas appliquées lorsque le package est installé après la mise à niveau

| | |
| --- | --- |
| **Description** | Les transformations xdt ne sont pas prises en `.xdt` charge avec PackageReference et les fichiers sont ignorés lors de l’installation ou de la désinstallation d’un package.   |
| **Impact potentiel** | Les transformations xdt ne sont pas appliquées aux fichiers XML de projet, le `web.config.install.xdt` plus `web.config.uninstall.xdt`souvent, et, ce qui` web.config` signifie que le fichier du projet n’est pas mis à jour lors de l’installation ou de la désinstallation du package. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Les assemblys dans la racine lib sont ignorés lors de l’installation du package après la migration

| | |
| --- | --- |
| **Description** | Avec PackageReference, les assemblys présents à la racine `lib` du dossier sans un sous-dossier spécifique au Framework cible sont ignorés. NuGet recherche un sous-dossier correspondant au moniker du Framework cible (TFM) correspondant au Framework cible du projet et installe les assemblys correspondants dans le projet. |
| **Impact potentiel** | Les packages qui n’ont pas de sous-dossier correspondant au moniker du Framework cible (TFM) correspondant au Framework cible du projet peuvent ne pas se comporter comme prévu après la transition ou l’échec de l’installation pendant la migration |

## <a name="found-an-issue-report-it"></a>Vous avez rencontré un problème? Rapport!

Si vous rencontrez un problème avec l’expérience de migration, veuillez [Envoyer un problème sur le dépôt github NuGet](https://github.com/NuGet/Home/issues/).
