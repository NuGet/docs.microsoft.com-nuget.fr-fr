---
title: NuGet empaqueter et restaurer en tant que MSBuild cibles
description: NuGet la fonction Pack et la restauration peuvent fonctionner directement en tant que MSBuild cibles avec NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 47411641db47884f79f2bc9a4aa00035fc79993b
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387372"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="58e13-103">NuGet empaqueter et restaurer en tant que MSBuild cibles</span><span class="sxs-lookup"><span data-stu-id="58e13-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="58e13-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="58e13-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="58e13-105">Avec le format [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + peut stocker toutes les métadonnées de manifeste directement dans un fichier projet plutôt que d’utiliser un `.nuspec` fichier séparé.</span><span class="sxs-lookup"><span data-stu-id="58e13-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="58e13-106">Avec MSBuild 15.1 +, NuGet est également un citoyen de première classe MSBuild avec les `pack` cibles et, `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="58e13-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="58e13-107">Ces cibles vous permettent de travailler avec NuGet n’importe quelle autre MSBuild tâche ou cible.</span><span class="sxs-lookup"><span data-stu-id="58e13-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="58e13-108">Pour obtenir des instructions sur la création d’un NuGet package à l’aide de MSBuild , consultez [créer un NuGet package à l’aide MSBuild de ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="58e13-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="58e13-109">(Pour NuGet 3. x et versions antérieures, vous utilisez à la place les commandes [Pack](../reference/cli-reference/cli-ref-pack.md) et [Restore](../reference/cli-reference/cli-ref-restore.md) dans l' NuGet interface CLI.)</span><span class="sxs-lookup"><span data-stu-id="58e13-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="58e13-110">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="58e13-110">Target build order</span></span>

<span data-ttu-id="58e13-111">Étant donné que `pack` et `restore` sont des  MSBuild cibles, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="58e13-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="58e13-112">Par exemple, imaginons que vous souhaitiez copier votre package sur un partage réseau après l’avoir compressé.</span><span class="sxs-lookup"><span data-stu-id="58e13-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="58e13-113">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="58e13-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="58e13-114">De même, vous pouvez écrire une MSBuild tâche, écrire votre propre cible et utiliser NuGet les propriétés de la MSBuild tâche.</span><span class="sxs-lookup"><span data-stu-id="58e13-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="58e13-115">`$(OutputPath)` est relatif et s’attend à ce que vous exécutiez la commande à partir de la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="58e13-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="58e13-116">Cible pack</span><span class="sxs-lookup"><span data-stu-id="58e13-116">pack target</span></span>

<span data-ttu-id="58e13-117">Pour les projets .NET qui utilisent le `PackageReference` format, l’utilisation de `msbuild -t:pack` dessine des entrées à partir du fichier projet à utiliser lors de la création d’un NuGet Package.</span><span class="sxs-lookup"><span data-stu-id="58e13-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="58e13-118">Le tableau suivant décrit les MSBuild propriétés qui peuvent être ajoutées à un fichier projet au sein du premier `<PropertyGroup>` nœud.</span><span class="sxs-lookup"><span data-stu-id="58e13-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="58e13-119">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="58e13-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="58e13-120">Pour plus de commodité, la table est organisée par la propriété équivalente dans un [ `.nuspec` fichier](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="58e13-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="58e13-121">`Owners` les `Summary` Propriétés et de `.nuspec` ne sont pas prises en charge avec MSBuild .</span><span class="sxs-lookup"><span data-stu-id="58e13-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="58e13-122">Attribut/ nuspec valeur</span><span class="sxs-lookup"><span data-stu-id="58e13-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="58e13-123">PropriétéMSBuild</span><span class="sxs-lookup"><span data-stu-id="58e13-123">MSBuild Property</span></span> | <span data-ttu-id="58e13-124">Default</span><span class="sxs-lookup"><span data-stu-id="58e13-124">Default</span></span> | <span data-ttu-id="58e13-125">Notes</span><span class="sxs-lookup"><span data-stu-id="58e13-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="58e13-126">`$(AssemblyName)` à partir de MSBuild</span><span class="sxs-lookup"><span data-stu-id="58e13-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="58e13-127">Version</span><span class="sxs-lookup"><span data-stu-id="58e13-127">Version</span></span> | <span data-ttu-id="58e13-128">Il s’agit d’une compatibilité semver, par exemple, `1.0.0` `1.0.0-beta` ou `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="58e13-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="58e13-129">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-129">empty</span></span> | <span data-ttu-id="58e13-130">Paramétrage des `PackageVersion` remplacements `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="58e13-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="58e13-131">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-131">empty</span></span> | <span data-ttu-id="58e13-132">`$(VersionSuffix)` à partir de MSBuild .</span><span class="sxs-lookup"><span data-stu-id="58e13-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="58e13-133">Paramétrage des `PackageVersion` remplacements `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="58e13-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="58e13-134">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="58e13-134">Username of the current user</span></span> | <span data-ttu-id="58e13-135">Liste délimitée par des points-virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la NuGet Galerie sur NuGet.org et sont utilisés pour faire référence croisée aux packages par les mêmes auteurs.</span><span class="sxs-lookup"><span data-stu-id="58e13-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="58e13-136">N/A</span><span class="sxs-lookup"><span data-stu-id="58e13-136">N/A</span></span> | <span data-ttu-id="58e13-137">Non présent dans nuspec</span><span class="sxs-lookup"><span data-stu-id="58e13-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="58e13-138">`PackageId`.</span><span class="sxs-lookup"><span data-stu-id="58e13-138">The `PackageId`</span></span> | <span data-ttu-id="58e13-139">Titre convivial du package, généralement utilisé dans les affichages de l’interface utilisateur comme sur nuget.org et dans le gestionnaire de package de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58e13-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="58e13-140">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="58e13-140">"Package Description"</span></span> | <span data-ttu-id="58e13-141">Description longue de l'assembly.</span><span class="sxs-lookup"><span data-stu-id="58e13-141">A long description for the assembly.</span></span> <span data-ttu-id="58e13-142">Si `PackageDescription` n’est pas spécifié, cette propriété est également utilisée comme description du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="58e13-143">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-143">empty</span></span> | <span data-ttu-id="58e13-144">Détails de copyright pour le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="58e13-145">Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="58e13-146">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-146">empty</span></span> | <span data-ttu-id="58e13-147">Correspond à `<license type="expression">`.</span><span class="sxs-lookup"><span data-stu-id="58e13-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="58e13-148">Consultez [compression d’une expression de licence ou d’un fichier de licence](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="58e13-149">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-149">empty</span></span> | <span data-ttu-id="58e13-150">Chemin d’accès à un fichier de licence dans le package si vous utilisez une licence personnalisée ou une licence à laquelle aucun identificateur SPDX n’a été affecté.</span><span class="sxs-lookup"><span data-stu-id="58e13-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="58e13-151">Vous devez explicitement compresser le fichier de licence référencé.</span><span class="sxs-lookup"><span data-stu-id="58e13-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="58e13-152">Correspond à `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="58e13-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="58e13-153">Consultez [compression d’une expression de licence ou d’un fichier de licence](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="58e13-154">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-154">empty</span></span> | <span data-ttu-id="58e13-155">`PackageLicenseUrl` est déconseillé.</span><span class="sxs-lookup"><span data-stu-id="58e13-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="58e13-156">Utilisez `PackageLicenseExpression` ou `PackageLicenseFile` à la place.</span><span class="sxs-lookup"><span data-stu-id="58e13-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="58e13-157">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="58e13-158">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-158">empty</span></span> | <span data-ttu-id="58e13-159">Chemin d’accès à une image dans le package à utiliser comme icône de package.</span><span class="sxs-lookup"><span data-stu-id="58e13-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="58e13-160">Vous devez explicitement compresser le fichier image icône référencé.</span><span class="sxs-lookup"><span data-stu-id="58e13-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="58e13-161">Pour plus d’informations, consultez [compression d’un fichier image d’icône](#packing-an-icon-image-file) et de [ `icon` métadonnées](./nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="58e13-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="58e13-162">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-162">empty</span></span> | <span data-ttu-id="58e13-163">`PackageIconUrl` est déconseillé en faveur de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="58e13-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="58e13-164">Toutefois, pour une expérience de niveau inférieur, vous devez spécifier `PackageIconUrl` en plus de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="58e13-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="58e13-165">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-165">empty</span></span> | <span data-ttu-id="58e13-166">Vous devez explicitement compresser le fichier Lisez-moi référencé.</span><span class="sxs-lookup"><span data-stu-id="58e13-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="58e13-167">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-167">empty</span></span> | <span data-ttu-id="58e13-168">Liste de balises séparées par un point-virgule qui désigne le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="58e13-169">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-169">empty</span></span> | <span data-ttu-id="58e13-170">Notes de publication du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="58e13-171">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-171">empty</span></span> | <span data-ttu-id="58e13-172">URL du référentiel utilisée pour cloner ou récupérer le code source.</span><span class="sxs-lookup"><span data-stu-id="58e13-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="58e13-173">Exemple : *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="58e13-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="58e13-174">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-174">empty</span></span> | <span data-ttu-id="58e13-175">Type de référentiel.</span><span class="sxs-lookup"><span data-stu-id="58e13-175">Repository type.</span></span> <span data-ttu-id="58e13-176">Exemples : `git` (valeur par défaut), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="58e13-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="58e13-177">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-177">empty</span></span> | <span data-ttu-id="58e13-178">Informations de branche de référentiel facultatives.</span><span class="sxs-lookup"><span data-stu-id="58e13-178">Optional repository branch information.</span></span> <span data-ttu-id="58e13-179">`RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="58e13-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="58e13-180">Exemple : *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="58e13-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="58e13-181">empty</span><span class="sxs-lookup"><span data-stu-id="58e13-181">empty</span></span> | <span data-ttu-id="58e13-182">Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré.</span><span class="sxs-lookup"><span data-stu-id="58e13-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="58e13-183">`RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="58e13-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="58e13-184">Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="58e13-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="58e13-185">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="58e13-185">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="58e13-186">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="58e13-186">pack target inputs</span></span>

| <span data-ttu-id="58e13-187">Propriété</span><span class="sxs-lookup"><span data-stu-id="58e13-187">Property</span></span> | <span data-ttu-id="58e13-188">Description</span><span class="sxs-lookup"><span data-stu-id="58e13-188">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="58e13-189">Valeur booléenne qui spécifie si le projet peut être compressé.</span><span class="sxs-lookup"><span data-stu-id="58e13-189">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="58e13-190">La valeur par défaut est `true`.</span><span class="sxs-lookup"><span data-stu-id="58e13-190">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="58e13-191">Affectez `true` la valeur pour supprimer les dépendances de package du NuGet package généré.</span><span class="sxs-lookup"><span data-stu-id="58e13-191">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="58e13-192">Spécifie la version du package obtenu.</span><span class="sxs-lookup"><span data-stu-id="58e13-192">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="58e13-193">Accepte toutes les formes de la NuGet chaîne de version.</span><span class="sxs-lookup"><span data-stu-id="58e13-193">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="58e13-194">La valeur par défaut est la valeur de `$(Version)`, autrement dit, de la propriété `Version` dans le projet.</span><span class="sxs-lookup"><span data-stu-id="58e13-194">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="58e13-195">Spécifie le nom du package obtenu.</span><span class="sxs-lookup"><span data-stu-id="58e13-195">Specifies the name for the resulting package.</span></span> <span data-ttu-id="58e13-196">Si non spécifié, l’opération `pack` utilise par défaut le `AssemblyName` ou le nom du répertoire comme nom du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-196">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="58e13-197">Description longue du package pour l’affichage de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58e13-197">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="58e13-198">Liste délimitée par des points-virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la NuGet Galerie sur NuGet.org et sont utilisés pour faire référence croisée aux packages par les mêmes auteurs.</span><span class="sxs-lookup"><span data-stu-id="58e13-198">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="58e13-199">Description longue de l'assembly.</span><span class="sxs-lookup"><span data-stu-id="58e13-199">A long description for the assembly.</span></span> <span data-ttu-id="58e13-200">Si `PackageDescription` n’est pas spécifié, cette propriété est également utilisée comme description du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-200">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="58e13-201">Détails de copyright pour le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-201">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="58e13-202">Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-202">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="58e13-203">Par défaut, il s’agit de `false`.</span><span class="sxs-lookup"><span data-stu-id="58e13-203">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="58e13-204">Valeur booléenne qui spécifie si le package est marqué en tant que dépendance de développement uniquement, ce qui empêche l’inclusion du package en tant que dépendance dans d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="58e13-204">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="58e13-205">Avec `PackageReference` ( NuGet 4.8 +), cet indicateur signifie également que les éléments multimédias de compilation sont exclus de la compilation.</span><span class="sxs-lookup"><span data-stu-id="58e13-205">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="58e13-206">Pour plus d'informations, voir [Prise en charge de DevelopmentDependency pour PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="58e13-206">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="58e13-207">Une expression ou un [identificateur de licence SPDX](https://spdx.org/licenses/) , par exemple, `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="58e13-207">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="58e13-208">Pour plus d’informations, consultez [compression d’une expression de licence ou d’un fichier de licence](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-208">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="58e13-209">Chemin d’accès à un fichier de licence dans le package si vous utilisez une licence personnalisée ou une licence à laquelle aucun identificateur SPDX n’a été affecté.</span><span class="sxs-lookup"><span data-stu-id="58e13-209">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="58e13-210">`PackageLicenseUrl` est déconseillé.</span><span class="sxs-lookup"><span data-stu-id="58e13-210">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="58e13-211">Utilisez `PackageLicenseExpression` ou `PackageLicenseFile` à la place.</span><span class="sxs-lookup"><span data-stu-id="58e13-211">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="58e13-212">Spécifie le chemin d’accès de l’icône de package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-212">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="58e13-213">Pour plus d’informations, consultez [compression d’une icône de fichier image](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-213">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="58e13-214">Notes de publication du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-214">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="58e13-215">Fichier Lisez-moi du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-215">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="58e13-216">Liste de balises séparées par un point-virgule qui désigne le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-216">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="58e13-217">Détermine le chemin de sortie dans lequel le package compressé est déposé.</span><span class="sxs-lookup"><span data-stu-id="58e13-217">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="58e13-218">La valeur par défaut est `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="58e13-218">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="58e13-219">Cette valeur booléenne indique si le package doit créer un package de symboles supplémentaire quand le projet est compressé.</span><span class="sxs-lookup"><span data-stu-id="58e13-219">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="58e13-220">Le format du package de symboles est contrôlé par la propriété `SymbolPackageFormat`.</span><span class="sxs-lookup"><span data-stu-id="58e13-220">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="58e13-221">Pour plus d’informations, consultez [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="58e13-221">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="58e13-222">Cette valeur booléenne indique si le processus de compression doit créer un package source.</span><span class="sxs-lookup"><span data-stu-id="58e13-222">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="58e13-223">Le package source contient le code source de la bibliothèque ainsi que les fichiers PDB.</span><span class="sxs-lookup"><span data-stu-id="58e13-223">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="58e13-224">Les fichiers sources sont placés dans le répertoire `src/ProjectName` dans le fichier de package obtenu.</span><span class="sxs-lookup"><span data-stu-id="58e13-224">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="58e13-225">Pour plus d’informations, consultez [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="58e13-225">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="58e13-226">Spécifie si tous les fichiers de sortie sont copiés dans le dossier *tools* au lieu du dossier *lib*.</span><span class="sxs-lookup"><span data-stu-id="58e13-226">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="58e13-227">Pour plus d’informations, consultez [IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="58e13-227">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="58e13-228">URL du référentiel utilisée pour cloner ou récupérer le code source.</span><span class="sxs-lookup"><span data-stu-id="58e13-228">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="58e13-229">Exemple : *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="58e13-229">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="58e13-230">Type de référentiel.</span><span class="sxs-lookup"><span data-stu-id="58e13-230">Repository type.</span></span> <span data-ttu-id="58e13-231">Exemples : `git` (valeur par défaut), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="58e13-231">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="58e13-232">Informations de branche de référentiel facultatives.</span><span class="sxs-lookup"><span data-stu-id="58e13-232">Optional repository branch information.</span></span> <span data-ttu-id="58e13-233">`RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="58e13-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="58e13-234">Exemple : *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="58e13-234">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="58e13-235">Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré.</span><span class="sxs-lookup"><span data-stu-id="58e13-235">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="58e13-236">`RepositoryUrl` doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="58e13-236">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="58e13-237">Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="58e13-237">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="58e13-238">Spécifie le format du package de symboles.</span><span class="sxs-lookup"><span data-stu-id="58e13-238">Specifies the format of the symbols package.</span></span> <span data-ttu-id="58e13-239">Si « Symbols. nupkg », un package de symboles hérités est créé avec une extension *. Symbols. nupkg* contenant des fichiers PDB, des dll et d’autres fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="58e13-239">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="58e13-240">Si « snupkg », un package de symboles snupkg est créé et contient les fichiers PDB portables.</span><span class="sxs-lookup"><span data-stu-id="58e13-240">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="58e13-241">La valeur par défaut est « Symbols. nupkg ».</span><span class="sxs-lookup"><span data-stu-id="58e13-241">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="58e13-242">Spécifie que `pack` ne doit pas exécuter l’analyse du package après la génération du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-242">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="58e13-243">Spécifie la version minimale du NuGet client qui peut installer ce package, appliquée par nuget.exe et le gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58e13-243">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="58e13-244">Cette valeur booléenne spécifie si les assemblys de sortie de la génération doivent être empaquetés dans le fichier *. nupkg* ou non.</span><span class="sxs-lookup"><span data-stu-id="58e13-244">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="58e13-245">Cette valeur booléenne spécifie si tous les éléments dont le type `Content` est sont inclus automatiquement dans le package résultant.</span><span class="sxs-lookup"><span data-stu-id="58e13-245">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="58e13-246">Par défaut, il s’agit de `true`.</span><span class="sxs-lookup"><span data-stu-id="58e13-246">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="58e13-247">Spécifie le dossier où placer les assemblys de sortie.</span><span class="sxs-lookup"><span data-stu-id="58e13-247">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="58e13-248">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="58e13-248">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="58e13-249">Pour plus d’informations, consultez [assemblys de sortie](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="58e13-249">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="58e13-250">Spécifie l’emplacement par défaut où tous les fichiers de contenu doivent être placés si `PackagePath` n’est pas spécifié pour eux.</span><span class="sxs-lookup"><span data-stu-id="58e13-250">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="58e13-251">La valeur par défaut est « content;contentFiles ».</span><span class="sxs-lookup"><span data-stu-id="58e13-251">The default value is "content;contentFiles".</span></span> <span data-ttu-id="58e13-252">Pour plus d’informations, consultez [Inclusion de contenu dans un package](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="58e13-252">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="58e13-253">Chemin d’accès relatif ou absolu au *.nuspec* fichier utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="58e13-253">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="58e13-254">S’il est spécifié, il est utilisé **exclusivement** pour les informations de Packaging, et toutes les informations contenues dans les projets ne sont pas utilisées.</span><span class="sxs-lookup"><span data-stu-id="58e13-254">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="58e13-255">Pour plus d’informations, consultez [compression à .nuspec l’aide d’un ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-255">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="58e13-256">Chemin d’accès de base pour le *.nuspec* fichier.</span><span class="sxs-lookup"><span data-stu-id="58e13-256">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="58e13-257">Pour plus d’informations, consultez [compression à .nuspec l’aide d’un ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-257">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="58e13-258">Liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="58e13-258">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="58e13-259">Pour plus d’informations, consultez [compression à .nuspec l’aide d’un ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="58e13-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="58e13-260">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="58e13-260">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="58e13-261">Supprimer les dépendances</span><span class="sxs-lookup"><span data-stu-id="58e13-261">Suppressing dependencies</span></span>

<span data-ttu-id="58e13-262">Pour supprimer les dépendances de package du NuGet package généré, affectez `SuppressDependenciesWhenPacking` la valeur à `true` qui autorisera l’ignorance de toutes les dépendances du fichier nupkg généré.</span><span class="sxs-lookup"><span data-stu-id="58e13-262">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="58e13-263">`PackageIconUrl` est déconseillé en faveur de la [`PackageIcon`](#packageicon) propriété.</span><span class="sxs-lookup"><span data-stu-id="58e13-263">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="58e13-264">À compter de NuGet 5,3 et de Visual Studio 2019 version 16,3, `pack` déclenche l’avertissement [NU5048](./errors-and-warnings/nu5048.md) si les métadonnées de package spécifient uniquement `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="58e13-264">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="58e13-265">Pour maintenir la compatibilité descendante avec les clients et les sources qui ne sont pas encore prises en charge `PackageIcon` , spécifiez à la fois `PackageIcon` et `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="58e13-265">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="58e13-266">Visual Studio prend en charge `PackageIcon` les packages provenant d’une source basée sur un dossier.</span><span class="sxs-lookup"><span data-stu-id="58e13-266">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="58e13-267">Compression d’un fichier image d’icône</span><span class="sxs-lookup"><span data-stu-id="58e13-267">Packing an icon image file</span></span>

<span data-ttu-id="58e13-268">Lors de la compression d’un fichier image icône, utilisez `PackageIcon` la propriété pour spécifier le chemin d’accès du fichier d’icône, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-268">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="58e13-269">En outre, assurez-vous que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-269">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="58e13-270">La taille du fichier image est limitée à 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="58e13-270">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="58e13-271">Les formats de fichiers pris en charge sont JPEG et PNG.</span><span class="sxs-lookup"><span data-stu-id="58e13-271">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="58e13-272">Nous recommandons une résolution d’image de 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="58e13-272">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="58e13-273">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58e13-273">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="58e13-274">[Exemple d’icône de package](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="58e13-274">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="58e13-275">Pour obtenir l' nuspec équivalent, jetez un coup d’œil à la [ nuspec référence de l’icône](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="58e13-275">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="58e13-276">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="58e13-276">PackageReadmeFile</span></span>

<span data-ttu-id="58e13-277">Lors de la compression d’un fichier Lisez-moi, vous devez utiliser la `PackageReadmeFile` propriété pour spécifier le chemin d’accès au package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-277">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="58e13-278">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-278">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="58e13-279">Les formats de fichiers pris en charge incluent uniquement la démarque (*. MD*).</span><span class="sxs-lookup"><span data-stu-id="58e13-279">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="58e13-280">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58e13-280">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="58e13-281">Pour obtenir l' nuspec équivalent, jetez un coup d’œil sur la [ nuspec Référence du fichier Readme](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="58e13-281">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="58e13-282">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="58e13-282">Output assemblies</span></span>

<span data-ttu-id="58e13-283">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="58e13-283">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="58e13-284">Les fichiers de sortie copiés dépendent de ce qui est MSBuild fourni par la `BuiltOutputProjectGroup` cible.</span><span class="sxs-lookup"><span data-stu-id="58e13-284">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="58e13-285">Il existe deux MSBuild  propriétés que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler l’emplacement des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="58e13-285">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="58e13-286">`IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-286">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="58e13-287">`BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="58e13-287">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="58e13-288">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="58e13-288">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="58e13-289">Références de package</span><span class="sxs-lookup"><span data-stu-id="58e13-289">Package references</span></span>

<span data-ttu-id="58e13-290">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="58e13-290">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="58e13-291">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="58e13-291">Project to project references</span></span>

<span data-ttu-id="58e13-292">Les références entre projets sont prises en compte par défaut en tant que NuGet références de package.</span><span class="sxs-lookup"><span data-stu-id="58e13-292">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="58e13-293">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58e13-293">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="58e13-294">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="58e13-294">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="58e13-295">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="58e13-295">Including content in a package</span></span>

<span data-ttu-id="58e13-296">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="58e13-296">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="58e13-297">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e13-297">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="58e13-298">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="58e13-298">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="58e13-299">Si vous souhaitez copier l’ensemble de votre contenu dans un ou plusieurs dossiers racine spécifiques (au lieu de `content` et `contentFiles` les deux), vous pouvez utiliser la MSBuild propriété `ContentTargetFolders` , qui a comme valeur par défaut « content ; contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="58e13-299">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="58e13-300">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="58e13-300">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="58e13-301">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="58e13-301">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="58e13-302">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-302">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="58e13-303">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="58e13-303">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="58e13-304">Il y a également une MSBuild propriété `$(IncludeContentInPack)` , qui a comme valeur par défaut `true` .</span><span class="sxs-lookup"><span data-stu-id="58e13-304">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="58e13-305">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="58e13-305">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="58e13-306">Les autres métadonnées spécifiques à un Pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` les jeux ```CopyToOutput``` et ```Flatten``` valeurs de l' ```contentFiles``` entrée dans la sortie nuspec .</span><span class="sxs-lookup"><span data-stu-id="58e13-306">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="58e13-307">Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="58e13-307">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="58e13-308">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="58e13-308">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="58e13-309">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="58e13-309">IncludeSymbols</span></span>

<span data-ttu-id="58e13-310">Quand vous utilisez `MSBuild -t:pack -p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="58e13-310">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="58e13-311">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="58e13-311">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="58e13-312">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="58e13-312">IncludeSource</span></span>

<span data-ttu-id="58e13-313">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="58e13-313">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="58e13-314">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="58e13-314">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="58e13-315">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="58e13-315">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="58e13-316">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="58e13-316">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="58e13-317">Compression d’une expression de licence ou d’un fichier de licence</span><span class="sxs-lookup"><span data-stu-id="58e13-317">Packing a license expression or a license file</span></span>

<span data-ttu-id="58e13-318">Lorsque vous utilisez une expression de licence, utilisez la `PackageLicenseExpression` propriété.</span><span class="sxs-lookup"><span data-stu-id="58e13-318">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="58e13-319">Pour obtenir un exemple, consultez [exemple d’expression de licence](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="58e13-319">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="58e13-320">Pour en savoir plus sur les expressions de licence et les licences acceptées par NuGet . org, consultez [métadonnées de licence](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="58e13-320">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="58e13-321">Lors de la compression d’un fichier de licence, utilisez `PackageLicenseFile` la propriété pour spécifier le chemin d’accès du package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="58e13-321">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="58e13-322">En outre, assurez-vous que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-322">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="58e13-323">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58e13-323">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="58e13-324">Pour obtenir un exemple, consultez [exemple de fichier de licence](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="58e13-324">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="58e13-325">Seul un de `PackageLicenseExpression` , `PackageLicenseFile` et `PackageLicenseUrl` peut être spécifié à la fois.</span><span class="sxs-lookup"><span data-stu-id="58e13-325">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="58e13-326">Compression d’un fichier sans extension</span><span class="sxs-lookup"><span data-stu-id="58e13-326">Packing a file without an extension</span></span>

<span data-ttu-id="58e13-327">Dans certains scénarios, par exemple lors de la compression d’un fichier de licence, vous souhaiterez peut-être inclure un fichier sans extension.</span><span class="sxs-lookup"><span data-stu-id="58e13-327">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="58e13-328">Pour des raisons historiques, NuGet  &  MSBuild traitez les chemins sans extension comme répertoires.</span><span class="sxs-lookup"><span data-stu-id="58e13-328">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="58e13-329">[Fichier sans exemple d’extension](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="58e13-329">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="58e13-330">IsTool</span><span class="sxs-lookup"><span data-stu-id="58e13-330">IsTool</span></span>

<span data-ttu-id="58e13-331">Lors de l’utilisation de `MSBuild -t:pack -p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="58e13-331">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="58e13-332">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="58e13-332">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="58e13-333">Compression à l’aide d’un `.nuspec` fichier</span><span class="sxs-lookup"><span data-stu-id="58e13-333">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="58e13-334">Bien qu’il soit recommandé d’inclure à la place [toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se trouvent généralement dans le fichier du `.nuspec` fichier projet, vous pouvez choisir d’utiliser un `.nuspec` fichier pour compresser votre projet.</span><span class="sxs-lookup"><span data-stu-id="58e13-334">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="58e13-335">Pour un projet de type non-SDK qui utilise `PackageReference` , vous devez effectuer `NuGet.Build.Tasks.Pack.targets` l’importation afin que la tâche Pack puisse être exécutée.</span><span class="sxs-lookup"><span data-stu-id="58e13-335">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="58e13-336">Vous devez toujours restaurer le projet avant de pouvoir le compresser nuspec .</span><span class="sxs-lookup"><span data-stu-id="58e13-336">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="58e13-337">(Un projet de type SDK comprend les cibles Pack par défaut.)</span><span class="sxs-lookup"><span data-stu-id="58e13-337">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="58e13-338">La version cible du .NET Framework du fichier projet n’est pas pertinente et n’est pas utilisée lors de la compression d’un nuspec .</span><span class="sxs-lookup"><span data-stu-id="58e13-338">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="58e13-339">Les trois MSBuild propriétés suivantes sont pertinentes pour la compression à l’aide d’un `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="58e13-339">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="58e13-340">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="58e13-340">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="58e13-341">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="58e13-341">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="58e13-342">En raison du mode de fonctionnement de l' MSBuild analyse de ligne de commande, plusieurs propriétés doivent être spécifiées comme suit : `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="58e13-342">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="58e13-343">`NuspecBasePath` : chemin de base pour le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="58e13-343">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="58e13-344">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="58e13-344">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="58e13-345">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="58e13-345">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="58e13-346">Notez que l’empaquetage d’un nuspec à l’aide de dotnet.exe ou MSBuild permet également de générer le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="58e13-346">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="58e13-347">Cela peut être évité en passant ```--no-build``` la propriété à dotnet.exe, qui est l’équivalent du paramètre ```<NoBuild>true</NoBuild> ``` dans votre fichier projet, ainsi que le paramètre ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="58e13-347">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="58e13-348">Voici un exemple de fichier *. csproj* pour compresser un nuspec fichier :</span><span class="sxs-lookup"><span data-stu-id="58e13-348">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="58e13-349">Points d’extension avancés pour créer un package personnalisé</span><span class="sxs-lookup"><span data-stu-id="58e13-349">Advanced extension points to create customized package</span></span>

<span data-ttu-id="58e13-350">La `pack` cible fournit deux points d’extension qui s’exécutent dans la build interne du Framework cible.</span><span class="sxs-lookup"><span data-stu-id="58e13-350">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="58e13-351">Les points d’extension prennent en charge l’inclusion de contenu et d’assemblys spécifiques au Framework cible dans un package :</span><span class="sxs-lookup"><span data-stu-id="58e13-351">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="58e13-352">`TargetsForTfmSpecificBuildOutput` cible : à utiliser pour les fichiers contenus dans le `lib` dossier ou dans un dossier spécifié à l’aide de `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="58e13-352">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="58e13-353">`TargetsForTfmSpecificContentInPackage` cible : à utiliser pour les fichiers en dehors de `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="58e13-353">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="58e13-354">Écrivez une cible personnalisée et spécifiez-la comme valeur de la `$(TargetsForTfmSpecificBuildOutput)` propriété.</span><span class="sxs-lookup"><span data-stu-id="58e13-354">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="58e13-355">Pour tous les fichiers qui doivent être placés dans `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans ItemGroup `BuildOutputInPackage` et définir les deux valeurs de métadonnées suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e13-355">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="58e13-356">`FinalOutputPath`: Le chemin d’accès absolu du fichier ; s’il n’est pas fourni, l’identité est utilisée pour évaluer le chemin source.</span><span class="sxs-lookup"><span data-stu-id="58e13-356">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="58e13-357">`TargetPath`: (Facultatif) définit le moment où le fichier doit être placé dans un sous-dossier au sein de `lib\<TargetFramework>` , comme les assemblys satellites qui se trouvent dans leurs dossiers de culture respectifs.</span><span class="sxs-lookup"><span data-stu-id="58e13-357">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="58e13-358">La valeur par défaut est le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="58e13-358">Defaults to the name of the file.</span></span>

<span data-ttu-id="58e13-359">Exemple :</span><span class="sxs-lookup"><span data-stu-id="58e13-359">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="58e13-360">Écrivez une cible personnalisée et spécifiez-la comme valeur de la `$(TargetsForTfmSpecificContentInPackage)` propriété.</span><span class="sxs-lookup"><span data-stu-id="58e13-360">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="58e13-361">Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e13-361">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="58e13-362">`PackagePath`: Chemin d’accès où le fichier doit être généré dans le package.</span><span class="sxs-lookup"><span data-stu-id="58e13-362">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="58e13-363">NuGet émet un avertissement si plusieurs fichiers sont ajoutés au même chemin d’accès de package.</span><span class="sxs-lookup"><span data-stu-id="58e13-363">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="58e13-364">`BuildAction`: Action de génération à assigner au fichier, obligatoire uniquement si le chemin d’accès du package se trouve dans le `contentFiles` dossier.</span><span class="sxs-lookup"><span data-stu-id="58e13-364">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="58e13-365">La valeur par défaut est « None ».</span><span class="sxs-lookup"><span data-stu-id="58e13-365">Defaults to "None".</span></span>

<span data-ttu-id="58e13-366">Exemple :</span><span class="sxs-lookup"><span data-stu-id="58e13-366">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="58e13-367">Cible restore</span><span class="sxs-lookup"><span data-stu-id="58e13-367">restore target</span></span>

<span data-ttu-id="58e13-368">`MSBuild -t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e13-368">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="58e13-369">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="58e13-369">Read all project to project references</span></span>
1. <span data-ttu-id="58e13-370">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="58e13-370">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="58e13-371">Transmettre des MSBuild données à NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="58e13-371">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="58e13-372">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="58e13-372">Run restore</span></span>
1. <span data-ttu-id="58e13-373">Télécharger des packages</span><span class="sxs-lookup"><span data-stu-id="58e13-373">Download packages</span></span>
1. <span data-ttu-id="58e13-374">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="58e13-374">Write assets file, targets, and props</span></span>

<span data-ttu-id="58e13-375">La `restore` cible fonctionne pour les projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="58e13-375">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="58e13-376">`MSBuild 16.5+` prend également [en charge](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) le `packages.config` format.</span><span class="sxs-lookup"><span data-stu-id="58e13-376">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="58e13-377">La `restore` cible ne [doit pas être exécutée](#restoring-and-building-with-one-msbuild-command) en association avec la `build` cible.</span><span class="sxs-lookup"><span data-stu-id="58e13-377">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="58e13-378">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="58e13-378">Restore properties</span></span>

<span data-ttu-id="58e13-379">Des paramètres de restauration supplémentaires peuvent provenir des MSBuild Propriétés du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="58e13-379">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="58e13-380">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `-p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="58e13-380">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="58e13-381">Propriété</span><span class="sxs-lookup"><span data-stu-id="58e13-381">Property</span></span> | <span data-ttu-id="58e13-382">Description</span><span class="sxs-lookup"><span data-stu-id="58e13-382">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="58e13-383">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="58e13-383">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="58e13-384">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58e13-384">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="58e13-385">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="58e13-385">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="58e13-386">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="58e13-386">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="58e13-387">Si la valeur est true, évite d’utiliser des packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="58e13-387">If true, avoids using cached packages.</span></span> <span data-ttu-id="58e13-388">Consultez [gestion des dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="58e13-388">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="58e13-389">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="58e13-389">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="58e13-390">Dossiers de secours, utilisés de la même façon que le dossier des packages de l’utilisateur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="58e13-390">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="58e13-391">Sources supplémentaires à utiliser pendant la restauration.</span><span class="sxs-lookup"><span data-stu-id="58e13-391">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="58e13-392">Dossiers de secours supplémentaires à utiliser lors de la restauration.</span><span class="sxs-lookup"><span data-stu-id="58e13-392">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="58e13-393">Exclut les dossiers de secours spécifiés dans `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="58e13-393">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="58e13-394">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="58e13-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="58e13-395">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="58e13-395">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="58e13-396">Lorsque les projets sont collectés via MSBuild , il détermine s’ils sont collectés à l’aide de l' `SkipNonexistentTargets` optimisation.</span><span class="sxs-lookup"><span data-stu-id="58e13-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="58e13-397">Si la valeur n’est pas définie, la valeur par défaut est `true` .</span><span class="sxs-lookup"><span data-stu-id="58e13-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="58e13-398">La conséquence est un comportement de basculement rapide lorsque les cibles d’un projet ne peuvent pas être importées.</span><span class="sxs-lookup"><span data-stu-id="58e13-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="58e13-399">Dossier de sortie, avec comme valeur par défaut `BaseIntermediateOutputPath` et le `obj` dossier.</span><span class="sxs-lookup"><span data-stu-id="58e13-399">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="58e13-400">Dans les projets basés sur PackageReference, force la résolution de toutes les dépendances même si la dernière restauration a réussi.</span><span class="sxs-lookup"><span data-stu-id="58e13-400">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="58e13-401">La spécification de cet indicateur est semblable à la suppression du `project.assets.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="58e13-401">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="58e13-402">Cela ne contourne pas le cache http.</span><span class="sxs-lookup"><span data-stu-id="58e13-402">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="58e13-403">Opte pour l’utilisation d’un fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="58e13-403">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="58e13-404">Exécutez la restauration en mode verrouillé.</span><span class="sxs-lookup"><span data-stu-id="58e13-404">Run restore in locked mode.</span></span> <span data-ttu-id="58e13-405">Cela signifie que la restauration ne réévaluera pas les dépendances.</span><span class="sxs-lookup"><span data-stu-id="58e13-405">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="58e13-406">Emplacement personnalisé pour le fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="58e13-406">A custom location for the lock file.</span></span> <span data-ttu-id="58e13-407">L’emplacement par défaut est à côté du projet et est nommé `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="58e13-407">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="58e13-408">Force la restauration à recalculer les dépendances et à mettre à jour le fichier de verrouillage sans aucun avertissement.</span><span class="sxs-lookup"><span data-stu-id="58e13-408">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="58e13-409">Commutateur d’abonnement qui restaure des projets avec packages.config. Prise en charge avec `MSBuild -t:restore` uniquement.</span><span class="sxs-lookup"><span data-stu-id="58e13-409">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="58e13-410">Un commutateur d’abonnement pour utiliser l’évaluation de graphique statique MSBuild au lieu de l’évaluation standard.</span><span class="sxs-lookup"><span data-stu-id="58e13-410">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="58e13-411">L’évaluation du graphique statique est une fonctionnalité expérimentale qui est beaucoup plus rapide pour les grandes pensions et les solutions.</span><span class="sxs-lookup"><span data-stu-id="58e13-411">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="58e13-412">Exemples</span><span class="sxs-lookup"><span data-stu-id="58e13-412">Examples</span></span>

<span data-ttu-id="58e13-413">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="58e13-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="58e13-414">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="58e13-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="58e13-415">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="58e13-415">Restore outputs</span></span>

<span data-ttu-id="58e13-416">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="58e13-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="58e13-417">Fichier</span><span class="sxs-lookup"><span data-stu-id="58e13-417">File</span></span> | <span data-ttu-id="58e13-418">Description</span><span class="sxs-lookup"><span data-stu-id="58e13-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="58e13-419">Contient le graphique de dépendance de toutes les références de package.</span><span class="sxs-lookup"><span data-stu-id="58e13-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="58e13-420">Références aux MSBuild propriétés contenues dans les packages</span><span class="sxs-lookup"><span data-stu-id="58e13-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="58e13-421">Références aux MSBuild cibles contenues dans les packages</span><span class="sxs-lookup"><span data-stu-id="58e13-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="58e13-422">Restauration et génération à l’aide d’une seule MSBuild commande</span><span class="sxs-lookup"><span data-stu-id="58e13-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="58e13-423">En raison du fait que NuGet peut restaurer des packages qui déplacent des MSBuild cibles et des props, les évaluations de la restauration et de la build sont exécutées avec des propriétés globales différentes.</span><span class="sxs-lookup"><span data-stu-id="58e13-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="58e13-424">Cela signifie que les éléments suivants auront un comportement imprévisible et souvent incorrect.</span><span class="sxs-lookup"><span data-stu-id="58e13-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="58e13-425">Au lieu de cela, l’approche recommandée est la suivante :</span><span class="sxs-lookup"><span data-stu-id="58e13-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="58e13-426">La même logique s’applique à d’autres cibles similaires à celles de `build` .</span><span class="sxs-lookup"><span data-stu-id="58e13-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="58e13-427">Restauration des projets PackageReference et packages.config avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="58e13-427">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="58e13-428">Avec MSBuild 16,5 +, packages.config sont également pris en charge pour `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="58e13-428">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="58e13-429">`packages.config` la restauration est disponible uniquement avec `MSBuild 16.5+` , et non avec `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="58e13-429">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="58e13-430">Restauration avec MSBuild évaluation de graphique statique</span><span class="sxs-lookup"><span data-stu-id="58e13-430">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="58e13-431">Avec MSBuild 16,6 +, NuGet a ajouté une fonctionnalité expérimentale pour utiliser l’évaluation de graphique statique à partir de la ligne de commande, ce qui améliore considérablement le temps de restauration pour les référentiels volumineux.</span><span class="sxs-lookup"><span data-stu-id="58e13-431">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="58e13-432">Vous pouvez également l’activer en définissant la propriété dans un répertoire. Build. props.</span><span class="sxs-lookup"><span data-stu-id="58e13-432">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="58e13-433">À compter de Visual Studio 2019. x et NuGet 5. x, cette fonctionnalité est considérée comme expérimentale et s’abonne.</span><span class="sxs-lookup"><span data-stu-id="58e13-433">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="58e13-434">Suivez la [ NuGet directive/Home # 9803](https://github.com/NuGet/Home/issues/9803) pour plus d’informations sur le moment où cette fonctionnalité sera activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="58e13-434">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="58e13-435">La restauration de graphiques statiques modifie la partie MSBuild de la restauration, la lecture et l’évaluation du projet, mais pas l’algorithme de restauration !</span><span class="sxs-lookup"><span data-stu-id="58e13-435">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="58e13-436">L’algorithme de restauration est le même pour tous les NuGet Outils ( NuGet . exe, MSBuild . exe, dotnet.exe et Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="58e13-436">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="58e13-437">Dans très peu de scénarios, la restauration de graphiques statiques peut se comporter différemment de la restauration en cours et certains PackageReferences ou références déclarés peuvent être manquants.</span><span class="sxs-lookup"><span data-stu-id="58e13-437">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="58e13-438">Pour faciliter l’utilisation de la migration vers la restauration de graphiques statiques, envisagez d’exécuter :</span><span class="sxs-lookup"><span data-stu-id="58e13-438">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="58e13-439">NuGet*ne* doit signaler aucune modification.</span><span class="sxs-lookup"><span data-stu-id="58e13-439">NuGet should *not* report any changes.</span></span> <span data-ttu-id="58e13-440">Si vous voyez une anomalie, veuillez envoyer un problème à [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="58e13-440">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="58e13-441">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="58e13-441">Replacing one library from a restore graph</span></span>

<span data-ttu-id="58e13-442">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="58e13-442">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="58e13-443">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="58e13-443">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="58e13-444">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="58e13-444">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```