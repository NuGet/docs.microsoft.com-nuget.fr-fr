---
title: Commandes pack et restore NuGet comme cibles MSBuild
description: Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: b450a5bfa3dcf70056c99a951f51a78845ef8438
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342451"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="628e3-103">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="628e3-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="628e3-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="628e3-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="628e3-105">Avec le format PackageReference, NuGet 4.0+ peut stocker toutes les métadonnées du manifeste directement dans un fichier projet, au lieu d’utiliser un fichier `.nuspec` distinct.</span><span class="sxs-lookup"><span data-stu-id="628e3-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="628e3-106">Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="628e3-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="628e3-107">Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="628e3-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="628e3-108">(Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../reference/cli-reference/cli-ref-pack.md) et [restore](../reference/cli-reference/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)</span><span class="sxs-lookup"><span data-stu-id="628e3-108">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="628e3-109">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="628e3-109">Target build order</span></span>

<span data-ttu-id="628e3-110">Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="628e3-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="628e3-111">Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression.</span><span class="sxs-lookup"><span data-stu-id="628e3-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="628e3-112">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="628e3-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="628e3-113">De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.</span><span class="sxs-lookup"><span data-stu-id="628e3-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="628e3-114">Cible pack</span><span class="sxs-lookup"><span data-stu-id="628e3-114">pack target</span></span>

<span data-ttu-id="628e3-115">Pour les projets .NET standard utilisant le format PackageReference, `msbuild -t:pack` l’utilisation de dessine des entrées à partir du fichier projet à utiliser lors de la création d’un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="628e3-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="628e3-116">Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier projet au sein du premier nœud `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="628e3-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="628e3-117">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="628e3-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="628e3-118">Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="628e3-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="628e3-119">Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.</span><span class="sxs-lookup"><span data-stu-id="628e3-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="628e3-120">Valeur d’attribut/NuSpec</span><span class="sxs-lookup"><span data-stu-id="628e3-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="628e3-121">Propriété MSBuild</span><span class="sxs-lookup"><span data-stu-id="628e3-121">MSBuild Property</span></span> | <span data-ttu-id="628e3-122">Default</span><span class="sxs-lookup"><span data-stu-id="628e3-122">Default</span></span> | <span data-ttu-id="628e3-123">Notes</span><span class="sxs-lookup"><span data-stu-id="628e3-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="628e3-124">Id</span><span class="sxs-lookup"><span data-stu-id="628e3-124">Id</span></span> | <span data-ttu-id="628e3-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="628e3-125">PackageId</span></span> | <span data-ttu-id="628e3-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="628e3-126">AssemblyName</span></span> | <span data-ttu-id="628e3-127">$(AssemblyName) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="628e3-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="628e3-128">Version</span><span class="sxs-lookup"><span data-stu-id="628e3-128">Version</span></span> | <span data-ttu-id="628e3-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="628e3-129">PackageVersion</span></span> | <span data-ttu-id="628e3-130">Version</span><span class="sxs-lookup"><span data-stu-id="628e3-130">Version</span></span> | <span data-ttu-id="628e3-131">Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 »</span><span class="sxs-lookup"><span data-stu-id="628e3-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="628e3-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="628e3-132">VersionPrefix</span></span> | <span data-ttu-id="628e3-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="628e3-133">PackageVersionPrefix</span></span> | <span data-ttu-id="628e3-134">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-134">empty</span></span> | <span data-ttu-id="628e3-135">La définition de PackageVersion remplace PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="628e3-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="628e3-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="628e3-136">VersionSuffix</span></span> | <span data-ttu-id="628e3-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="628e3-137">PackageVersionSuffix</span></span> | <span data-ttu-id="628e3-138">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-138">empty</span></span> | <span data-ttu-id="628e3-139">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="628e3-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="628e3-140">La définition de PackageVersion remplace PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="628e3-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="628e3-141">Auteurs</span><span class="sxs-lookup"><span data-stu-id="628e3-141">Authors</span></span> | <span data-ttu-id="628e3-142">Auteurs</span><span class="sxs-lookup"><span data-stu-id="628e3-142">Authors</span></span> | <span data-ttu-id="628e3-143">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="628e3-143">Username of the current user</span></span> | |
| <span data-ttu-id="628e3-144">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="628e3-144">Owners</span></span> | <span data-ttu-id="628e3-145">N/A</span><span class="sxs-lookup"><span data-stu-id="628e3-145">N/A</span></span> | <span data-ttu-id="628e3-146">Ne figure pas dans NuSpec</span><span class="sxs-lookup"><span data-stu-id="628e3-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="628e3-147">Titre</span><span class="sxs-lookup"><span data-stu-id="628e3-147">Title</span></span> | <span data-ttu-id="628e3-148">Titre</span><span class="sxs-lookup"><span data-stu-id="628e3-148">Title</span></span> | <span data-ttu-id="628e3-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="628e3-149">The PackageId</span></span>| |
| <span data-ttu-id="628e3-150">Description</span><span class="sxs-lookup"><span data-stu-id="628e3-150">Description</span></span> | <span data-ttu-id="628e3-151">Description</span><span class="sxs-lookup"><span data-stu-id="628e3-151">Description</span></span> | <span data-ttu-id="628e3-152">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="628e3-152">"Package Description"</span></span> | |
| <span data-ttu-id="628e3-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="628e3-153">Copyright</span></span> | <span data-ttu-id="628e3-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="628e3-154">Copyright</span></span> | <span data-ttu-id="628e3-155">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-155">empty</span></span> | |
| <span data-ttu-id="628e3-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="628e3-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="628e3-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="628e3-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="628e3-158">false</span><span class="sxs-lookup"><span data-stu-id="628e3-158">false</span></span> | |
| <span data-ttu-id="628e3-159">Licence</span><span class="sxs-lookup"><span data-stu-id="628e3-159">license</span></span> | <span data-ttu-id="628e3-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="628e3-160">PackageLicenseExpression</span></span> | <span data-ttu-id="628e3-161">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-161">empty</span></span> | <span data-ttu-id="628e3-162">Correspond à`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="628e3-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="628e3-163">Licence</span><span class="sxs-lookup"><span data-stu-id="628e3-163">license</span></span> | <span data-ttu-id="628e3-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="628e3-164">PackageLicenseFile</span></span> | <span data-ttu-id="628e3-165">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-165">empty</span></span> | <span data-ttu-id="628e3-166">Correspond à `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="628e3-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="628e3-167">Vous devrez peut-être compresser explicitement le fichier de licence référencé.</span><span class="sxs-lookup"><span data-stu-id="628e3-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="628e3-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-168">LicenseUrl</span></span> | <span data-ttu-id="628e3-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-169">PackageLicenseUrl</span></span> | <span data-ttu-id="628e3-170">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-170">empty</span></span> | <span data-ttu-id="628e3-171">`licenseUrl`est déconseillé, utilisez la propriété PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="628e3-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="628e3-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-172">ProjectUrl</span></span> | <span data-ttu-id="628e3-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-173">PackageProjectUrl</span></span> | <span data-ttu-id="628e3-174">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-174">empty</span></span> | |
| <span data-ttu-id="628e3-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-175">IconUrl</span></span> | <span data-ttu-id="628e3-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-176">PackageIconUrl</span></span> | <span data-ttu-id="628e3-177">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-177">empty</span></span> | |
| <span data-ttu-id="628e3-178">Balises</span><span class="sxs-lookup"><span data-stu-id="628e3-178">Tags</span></span> | <span data-ttu-id="628e3-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="628e3-179">PackageTags</span></span> | <span data-ttu-id="628e3-180">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-180">empty</span></span> | <span data-ttu-id="628e3-181">Les balises sont séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="628e3-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="628e3-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="628e3-182">ReleaseNotes</span></span> | <span data-ttu-id="628e3-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="628e3-183">PackageReleaseNotes</span></span> | <span data-ttu-id="628e3-184">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-184">empty</span></span> | |
| <span data-ttu-id="628e3-185">Référentiel/URL</span><span class="sxs-lookup"><span data-stu-id="628e3-185">Repository/Url</span></span> | <span data-ttu-id="628e3-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-186">RepositoryUrl</span></span> | <span data-ttu-id="628e3-187">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-187">empty</span></span> | <span data-ttu-id="628e3-188">URL du référentiel utilisée pour cloner ou récupérer le code source.</span><span class="sxs-lookup"><span data-stu-id="628e3-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="628e3-189">Tels *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="628e3-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="628e3-190">Dépôt/type</span><span class="sxs-lookup"><span data-stu-id="628e3-190">Repository/Type</span></span> | <span data-ttu-id="628e3-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="628e3-191">RepositoryType</span></span> | <span data-ttu-id="628e3-192">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-192">empty</span></span> | <span data-ttu-id="628e3-193">Type de référentiel.</span><span class="sxs-lookup"><span data-stu-id="628e3-193">Repository type.</span></span> <span data-ttu-id="628e3-194">Exemples: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="628e3-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="628e3-195">Référentiel/branche</span><span class="sxs-lookup"><span data-stu-id="628e3-195">Repository/Branch</span></span> | <span data-ttu-id="628e3-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="628e3-196">RepositoryBranch</span></span> | <span data-ttu-id="628e3-197">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-197">empty</span></span> | <span data-ttu-id="628e3-198">Informations de branche de référentiel facultatives.</span><span class="sxs-lookup"><span data-stu-id="628e3-198">Optional repository branch information.</span></span> <span data-ttu-id="628e3-199">*RepositoryUrl* doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="628e3-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="628e3-200">Exemple: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="628e3-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="628e3-201">Dépôt/validation</span><span class="sxs-lookup"><span data-stu-id="628e3-201">Repository/Commit</span></span> | <span data-ttu-id="628e3-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="628e3-202">RepositoryCommit</span></span> | <span data-ttu-id="628e3-203">vide</span><span class="sxs-lookup"><span data-stu-id="628e3-203">empty</span></span> | <span data-ttu-id="628e3-204">Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré.</span><span class="sxs-lookup"><span data-stu-id="628e3-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="628e3-205">*RepositoryUrl* doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="628e3-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="628e3-206">Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="628e3-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="628e3-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="628e3-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="628e3-208">Récapitulatif</span><span class="sxs-lookup"><span data-stu-id="628e3-208">Summary</span></span> | <span data-ttu-id="628e3-209">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="628e3-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="628e3-210">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="628e3-210">pack target inputs</span></span>

- <span data-ttu-id="628e3-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="628e3-211">IsPackable</span></span>
- <span data-ttu-id="628e3-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="628e3-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="628e3-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="628e3-213">PackageVersion</span></span>
- <span data-ttu-id="628e3-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="628e3-214">PackageId</span></span>
- <span data-ttu-id="628e3-215">Auteurs</span><span class="sxs-lookup"><span data-stu-id="628e3-215">Authors</span></span>
- <span data-ttu-id="628e3-216">Description</span><span class="sxs-lookup"><span data-stu-id="628e3-216">Description</span></span>
- <span data-ttu-id="628e3-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="628e3-217">Copyright</span></span>
- <span data-ttu-id="628e3-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="628e3-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="628e3-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="628e3-219">DevelopmentDependency</span></span>
- <span data-ttu-id="628e3-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="628e3-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="628e3-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="628e3-221">PackageLicenseFile</span></span>
- <span data-ttu-id="628e3-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="628e3-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-223">PackageProjectUrl</span></span>
- <span data-ttu-id="628e3-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-224">PackageIconUrl</span></span>
- <span data-ttu-id="628e3-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="628e3-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="628e3-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="628e3-226">PackageTags</span></span>
- <span data-ttu-id="628e3-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="628e3-227">PackageOutputPath</span></span>
- <span data-ttu-id="628e3-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="628e3-228">IncludeSymbols</span></span>
- <span data-ttu-id="628e3-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="628e3-229">IncludeSource</span></span>
- <span data-ttu-id="628e3-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="628e3-230">PackageTypes</span></span>
- <span data-ttu-id="628e3-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="628e3-231">IsTool</span></span>
- <span data-ttu-id="628e3-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-232">RepositoryUrl</span></span>
- <span data-ttu-id="628e3-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="628e3-233">RepositoryType</span></span>
- <span data-ttu-id="628e3-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="628e3-234">RepositoryBranch</span></span>
- <span data-ttu-id="628e3-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="628e3-235">RepositoryCommit</span></span>
- <span data-ttu-id="628e3-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="628e3-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="628e3-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="628e3-237">MinClientVersion</span></span>
- <span data-ttu-id="628e3-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="628e3-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="628e3-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="628e3-239">IncludeContentInPack</span></span>
- <span data-ttu-id="628e3-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="628e3-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="628e3-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="628e3-241">ContentTargetFolders</span></span>
- <span data-ttu-id="628e3-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="628e3-242">NuspecFile</span></span>
- <span data-ttu-id="628e3-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="628e3-243">NuspecBasePath</span></span>
- <span data-ttu-id="628e3-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="628e3-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="628e3-245">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="628e3-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="628e3-246">Supprimer les dépendances</span><span class="sxs-lookup"><span data-stu-id="628e3-246">Suppress dependencies</span></span>

<span data-ttu-id="628e3-247">Pour supprimer les dépendances de package du package NuGet `SuppressDependenciesWhenPacking` généré `true` , affectez la valeur à qui autorisera l’ignorance de toutes les dépendances du fichier nupkg généré.</span><span class="sxs-lookup"><span data-stu-id="628e3-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="628e3-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="628e3-248">PackageIconUrl</span></span>

<span data-ttu-id="628e3-249">Dans le cadre de la modification du [problème NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sera finalement remplacé par `PackageIconUri` et peut être le chemin d’accès relatif à un fichier icône qui sera inclus à la racine du package résultant.</span><span class="sxs-lookup"><span data-stu-id="628e3-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="628e3-250">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="628e3-250">Output assemblies</span></span>

<span data-ttu-id="628e3-251">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="628e3-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="628e3-252">Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="628e3-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="628e3-253">Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="628e3-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="628e3-254">`IncludeBuildOutput`: Valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="628e3-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="628e3-255">`BuildOutputTargetFolder`: Spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="628e3-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="628e3-256">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="628e3-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="628e3-257">Références de package</span><span class="sxs-lookup"><span data-stu-id="628e3-257">Package references</span></span>

<span data-ttu-id="628e3-258">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="628e3-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="628e3-259">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="628e3-259">Project to project references</span></span>

<span data-ttu-id="628e3-260">Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :</span><span class="sxs-lookup"><span data-stu-id="628e3-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="628e3-261">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="628e3-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="628e3-262">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="628e3-262">Including content in a package</span></span>

<span data-ttu-id="628e3-263">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="628e3-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="628e3-264">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="628e3-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="628e3-265">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="628e3-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="628e3-266">Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="628e3-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="628e3-267">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="628e3-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="628e3-268">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="628e3-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="628e3-269">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="628e3-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="628e3-270">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="628e3-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="628e3-271">Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`.</span><span class="sxs-lookup"><span data-stu-id="628e3-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="628e3-272">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="628e3-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="628e3-273">D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.</span><span class="sxs-lookup"><span data-stu-id="628e3-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="628e3-274">Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="628e3-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="628e3-275">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="628e3-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="628e3-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="628e3-276">IncludeSymbols</span></span>

<span data-ttu-id="628e3-277">Quand vous utilisez `MSBuild -t:pack -p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="628e3-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="628e3-278">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="628e3-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="628e3-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="628e3-279">IncludeSource</span></span>

<span data-ttu-id="628e3-280">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="628e3-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="628e3-281">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="628e3-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="628e3-282">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="628e3-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="628e3-283">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="628e3-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="628e3-284">Compression d’une expression de licence ou d’un fichier de licence</span><span class="sxs-lookup"><span data-stu-id="628e3-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="628e3-285">Lors de l’utilisation d’une expression de licence, la propriété PackageLicenseExpression doit être utilisée.</span><span class="sxs-lookup"><span data-stu-id="628e3-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="628e3-286">[Exemple d’expression de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="628e3-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="628e3-287">[En savoir plus sur les expressions de licence et les licences acceptées par NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="628e3-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="628e3-288">Lors de l’empaquetage d’un fichier de licence, vous devez utiliser la propriété PackageLicenseFile pour spécifier le chemin d’accès au package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="628e3-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="628e3-289">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="628e3-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="628e3-290">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="628e3-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="628e3-291">[Exemple de fichier de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="628e3-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="628e3-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="628e3-292">IsTool</span></span>

<span data-ttu-id="628e3-293">Lors de l’utilisation de `MSBuild -t:pack -p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="628e3-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="628e3-294">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="628e3-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="628e3-295">Compression à l’aide d’un fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="628e3-295">Packing using a .nuspec</span></span>

<span data-ttu-id="628e3-296">Bien qu’il soit recommandé d’inclure à la place [toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se `.nuspec` trouvent généralement dans le fichier du fichier projet, vous pouvez choisir d' `.nuspec` utiliser un fichier pour compresser votre projet.</span><span class="sxs-lookup"><span data-stu-id="628e3-296">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="628e3-297">Pour un projet de type non-SDK qui utilise `PackageReference`, vous devez effectuer `NuGet.Build.Tasks.Pack.targets` l’importation afin que la tâche Pack puisse être exécutée.</span><span class="sxs-lookup"><span data-stu-id="628e3-297">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="628e3-298">Vous devez toujours restaurer le projet avant de pouvoir compresser un fichier NuSpec.</span><span class="sxs-lookup"><span data-stu-id="628e3-298">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="628e3-299">(Un projet de type SDK comprend les cibles Pack par défaut.)</span><span class="sxs-lookup"><span data-stu-id="628e3-299">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="628e3-300">La version cible du .NET Framework du fichier projet n’est pas pertinente et n’est pas utilisée lors de la compression d’un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="628e3-300">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="628e3-301">Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="628e3-301">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="628e3-302">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="628e3-302">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="628e3-303">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="628e3-303">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="628e3-304">En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="628e3-304">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="628e3-305">`NuspecBasePath`: Chemin d’accès de `.nuspec` base pour le fichier.</span><span class="sxs-lookup"><span data-stu-id="628e3-305">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="628e3-306">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="628e3-306">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="628e3-307">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="628e3-307">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="628e3-308">Notez que le compactage d’un NuSpec à l’aide de dotnet. exe ou de MSBuild permet également de générer le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="628e3-308">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="628e3-309">Cela peut être évité en passant ```--no-build``` la propriété à dotnet. exe, qui est l’équivalent du ```<NoBuild>true</NoBuild> ``` paramètre dans votre fichier projet, ainsi que ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` le paramètre dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="628e3-309">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="628e3-310">Voici un exemple de fichier *. csproj* pour compresser un fichier NuSpec:</span><span class="sxs-lookup"><span data-stu-id="628e3-310">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="628e3-311">Points d’extension avancés pour créer un package personnalisé</span><span class="sxs-lookup"><span data-stu-id="628e3-311">Advanced extension points to create customized package</span></span>

<span data-ttu-id="628e3-312">La `pack` cible fournit deux points d’extension qui s’exécutent dans la build interne du Framework cible.</span><span class="sxs-lookup"><span data-stu-id="628e3-312">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="628e3-313">Les points d’extension prennent en charge l’inclusion de contenu et d’assemblys spécifiques au Framework cible dans un package:</span><span class="sxs-lookup"><span data-stu-id="628e3-313">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="628e3-314">`TargetsForTfmSpecificBuildOutput`Indicatif Utilisez pour les fichiers contenus `lib` dans le dossier ou dans un `BuildOutputTargetFolder`dossier spécifié à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="628e3-314">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="628e3-315">`TargetsForTfmSpecificContentInPackage`Indicatif Utilisez pour les `BuildOutputTargetFolder`fichiers en dehors de.</span><span class="sxs-lookup"><span data-stu-id="628e3-315">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="628e3-316">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="628e3-316">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="628e3-317">Écrivez une cible personnalisée et spécifiez-la comme valeur de `$(TargetsForTfmSpecificBuildOutput)` la propriété.</span><span class="sxs-lookup"><span data-stu-id="628e3-317">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="628e3-318">Pour tous les fichiers qui doivent être placés dans `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans ItemGroup `BuildOutputInPackage` et définir les deux valeurs de métadonnées suivantes:</span><span class="sxs-lookup"><span data-stu-id="628e3-318">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="628e3-319">`FinalOutputPath`: Chemin d’accès absolu du fichier; s’il n’est pas fourni, l’identité est utilisée pour évaluer le chemin source.</span><span class="sxs-lookup"><span data-stu-id="628e3-319">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="628e3-320">`TargetPath`:  Facultatif Définie lorsque le fichier doit être placé dans un sous-dossier `lib\<TargetFramework>` au sein de, comme les assemblys satellites qui se trouvent dans leurs dossiers de culture respectifs.</span><span class="sxs-lookup"><span data-stu-id="628e3-320">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="628e3-321">La valeur par défaut est le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="628e3-321">Defaults to the name of the file.</span></span>

<span data-ttu-id="628e3-322">Exemple :</span><span class="sxs-lookup"><span data-stu-id="628e3-322">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="628e3-323">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="628e3-323">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="628e3-324">Écrivez une cible personnalisée et spécifiez-la comme valeur de `$(TargetsForTfmSpecificContentInPackage)` la propriété.</span><span class="sxs-lookup"><span data-stu-id="628e3-324">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="628e3-325">Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes:</span><span class="sxs-lookup"><span data-stu-id="628e3-325">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="628e3-326">`PackagePath`: Chemin d’accès où le fichier doit être généré dans le package.</span><span class="sxs-lookup"><span data-stu-id="628e3-326">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="628e3-327">NuGet émet un avertissement si plusieurs fichiers sont ajoutés au même chemin d’accès de package.</span><span class="sxs-lookup"><span data-stu-id="628e3-327">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="628e3-328">`BuildAction`: Action de génération à assigner au fichier, obligatoire uniquement si le chemin d’accès du `contentFiles` package se trouve dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="628e3-328">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="628e3-329">La valeur par défaut est «None».</span><span class="sxs-lookup"><span data-stu-id="628e3-329">Defaults to "None".</span></span>

<span data-ttu-id="628e3-330">Exemple :</span><span class="sxs-lookup"><span data-stu-id="628e3-330">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="628e3-331">Cible restore</span><span class="sxs-lookup"><span data-stu-id="628e3-331">restore target</span></span>

<span data-ttu-id="628e3-332">`MSBuild -t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="628e3-332">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="628e3-333">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="628e3-333">Read all project to project references</span></span>
1. <span data-ttu-id="628e3-334">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="628e3-334">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="628e3-335">Passer des données MSBuild à NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="628e3-335">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="628e3-336">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="628e3-336">Run restore</span></span>
1. <span data-ttu-id="628e3-337">Télécharger les packages</span><span class="sxs-lookup"><span data-stu-id="628e3-337">Download packages</span></span>
1. <span data-ttu-id="628e3-338">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="628e3-338">Write assets file, targets, and props</span></span>

<span data-ttu-id="628e3-339">La `restore` cible fonctionne **uniquement** pour les projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="628e3-339">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="628e3-340">Il ne fonctionne **pas** pour les projets qui `packages.config` utilisent le format; utilisez la [restauration NuGet](../reference/cli-reference/cli-ref-restore.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="628e3-340">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="628e3-341">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="628e3-341">Restore properties</span></span>

<span data-ttu-id="628e3-342">Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="628e3-342">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="628e3-343">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `-p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="628e3-343">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="628e3-344">Propriété</span><span class="sxs-lookup"><span data-stu-id="628e3-344">Property</span></span> | <span data-ttu-id="628e3-345">Description</span><span class="sxs-lookup"><span data-stu-id="628e3-345">Description</span></span> |
|--------|--------|
| <span data-ttu-id="628e3-346">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="628e3-346">RestoreSources</span></span> | <span data-ttu-id="628e3-347">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="628e3-347">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="628e3-348">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="628e3-348">RestorePackagesPath</span></span> | <span data-ttu-id="628e3-349">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="628e3-349">User packages folder path.</span></span> |
| <span data-ttu-id="628e3-350">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="628e3-350">RestoreDisableParallel</span></span> | <span data-ttu-id="628e3-351">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="628e3-351">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="628e3-352">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="628e3-352">RestoreConfigFile</span></span> | <span data-ttu-id="628e3-353">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="628e3-353">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="628e3-354">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="628e3-354">RestoreNoCache</span></span> | <span data-ttu-id="628e3-355">Si la valeur est true, évite d’utiliser des packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="628e3-355">If true, avoids using cached packages.</span></span> <span data-ttu-id="628e3-356">Consultez [gestion des dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="628e3-356">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="628e3-357">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="628e3-357">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="628e3-358">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="628e3-358">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="628e3-359">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="628e3-359">RestoreFallbackFolders</span></span> | <span data-ttu-id="628e3-360">Dossiers de secours, utilisés de la même façon que le dossier des packages de l’utilisateur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="628e3-360">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="628e3-361">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="628e3-361">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="628e3-362">Sources supplémentaires à utiliser pendant la restauration.</span><span class="sxs-lookup"><span data-stu-id="628e3-362">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="628e3-363">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="628e3-363">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="628e3-364">Dossiers de secours supplémentaires à utiliser lors de la restauration.</span><span class="sxs-lookup"><span data-stu-id="628e3-364">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="628e3-365">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="628e3-365">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="628e3-366">Exclut les dossiers de secours spécifiés dans`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="628e3-366">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="628e3-367">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="628e3-367">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="628e3-368">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="628e3-368">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="628e3-369">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="628e3-369">RestoreGraphProjectInput</span></span> | <span data-ttu-id="628e3-370">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="628e3-370">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="628e3-371">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="628e3-371">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="628e3-372">Lorsque les projets sont collectés via MSBuild, il détermine s’ils sont collectés à l’aide de l' `SkipNonexistentTargets` optimisation.</span><span class="sxs-lookup"><span data-stu-id="628e3-372">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="628e3-373">Si la valeur n’est pas définie `true`, la valeur par défaut est.</span><span class="sxs-lookup"><span data-stu-id="628e3-373">When not set, defaults to `true`.</span></span> <span data-ttu-id="628e3-374">La conséquence est un comportement de basculement rapide lorsque les cibles d’un projet ne peuvent pas être importées.</span><span class="sxs-lookup"><span data-stu-id="628e3-374">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="628e3-375">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="628e3-375">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="628e3-376">Dossier de sortie, avec `BaseIntermediateOutputPath` comme valeur par défaut et le `obj` dossier.</span><span class="sxs-lookup"><span data-stu-id="628e3-376">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="628e3-377">Exemples</span><span class="sxs-lookup"><span data-stu-id="628e3-377">Examples</span></span>

<span data-ttu-id="628e3-378">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="628e3-378">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="628e3-379">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="628e3-379">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="628e3-380">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="628e3-380">Restore outputs</span></span>

<span data-ttu-id="628e3-381">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="628e3-381">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="628e3-382">Fichier</span><span class="sxs-lookup"><span data-stu-id="628e3-382">File</span></span> | <span data-ttu-id="628e3-383">Description</span><span class="sxs-lookup"><span data-stu-id="628e3-383">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="628e3-384">Contient le graphique de dépendance de toutes les références de package.</span><span class="sxs-lookup"><span data-stu-id="628e3-384">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="628e3-385">Références à des propriétés MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="628e3-385">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="628e3-386">Références à des cibles MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="628e3-386">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="628e3-387">Restauration et génération à l’aide d’une commande MSBuild</span><span class="sxs-lookup"><span data-stu-id="628e3-387">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="628e3-388">En raison du fait que NuGet peut restaurer des packages qui déplacent des cibles et des props MSBuild, les évaluations de la restauration et de la build sont exécutées avec des propriétés globales différentes.</span><span class="sxs-lookup"><span data-stu-id="628e3-388">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="628e3-389">Cela signifie que les éléments suivants auront un comportement imprévisible et souvent incorrect.</span><span class="sxs-lookup"><span data-stu-id="628e3-389">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="628e3-390">Au lieu de cela, l’approche recommandée est la suivante:</span><span class="sxs-lookup"><span data-stu-id="628e3-390">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="628e3-391">La même logique s’applique à d’autres cibles `build`similaires à celles de.</span><span class="sxs-lookup"><span data-stu-id="628e3-391">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="628e3-392">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="628e3-392">PackageTargetFallback</span></span>

<span data-ttu-id="628e3-393">L’élément `PackageTargetFallback` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="628e3-393">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="628e3-394">Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../reference/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="628e3-394">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="628e3-395">Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.</span><span class="sxs-lookup"><span data-stu-id="628e3-395">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="628e3-396">Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue.</span><span class="sxs-lookup"><span data-stu-id="628e3-396">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="628e3-397">Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :</span><span class="sxs-lookup"><span data-stu-id="628e3-397">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="628e3-398">Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="628e3-398">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="628e3-399">Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="628e3-399">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="628e3-400">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="628e3-400">Replacing one library from a restore graph</span></span>

<span data-ttu-id="628e3-401">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="628e3-401">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="628e3-402">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="628e3-402">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="628e3-403">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="628e3-403">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
