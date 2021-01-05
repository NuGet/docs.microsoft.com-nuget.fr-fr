---
title: Commandes pack et restore NuGet comme cibles MSBuild
description: Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 66df4e0e4739300608fd5f9e44eea5bcd00079c8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699890"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="44cf8-103">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="44cf8-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="44cf8-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="44cf8-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="44cf8-105">Avec le format [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + peut stocker toutes les métadonnées de manifeste directement dans un fichier projet plutôt que d’utiliser un `.nuspec` fichier séparé.</span><span class="sxs-lookup"><span data-stu-id="44cf8-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="44cf8-106">Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="44cf8-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="44cf8-107">Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="44cf8-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="44cf8-108">Pour obtenir des instructions sur la création d’un package NuGet à l’aide de MSBuild, consultez [créer un package NuGet à l’aide de MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="44cf8-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="44cf8-109">(Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../reference/cli-reference/cli-ref-pack.md) et [restore](../reference/cli-reference/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)</span><span class="sxs-lookup"><span data-stu-id="44cf8-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="44cf8-110">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="44cf8-110">Target build order</span></span>

<span data-ttu-id="44cf8-111">Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="44cf8-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="44cf8-112">Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression.</span><span class="sxs-lookup"><span data-stu-id="44cf8-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="44cf8-113">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="44cf8-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="44cf8-114">De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.</span><span class="sxs-lookup"><span data-stu-id="44cf8-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="44cf8-115">`$(OutputPath)` est relatif et s’attend à ce que vous exécutiez la commande à partir de la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="44cf8-116">Cible pack</span><span class="sxs-lookup"><span data-stu-id="44cf8-116">pack target</span></span>

<span data-ttu-id="44cf8-117">Pour les projets .NET Standard utilisant le format PackageReference, l’utilisation de `msbuild -t:pack` dessine des entrées à partir du fichier projet à utiliser lors de la création d’un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="44cf8-118">Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier projet au sein du premier nœud `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="44cf8-119">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="44cf8-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="44cf8-120">Pour des raisons pratiques, la table est organisée par la propriété équivalente dans un [ `.nuspec` fichier](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="44cf8-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="44cf8-121">Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.</span><span class="sxs-lookup"><span data-stu-id="44cf8-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="44cf8-122">Valeur d’attribut/NuSpec</span><span class="sxs-lookup"><span data-stu-id="44cf8-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="44cf8-123">Propriété MSBuild</span><span class="sxs-lookup"><span data-stu-id="44cf8-123">MSBuild Property</span></span> | <span data-ttu-id="44cf8-124">Default</span><span class="sxs-lookup"><span data-stu-id="44cf8-124">Default</span></span> | <span data-ttu-id="44cf8-125">Notes</span><span class="sxs-lookup"><span data-stu-id="44cf8-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="44cf8-126">Id</span><span class="sxs-lookup"><span data-stu-id="44cf8-126">Id</span></span> | <span data-ttu-id="44cf8-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="44cf8-127">PackageId</span></span> | <span data-ttu-id="44cf8-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="44cf8-128">AssemblyName</span></span> | <span data-ttu-id="44cf8-129">$(AssemblyName) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="44cf8-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="44cf8-130">Version</span><span class="sxs-lookup"><span data-stu-id="44cf8-130">Version</span></span> | <span data-ttu-id="44cf8-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="44cf8-131">PackageVersion</span></span> | <span data-ttu-id="44cf8-132">Version</span><span class="sxs-lookup"><span data-stu-id="44cf8-132">Version</span></span> | <span data-ttu-id="44cf8-133">Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 »</span><span class="sxs-lookup"><span data-stu-id="44cf8-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="44cf8-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="44cf8-134">VersionPrefix</span></span> | <span data-ttu-id="44cf8-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="44cf8-135">PackageVersionPrefix</span></span> | <span data-ttu-id="44cf8-136">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-136">empty</span></span> | <span data-ttu-id="44cf8-137">La définition de PackageVersion remplace PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="44cf8-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="44cf8-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="44cf8-138">VersionSuffix</span></span> | <span data-ttu-id="44cf8-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="44cf8-139">PackageVersionSuffix</span></span> | <span data-ttu-id="44cf8-140">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-140">empty</span></span> | <span data-ttu-id="44cf8-141">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="44cf8-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="44cf8-142">La définition de PackageVersion remplace PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="44cf8-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="44cf8-143">Auteurs</span><span class="sxs-lookup"><span data-stu-id="44cf8-143">Authors</span></span> | <span data-ttu-id="44cf8-144">Auteurs</span><span class="sxs-lookup"><span data-stu-id="44cf8-144">Authors</span></span> | <span data-ttu-id="44cf8-145">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="44cf8-145">Username of the current user</span></span> | |
| <span data-ttu-id="44cf8-146">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="44cf8-146">Owners</span></span> | <span data-ttu-id="44cf8-147">N/A</span><span class="sxs-lookup"><span data-stu-id="44cf8-147">N/A</span></span> | <span data-ttu-id="44cf8-148">Ne figure pas dans NuSpec</span><span class="sxs-lookup"><span data-stu-id="44cf8-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="44cf8-149">Titre</span><span class="sxs-lookup"><span data-stu-id="44cf8-149">Title</span></span> | <span data-ttu-id="44cf8-150">Titre</span><span class="sxs-lookup"><span data-stu-id="44cf8-150">Title</span></span> | <span data-ttu-id="44cf8-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="44cf8-151">The PackageId</span></span>| |
| <span data-ttu-id="44cf8-152">Description</span><span class="sxs-lookup"><span data-stu-id="44cf8-152">Description</span></span> | <span data-ttu-id="44cf8-153">Description</span><span class="sxs-lookup"><span data-stu-id="44cf8-153">Description</span></span> | <span data-ttu-id="44cf8-154">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="44cf8-154">"Package Description"</span></span> | |
| <span data-ttu-id="44cf8-155">copyright</span><span class="sxs-lookup"><span data-stu-id="44cf8-155">Copyright</span></span> | <span data-ttu-id="44cf8-156">copyright</span><span class="sxs-lookup"><span data-stu-id="44cf8-156">Copyright</span></span> | <span data-ttu-id="44cf8-157">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-157">empty</span></span> | |
| <span data-ttu-id="44cf8-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="44cf8-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="44cf8-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="44cf8-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="44cf8-160">false</span><span class="sxs-lookup"><span data-stu-id="44cf8-160">false</span></span> | |
| <span data-ttu-id="44cf8-161">license</span><span class="sxs-lookup"><span data-stu-id="44cf8-161">license</span></span> | <span data-ttu-id="44cf8-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="44cf8-162">PackageLicenseExpression</span></span> | <span data-ttu-id="44cf8-163">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-163">empty</span></span> | <span data-ttu-id="44cf8-164">Correspond à `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="44cf8-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="44cf8-165">license</span><span class="sxs-lookup"><span data-stu-id="44cf8-165">license</span></span> | <span data-ttu-id="44cf8-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-166">PackageLicenseFile</span></span> | <span data-ttu-id="44cf8-167">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-167">empty</span></span> | <span data-ttu-id="44cf8-168">Correspond à `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="44cf8-169">Vous devez explicitement compresser le fichier de licence référencé.</span><span class="sxs-lookup"><span data-stu-id="44cf8-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="44cf8-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-170">LicenseUrl</span></span> | <span data-ttu-id="44cf8-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-171">PackageLicenseUrl</span></span> | <span data-ttu-id="44cf8-172">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-172">empty</span></span> | <span data-ttu-id="44cf8-173">`PackageLicenseUrl` est déconseillé, utilisez la propriété PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="44cf8-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-174">ProjectUrl</span></span> | <span data-ttu-id="44cf8-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-175">PackageProjectUrl</span></span> | <span data-ttu-id="44cf8-176">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-176">empty</span></span> | |
| <span data-ttu-id="44cf8-177">Icône</span><span class="sxs-lookup"><span data-stu-id="44cf8-177">Icon</span></span> | <span data-ttu-id="44cf8-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="44cf8-178">PackageIcon</span></span> | <span data-ttu-id="44cf8-179">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-179">empty</span></span> | <span data-ttu-id="44cf8-180">Vous devez explicitement compresser le fichier image icône référencé.</span><span class="sxs-lookup"><span data-stu-id="44cf8-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="44cf8-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-181">IconUrl</span></span> | <span data-ttu-id="44cf8-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-182">PackageIconUrl</span></span> | <span data-ttu-id="44cf8-183">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-183">empty</span></span> | <span data-ttu-id="44cf8-184">Pour une expérience de niveau inférieur, `PackageIconUrl` vous devez spécifier en plus de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="44cf8-185">Plus long terme, `PackageIconUrl` sera déconseillé.</span><span class="sxs-lookup"><span data-stu-id="44cf8-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="44cf8-186">Étiquettes</span><span class="sxs-lookup"><span data-stu-id="44cf8-186">Tags</span></span> | <span data-ttu-id="44cf8-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="44cf8-187">PackageTags</span></span> | <span data-ttu-id="44cf8-188">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-188">empty</span></span> | <span data-ttu-id="44cf8-189">Les balises sont séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="44cf8-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="44cf8-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="44cf8-190">ReleaseNotes</span></span> | <span data-ttu-id="44cf8-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="44cf8-191">PackageReleaseNotes</span></span> | <span data-ttu-id="44cf8-192">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-192">empty</span></span> | |
| <span data-ttu-id="44cf8-193">Référentiel/URL</span><span class="sxs-lookup"><span data-stu-id="44cf8-193">Repository/Url</span></span> | <span data-ttu-id="44cf8-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-194">RepositoryUrl</span></span> | <span data-ttu-id="44cf8-195">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-195">empty</span></span> | <span data-ttu-id="44cf8-196">URL du référentiel utilisée pour cloner ou récupérer le code source.</span><span class="sxs-lookup"><span data-stu-id="44cf8-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="44cf8-197">Tels *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="44cf8-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="44cf8-198">Dépôt/type</span><span class="sxs-lookup"><span data-stu-id="44cf8-198">Repository/Type</span></span> | <span data-ttu-id="44cf8-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="44cf8-199">RepositoryType</span></span> | <span data-ttu-id="44cf8-200">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-200">empty</span></span> | <span data-ttu-id="44cf8-201">Type de référentiel.</span><span class="sxs-lookup"><span data-stu-id="44cf8-201">Repository type.</span></span> <span data-ttu-id="44cf8-202">Exemples : *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="44cf8-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="44cf8-203">Référentiel/branche</span><span class="sxs-lookup"><span data-stu-id="44cf8-203">Repository/Branch</span></span> | <span data-ttu-id="44cf8-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="44cf8-204">RepositoryBranch</span></span> | <span data-ttu-id="44cf8-205">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-205">empty</span></span> | <span data-ttu-id="44cf8-206">Informations de branche de référentiel facultatives.</span><span class="sxs-lookup"><span data-stu-id="44cf8-206">Optional repository branch information.</span></span> <span data-ttu-id="44cf8-207">*RepositoryUrl* doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="44cf8-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="44cf8-208">Exemple : *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="44cf8-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="44cf8-209">Dépôt/validation</span><span class="sxs-lookup"><span data-stu-id="44cf8-209">Repository/Commit</span></span> | <span data-ttu-id="44cf8-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="44cf8-210">RepositoryCommit</span></span> | <span data-ttu-id="44cf8-211">empty</span><span class="sxs-lookup"><span data-stu-id="44cf8-211">empty</span></span> | <span data-ttu-id="44cf8-212">Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré.</span><span class="sxs-lookup"><span data-stu-id="44cf8-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="44cf8-213">*RepositoryUrl* doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="44cf8-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="44cf8-214">Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="44cf8-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="44cf8-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="44cf8-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="44cf8-216">Résumé</span><span class="sxs-lookup"><span data-stu-id="44cf8-216">Summary</span></span> | <span data-ttu-id="44cf8-217">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="44cf8-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="44cf8-218">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="44cf8-218">pack target inputs</span></span>

- <span data-ttu-id="44cf8-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="44cf8-219">IsPackable</span></span>
- <span data-ttu-id="44cf8-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="44cf8-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="44cf8-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="44cf8-221">PackageVersion</span></span>
- <span data-ttu-id="44cf8-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="44cf8-222">PackageId</span></span>
- <span data-ttu-id="44cf8-223">Auteurs</span><span class="sxs-lookup"><span data-stu-id="44cf8-223">Authors</span></span>
- <span data-ttu-id="44cf8-224">Description</span><span class="sxs-lookup"><span data-stu-id="44cf8-224">Description</span></span>
- <span data-ttu-id="44cf8-225">copyright</span><span class="sxs-lookup"><span data-stu-id="44cf8-225">Copyright</span></span>
- <span data-ttu-id="44cf8-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="44cf8-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="44cf8-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="44cf8-227">DevelopmentDependency</span></span>
- <span data-ttu-id="44cf8-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="44cf8-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="44cf8-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-229">PackageLicenseFile</span></span>
- <span data-ttu-id="44cf8-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="44cf8-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-231">PackageProjectUrl</span></span>
- <span data-ttu-id="44cf8-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-232">PackageIconUrl</span></span>
- <span data-ttu-id="44cf8-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="44cf8-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="44cf8-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="44cf8-234">PackageTags</span></span>
- <span data-ttu-id="44cf8-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="44cf8-235">PackageOutputPath</span></span>
- <span data-ttu-id="44cf8-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="44cf8-236">IncludeSymbols</span></span>
- <span data-ttu-id="44cf8-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="44cf8-237">IncludeSource</span></span>
- <span data-ttu-id="44cf8-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="44cf8-238">PackageTypes</span></span>
- <span data-ttu-id="44cf8-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="44cf8-239">IsTool</span></span>
- <span data-ttu-id="44cf8-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-240">RepositoryUrl</span></span>
- <span data-ttu-id="44cf8-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="44cf8-241">RepositoryType</span></span>
- <span data-ttu-id="44cf8-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="44cf8-242">RepositoryBranch</span></span>
- <span data-ttu-id="44cf8-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="44cf8-243">RepositoryCommit</span></span>
- <span data-ttu-id="44cf8-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="44cf8-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="44cf8-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="44cf8-245">MinClientVersion</span></span>
- <span data-ttu-id="44cf8-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="44cf8-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="44cf8-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="44cf8-247">IncludeContentInPack</span></span>
- <span data-ttu-id="44cf8-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="44cf8-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="44cf8-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="44cf8-249">ContentTargetFolders</span></span>
- <span data-ttu-id="44cf8-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-250">NuspecFile</span></span>
- <span data-ttu-id="44cf8-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="44cf8-251">NuspecBasePath</span></span>
- <span data-ttu-id="44cf8-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="44cf8-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="44cf8-253">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="44cf8-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="44cf8-254">Supprimer les dépendances</span><span class="sxs-lookup"><span data-stu-id="44cf8-254">Suppress dependencies</span></span>

<span data-ttu-id="44cf8-255">Pour supprimer les dépendances de package du package NuGet généré, affectez `SuppressDependenciesWhenPacking` la valeur à `true` qui autorisera l’ignorance de toutes les dépendances du fichier nupkg généré.</span><span class="sxs-lookup"><span data-stu-id="44cf8-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="44cf8-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="44cf8-256">PackageIconUrl</span></span>

<span data-ttu-id="44cf8-257">`PackageIconUrl` sera dépréciée en faveur de la nouvelle [`PackageIcon`](#packageicon) propriété.</span><span class="sxs-lookup"><span data-stu-id="44cf8-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="44cf8-258">À compter de NuGet 5,3 & Visual Studio 2019 version 16,3, `pack` génère un avertissement [NU5048](./errors-and-warnings/nu5048.md) si les métadonnées de package spécifient uniquement `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="44cf8-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="44cf8-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="44cf8-260">Vous devez spécifier à la fois `PackageIcon` et `PackageIconUrl` pour assurer la compatibilité descendante avec les clients et les sources qui ne prennent pas encore en charge `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="44cf8-261">Visual Studio prendra en charge `PackageIcon` les packages provenant d’une source basée sur des dossiers dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="44cf8-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="44cf8-262">Compression d’un fichier image d’icône</span><span class="sxs-lookup"><span data-stu-id="44cf8-262">Packing an icon image file</span></span>

<span data-ttu-id="44cf8-263">Lors de la compression d’un fichier image icône, vous devez utiliser `PackageIcon` la propriété pour spécifier le chemin d’accès du package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="44cf8-264">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="44cf8-265">La taille du fichier image est limitée à 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="44cf8-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="44cf8-266">Les formats de fichiers pris en charge sont JPEG et PNG.</span><span class="sxs-lookup"><span data-stu-id="44cf8-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="44cf8-267">Nous recommandons une résolution d’image de 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="44cf8-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="44cf8-268">Exemple :</span><span class="sxs-lookup"><span data-stu-id="44cf8-268">For example:</span></span>

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

<span data-ttu-id="44cf8-269">[Exemple d’icône de package](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="44cf8-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="44cf8-270">Pour l’équivalent NuSpec, consultez la [référence NuSpec pour l’icône](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="44cf8-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="44cf8-271">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="44cf8-271">Output assemblies</span></span>

<span data-ttu-id="44cf8-272">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="44cf8-273">Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="44cf8-274">Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="44cf8-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="44cf8-275">`IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="44cf8-276">`BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="44cf8-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="44cf8-277">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="44cf8-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="44cf8-278">Références de package</span><span class="sxs-lookup"><span data-stu-id="44cf8-278">Package references</span></span>

<span data-ttu-id="44cf8-279">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="44cf8-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="44cf8-280">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="44cf8-280">Project to project references</span></span>

<span data-ttu-id="44cf8-281">Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :</span><span class="sxs-lookup"><span data-stu-id="44cf8-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="44cf8-282">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="44cf8-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="44cf8-283">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="44cf8-283">Including content in a package</span></span>

<span data-ttu-id="44cf8-284">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="44cf8-285">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="44cf8-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="44cf8-286">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="44cf8-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="44cf8-287">Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="44cf8-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="44cf8-288">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="44cf8-289">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="44cf8-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="44cf8-290">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="44cf8-291">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="44cf8-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="44cf8-292">Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="44cf8-293">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="44cf8-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="44cf8-294">D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.</span><span class="sxs-lookup"><span data-stu-id="44cf8-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="44cf8-295">Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="44cf8-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="44cf8-296">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="44cf8-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="44cf8-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="44cf8-297">IncludeSymbols</span></span>

<span data-ttu-id="44cf8-298">Quand vous utilisez `MSBuild -t:pack -p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="44cf8-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="44cf8-299">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="44cf8-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="44cf8-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="44cf8-300">IncludeSource</span></span>

<span data-ttu-id="44cf8-301">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="44cf8-302">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="44cf8-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="44cf8-303">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="44cf8-304">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="44cf8-305">Compression d’une expression de licence ou d’un fichier de licence</span><span class="sxs-lookup"><span data-stu-id="44cf8-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="44cf8-306">Lors de l’utilisation d’une expression de licence, la propriété PackageLicenseExpression doit être utilisée.</span><span class="sxs-lookup"><span data-stu-id="44cf8-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="44cf8-307">[Exemple d’expression de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="44cf8-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="44cf8-308">[En savoir plus sur les expressions de licence et les licences acceptées par NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="44cf8-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="44cf8-309">Lors de l’empaquetage d’un fichier de licence, vous devez utiliser la propriété PackageLicenseFile pour spécifier le chemin d’accès au package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="44cf8-310">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="44cf8-311">Exemple :</span><span class="sxs-lookup"><span data-stu-id="44cf8-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="44cf8-312">[Exemple de fichier de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="44cf8-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="44cf8-313">Compression d’un fichier sans extension</span><span class="sxs-lookup"><span data-stu-id="44cf8-313">Packing a file without an extension</span></span>

<span data-ttu-id="44cf8-314">Dans certains scénarios, par exemple lors de la compression d’un fichier de licence, vous souhaiterez peut-être inclure un fichier sans extension.</span><span class="sxs-lookup"><span data-stu-id="44cf8-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="44cf8-315">Pour des raisons historiques, NuGet & MSBuild traitent les chemins d’accès sans extension comme répertoires.</span><span class="sxs-lookup"><span data-stu-id="44cf8-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="44cf8-316">[Fichier sans exemple d’extension](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="44cf8-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="44cf8-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="44cf8-317">IsTool</span></span>

<span data-ttu-id="44cf8-318">Lors de l’utilisation de `MSBuild -t:pack -p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="44cf8-319">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="44cf8-320">Compression à l’aide d’un fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="44cf8-320">Packing using a .nuspec</span></span>

<span data-ttu-id="44cf8-321">Bien qu’il soit recommandé d’inclure à la place [toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se trouvent généralement dans le fichier du `.nuspec` fichier projet, vous pouvez choisir d’utiliser un `.nuspec` fichier pour compresser votre projet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="44cf8-322">Pour un projet de type non-SDK qui utilise `PackageReference` , vous devez effectuer `NuGet.Build.Tasks.Pack.targets` l’importation afin que la tâche Pack puisse être exécutée.</span><span class="sxs-lookup"><span data-stu-id="44cf8-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="44cf8-323">Vous devez toujours restaurer le projet avant de pouvoir compresser un fichier NuSpec.</span><span class="sxs-lookup"><span data-stu-id="44cf8-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="44cf8-324">(Un projet de type SDK comprend les cibles Pack par défaut.)</span><span class="sxs-lookup"><span data-stu-id="44cf8-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="44cf8-325">La version cible du .NET Framework du fichier projet n’est pas pertinente et n’est pas utilisée lors de la compression d’un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="44cf8-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="44cf8-326">Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="44cf8-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="44cf8-327">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="44cf8-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="44cf8-328">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="44cf8-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="44cf8-329">En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="44cf8-330">`NuspecBasePath` : chemin de base pour le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="44cf8-331">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="44cf8-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="44cf8-332">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="44cf8-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="44cf8-333">Notez que le compactage d’un NuSpec à l’aide de dotnet.exe ou de MSBuild permet également de générer le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="44cf8-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="44cf8-334">Cela peut être évité en passant ```--no-build``` la propriété à dotnet.exe, qui est l’équivalent du paramètre ```<NoBuild>true</NoBuild> ``` dans votre fichier projet, ainsi que le paramètre ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="44cf8-335">Voici un exemple de fichier *. csproj* pour compresser un fichier NuSpec :</span><span class="sxs-lookup"><span data-stu-id="44cf8-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="44cf8-336">Points d’extension avancés pour créer un package personnalisé</span><span class="sxs-lookup"><span data-stu-id="44cf8-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="44cf8-337">La `pack` cible fournit deux points d’extension qui s’exécutent dans la build interne du Framework cible.</span><span class="sxs-lookup"><span data-stu-id="44cf8-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="44cf8-338">Les points d’extension prennent en charge l’inclusion de contenu et d’assemblys spécifiques au Framework cible dans un package :</span><span class="sxs-lookup"><span data-stu-id="44cf8-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="44cf8-339">`TargetsForTfmSpecificBuildOutput` cible : à utiliser pour les fichiers contenus dans le `lib` dossier ou dans un dossier spécifié à l’aide de `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="44cf8-340">`TargetsForTfmSpecificContentInPackage` cible : à utiliser pour les fichiers en dehors de `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="44cf8-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="44cf8-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="44cf8-342">Écrivez une cible personnalisée et spécifiez-la comme valeur de la `$(TargetsForTfmSpecificBuildOutput)` propriété.</span><span class="sxs-lookup"><span data-stu-id="44cf8-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="44cf8-343">Pour tous les fichiers qui doivent être placés dans `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans ItemGroup `BuildOutputInPackage` et définir les deux valeurs de métadonnées suivantes :</span><span class="sxs-lookup"><span data-stu-id="44cf8-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="44cf8-344">`FinalOutputPath`: Le chemin d’accès absolu du fichier ; s’il n’est pas fourni, l’identité est utilisée pour évaluer le chemin source.</span><span class="sxs-lookup"><span data-stu-id="44cf8-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="44cf8-345">`TargetPath`: (Facultatif) définit le moment où le fichier doit être placé dans un sous-dossier au sein de `lib\<TargetFramework>` , comme les assemblys satellites qui se trouvent dans leurs dossiers de culture respectifs.</span><span class="sxs-lookup"><span data-stu-id="44cf8-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="44cf8-346">La valeur par défaut est le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="44cf8-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="44cf8-347">Exemple :</span><span class="sxs-lookup"><span data-stu-id="44cf8-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="44cf8-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="44cf8-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="44cf8-349">Écrivez une cible personnalisée et spécifiez-la comme valeur de la `$(TargetsForTfmSpecificContentInPackage)` propriété.</span><span class="sxs-lookup"><span data-stu-id="44cf8-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="44cf8-350">Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes :</span><span class="sxs-lookup"><span data-stu-id="44cf8-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="44cf8-351">`PackagePath`: Chemin d’accès où le fichier doit être généré dans le package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="44cf8-352">NuGet émet un avertissement si plusieurs fichiers sont ajoutés au même chemin d’accès de package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="44cf8-353">`BuildAction`: Action de génération à assigner au fichier, obligatoire uniquement si le chemin d’accès du package se trouve dans le `contentFiles` dossier.</span><span class="sxs-lookup"><span data-stu-id="44cf8-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="44cf8-354">La valeur par défaut est « None ».</span><span class="sxs-lookup"><span data-stu-id="44cf8-354">Defaults to "None".</span></span>

<span data-ttu-id="44cf8-355">Exemple :</span><span class="sxs-lookup"><span data-stu-id="44cf8-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="44cf8-356">Cible restore</span><span class="sxs-lookup"><span data-stu-id="44cf8-356">restore target</span></span>

<span data-ttu-id="44cf8-357">`MSBuild -t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="44cf8-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="44cf8-358">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="44cf8-358">Read all project to project references</span></span>
1. <span data-ttu-id="44cf8-359">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="44cf8-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="44cf8-360">Passer des données MSBuild à NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="44cf8-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="44cf8-361">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="44cf8-361">Run restore</span></span>
1. <span data-ttu-id="44cf8-362">Télécharger des packages</span><span class="sxs-lookup"><span data-stu-id="44cf8-362">Download packages</span></span>
1. <span data-ttu-id="44cf8-363">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="44cf8-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="44cf8-364">La `restore` cible fonctionne pour les projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="44cf8-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="44cf8-365">`MSBuild 16.5+` prend également [en charge](#restoring-packagereference-and-packagesconfig-with-msbuild) le `packages.config` format.</span><span class="sxs-lookup"><span data-stu-id="44cf8-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="44cf8-366">La `restore` cible ne [doit pas être exécutée](#restoring-and-building-with-one-msbuild-command) en association avec la `build` cible.</span><span class="sxs-lookup"><span data-stu-id="44cf8-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="44cf8-367">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="44cf8-367">Restore properties</span></span>

<span data-ttu-id="44cf8-368">Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="44cf8-369">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `-p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="44cf8-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="44cf8-370">Propriété</span><span class="sxs-lookup"><span data-stu-id="44cf8-370">Property</span></span> | <span data-ttu-id="44cf8-371">Description</span><span class="sxs-lookup"><span data-stu-id="44cf8-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="44cf8-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="44cf8-372">RestoreSources</span></span> | <span data-ttu-id="44cf8-373">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="44cf8-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="44cf8-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="44cf8-374">RestorePackagesPath</span></span> | <span data-ttu-id="44cf8-375">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44cf8-375">User packages folder path.</span></span> |
| <span data-ttu-id="44cf8-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="44cf8-376">RestoreDisableParallel</span></span> | <span data-ttu-id="44cf8-377">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="44cf8-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="44cf8-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-378">RestoreConfigFile</span></span> | <span data-ttu-id="44cf8-379">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="44cf8-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="44cf8-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="44cf8-380">RestoreNoCache</span></span> | <span data-ttu-id="44cf8-381">Si la valeur est true, évite d’utiliser des packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="44cf8-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="44cf8-382">Consultez [gestion des dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="44cf8-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="44cf8-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="44cf8-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="44cf8-384">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="44cf8-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="44cf8-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="44cf8-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="44cf8-386">Dossiers de secours, utilisés de la même façon que le dossier des packages de l’utilisateur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="44cf8-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="44cf8-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="44cf8-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="44cf8-388">Sources supplémentaires à utiliser pendant la restauration.</span><span class="sxs-lookup"><span data-stu-id="44cf8-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="44cf8-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="44cf8-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="44cf8-390">Dossiers de secours supplémentaires à utiliser lors de la restauration.</span><span class="sxs-lookup"><span data-stu-id="44cf8-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="44cf8-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="44cf8-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="44cf8-392">Exclut les dossiers de secours spécifiés dans `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="44cf8-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="44cf8-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="44cf8-394">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="44cf8-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="44cf8-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="44cf8-396">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="44cf8-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="44cf8-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="44cf8-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="44cf8-398">Lorsque les projets sont collectés via MSBuild, il détermine s’ils sont collectés à l’aide de l' `SkipNonexistentTargets` optimisation.</span><span class="sxs-lookup"><span data-stu-id="44cf8-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="44cf8-399">Si la valeur n’est pas définie, la valeur par défaut est `true` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="44cf8-400">La conséquence est un comportement de basculement rapide lorsque les cibles d’un projet ne peuvent pas être importées.</span><span class="sxs-lookup"><span data-stu-id="44cf8-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="44cf8-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="44cf8-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="44cf8-402">Dossier de sortie, avec comme valeur par défaut `BaseIntermediateOutputPath` et le `obj` dossier.</span><span class="sxs-lookup"><span data-stu-id="44cf8-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="44cf8-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="44cf8-403">RestoreForce</span></span> | <span data-ttu-id="44cf8-404">Dans les projets basés sur PackageReference, force la résolution de toutes les dépendances même si la dernière restauration a réussi.</span><span class="sxs-lookup"><span data-stu-id="44cf8-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="44cf8-405">La spécification de cet indicateur est semblable à la suppression du `project.assets.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="44cf8-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="44cf8-406">Cela ne contourne pas le cache http.</span><span class="sxs-lookup"><span data-stu-id="44cf8-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="44cf8-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="44cf8-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="44cf8-408">Opte pour l’utilisation d’un fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="44cf8-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="44cf8-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="44cf8-409">RestoreLockedMode</span></span> | <span data-ttu-id="44cf8-410">Exécutez la restauration en mode verrouillé.</span><span class="sxs-lookup"><span data-stu-id="44cf8-410">Run restore in locked mode.</span></span> <span data-ttu-id="44cf8-411">Cela signifie que la restauration ne réévaluera pas les dépendances.</span><span class="sxs-lookup"><span data-stu-id="44cf8-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="44cf8-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="44cf8-412">NuGetLockFilePath</span></span> | <span data-ttu-id="44cf8-413">Emplacement personnalisé pour le fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="44cf8-413">A custom location for the lock file.</span></span> <span data-ttu-id="44cf8-414">L’emplacement par défaut est à côté du projet et est nommé `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="44cf8-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="44cf8-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="44cf8-416">Force la restauration à recalculer les dépendances et à mettre à jour le fichier de verrouillage sans aucun avertissement.</span><span class="sxs-lookup"><span data-stu-id="44cf8-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="44cf8-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="44cf8-417">RestorePackagesConfig</span></span> | <span data-ttu-id="44cf8-418">Commutateur d’abonnement qui restaure les projets avec packages.config. Prise en charge avec `MSBuild -t:restore` uniquement.</span><span class="sxs-lookup"><span data-stu-id="44cf8-418">An opt in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |

#### <a name="examples"></a><span data-ttu-id="44cf8-419">Exemples</span><span class="sxs-lookup"><span data-stu-id="44cf8-419">Examples</span></span>

<span data-ttu-id="44cf8-420">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="44cf8-420">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="44cf8-421">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="44cf8-421">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="44cf8-422">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="44cf8-422">Restore outputs</span></span>

<span data-ttu-id="44cf8-423">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="44cf8-423">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="44cf8-424">Fichier</span><span class="sxs-lookup"><span data-stu-id="44cf8-424">File</span></span> | <span data-ttu-id="44cf8-425">Description</span><span class="sxs-lookup"><span data-stu-id="44cf8-425">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="44cf8-426">Contient le graphique de dépendance de toutes les références de package.</span><span class="sxs-lookup"><span data-stu-id="44cf8-426">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="44cf8-427">Références à des propriétés MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="44cf8-427">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="44cf8-428">Références à des cibles MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="44cf8-428">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="44cf8-429">Restauration et génération à l’aide d’une commande MSBuild</span><span class="sxs-lookup"><span data-stu-id="44cf8-429">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="44cf8-430">En raison du fait que NuGet peut restaurer des packages qui déplacent des cibles et des props MSBuild, les évaluations de la restauration et de la build sont exécutées avec des propriétés globales différentes.</span><span class="sxs-lookup"><span data-stu-id="44cf8-430">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="44cf8-431">Cela signifie que les éléments suivants auront un comportement imprévisible et souvent incorrect.</span><span class="sxs-lookup"><span data-stu-id="44cf8-431">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="44cf8-432">Au lieu de cela, l’approche recommandée est la suivante :</span><span class="sxs-lookup"><span data-stu-id="44cf8-432">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="44cf8-433">La même logique s’applique à d’autres cibles similaires à celles de `build` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-433">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="44cf8-434">Restauration de PackageReference et packages.config avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="44cf8-434">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="44cf8-435">Avec MSBuild 16,5 +, packages.config sont également pris en charge pour `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="44cf8-435">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="44cf8-436">`packages.config` la restauration est disponible uniquement avec `MSBuild 16.5+` , et non avec `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="44cf8-436">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="44cf8-437">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="44cf8-437">PackageTargetFallback</span></span>

<span data-ttu-id="44cf8-438">L’élément `PackageTargetFallback` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="44cf8-438">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="44cf8-439">Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../reference/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-439">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="44cf8-440">Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.</span><span class="sxs-lookup"><span data-stu-id="44cf8-440">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="44cf8-441">Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue.</span><span class="sxs-lookup"><span data-stu-id="44cf8-441">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="44cf8-442">Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :</span><span class="sxs-lookup"><span data-stu-id="44cf8-442">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="44cf8-443">Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="44cf8-443">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="44cf8-444">Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="44cf8-444">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="44cf8-445">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="44cf8-445">Replacing one library from a restore graph</span></span>

<span data-ttu-id="44cf8-446">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="44cf8-446">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="44cf8-447">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="44cf8-447">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="44cf8-448">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="44cf8-448">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
