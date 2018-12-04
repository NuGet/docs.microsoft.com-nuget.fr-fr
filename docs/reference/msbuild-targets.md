---
title: Commandes pack et restore NuGet comme cibles MSBuild
description: Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9427d87f69a2e942a9802fbdae5193eead1c724
ms.sourcegitcommit: af58d59669674c3bc0a230d5764e37020a9a3f1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52831018"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5f491-103">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="5f491-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5f491-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="5f491-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="5f491-105">Avec le format PackageReference, NuGet 4.0+ peut stocker toutes les métadonnées du manifeste directement dans un fichier projet, au lieu d’utiliser un fichier `.nuspec` distinct.</span><span class="sxs-lookup"><span data-stu-id="5f491-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5f491-106">Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5f491-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5f491-107">Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5f491-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5f491-108">(Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../tools/cli-ref-pack.md) et [restore](../tools/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)</span><span class="sxs-lookup"><span data-stu-id="5f491-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5f491-109">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="5f491-109">Target build order</span></span>

<span data-ttu-id="5f491-110">Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="5f491-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5f491-111">Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression.</span><span class="sxs-lookup"><span data-stu-id="5f491-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5f491-112">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="5f491-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="5f491-113">De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5f491-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5f491-114">Cible pack</span><span class="sxs-lookup"><span data-stu-id="5f491-114">pack target</span></span>

<span data-ttu-id="5f491-115">Pour les projets .NET Standard en utilisant le format PackageReference, à l’aide de `msbuild -t:pack` dessine des entrées à partir du fichier de projet à utiliser pour créer un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="5f491-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="5f491-116">Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier projet au sein du premier nœud `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="5f491-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5f491-117">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="5f491-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5f491-118">Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5f491-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5f491-119">Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5f491-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5f491-120">Valeur d’attribut/NuSpec</span><span class="sxs-lookup"><span data-stu-id="5f491-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5f491-121">Propriété MSBuild</span><span class="sxs-lookup"><span data-stu-id="5f491-121">MSBuild Property</span></span> | <span data-ttu-id="5f491-122">Par défaut</span><span class="sxs-lookup"><span data-stu-id="5f491-122">Default</span></span> | <span data-ttu-id="5f491-123">Notes</span><span class="sxs-lookup"><span data-stu-id="5f491-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5f491-124">Id</span><span class="sxs-lookup"><span data-stu-id="5f491-124">Id</span></span> | <span data-ttu-id="5f491-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="5f491-125">PackageId</span></span> | <span data-ttu-id="5f491-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5f491-126">AssemblyName</span></span> | <span data-ttu-id="5f491-127">$(AssemblyName) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="5f491-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5f491-128">Version</span><span class="sxs-lookup"><span data-stu-id="5f491-128">Version</span></span> | <span data-ttu-id="5f491-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5f491-129">PackageVersion</span></span> | <span data-ttu-id="5f491-130">Version</span><span class="sxs-lookup"><span data-stu-id="5f491-130">Version</span></span> | <span data-ttu-id="5f491-131">Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 »</span><span class="sxs-lookup"><span data-stu-id="5f491-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5f491-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5f491-132">VersionPrefix</span></span> | <span data-ttu-id="5f491-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5f491-133">PackageVersionPrefix</span></span> | <span data-ttu-id="5f491-134">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-134">empty</span></span> | <span data-ttu-id="5f491-135">La définition de PackageVersion remplace PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5f491-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5f491-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5f491-136">VersionSuffix</span></span> | <span data-ttu-id="5f491-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5f491-137">PackageVersionSuffix</span></span> | <span data-ttu-id="5f491-138">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-138">empty</span></span> | <span data-ttu-id="5f491-139">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5f491-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5f491-140">La définition de PackageVersion remplace PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5f491-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5f491-141">Auteurs</span><span class="sxs-lookup"><span data-stu-id="5f491-141">Authors</span></span> | <span data-ttu-id="5f491-142">Auteurs</span><span class="sxs-lookup"><span data-stu-id="5f491-142">Authors</span></span> | <span data-ttu-id="5f491-143">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="5f491-143">Username of the current user</span></span> | |
| <span data-ttu-id="5f491-144">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="5f491-144">Owners</span></span> | <span data-ttu-id="5f491-145">N/A</span><span class="sxs-lookup"><span data-stu-id="5f491-145">N/A</span></span> | <span data-ttu-id="5f491-146">Ne figure pas dans NuSpec</span><span class="sxs-lookup"><span data-stu-id="5f491-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5f491-147">Titre</span><span class="sxs-lookup"><span data-stu-id="5f491-147">Title</span></span> | <span data-ttu-id="5f491-148">Titre</span><span class="sxs-lookup"><span data-stu-id="5f491-148">Title</span></span> | <span data-ttu-id="5f491-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="5f491-149">The PackageId</span></span>| |
| <span data-ttu-id="5f491-150">Description</span><span class="sxs-lookup"><span data-stu-id="5f491-150">Description</span></span> | <span data-ttu-id="5f491-151">Description</span><span class="sxs-lookup"><span data-stu-id="5f491-151">Description</span></span> | <span data-ttu-id="5f491-152">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="5f491-152">"Package Description"</span></span> | |
| <span data-ttu-id="5f491-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="5f491-153">Copyright</span></span> | <span data-ttu-id="5f491-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="5f491-154">Copyright</span></span> | <span data-ttu-id="5f491-155">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-155">empty</span></span> | |
| <span data-ttu-id="5f491-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5f491-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5f491-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5f491-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5f491-158">False</span><span class="sxs-lookup"><span data-stu-id="5f491-158">false</span></span> | |
| <span data-ttu-id="5f491-159">licence</span><span class="sxs-lookup"><span data-stu-id="5f491-159">license</span></span> | <span data-ttu-id="5f491-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="5f491-160">PackageLicenseExpression</span></span> | <span data-ttu-id="5f491-161">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-161">empty</span></span> | <span data-ttu-id="5f491-162">Correspond à `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="5f491-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="5f491-163">licence</span><span class="sxs-lookup"><span data-stu-id="5f491-163">license</span></span> | <span data-ttu-id="5f491-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5f491-164">PackageLicenseFile</span></span> | <span data-ttu-id="5f491-165">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-165">empty</span></span> | <span data-ttu-id="5f491-166">Correspond à `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="5f491-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="5f491-167">Vous devrez peut-être pack explicitement le fichier de licence référencé.</span><span class="sxs-lookup"><span data-stu-id="5f491-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="5f491-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-168">LicenseUrl</span></span> | <span data-ttu-id="5f491-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-169">PackageLicenseUrl</span></span> | <span data-ttu-id="5f491-170">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-170">empty</span></span> | <span data-ttu-id="5f491-171">`licenseUrl` est déconseillé, utilisez la propriété PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5f491-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="5f491-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-172">ProjectUrl</span></span> | <span data-ttu-id="5f491-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-173">PackageProjectUrl</span></span> | <span data-ttu-id="5f491-174">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-174">empty</span></span> | |
| <span data-ttu-id="5f491-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-175">IconUrl</span></span> | <span data-ttu-id="5f491-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-176">PackageIconUrl</span></span> | <span data-ttu-id="5f491-177">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-177">empty</span></span> | |
| <span data-ttu-id="5f491-178">Balises</span><span class="sxs-lookup"><span data-stu-id="5f491-178">Tags</span></span> | <span data-ttu-id="5f491-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5f491-179">PackageTags</span></span> | <span data-ttu-id="5f491-180">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-180">empty</span></span> | <span data-ttu-id="5f491-181">Les balises sont séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5f491-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5f491-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5f491-182">ReleaseNotes</span></span> | <span data-ttu-id="5f491-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5f491-183">PackageReleaseNotes</span></span> | <span data-ttu-id="5f491-184">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-184">empty</span></span> | |
| <span data-ttu-id="5f491-185">Url/du référentiel</span><span class="sxs-lookup"><span data-stu-id="5f491-185">Repository/Url</span></span> | <span data-ttu-id="5f491-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-186">RepositoryUrl</span></span> | <span data-ttu-id="5f491-187">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-187">empty</span></span> | <span data-ttu-id="5f491-188">URL du référentiel utilisé pour cloner ou extraire le code source.</span><span class="sxs-lookup"><span data-stu-id="5f491-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="5f491-189">Exemple : *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="5f491-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="5f491-190">/ Type de référentiel</span><span class="sxs-lookup"><span data-stu-id="5f491-190">Repository/Type</span></span> | <span data-ttu-id="5f491-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5f491-191">RepositoryType</span></span> | <span data-ttu-id="5f491-192">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-192">empty</span></span> | <span data-ttu-id="5f491-193">Type de référentiel.</span><span class="sxs-lookup"><span data-stu-id="5f491-193">Repository type.</span></span> <span data-ttu-id="5f491-194">Exemples : *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="5f491-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="5f491-195">/ Branche du référentiel</span><span class="sxs-lookup"><span data-stu-id="5f491-195">Repository/Branch</span></span> | <span data-ttu-id="5f491-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5f491-196">RepositoryBranch</span></span> | <span data-ttu-id="5f491-197">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-197">empty</span></span> | <span data-ttu-id="5f491-198">Informations de branche de référentiel facultatif.</span><span class="sxs-lookup"><span data-stu-id="5f491-198">Optional repository branch information.</span></span> <span data-ttu-id="5f491-199">*RepositoryUrl* doit également être spécifié pour cette propriété à inclure.</span><span class="sxs-lookup"><span data-stu-id="5f491-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5f491-200">Exemple : *master* (4.7.0+ NuGet)</span><span class="sxs-lookup"><span data-stu-id="5f491-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5f491-201">Référentiel/validation</span><span class="sxs-lookup"><span data-stu-id="5f491-201">Repository/Commit</span></span> | <span data-ttu-id="5f491-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5f491-202">RepositoryCommit</span></span> | <span data-ttu-id="5f491-203">vide</span><span class="sxs-lookup"><span data-stu-id="5f491-203">empty</span></span> | <span data-ttu-id="5f491-204">Validation du référentiel facultatif ou l’ensemble de modifications pour indiquer à qui la source du package a été créé.</span><span class="sxs-lookup"><span data-stu-id="5f491-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="5f491-205">*RepositoryUrl* doit également être spécifié pour cette propriété à inclure.</span><span class="sxs-lookup"><span data-stu-id="5f491-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5f491-206">Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (4.7.0+ NuGet)</span><span class="sxs-lookup"><span data-stu-id="5f491-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5f491-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="5f491-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5f491-208">Récapitulatif</span><span class="sxs-lookup"><span data-stu-id="5f491-208">Summary</span></span> | <span data-ttu-id="5f491-209">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="5f491-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5f491-210">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="5f491-210">pack target inputs</span></span>

- <span data-ttu-id="5f491-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5f491-211">IsPackable</span></span>
- <span data-ttu-id="5f491-212">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5f491-212">PackageVersion</span></span>
- <span data-ttu-id="5f491-213">PackageId</span><span class="sxs-lookup"><span data-stu-id="5f491-213">PackageId</span></span>
- <span data-ttu-id="5f491-214">Auteurs</span><span class="sxs-lookup"><span data-stu-id="5f491-214">Authors</span></span>
- <span data-ttu-id="5f491-215">Description</span><span class="sxs-lookup"><span data-stu-id="5f491-215">Description</span></span>
- <span data-ttu-id="5f491-216">Copyright</span><span class="sxs-lookup"><span data-stu-id="5f491-216">Copyright</span></span>
- <span data-ttu-id="5f491-217">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5f491-217">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5f491-218">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5f491-218">DevelopmentDependency</span></span>
- <span data-ttu-id="5f491-219">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="5f491-219">PackageLicenseExpression</span></span>
- <span data-ttu-id="5f491-220">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5f491-220">PackageLicenseFile</span></span>
- <span data-ttu-id="5f491-221">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-221">PackageLicenseUrl</span></span>
- <span data-ttu-id="5f491-222">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-222">PackageProjectUrl</span></span>
- <span data-ttu-id="5f491-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-223">PackageIconUrl</span></span>
- <span data-ttu-id="5f491-224">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5f491-224">PackageReleaseNotes</span></span>
- <span data-ttu-id="5f491-225">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5f491-225">PackageTags</span></span>
- <span data-ttu-id="5f491-226">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5f491-226">PackageOutputPath</span></span>
- <span data-ttu-id="5f491-227">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5f491-227">IncludeSymbols</span></span>
- <span data-ttu-id="5f491-228">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5f491-228">IncludeSource</span></span>
- <span data-ttu-id="5f491-229">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5f491-229">PackageTypes</span></span>
- <span data-ttu-id="5f491-230">IsTool</span><span class="sxs-lookup"><span data-stu-id="5f491-230">IsTool</span></span>
- <span data-ttu-id="5f491-231">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-231">RepositoryUrl</span></span>
- <span data-ttu-id="5f491-232">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5f491-232">RepositoryType</span></span>
- <span data-ttu-id="5f491-233">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5f491-233">RepositoryBranch</span></span>
- <span data-ttu-id="5f491-234">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5f491-234">RepositoryCommit</span></span>
- <span data-ttu-id="5f491-235">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5f491-235">NoPackageAnalysis</span></span>
- <span data-ttu-id="5f491-236">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5f491-236">MinClientVersion</span></span>
- <span data-ttu-id="5f491-237">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5f491-237">IncludeBuildOutput</span></span>
- <span data-ttu-id="5f491-238">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5f491-238">IncludeContentInPack</span></span>
- <span data-ttu-id="5f491-239">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5f491-239">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5f491-240">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5f491-240">ContentTargetFolders</span></span>
- <span data-ttu-id="5f491-241">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5f491-241">NuspecFile</span></span>
- <span data-ttu-id="5f491-242">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5f491-242">NuspecBasePath</span></span>
- <span data-ttu-id="5f491-243">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5f491-243">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5f491-244">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="5f491-244">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5f491-245">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5f491-245">PackageIconUrl</span></span>

<span data-ttu-id="5f491-246">Dans le cadre de la modification pour [NuGet problème 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sera finalement remplacée par `PackageIconUri` et peut être un chemin relatif vers un fichier d’icône qui sera inclus à la racine du package obtenu.</span><span class="sxs-lookup"><span data-stu-id="5f491-246">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5f491-247">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="5f491-247">Output assemblies</span></span>

<span data-ttu-id="5f491-248">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="5f491-248">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5f491-249">Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="5f491-249">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5f491-250">Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="5f491-250">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5f491-251">`IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="5f491-251">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5f491-252">`BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="5f491-252">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5f491-253">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="5f491-253">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5f491-254">Références de package</span><span class="sxs-lookup"><span data-stu-id="5f491-254">Package references</span></span>

<span data-ttu-id="5f491-255">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="5f491-255">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5f491-256">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="5f491-256">Project to project references</span></span>

<span data-ttu-id="5f491-257">Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :</span><span class="sxs-lookup"><span data-stu-id="5f491-257">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5f491-258">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="5f491-258">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5f491-259">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="5f491-259">Including content in a package</span></span>

<span data-ttu-id="5f491-260">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="5f491-260">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5f491-261">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5f491-261">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="5f491-262">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="5f491-262">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5f491-263">Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="5f491-263">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5f491-264">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="5f491-264">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5f491-265">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5f491-265">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5f491-266">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="5f491-266">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5f491-267">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="5f491-267">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5f491-268">Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`.</span><span class="sxs-lookup"><span data-stu-id="5f491-268">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5f491-269">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="5f491-269">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5f491-270">D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.</span><span class="sxs-lookup"><span data-stu-id="5f491-270">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5f491-271">Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="5f491-271">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5f491-272">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="5f491-272">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5f491-273">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5f491-273">IncludeSymbols</span></span>

<span data-ttu-id="5f491-274">Quand vous utilisez `MSBuild -t:pack -p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="5f491-274">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5f491-275">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="5f491-275">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5f491-276">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5f491-276">IncludeSource</span></span>

<span data-ttu-id="5f491-277">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="5f491-277">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5f491-278">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="5f491-278">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5f491-279">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="5f491-279">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5f491-280">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="5f491-280">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="5f491-281">Une expression de licence ou d’un fichier de licence de livraison</span><span class="sxs-lookup"><span data-stu-id="5f491-281">Packing a license expression or a license file</span></span>

<span data-ttu-id="5f491-282">Lorsque vous utilisez une expression de la licence, la propriété PackageLicenseExpression doit être utilisée.</span><span class="sxs-lookup"><span data-stu-id="5f491-282">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="5f491-283">[Exemple d’expression de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="5f491-283">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

<span data-ttu-id="5f491-284">Lors de la compression d’un fichier de licence, vous devez utiliser PackageLicenseFile propriété pour spécifier le chemin du package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="5f491-284">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="5f491-285">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="5f491-285">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="5f491-286">Exemple :</span><span class="sxs-lookup"><span data-stu-id="5f491-286">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
<span data-ttu-id="5f491-287">[Exemple de fichier de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="5f491-287">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="5f491-288">IsTool</span><span class="sxs-lookup"><span data-stu-id="5f491-288">IsTool</span></span>

<span data-ttu-id="5f491-289">Lors de l’utilisation de `MSBuild -t:pack -p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="5f491-289">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5f491-290">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="5f491-290">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5f491-291">Compression à l’aide d’un fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="5f491-291">Packing using a .nuspec</span></span>

<span data-ttu-id="5f491-292">Vous pouvez utiliser un `.nuspec` fichier à compresser votre projet, sous réserve que vous avez un fichier de projet SDK à importer `NuGet.Build.Tasks.Pack.targets` afin que la tâche pack peut être exécutée.</span><span class="sxs-lookup"><span data-stu-id="5f491-292">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5f491-293">Vous devez toujours restaurer le projet avant que vous pouvez choisir un fichier nuspec.</span><span class="sxs-lookup"><span data-stu-id="5f491-293">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="5f491-294">Le framework cible du fichier projet n’est pas pertinent et pas utilisé lors de la compression d’un fichier nuspec.</span><span class="sxs-lookup"><span data-stu-id="5f491-294">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="5f491-295">Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="5f491-295">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5f491-296">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="5f491-296">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5f491-297">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5f491-297">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5f491-298">En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="5f491-298">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5f491-299">`NuspecBasePath` : chemin de base pour le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5f491-299">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5f491-300">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="5f491-300">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5f491-301">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="5f491-301">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5f491-302">Veuillez noter qu’un nuspec de livraison à l’aide de dotnet.exe ou msbuild permet d’accéder à la génération du projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="5f491-302">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="5f491-303">Cela peut être évité en passant ```--no-build``` dotnet.exe, qui est l’équivalent du paramètre de propriété ```<NoBuild>true</NoBuild> ``` dans votre fichier projet, ainsi que de paramètre ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` dans le fichier projet</span><span class="sxs-lookup"><span data-stu-id="5f491-303">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="5f491-304">Un exemple d’un fichier csproj pour compresser un fichier nuspec est :</span><span class="sxs-lookup"><span data-stu-id="5f491-304">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="5f491-305">Avancée des points d’extension pour créer le package personnalisé</span><span class="sxs-lookup"><span data-stu-id="5f491-305">Advanced extension points to create customized package</span></span>

<span data-ttu-id="5f491-306">Le `pack` cible fournit deux points d’extension qui s’exécutent dans la build spécifique du framework cible interne,.</span><span class="sxs-lookup"><span data-stu-id="5f491-306">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="5f491-307">Les points d’extension prise en charge inclusion de contenu spécifique du framework cible et les assemblys dans un package :</span><span class="sxs-lookup"><span data-stu-id="5f491-307">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="5f491-308">`TargetsForTfmSpecificBuildOutput` cible : utilisation de fichiers à l’intérieur de la `lib` dossier ou un dossier spécifié à l’aide `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="5f491-308">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="5f491-309">`TargetsForTfmSpecificContentInPackage` cible : utilisation de fichiers en dehors de la `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="5f491-309">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="5f491-310">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5f491-310">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="5f491-311">Écrire une cible personnalisée et spécifiez-le comme valeur de la `$(TargetsForTfmSpecificBuildOutput)` propriété.</span><span class="sxs-lookup"><span data-stu-id="5f491-311">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="5f491-312">Pour tous les fichiers qui doivent passer dans le `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans un ItemGroup `BuildOutputInPackage` et définissez les deux valeurs de métadonnées suivantes :</span><span class="sxs-lookup"><span data-stu-id="5f491-312">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="5f491-313">`FinalOutputPath`: Le chemin d’accès absolu du fichier ; Si n’est fourni, l’identité est utilisée pour évaluer le chemin d’accès source.</span><span class="sxs-lookup"><span data-stu-id="5f491-313">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="5f491-314">`TargetPath`: (Facultatif) défini quand le fichier doit aller dans un sous-dossier au sein de `lib\<TargetFramework>` , tels que les assemblys satellites disponibles vont dans leurs dossiers de culture respectifs.</span><span class="sxs-lookup"><span data-stu-id="5f491-314">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="5f491-315">La valeur par défaut est le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="5f491-315">Defaults to the name of the file.</span></span>

<span data-ttu-id="5f491-316">Exemple :</span><span class="sxs-lookup"><span data-stu-id="5f491-316">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="5f491-317">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="5f491-317">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="5f491-318">Écrire une cible personnalisée et spécifiez-le comme valeur de la `$(TargetsForTfmSpecificContentInPackage)` propriété.</span><span class="sxs-lookup"><span data-stu-id="5f491-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="5f491-319">Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans un ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes :</span><span class="sxs-lookup"><span data-stu-id="5f491-319">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="5f491-320">`PackagePath`: Chemin d’accès où le fichier doit être sortie dans le package.</span><span class="sxs-lookup"><span data-stu-id="5f491-320">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="5f491-321">NuGet émet un avertissement si plus d’un fichier est ajouté à la même chemin d’accès du package.</span><span class="sxs-lookup"><span data-stu-id="5f491-321">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="5f491-322">`BuildAction`: L’action de génération à assigner au fichier, requis uniquement si le chemin d’accès du package est dans le `contentFiles` dossier.</span><span class="sxs-lookup"><span data-stu-id="5f491-322">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="5f491-323">Valeur par défaut est « None ».</span><span class="sxs-lookup"><span data-stu-id="5f491-323">Defaults to "None".</span></span>

<span data-ttu-id="5f491-324">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="5f491-324">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="5f491-325">Cible restore</span><span class="sxs-lookup"><span data-stu-id="5f491-325">restore target</span></span>

<span data-ttu-id="5f491-326">`MSBuild -t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5f491-326">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5f491-327">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="5f491-327">Read all project to project references</span></span>
1. <span data-ttu-id="5f491-328">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="5f491-328">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5f491-329">Passer des données msbuild à NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="5f491-329">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5f491-330">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="5f491-330">Run restore</span></span>
1. <span data-ttu-id="5f491-331">Télécharger les packages</span><span class="sxs-lookup"><span data-stu-id="5f491-331">Download packages</span></span>
1. <span data-ttu-id="5f491-332">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="5f491-332">Write assets file, targets, and props</span></span>

<span data-ttu-id="5f491-333">Le `restore` cibler works **uniquement** pour les projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="5f491-333">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="5f491-334">C’est le cas **pas** Professionnel pour les projets utilisant le `packages.config` format ; utiliser [restauration nuget](../tools/cli-ref-restore.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="5f491-334">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5f491-335">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="5f491-335">Restore properties</span></span>

<span data-ttu-id="5f491-336">Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="5f491-336">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5f491-337">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `-p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="5f491-337">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5f491-338">Propriété</span><span class="sxs-lookup"><span data-stu-id="5f491-338">Property</span></span> | <span data-ttu-id="5f491-339">Description</span><span class="sxs-lookup"><span data-stu-id="5f491-339">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5f491-340">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5f491-340">RestoreSources</span></span> | <span data-ttu-id="5f491-341">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5f491-341">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5f491-342">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5f491-342">RestorePackagesPath</span></span> | <span data-ttu-id="5f491-343">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5f491-343">User packages folder path.</span></span> |
| <span data-ttu-id="5f491-344">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5f491-344">RestoreDisableParallel</span></span> | <span data-ttu-id="5f491-345">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="5f491-345">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5f491-346">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5f491-346">RestoreConfigFile</span></span> | <span data-ttu-id="5f491-347">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="5f491-347">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5f491-348">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5f491-348">RestoreNoCache</span></span> | <span data-ttu-id="5f491-349">Si la valeur est true, permet d’éviter l’utilisation de packages de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="5f491-349">If true, avoids using cached packages.</span></span> <span data-ttu-id="5f491-350">Consultez [gérer les packages globaux et les dossiers de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5f491-350">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="5f491-351">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5f491-351">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5f491-352">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="5f491-352">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5f491-353">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5f491-353">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5f491-354">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="5f491-354">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5f491-355">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5f491-355">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5f491-356">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="5f491-356">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5f491-357">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="5f491-357">RestoreOutputPath</span></span> | <span data-ttu-id="5f491-358">Dossier de sortie qui est par défaut le dossier `obj`.</span><span class="sxs-lookup"><span data-stu-id="5f491-358">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="5f491-359">Exemples</span><span class="sxs-lookup"><span data-stu-id="5f491-359">Examples</span></span>

<span data-ttu-id="5f491-360">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="5f491-360">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="5f491-361">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="5f491-361">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5f491-362">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="5f491-362">Restore outputs</span></span>

<span data-ttu-id="5f491-363">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="5f491-363">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5f491-364">Fichier</span><span class="sxs-lookup"><span data-stu-id="5f491-364">File</span></span> | <span data-ttu-id="5f491-365">Description</span><span class="sxs-lookup"><span data-stu-id="5f491-365">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5f491-366">Contient le graphique de dépendance de toutes les références de package.</span><span class="sxs-lookup"><span data-stu-id="5f491-366">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5f491-367">Références à des propriétés MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="5f491-367">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5f491-368">Références à des cibles MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="5f491-368">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="5f491-369">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5f491-369">PackageTargetFallback</span></span>

<span data-ttu-id="5f491-370">L’élément `PackageTargetFallback` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="5f491-370">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5f491-371">Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../reference/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="5f491-371">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5f491-372">Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.</span><span class="sxs-lookup"><span data-stu-id="5f491-372">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5f491-373">Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue.</span><span class="sxs-lookup"><span data-stu-id="5f491-373">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5f491-374">Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :</span><span class="sxs-lookup"><span data-stu-id="5f491-374">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5f491-375">Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="5f491-375">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5f491-376">Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="5f491-376">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5f491-377">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="5f491-377">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5f491-378">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="5f491-378">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5f491-379">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="5f491-379">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5f491-380">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="5f491-380">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
