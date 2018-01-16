---
title: Restauration des packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Explique comment NuGet restaure les packages dont dépend un projet, y compris comment désactiver la restauration et restreindre les versions."
keywords: "Restauration des packages NuGet, installation des packages NuGet, installation de package, restauration des packages, versions des dépendances, désactivation de la restauration automatique, restriction des versions de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a><span data-ttu-id="b1bfd-104">Restauration des packages</span><span class="sxs-lookup"><span data-stu-id="b1bfd-104">Package Restore</span></span>

<span data-ttu-id="b1bfd-105">Pour promouvoir un environnement de développement plus propre et pour réduire la taille du référentiel, la fonctionnalité de **restauration des packages** de NuGet installe tous les packages référencés avant la génération d’un projet.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="b1bfd-106">Cette fonctionnalité largement utilisée garantit la disponibilité de toutes les dépendances dans un projet, sans que les packages ne doivent être stockés dans le contrôle de code source (consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md) pour configurer votre référentiel de manière à exclure les fichiers binaires des packages).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="b1bfd-107">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-107">In this topic:</span></span>
- [<span data-ttu-id="b1bfd-108">Guide rapide pour restaurer des packages</span><span class="sxs-lookup"><span data-stu-id="b1bfd-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="b1bfd-109">Présentation de la restauration de package</span><span class="sxs-lookup"><span data-stu-id="b1bfd-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="b1bfd-110">Activation et désactivation de la restauration des packages</span><span class="sxs-lookup"><span data-stu-id="b1bfd-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="b1bfd-111">Restriction des versions de package avec la restauration</span><span class="sxs-lookup"><span data-stu-id="b1bfd-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="b1bfd-112">[Restauration en ligne de commande](#command-line-restore), pour toutes les versions de NuGet</span><span class="sxs-lookup"><span data-stu-id="b1bfd-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="b1bfd-113">[Restauration automatique dans Visual Studio](#automatic-restore-in-visual-studio), pour NuGet 2.7 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="b1bfd-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="b1bfd-114">[Restauration intégrée à MSBuild dans Visual Studio](#msbuild-integrated-restore), pour NuGet 2.6 et versions antérieures</span><span class="sxs-lookup"><span data-stu-id="b1bfd-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="b1bfd-115">Restauration des packages avec Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="b1bfd-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="b1bfd-116">Le comportement de restauration varie selon la version. Pour vérifier votre version de NuGet, exécutez `nuget.exe` sur la ligne de commande, puis regardez la première ligne de sortie.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="b1bfd-117">Pour plus d’informations concernant la restauration des packages sur les serveurs de builds, consultez [Restauration des packages avec TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="b1bfd-118">Les projets configurés pour la restauration de package fonctionnent également avec xbuild sur Mono.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="b1bfd-119">Guide rapide pour restaurer des packages</span><span class="sxs-lookup"><span data-stu-id="b1bfd-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="b1bfd-120">Si vous voyez l’erreur « Ce projet fait référence à des packages NuGet qui sont manquants sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », activez la restauration automatique en suivant les instructions de la section [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="b1bfd-121">Présentation de la restauration de package</span><span class="sxs-lookup"><span data-stu-id="b1bfd-121">Package restore overview</span></span>

<span data-ttu-id="b1bfd-122">Tout d’abord, les références de package sont conservées dans l’un des formats de gestion de package suivants, selon le type du projet et la version de NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="b1bfd-123">Notez que NuGet 4 et MSBuild 15.1 sont installés avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="b1bfd-124">Méthode</span><span class="sxs-lookup"><span data-stu-id="b1bfd-124">Method</span></span> | <span data-ttu-id="b1bfd-125">Version de NuGet</span><span class="sxs-lookup"><span data-stu-id="b1bfd-125">NuGet Version</span></span> | <span data-ttu-id="b1bfd-126">Description</span><span class="sxs-lookup"><span data-stu-id="b1bfd-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="b1bfd-127">2.x+</span><span class="sxs-lookup"><span data-stu-id="b1bfd-127">2.x+</span></span> | <span data-ttu-id="b1bfd-128">Répertorie l’ensemble complet de dépendances.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="b1bfd-129">Les packages ajoutés à `packages.config` doivent également être ajoutés au fichier projet, tout comme les cibles et les propriétés.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="b1bfd-130">Il s’agit de la méthode de référence pour toutes les versions de NuGet. Cependant, comparée aux autres options, cette méthode ralentit les performances</span><span class="sxs-lookup"><span data-stu-id="b1bfd-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="b1bfd-131">(consultez [Schéma packages.config](../schema/packages-config.md)).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="b1bfd-132">3.x+</span><span class="sxs-lookup"><span data-stu-id="b1bfd-132">3.x+</span></span> | <span data-ttu-id="b1bfd-133">Utilisé uniquement par défaut avec les projets UWP. Toutefois, les projets peuvent être convertis à partir de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="b1bfd-134">`project.json` répertorie uniquement les dépendances de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="b1bfd-135">Les références, les cibles et les propriétés sont ajoutées dynamiquement au projet lors de la génération, ce qui permet de meilleures performances par rapport à `packages.config`</span><span class="sxs-lookup"><span data-stu-id="b1bfd-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="b1bfd-136">(consultez [Schéma project.json](../schema/project-json.md)).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="b1bfd-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="b1bfd-137">PackageReference</span></span> | <span data-ttu-id="b1bfd-138">4.x+</span><span class="sxs-lookup"><span data-stu-id="b1bfd-138">4.x+</span></span> | <span data-ttu-id="b1bfd-139">Répertorie les dépendances directement dans le fichier projet, dans le nœud `<PackageReference>`, en même temps que `<Reference>` et `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="b1bfd-140">Son fonctionnement est similaire à celui de `project.json`. Consultez [Références de package dans les fichiers projet](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="b1bfd-141">Ensuite, vous pouvez démarrer une restauration à l’aide de la liste de références de plusieurs façons :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="b1bfd-142">À partir de la ligne de commande ou dans la [console du gestionnaire de package](../tools/Package-Manager-Console.md) :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="b1bfd-143">Commande</span><span class="sxs-lookup"><span data-stu-id="b1bfd-143">Command</span></span> | <span data-ttu-id="b1bfd-144">Scénarios applicables</span><span class="sxs-lookup"><span data-stu-id="b1bfd-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="b1bfd-145">Toutes les versions de NuGet et tous les types référence.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="b1bfd-146">Consultez [Restauration en ligne de commande](#command-line-restore) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="b1bfd-147">Comme avec `nuget restore` pour les projets .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="b1bfd-148">Consultez [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-148">See [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="b1bfd-149">NuGet 4.x+ et MSBuild 15.1+ avec les [références de package dans les fichiers projet](../Consume-Packages/Package-References-in-Project-Files.md) uniquement.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="b1bfd-150">`nuget restore` et `dotnet restore` utilisent cette commande pour les projets applicables.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="b1bfd-151">Consultez [Commandes pack et restore NuGet comme cibles MSBuild - restore target](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="b1bfd-152">Visual Studio restaure également des packages à différents moments :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="b1bfd-153">Type</span><span class="sxs-lookup"><span data-stu-id="b1bfd-153">Type</span></span> | <span data-ttu-id="b1bfd-154">Moment de la restauration</span><span class="sxs-lookup"><span data-stu-id="b1bfd-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="b1bfd-155">Restauration de modèle</span><span class="sxs-lookup"><span data-stu-id="b1bfd-155">Template restore</span></span> | <span data-ttu-id="b1bfd-156">Lors de la création d’un projet, puisque certains modèles dépendent de packages externes.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="b1bfd-157">Restauration de build</span><span class="sxs-lookup"><span data-stu-id="b1bfd-157">Build restore</span></span> | <span data-ttu-id="b1bfd-158">La première étape d’une génération.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-158">As the first step of a build.</span></span> |
| <span data-ttu-id="b1bfd-159">Restauration de solution</span><span class="sxs-lookup"><span data-stu-id="b1bfd-159">Solution restore</span></span> | <span data-ttu-id="b1bfd-160">Lorsque l’utilisateur clique avec le bouton droit sur une solution et sélectionne **Restaurer des packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="b1bfd-161">Restauration après modification du projet</span><span class="sxs-lookup"><span data-stu-id="b1bfd-161">Restore on project change</span></span> | <span data-ttu-id="b1bfd-162">*(NuGet 4.x uniquement)* Quand un projet basé sur le SDK .NET Core est utilisé, y compris lorsque l’état du projet change.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="b1bfd-163">Activation et désactivation de la restauration des packages</span><span class="sxs-lookup"><span data-stu-id="b1bfd-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="b1bfd-164">La restauration du package est généralement activée via **Outils > Options > Gestionnaire de package NuGet** dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Contrôle du comportement de la restauration de package via les options du gestionnaire de package NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="b1bfd-166">**Autoriser NuGet à télécharger les packages manquants** : contrôle toutes les formes de restauration de package, en modifiant la valeur du paramètre `packageRestore/enabled` dans le fichier `%AppData%\NuGet\NuGet.Config`, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="b1bfd-167">Le paramètre `packageRestore/enabled` peut être remplacé globalement en définissant une variable d’environnement appelée **EnableNuGetPackageRestore** sur la valeur TRUE ou FALSE, avant le lancement de Visual Studio ou le démarrage d’une génération.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="b1bfd-168">**Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** : contrôle la restauration automatique pour NuGet 2.7 et versions ultérieures, en modifiant la valeur du paramètre `packageRestore/automatic` dans le fichier `%AppData%\NuGet\NuGet.Config`, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="b1bfd-169">Pour référence, consultez [Fichier config NuGet - Section packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="b1bfd-170">Dans certains cas, un développeur ou une société peuvent vouloir activer ou désactiver la restauration de package sur un ordinateur par défaut pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="b1bfd-171">Pour cela, ajoutez les paramètres ci-dessus au fichier de configuration NuGet global situé dans `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="b1bfd-172">Chaque utilisateur peut ensuite activer la restauration au niveau d’un projet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="b1bfd-173">Pour plus d’informations sur la façon dont NuGet hiérarchise les fichiers de configuration, consultez [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="b1bfd-174">Restriction des versions de package avec la restauration</span><span class="sxs-lookup"><span data-stu-id="b1bfd-174">Constraining package versions with restore</span></span>

<span data-ttu-id="b1bfd-175">Lorsque NuGet restaure des packages avec l’une des méthodes disponibles, il respecte toutes les restrictions spécifiées dans `packages.config`, `project.json` ou le fichier projet :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="b1bfd-176">`packages.config` : permet de spécifier une plage de versions dans la propriété `allowedVersion` de la dépendance.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="b1bfd-177">Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="b1bfd-178">Exemple :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="b1bfd-179">`project.json` : permet de spécifier une plage de versions directement avec le numéro de version de la dépendance.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="b1bfd-180">Exemple :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="b1bfd-181">Références de package dans les fichiers projet : spécifiez une plage de versions directement avec le numéro de version de la dépendance.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="b1bfd-182">Exemple :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="b1bfd-183">Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="b1bfd-184">Restauration en ligne de commande</span><span class="sxs-lookup"><span data-stu-id="b1bfd-184">Command-line restore</span></span>

<span data-ttu-id="b1bfd-185">Pour NuGet 2.7 et versions ultérieures, utilisez la commande [Restore](../tools/cli-ref-restore.md) pour restaurer tous les packages d’une solution (qu’elle utilise `packages.config`, `project.json` ou les références de package dans les fichiers projet).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="b1bfd-186">Pour un dossier de projet donné comme `c:\proj\app`, chacune des variations courantes ci-dessous restaure les packages :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="b1bfd-187">Pour NuGet 4.0+ et MSBuild 15.1+, vous pouvez également utiliser `MSBuild /t:restore`, comme décrit dans [Commandes pack et restore NuGet comme cibles MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="b1bfd-188">Restauration au moment de la génération dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b1bfd-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="b1bfd-189">Par défaut, Visual Studio restaure automatiquement les packages manquants au début d’une génération.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="b1bfd-190">Ce comportement peut être modifié en désactivant l’option **Outils > Options > Gestionnaire de package NuGet > Général > Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="b1bfd-191">Lorsqu’elle est activée, la restauration automatique fonctionne de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="b1bfd-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="b1bfd-192">Lorsqu’une génération démarre, Visual Studio indique à NuGet de restaurer les packages.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="b1bfd-193">NuGet recherche de manière récursive tous les fichiers `packages.config` dans la solution, recherche `project.json`, ou effectue une recherche dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="b1bfd-194">Pour chaque package répertorié dans les fichiers de référence, NuGet vérifie s’il existe déjà dans la solution (le dossier `packages`, `project.lock.json` ou `project.assets.json`, selon que le projet utilise `packages.config`, `project.json` ou les références de package des fichiers projet).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="b1bfd-195">Si le package est introuvable, NuGet tente tout d’abord de le récupérer à partir de son cache (consultez [Gestion du cache NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="b1bfd-196">Si le package ne se trouve pas dans le cache, NuGet tente de télécharger le package à partir des sources activées qui figurent sous **Outils > Options > Gestionnaire de package NuGet > Sources de package**, en suivant l’ordre dans lequel apparaissent les sources.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="b1bfd-197">Dans ce cas, NuGet n’indique pas que le package est introuvable tant que toutes les sources n’ont pas été vérifiées. Une fois toutes les sources vérifiées, le package est signalé comme étant introuvable dans la dernière source de la liste.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="b1bfd-198">Cependant, cette erreur signifie également que le package ne se trouvait dans aucune autre source, même si aucune erreur ne s’est affichée pour les autres sources.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="b1bfd-199">Si le téléchargement réussit, NuGet met en cache le package et l’installe dans la solution (là encore, dans le dossier `packages`, dans `project.lock.json` ou dans ou `project.assets.json`). Sinon, NuGet échoue, ainsi que la génération.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="b1bfd-200">Durant ce processus, une boîte de dialogue de progression s’affiche, avec une option permettant d’annuler la restauration du package.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="b1bfd-201">Restauration des packages avec Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="b1bfd-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="b1bfd-202">La restauration de package est couramment utilisée lors de la génération de projets sur des serveurs de builds, ainsi qu’avec Team Foundation Server (TFS) et Visual Studio Team Services (et d’autres systèmes de génération, qui ne sont pas abordés ici).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="b1bfd-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="b1bfd-203">Visual Studio Team Services</span></span>

<span data-ttu-id="b1bfd-204">Lorsque vous créez une définition de build dans Team Services, vous devez inclure la tâche Restaurer les packages NuGet dans la définition avant de procéder à toute tâche de génération.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="b1bfd-205">Cette tâche est incluse par défaut dans plusieurs modèles de build.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-205">This task is included by default in a number of build templates.</span></span>

![Tâche de restauration de package NuGet dans une définition de build Visual Studio Team Services](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="b1bfd-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="b1bfd-207">Team Foundation Server</span></span>

<span data-ttu-id="b1bfd-208">Avec TFS 2013 et versions ultérieures, les packages sont automatiquement restaurés par défaut lors de la génération, sous réserve que vous utilisiez un modèle Team Build pour Team Foundation Server 2013 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="b1bfd-209">Si vous utilisez une version antérieure des modèles de build (par exemple, dans un projet qui a été migré à partir de versions antérieures de TFS), vous devrez également migrer les modèles de build vers TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="b1bfd-210">Autrement dit, vous allez recréer les parties personnalisées des modèles de build à l’aide du modèle adapté à votre contrôle de code source (TFVC ou Git).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="b1bfd-211">Pour les versions antérieures de TFS, vous pouvez simplement inclure une étape de génération destinée à appeler une [restauration en ligne de commande](#command-line-restore), comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="b1bfd-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="b1bfd-212">Pour plus d’informations, consultez [Procédure pas à pas pour la restauration des packages NuGet avec Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="b1bfd-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
