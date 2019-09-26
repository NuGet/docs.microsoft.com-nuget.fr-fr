---
title: Migration du format package.config au format PackageReference
description: Détails sur la migration d'un projet du format de gestion package.config vers le format PackageReference dans le cadre de la prise en charge par NuGet 4.0+ et VS2017 et .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 6f659af6b09a12be54a5ef843d34f956119b33f4
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520489"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="234f5-103">Migrer de packages.config vers PackageReference</span><span class="sxs-lookup"><span data-stu-id="234f5-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="234f5-104">Visual Studio 2017 15.7 ou version ultérieure prend en charge la migration d'un projet du format de gestion [packages.config](../reference/packages-config.md) vers le format [PackageReference](../consume-packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="234f5-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](../reference/packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="234f5-105">Avantages de l’utilisation de PackageReference</span><span class="sxs-lookup"><span data-stu-id="234f5-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="234f5-106">**Gestion de toutes les dépendances du projet depuis un même endroit** : Tout comme les références de projet à projet et les références d'assembly, les références de packages NuGet (utilisant le nœud `PackageReference`) sont gérées directement dans des fichiers de projet plutôt que dans un fichier packages.config distinct.</span><span class="sxs-lookup"><span data-stu-id="234f5-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="234f5-107">**Vue épurée des dépendances de niveau supérieur** : Contrairement au format packages.config, PackageReference répertorie uniquement les packages NuGet que vous avez installés directement dans le projet.</span><span class="sxs-lookup"><span data-stu-id="234f5-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="234f5-108">Ainsi, l'interface utilisateur de NuGet Package Manager et le fichier projet ne sont pas encombrés de dépendances de niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="234f5-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="234f5-109">**Amélioration des performances** : Si le format PackageReference est utilisé, les packages sont conservés dans le dossier *global-packages* (comme l’explique l’article [Gérer les dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md)) plutôt que dans un dossier `packages` au sein de la solution.</span><span class="sxs-lookup"><span data-stu-id="234f5-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="234f5-110">En conséquence, PackageReference est plus rapide et consomme moins d'espace disque.</span><span class="sxs-lookup"><span data-stu-id="234f5-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="234f5-111">**Contrôle précis des dépendances et du flux de contenu** : L'utilisation des fonctionnalités existantes de MSBuild vous permet de [ référencer conditionnellement un package NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) et de choisir des références de packages par framework cible, configuration, plate-forme ou autres pivots.</span><span class="sxs-lookup"><span data-stu-id="234f5-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="234f5-112">**PackageReference est en cours de développement** : Voir [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements) (Problèmes relatifs à PackageReference sur GitHub).</span><span class="sxs-lookup"><span data-stu-id="234f5-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="234f5-113">packages.config n’est plus en cours de développement.</span><span class="sxs-lookup"><span data-stu-id="234f5-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="234f5-114">Limitations</span><span class="sxs-lookup"><span data-stu-id="234f5-114">Limitations</span></span>

* <span data-ttu-id="234f5-115">NuGet PackageReference n'est pas disponible dans Visual Studio 2015 et versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="234f5-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="234f5-116">Les projets migrés ne peuvent être ouverts que dans Visual Studio 2017 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="234f5-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="234f5-117">La migration n’est actuellement pas possible pour les projets C++ et ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="234f5-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="234f5-118">Certains packages peuvent ne pas être entièrement compatibles avec PackageReference.</span><span class="sxs-lookup"><span data-stu-id="234f5-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="234f5-119">Pour plus d’informations, voir la section [Problèmes de compatibilité des packages](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="234f5-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="234f5-120">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="234f5-120">Known Issues</span></span>

1. <span data-ttu-id="234f5-121">L’option `Migrate packages.config to PackageReference...` n’est pas disponible dans le menu contextuel</span><span class="sxs-lookup"><span data-stu-id="234f5-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="234f5-122">Problème</span><span class="sxs-lookup"><span data-stu-id="234f5-122">Issue</span></span> 
 
<span data-ttu-id="234f5-123">À la première ouverture d’un projet, il peut arriver que NuGet ne s’initialise pas tant qu’aucune opération NuGet n’a été réalisée.</span><span class="sxs-lookup"><span data-stu-id="234f5-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="234f5-124">Dans ce cas, l’option de migration ne s’affiche pas dans le menu contextuel sur `packages.config` ou `References`.</span><span class="sxs-lookup"><span data-stu-id="234f5-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="234f5-125">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="234f5-125">Workaround</span></span> 

<span data-ttu-id="234f5-126">Effectuez l’une des actions NuGet suivantes :</span><span class="sxs-lookup"><span data-stu-id="234f5-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="234f5-127">Ouvrez l’interface utilisateur du Gestionnaire de package : cliquez avec le bouton droit sur `References` et sélectionnez `Manage NuGet Packages...`.</span><span class="sxs-lookup"><span data-stu-id="234f5-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="234f5-128">Ouvrez la console du Gestionnaire de package : dans `Tools > NuGet Package Manager`, sélectionnez `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="234f5-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="234f5-129">Exécutez la restauration NuGet : cliquez avec le bouton droit sur le nœud de la solution dans l’Explorateur de solutions, puis sélectionnez `Restore NuGet Packages`.</span><span class="sxs-lookup"><span data-stu-id="234f5-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="234f5-130">Générez le projet qui déclenche également la restauration NuGet.</span><span class="sxs-lookup"><span data-stu-id="234f5-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="234f5-131">L’option de migration devrait apparaître.</span><span class="sxs-lookup"><span data-stu-id="234f5-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="234f5-132">Notez qu’elle n’est pas prise en charge et ne s’affiche pas pour les types de projets ASP.NET et C++.</span><span class="sxs-lookup"><span data-stu-id="234f5-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="234f5-133">Étapes de la migration</span><span class="sxs-lookup"><span data-stu-id="234f5-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="234f5-134">Avant le début de la migration, Visual Studio crée une sauvegarde du projet pour vous permettre de [retourner au format packages.config](#how-to-roll-back-to-packagesconfig) si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="234f5-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="234f5-135">Ouvrez une solution contenant un projet en utilisant `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="234f5-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="234f5-136">Dans **Explorateur de solutions**, cliquez avec le bouton droit de la souris sur le nœud **Références** ou sur le fichier `packages.config`, puis sélectionnez **Migrer packages.config vers PackageReference**.</span><span class="sxs-lookup"><span data-stu-id="234f5-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="234f5-137">Le migrateur analyse les références des packages NuGet du projet et tente de les classer dans la catégorie des **dépendances de niveau supérieur** (packages NuGet que vous avez installés directement) et des **dépendances transitoires** (packages qui ont été installés en tant que dépendances de packages de niveau supérieur).</span><span class="sxs-lookup"><span data-stu-id="234f5-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="234f5-138">PackageReference prend en charge la restauration des packages transitifs et résout les dépendances de manière dynamique, ce qui signifie que les dépendances transitives n'ont pas à être installées explicitement.</span><span class="sxs-lookup"><span data-stu-id="234f5-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="234f5-139">(Facultatif) Vous pouvez traiter un package NuGet classé comme une dépendance transitive en tant que dépendance de niveau supérieur en sélectionnant l'option **Top-Level** (niveau supérieur) pour ce package.</span><span class="sxs-lookup"><span data-stu-id="234f5-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="234f5-140">Cette option est automatiquement définie pour les packages contenant des ressources qui ne s'exécutent pas de manière transitoire (celles des dossiers `build`, `buildCrossTargeting`, `contentFiles` ou `analyzers`) et celles marquées comme des dépendances de développement (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="234f5-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="234f5-141">Vérifiez les éventuels [problèmes de compatibilité des packages](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="234f5-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="234f5-142">Sélectionnez **OK** pour commencer la migration.</span><span class="sxs-lookup"><span data-stu-id="234f5-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="234f5-143">À la fin de la migration, Visual Studio fournit un rapport indiquant un chemin d'accès à la sauvegarde, la liste des packages installés (dépendances de niveau supérieur), une liste des packages référencés comme dépendances transitives, et une liste des problèmes de compatibilité identifiés au début de la migration.</span><span class="sxs-lookup"><span data-stu-id="234f5-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="234f5-144">Le rapport est enregistré dans le dossier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="234f5-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="234f5-145">Vérifiez la génération et l’exécution de la solution.</span><span class="sxs-lookup"><span data-stu-id="234f5-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="234f5-146">Si vous rencontrez des problèmes, [signalez-les sur GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="234f5-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="234f5-147">Revenir à packages.config</span><span class="sxs-lookup"><span data-stu-id="234f5-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="234f5-148">Fermez le projet migré.</span><span class="sxs-lookup"><span data-stu-id="234f5-148">Close the migrated project.</span></span>

1. <span data-ttu-id="234f5-149">Copiez le fichier projet et `packages.config` de la sauvegarde (généralement `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) dans le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="234f5-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="234f5-150">Supprimez le dossier obj s'il existe dans le répertoire racine du projet.</span><span class="sxs-lookup"><span data-stu-id="234f5-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="234f5-151">Ouvrez le projet.</span><span class="sxs-lookup"><span data-stu-id="234f5-151">Open the project.</span></span>

1. <span data-ttu-id="234f5-152">Ouvrez la Console du Gestionnaire de package à partir de la commande de menu **Outils > Gestionnaire de package NuGet > Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="234f5-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="234f5-153">Exécutez la commande suivante dans la console :</span><span class="sxs-lookup"><span data-stu-id="234f5-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="234f5-154">Créer un package après la migration</span><span class="sxs-lookup"><span data-stu-id="234f5-154">Create a package after migration</span></span>

<span data-ttu-id="234f5-155">Une fois la migration terminée, nous vous recommandons d'ajouter une référence au package nuget [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack), puis d'utiliser [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="234f5-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="234f5-156">Bien que certains scénarios vous permettent d’utiliser `dotnet.exe pack` au lieu de `msbuild -t:pack`, cette méthode n'est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="234f5-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="234f5-157">Problèmes de compatibilité des packages</span><span class="sxs-lookup"><span data-stu-id="234f5-157">Package compatibility issues</span></span>

<span data-ttu-id="234f5-158">Certains aspects autrefois pris en charge dans packages.config ne le sont plus dans PackageReference.</span><span class="sxs-lookup"><span data-stu-id="234f5-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="234f5-159">Le migrateur analyse et détecte ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="234f5-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="234f5-160">Tout package présentant un ou plusieurs des problèmes suivants risque de ne pas se comporter comme prévu après la migration.</span><span class="sxs-lookup"><span data-stu-id="234f5-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="234f5-161">Les scripts « install.ps1 » sont ignorés lorsque le package est installé après la migration</span><span class="sxs-lookup"><span data-stu-id="234f5-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="234f5-162">**Description**</span><span class="sxs-lookup"><span data-stu-id="234f5-162">**Description**</span></span> | <span data-ttu-id="234f5-163">Avec PackageReference, les scripts PowerShell install.ps1 et uninstall.ps1 ne sont pas exécutés pendant l'installation ou la désinstallation d'un package.</span><span class="sxs-lookup"><span data-stu-id="234f5-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="234f5-164">**Impact potentiel**</span><span class="sxs-lookup"><span data-stu-id="234f5-164">**Potential impact**</span></span> | <span data-ttu-id="234f5-165">Les packages qui dépendent de ces scripts pour configurer certains comportements dans le projet de destination peuvent ne pas fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="234f5-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="234f5-166">Les ressources « content » sont ignorées lorsque le package est installé après la migration</span><span class="sxs-lookup"><span data-stu-id="234f5-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="234f5-167">**Description**</span><span class="sxs-lookup"><span data-stu-id="234f5-167">**Description**</span></span> | <span data-ttu-id="234f5-168">Les ressources du dossier `content` d'un package ne sont pas prises en charge par PackageReference et sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="234f5-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="234f5-169">PackageReference ajoute la prise en charge de `contentFiles` pour permettre une meilleure prise en charge transitive et le partage de contenu.</span><span class="sxs-lookup"><span data-stu-id="234f5-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="234f5-170">**Impact potentiel**</span><span class="sxs-lookup"><span data-stu-id="234f5-170">**Potential impact**</span></span> | <span data-ttu-id="234f5-171">les ressources dans `content` ne sont pas copiées dans le projet et le code de projet qui dépend de la présence de ces ressources nécessite une refactorisation.</span><span class="sxs-lookup"><span data-stu-id="234f5-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="234f5-172">Les transformations XDT ne sont pas appliquées lorsque le package est installé après la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="234f5-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="234f5-173">**Description**</span><span class="sxs-lookup"><span data-stu-id="234f5-173">**Description**</span></span> | <span data-ttu-id="234f5-174">Les transformations XDT ne sont pas prises en charge avec PackageReference et les fichiers `.xdt` sont ignorés lors de l'installation ou de la désinstallation d'un package.</span><span class="sxs-lookup"><span data-stu-id="234f5-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="234f5-175">**Impact potentiel**</span><span class="sxs-lookup"><span data-stu-id="234f5-175">**Potential impact**</span></span> | <span data-ttu-id="234f5-176">les transformations XDT ne sont appliquées à aucun fichier XML du projet, le plus souvent, `web.config.install.xdt` et `web.config.uninstall.xdt`, ce qui signifie que le fichier ` web.config` du projet n'est pas mis à jour lorsque le package est installé ou désinstallé.</span><span class="sxs-lookup"><span data-stu-id="234f5-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="234f5-177">Les assemblys à la racine de la bibliothèque sont ignorés lorsque le package est installé après la migration</span><span class="sxs-lookup"><span data-stu-id="234f5-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="234f5-178">**Description**</span><span class="sxs-lookup"><span data-stu-id="234f5-178">**Description**</span></span> | <span data-ttu-id="234f5-179">Avec PackageReference, les assemblys présents à la racine du dossier `lib` sans sous-dossier spécifique au framework cible sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="234f5-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="234f5-180">NuGet recherche un sous-dossier correspondant au moniker de framework cible (TFM) pour le framework cible du projet, puis installe les assemblys correspondants dans le projet.</span><span class="sxs-lookup"><span data-stu-id="234f5-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="234f5-181">**Impact potentiel**</span><span class="sxs-lookup"><span data-stu-id="234f5-181">**Potential impact**</span></span> | <span data-ttu-id="234f5-182">Les packages sans sous-dossier correspondant au moniker de framework cible (TFM) pour le framework cible du projet peuvent ne pas se comporter comme prévu après la transition, ou l'installation peut échouer pendant la migration</span><span class="sxs-lookup"><span data-stu-id="234f5-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="234f5-183">Vous avez rencontré un problème ?</span><span class="sxs-lookup"><span data-stu-id="234f5-183">Found an issue?</span></span> <span data-ttu-id="234f5-184">Signalez-le !</span><span class="sxs-lookup"><span data-stu-id="234f5-184">Report it!</span></span>

<span data-ttu-id="234f5-185">Si vous rencontrez un problème avec l'expérience de migration, veuillez [signaler ce problème sur le référentiel NuGet GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="234f5-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>