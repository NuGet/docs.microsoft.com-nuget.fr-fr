---
title: Commandes pack et restore NuGet comme cibles MSBuild
description: Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16b8ff532b87a3e3f96029e77dd166eb39294c0b
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815347"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="eda97-103">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="eda97-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="eda97-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="eda97-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="eda97-105">Avec le format [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + peut stocker toutes les métadonnées de manifeste directement dans un fichier projet plutôt que `.nuspec` d’utiliser un fichier séparé.</span><span class="sxs-lookup"><span data-stu-id="eda97-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="eda97-106">Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="eda97-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="eda97-107">Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eda97-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="eda97-108">Pour obtenir des instructions sur la création d’un package NuGet à l’aide de MSBuild, consultez [créer un package NuGet à l’aide de MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="eda97-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="eda97-109">(Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../reference/cli-reference/cli-ref-pack.md) et [restore](../reference/cli-reference/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)</span><span class="sxs-lookup"><span data-stu-id="eda97-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="eda97-110">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="eda97-110">Target build order</span></span>

<span data-ttu-id="eda97-111">Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="eda97-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="eda97-112">Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression.</span><span class="sxs-lookup"><span data-stu-id="eda97-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="eda97-113">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="eda97-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="eda97-114">De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eda97-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="eda97-115">`$(OutputPath)`est relatif et s’attend à ce que vous exécutiez la commande à partir de la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="eda97-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="eda97-116">Cible pack</span><span class="sxs-lookup"><span data-stu-id="eda97-116">pack target</span></span>

<span data-ttu-id="eda97-117">Pour les projets .NET standard utilisant le format PackageReference, `msbuild -t:pack` l’utilisation de dessine des entrées à partir du fichier projet à utiliser lors de la création d’un package NuGet.</span><span class="sxs-lookup"><span data-stu-id="eda97-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="eda97-118">Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier projet au sein du premier nœud `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="eda97-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="eda97-119">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="eda97-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="eda97-120">Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="eda97-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="eda97-121">Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eda97-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="eda97-122">Valeur d’attribut/NuSpec</span><span class="sxs-lookup"><span data-stu-id="eda97-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="eda97-123">Propriété MSBuild</span><span class="sxs-lookup"><span data-stu-id="eda97-123">MSBuild Property</span></span> | <span data-ttu-id="eda97-124">Default</span><span class="sxs-lookup"><span data-stu-id="eda97-124">Default</span></span> | <span data-ttu-id="eda97-125">Notes</span><span class="sxs-lookup"><span data-stu-id="eda97-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="eda97-126">Id</span><span class="sxs-lookup"><span data-stu-id="eda97-126">Id</span></span> | <span data-ttu-id="eda97-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="eda97-127">PackageId</span></span> | <span data-ttu-id="eda97-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="eda97-128">AssemblyName</span></span> | <span data-ttu-id="eda97-129">$(AssemblyName) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="eda97-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="eda97-130">Version</span><span class="sxs-lookup"><span data-stu-id="eda97-130">Version</span></span> | <span data-ttu-id="eda97-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="eda97-131">PackageVersion</span></span> | <span data-ttu-id="eda97-132">Version</span><span class="sxs-lookup"><span data-stu-id="eda97-132">Version</span></span> | <span data-ttu-id="eda97-133">Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 »</span><span class="sxs-lookup"><span data-stu-id="eda97-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="eda97-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eda97-134">VersionPrefix</span></span> | <span data-ttu-id="eda97-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eda97-135">PackageVersionPrefix</span></span> | <span data-ttu-id="eda97-136">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-136">empty</span></span> | <span data-ttu-id="eda97-137">La définition de PackageVersion remplace PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eda97-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="eda97-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eda97-138">VersionSuffix</span></span> | <span data-ttu-id="eda97-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eda97-139">PackageVersionSuffix</span></span> | <span data-ttu-id="eda97-140">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-140">empty</span></span> | <span data-ttu-id="eda97-141">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eda97-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="eda97-142">La définition de PackageVersion remplace PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eda97-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="eda97-143">Auteurs</span><span class="sxs-lookup"><span data-stu-id="eda97-143">Authors</span></span> | <span data-ttu-id="eda97-144">Auteurs</span><span class="sxs-lookup"><span data-stu-id="eda97-144">Authors</span></span> | <span data-ttu-id="eda97-145">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="eda97-145">Username of the current user</span></span> | |
| <span data-ttu-id="eda97-146">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="eda97-146">Owners</span></span> | <span data-ttu-id="eda97-147">S.O.</span><span class="sxs-lookup"><span data-stu-id="eda97-147">N/A</span></span> | <span data-ttu-id="eda97-148">Ne figure pas dans NuSpec</span><span class="sxs-lookup"><span data-stu-id="eda97-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="eda97-149">Titre</span><span class="sxs-lookup"><span data-stu-id="eda97-149">Title</span></span> | <span data-ttu-id="eda97-150">Titre</span><span class="sxs-lookup"><span data-stu-id="eda97-150">Title</span></span> | <span data-ttu-id="eda97-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="eda97-151">The PackageId</span></span>| |
| <span data-ttu-id="eda97-152">Description</span><span class="sxs-lookup"><span data-stu-id="eda97-152">Description</span></span> | <span data-ttu-id="eda97-153">Description</span><span class="sxs-lookup"><span data-stu-id="eda97-153">Description</span></span> | <span data-ttu-id="eda97-154">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="eda97-154">"Package Description"</span></span> | |
| <span data-ttu-id="eda97-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="eda97-155">Copyright</span></span> | <span data-ttu-id="eda97-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="eda97-156">Copyright</span></span> | <span data-ttu-id="eda97-157">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-157">empty</span></span> | |
| <span data-ttu-id="eda97-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eda97-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="eda97-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eda97-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="eda97-160">false</span><span class="sxs-lookup"><span data-stu-id="eda97-160">false</span></span> | |
| <span data-ttu-id="eda97-161">licence</span><span class="sxs-lookup"><span data-stu-id="eda97-161">license</span></span> | <span data-ttu-id="eda97-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="eda97-162">PackageLicenseExpression</span></span> | <span data-ttu-id="eda97-163">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-163">empty</span></span> | <span data-ttu-id="eda97-164">Correspond à`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="eda97-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="eda97-165">licence</span><span class="sxs-lookup"><span data-stu-id="eda97-165">license</span></span> | <span data-ttu-id="eda97-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="eda97-166">PackageLicenseFile</span></span> | <span data-ttu-id="eda97-167">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-167">empty</span></span> | <span data-ttu-id="eda97-168">Correspond à `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="eda97-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="eda97-169">Vous devrez peut-être compresser explicitement le fichier de licence référencé.</span><span class="sxs-lookup"><span data-stu-id="eda97-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="eda97-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-170">LicenseUrl</span></span> | <span data-ttu-id="eda97-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-171">PackageLicenseUrl</span></span> | <span data-ttu-id="eda97-172">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-172">empty</span></span> | <span data-ttu-id="eda97-173">`PackageLicenseUrl`est déconseillé, utilisez la propriété PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="eda97-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="eda97-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-174">ProjectUrl</span></span> | <span data-ttu-id="eda97-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-175">PackageProjectUrl</span></span> | <span data-ttu-id="eda97-176">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-176">empty</span></span> | |
| <span data-ttu-id="eda97-177">Icône</span><span class="sxs-lookup"><span data-stu-id="eda97-177">Icon</span></span> | <span data-ttu-id="eda97-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="eda97-178">PackageIcon</span></span> | <span data-ttu-id="eda97-179">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-179">empty</span></span> | <span data-ttu-id="eda97-180">Vous devrez peut-être compresser explicitement le fichier image icône référencé.</span><span class="sxs-lookup"><span data-stu-id="eda97-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="eda97-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-181">IconUrl</span></span> | <span data-ttu-id="eda97-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-182">PackageIconUrl</span></span> | <span data-ttu-id="eda97-183">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-183">empty</span></span> | <span data-ttu-id="eda97-184">`PackageIconUrl`est déconseillé, utilisez la propriété PackageIcon</span><span class="sxs-lookup"><span data-stu-id="eda97-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="eda97-185">Balises</span><span class="sxs-lookup"><span data-stu-id="eda97-185">Tags</span></span> | <span data-ttu-id="eda97-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="eda97-186">PackageTags</span></span> | <span data-ttu-id="eda97-187">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-187">empty</span></span> | <span data-ttu-id="eda97-188">Les balises sont séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="eda97-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="eda97-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eda97-189">ReleaseNotes</span></span> | <span data-ttu-id="eda97-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eda97-190">PackageReleaseNotes</span></span> | <span data-ttu-id="eda97-191">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-191">empty</span></span> | |
| <span data-ttu-id="eda97-192">Référentiel/URL</span><span class="sxs-lookup"><span data-stu-id="eda97-192">Repository/Url</span></span> | <span data-ttu-id="eda97-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-193">RepositoryUrl</span></span> | <span data-ttu-id="eda97-194">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-194">empty</span></span> | <span data-ttu-id="eda97-195">URL du référentiel utilisée pour cloner ou récupérer le code source.</span><span class="sxs-lookup"><span data-stu-id="eda97-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eda97-196">Tels *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="eda97-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="eda97-197">Dépôt/type</span><span class="sxs-lookup"><span data-stu-id="eda97-197">Repository/Type</span></span> | <span data-ttu-id="eda97-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="eda97-198">RepositoryType</span></span> | <span data-ttu-id="eda97-199">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-199">empty</span></span> | <span data-ttu-id="eda97-200">Type de référentiel.</span><span class="sxs-lookup"><span data-stu-id="eda97-200">Repository type.</span></span> <span data-ttu-id="eda97-201">Exemples : *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="eda97-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="eda97-202">Référentiel/branche</span><span class="sxs-lookup"><span data-stu-id="eda97-202">Repository/Branch</span></span> | <span data-ttu-id="eda97-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="eda97-203">RepositoryBranch</span></span> | <span data-ttu-id="eda97-204">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-204">empty</span></span> | <span data-ttu-id="eda97-205">Informations de branche de référentiel facultatives.</span><span class="sxs-lookup"><span data-stu-id="eda97-205">Optional repository branch information.</span></span> <span data-ttu-id="eda97-206">*RepositoryUrl* doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="eda97-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="eda97-207">Exemple : *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="eda97-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="eda97-208">Dépôt/validation</span><span class="sxs-lookup"><span data-stu-id="eda97-208">Repository/Commit</span></span> | <span data-ttu-id="eda97-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="eda97-209">RepositoryCommit</span></span> | <span data-ttu-id="eda97-210">vide</span><span class="sxs-lookup"><span data-stu-id="eda97-210">empty</span></span> | <span data-ttu-id="eda97-211">Validation ou ensemble de modifications de référentiel facultatif pour indiquer la source à partir de laquelle le package a été généré.</span><span class="sxs-lookup"><span data-stu-id="eda97-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eda97-212">*RepositoryUrl* doit également être spécifié pour que cette propriété soit incluse.</span><span class="sxs-lookup"><span data-stu-id="eda97-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="eda97-213">Exemple : *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="eda97-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="eda97-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="eda97-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="eda97-215">Récapitulatif</span><span class="sxs-lookup"><span data-stu-id="eda97-215">Summary</span></span> | <span data-ttu-id="eda97-216">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="eda97-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="eda97-217">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="eda97-217">pack target inputs</span></span>

- <span data-ttu-id="eda97-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="eda97-218">IsPackable</span></span>
- <span data-ttu-id="eda97-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="eda97-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="eda97-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="eda97-220">PackageVersion</span></span>
- <span data-ttu-id="eda97-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="eda97-221">PackageId</span></span>
- <span data-ttu-id="eda97-222">Auteurs</span><span class="sxs-lookup"><span data-stu-id="eda97-222">Authors</span></span>
- <span data-ttu-id="eda97-223">Description</span><span class="sxs-lookup"><span data-stu-id="eda97-223">Description</span></span>
- <span data-ttu-id="eda97-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="eda97-224">Copyright</span></span>
- <span data-ttu-id="eda97-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eda97-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="eda97-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="eda97-226">DevelopmentDependency</span></span>
- <span data-ttu-id="eda97-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="eda97-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="eda97-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="eda97-228">PackageLicenseFile</span></span>
- <span data-ttu-id="eda97-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="eda97-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-230">PackageProjectUrl</span></span>
- <span data-ttu-id="eda97-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-231">PackageIconUrl</span></span>
- <span data-ttu-id="eda97-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eda97-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="eda97-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="eda97-233">PackageTags</span></span>
- <span data-ttu-id="eda97-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="eda97-234">PackageOutputPath</span></span>
- <span data-ttu-id="eda97-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eda97-235">IncludeSymbols</span></span>
- <span data-ttu-id="eda97-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eda97-236">IncludeSource</span></span>
- <span data-ttu-id="eda97-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="eda97-237">PackageTypes</span></span>
- <span data-ttu-id="eda97-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="eda97-238">IsTool</span></span>
- <span data-ttu-id="eda97-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-239">RepositoryUrl</span></span>
- <span data-ttu-id="eda97-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="eda97-240">RepositoryType</span></span>
- <span data-ttu-id="eda97-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="eda97-241">RepositoryBranch</span></span>
- <span data-ttu-id="eda97-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="eda97-242">RepositoryCommit</span></span>
- <span data-ttu-id="eda97-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="eda97-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="eda97-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="eda97-244">MinClientVersion</span></span>
- <span data-ttu-id="eda97-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="eda97-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="eda97-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="eda97-246">IncludeContentInPack</span></span>
- <span data-ttu-id="eda97-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="eda97-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="eda97-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="eda97-248">ContentTargetFolders</span></span>
- <span data-ttu-id="eda97-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="eda97-249">NuspecFile</span></span>
- <span data-ttu-id="eda97-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="eda97-250">NuspecBasePath</span></span>
- <span data-ttu-id="eda97-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="eda97-251">NuspecProperties</span></span>
- <span data-ttu-id="eda97-252">Déterministe</span><span class="sxs-lookup"><span data-stu-id="eda97-252">Deterministic</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="eda97-253">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="eda97-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="eda97-254">Supprimer les dépendances</span><span class="sxs-lookup"><span data-stu-id="eda97-254">Suppress dependencies</span></span>

<span data-ttu-id="eda97-255">Pour supprimer les dépendances de package du package NuGet `SuppressDependenciesWhenPacking` généré `true` , affectez la valeur à qui autorisera l’ignorance de toutes les dépendances du fichier nupkg généré.</span><span class="sxs-lookup"><span data-stu-id="eda97-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="eda97-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eda97-256">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="eda97-257">PackageIconUrl est déconseillé.</span><span class="sxs-lookup"><span data-stu-id="eda97-257">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="eda97-258">Utilisez [PackageIcon](#packing-an-icon-image-file) à la place.</span><span class="sxs-lookup"><span data-stu-id="eda97-258">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="eda97-259">Compression d’un fichier image d’icône</span><span class="sxs-lookup"><span data-stu-id="eda97-259">Packing an icon image file</span></span>

<span data-ttu-id="eda97-260">Lors de la compression d’un fichier image icône, vous devez utiliser la propriété PackageIcon pour spécifier le chemin d’accès au package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="eda97-260">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eda97-261">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="eda97-261">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="eda97-262">La taille du fichier image est limitée à 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="eda97-262">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="eda97-263">Les formats de fichiers pris en charge sont JPEG et PNG.</span><span class="sxs-lookup"><span data-stu-id="eda97-263">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="eda97-264">Nous recommandons une résolution d’image de 64x64.</span><span class="sxs-lookup"><span data-stu-id="eda97-264">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="eda97-265">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eda97-265">For example:</span></span>

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

<span data-ttu-id="eda97-266">[Exemple d’icône de package](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="eda97-266">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="eda97-267">Pour l’équivalent NuSpec, consultez la [référence NuSpec pour l’icône](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="eda97-267">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="eda97-268">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="eda97-268">Output assemblies</span></span>

<span data-ttu-id="eda97-269">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="eda97-269">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="eda97-270">Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="eda97-270">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="eda97-271">Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="eda97-271">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="eda97-272">`IncludeBuildOutput`: Valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="eda97-272">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="eda97-273">`BuildOutputTargetFolder`: Spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="eda97-273">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="eda97-274">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="eda97-274">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="eda97-275">Références de package</span><span class="sxs-lookup"><span data-stu-id="eda97-275">Package references</span></span>

<span data-ttu-id="eda97-276">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="eda97-276">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="eda97-277">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="eda97-277">Project to project references</span></span>

<span data-ttu-id="eda97-278">Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :</span><span class="sxs-lookup"><span data-stu-id="eda97-278">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="eda97-279">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="eda97-279">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="deterministic"></a><span data-ttu-id="eda97-280">Déterministe</span><span class="sxs-lookup"><span data-stu-id="eda97-280">Deterministic</span></span>

<span data-ttu-id="eda97-281">Lorsque vous `MSBuild -t:pack -p:Deterministic=true`utilisez, plusieurs appels de la cible Pack génèrent exactement le même package.</span><span class="sxs-lookup"><span data-stu-id="eda97-281">When using `MSBuild -t:pack -p:Deterministic=true`, multiple invocations of the the pack target will generate the exact same package.</span></span>
<span data-ttu-id="eda97-282">La sortie de la commande à en-tête pack n’est pas affectée par l’État ambiant de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eda97-282">The output of the pack command is not affected by the ambient state of the machine.</span></span> <span data-ttu-id="eda97-283">En particulier, les entrées zip sont horodatées en tant que 1980-01-01.</span><span class="sxs-lookup"><span data-stu-id="eda97-283">Specifically zip entries will be timestamped as 1980-01-01.</span></span> <span data-ttu-id="eda97-284">Pour obtenir un déterminisme complet, les assemblys doivent être générés avec l’option [de compilateur correspondante-déterministe](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="eda97-284">To achieve full determinism, the assemblies should be built with the respective compiler option [-deterministic](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span></span>
<span data-ttu-id="eda97-285">Il est recommandé de spécifier la propriété déterministe comme suit, afin que le compilateur et NuGet le respecte.</span><span class="sxs-lookup"><span data-stu-id="eda97-285">It is recommended that you specify the deterministic property like following, so both the compiler and NuGet will respect it.</span></span>

```xml
<PropertyGroup>
  <Deterministic>true</Deterministic>
</PropertyGroup>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="eda97-286">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="eda97-286">Including content in a package</span></span>

<span data-ttu-id="eda97-287">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="eda97-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="eda97-288">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="eda97-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="eda97-289">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="eda97-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="eda97-290">Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="eda97-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="eda97-291">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="eda97-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="eda97-292">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="eda97-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="eda97-293">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="eda97-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="eda97-294">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="eda97-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="eda97-295">Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`.</span><span class="sxs-lookup"><span data-stu-id="eda97-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="eda97-296">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="eda97-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="eda97-297">D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.</span><span class="sxs-lookup"><span data-stu-id="eda97-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="eda97-298">Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="eda97-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="eda97-299">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="eda97-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="eda97-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eda97-300">IncludeSymbols</span></span>

<span data-ttu-id="eda97-301">Quand vous utilisez `MSBuild -t:pack -p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="eda97-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="eda97-302">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="eda97-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="eda97-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eda97-303">IncludeSource</span></span>

<span data-ttu-id="eda97-304">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="eda97-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="eda97-305">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="eda97-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="eda97-306">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="eda97-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="eda97-307">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="eda97-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="eda97-308">Compression d’une expression de licence ou d’un fichier de licence</span><span class="sxs-lookup"><span data-stu-id="eda97-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="eda97-309">Lors de l’utilisation d’une expression de licence, la propriété PackageLicenseExpression doit être utilisée.</span><span class="sxs-lookup"><span data-stu-id="eda97-309">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="eda97-310">[Exemple d’expression de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="eda97-310">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="eda97-311">[En savoir plus sur les expressions de licence et les licences acceptées par NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="eda97-311">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="eda97-312">Lors de l’empaquetage d’un fichier de licence, vous devez utiliser la propriété PackageLicenseFile pour spécifier le chemin d’accès au package, relatif à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="eda97-312">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eda97-313">En outre, vous devez vous assurer que le fichier est inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="eda97-313">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="eda97-314">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eda97-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="eda97-315">[Exemple de fichier de licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="eda97-315">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="eda97-316">IsTool</span><span class="sxs-lookup"><span data-stu-id="eda97-316">IsTool</span></span>

<span data-ttu-id="eda97-317">Lors de l’utilisation de `MSBuild -t:pack -p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="eda97-317">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="eda97-318">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="eda97-318">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="eda97-319">Compression à l’aide d’un fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="eda97-319">Packing using a .nuspec</span></span>

<span data-ttu-id="eda97-320">Bien qu’il soit recommandé d’inclure à la place [toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se `.nuspec` trouvent généralement dans le fichier du fichier projet, vous pouvez choisir d' `.nuspec` utiliser un fichier pour compresser votre projet.</span><span class="sxs-lookup"><span data-stu-id="eda97-320">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="eda97-321">Pour un projet de type non-SDK qui utilise `PackageReference`, vous devez effectuer `NuGet.Build.Tasks.Pack.targets` l’importation afin que la tâche Pack puisse être exécutée.</span><span class="sxs-lookup"><span data-stu-id="eda97-321">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="eda97-322">Vous devez toujours restaurer le projet avant de pouvoir compresser un fichier NuSpec.</span><span class="sxs-lookup"><span data-stu-id="eda97-322">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="eda97-323">(Un projet de type SDK comprend les cibles Pack par défaut.)</span><span class="sxs-lookup"><span data-stu-id="eda97-323">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="eda97-324">La version cible du .NET Framework du fichier projet n’est pas pertinente et n’est pas utilisée lors de la compression d’un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="eda97-324">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="eda97-325">Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="eda97-325">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="eda97-326">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="eda97-326">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="eda97-327">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="eda97-327">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="eda97-328">En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="eda97-328">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="eda97-329">`NuspecBasePath`: Chemin d’accès de `.nuspec` base pour le fichier.</span><span class="sxs-lookup"><span data-stu-id="eda97-329">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="eda97-330">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="eda97-330">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eda97-331">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="eda97-331">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eda97-332">Notez que le compactage d’un NuSpec à l’aide de dotnet. exe ou de MSBuild permet également de générer le projet par défaut.</span><span class="sxs-lookup"><span data-stu-id="eda97-332">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="eda97-333">Cela peut être évité en passant ```--no-build``` la propriété à dotnet. exe, qui est l’équivalent du ```<NoBuild>true</NoBuild> ``` paramètre dans votre fichier projet, ainsi que ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` le paramètre dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="eda97-333">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="eda97-334">Voici un exemple de fichier *. csproj* pour compresser un fichier NuSpec :</span><span class="sxs-lookup"><span data-stu-id="eda97-334">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="eda97-335">Points d’extension avancés pour créer un package personnalisé</span><span class="sxs-lookup"><span data-stu-id="eda97-335">Advanced extension points to create customized package</span></span>

<span data-ttu-id="eda97-336">La `pack` cible fournit deux points d’extension qui s’exécutent dans la build interne du Framework cible.</span><span class="sxs-lookup"><span data-stu-id="eda97-336">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="eda97-337">Les points d’extension prennent en charge l’inclusion de contenu et d’assemblys spécifiques au Framework cible dans un package :</span><span class="sxs-lookup"><span data-stu-id="eda97-337">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="eda97-338">`TargetsForTfmSpecificBuildOutput`Indicatif Utilisez pour les fichiers contenus `lib` dans le dossier ou dans un `BuildOutputTargetFolder`dossier spécifié à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="eda97-338">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="eda97-339">`TargetsForTfmSpecificContentInPackage`Indicatif Utilisez pour les `BuildOutputTargetFolder`fichiers en dehors de.</span><span class="sxs-lookup"><span data-stu-id="eda97-339">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="eda97-340">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="eda97-340">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="eda97-341">Écrivez une cible personnalisée et spécifiez-la comme valeur de `$(TargetsForTfmSpecificBuildOutput)` la propriété.</span><span class="sxs-lookup"><span data-stu-id="eda97-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="eda97-342">Pour tous les fichiers qui doivent être placés dans `BuildOutputTargetFolder` (lib par défaut), la cible doit écrire ces fichiers dans ItemGroup `BuildOutputInPackage` et définir les deux valeurs de métadonnées suivantes :</span><span class="sxs-lookup"><span data-stu-id="eda97-342">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="eda97-343">`FinalOutputPath`: Chemin d’accès absolu du fichier ; s’il n’est pas fourni, l’identité est utilisée pour évaluer le chemin source.</span><span class="sxs-lookup"><span data-stu-id="eda97-343">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="eda97-344">`TargetPath`:  Facultatif Définie lorsque le fichier doit être placé dans un sous-dossier `lib\<TargetFramework>` au sein de, comme les assemblys satellites qui se trouvent dans leurs dossiers de culture respectifs.</span><span class="sxs-lookup"><span data-stu-id="eda97-344">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="eda97-345">La valeur par défaut est le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="eda97-345">Defaults to the name of the file.</span></span>

<span data-ttu-id="eda97-346">Exemple :</span><span class="sxs-lookup"><span data-stu-id="eda97-346">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="eda97-347">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="eda97-347">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="eda97-348">Écrivez une cible personnalisée et spécifiez-la comme valeur de `$(TargetsForTfmSpecificContentInPackage)` la propriété.</span><span class="sxs-lookup"><span data-stu-id="eda97-348">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="eda97-349">Pour tous les fichiers à inclure dans le package, la cible doit écrire ces fichiers dans ItemGroup `TfmSpecificPackageFile` et définir les métadonnées facultatives suivantes :</span><span class="sxs-lookup"><span data-stu-id="eda97-349">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="eda97-350">`PackagePath`: Chemin d’accès où le fichier doit être généré dans le package.</span><span class="sxs-lookup"><span data-stu-id="eda97-350">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="eda97-351">NuGet émet un avertissement si plusieurs fichiers sont ajoutés au même chemin d’accès de package.</span><span class="sxs-lookup"><span data-stu-id="eda97-351">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="eda97-352">`BuildAction`: Action de génération à assigner au fichier, obligatoire uniquement si le chemin d’accès du `contentFiles` package se trouve dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="eda97-352">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="eda97-353">La valeur par défaut est « None ».</span><span class="sxs-lookup"><span data-stu-id="eda97-353">Defaults to "None".</span></span>

<span data-ttu-id="eda97-354">Exemple :</span><span class="sxs-lookup"><span data-stu-id="eda97-354">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="eda97-355">Cible restore</span><span class="sxs-lookup"><span data-stu-id="eda97-355">restore target</span></span>

<span data-ttu-id="eda97-356">`MSBuild -t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="eda97-356">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="eda97-357">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="eda97-357">Read all project to project references</span></span>
1. <span data-ttu-id="eda97-358">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="eda97-358">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="eda97-359">Passer des données MSBuild à NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="eda97-359">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="eda97-360">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="eda97-360">Run restore</span></span>
1. <span data-ttu-id="eda97-361">Télécharger les packages</span><span class="sxs-lookup"><span data-stu-id="eda97-361">Download packages</span></span>
1. <span data-ttu-id="eda97-362">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="eda97-362">Write assets file, targets, and props</span></span>

<span data-ttu-id="eda97-363">La `restore` cible fonctionne **uniquement** pour les projets utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="eda97-363">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="eda97-364">Il ne fonctionne **pas** pour les projets qui `packages.config` utilisent le format ; utilisez la [restauration NuGet](../reference/cli-reference/cli-ref-restore.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="eda97-364">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="eda97-365">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="eda97-365">Restore properties</span></span>

<span data-ttu-id="eda97-366">Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="eda97-366">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="eda97-367">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `-p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="eda97-367">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="eda97-368">Propriété</span><span class="sxs-lookup"><span data-stu-id="eda97-368">Property</span></span> | <span data-ttu-id="eda97-369">Description</span><span class="sxs-lookup"><span data-stu-id="eda97-369">Description</span></span> |
|--------|--------|
| <span data-ttu-id="eda97-370">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="eda97-370">RestoreSources</span></span> | <span data-ttu-id="eda97-371">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="eda97-371">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="eda97-372">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="eda97-372">RestorePackagesPath</span></span> | <span data-ttu-id="eda97-373">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eda97-373">User packages folder path.</span></span> |
| <span data-ttu-id="eda97-374">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="eda97-374">RestoreDisableParallel</span></span> | <span data-ttu-id="eda97-375">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="eda97-375">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="eda97-376">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="eda97-376">RestoreConfigFile</span></span> | <span data-ttu-id="eda97-377">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="eda97-377">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="eda97-378">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="eda97-378">RestoreNoCache</span></span> | <span data-ttu-id="eda97-379">Si la valeur est true, évite d’utiliser des packages mis en cache.</span><span class="sxs-lookup"><span data-stu-id="eda97-379">If true, avoids using cached packages.</span></span> <span data-ttu-id="eda97-380">Consultez [gestion des dossiers de packages globaux et de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="eda97-380">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="eda97-381">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="eda97-381">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="eda97-382">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="eda97-382">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="eda97-383">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="eda97-383">RestoreFallbackFolders</span></span> | <span data-ttu-id="eda97-384">Dossiers de secours, utilisés de la même façon que le dossier des packages de l’utilisateur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="eda97-384">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="eda97-385">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="eda97-385">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="eda97-386">Sources supplémentaires à utiliser pendant la restauration.</span><span class="sxs-lookup"><span data-stu-id="eda97-386">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="eda97-387">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="eda97-387">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="eda97-388">Dossiers de secours supplémentaires à utiliser lors de la restauration.</span><span class="sxs-lookup"><span data-stu-id="eda97-388">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="eda97-389">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="eda97-389">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="eda97-390">Exclut les dossiers de secours spécifiés dans`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="eda97-390">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="eda97-391">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="eda97-391">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="eda97-392">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="eda97-392">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="eda97-393">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="eda97-393">RestoreGraphProjectInput</span></span> | <span data-ttu-id="eda97-394">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="eda97-394">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="eda97-395">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="eda97-395">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="eda97-396">Lorsque les projets sont collectés via MSBuild, il détermine s’ils sont collectés à l’aide de l' `SkipNonexistentTargets` optimisation.</span><span class="sxs-lookup"><span data-stu-id="eda97-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="eda97-397">Si la valeur n’est pas définie `true`, la valeur par défaut est.</span><span class="sxs-lookup"><span data-stu-id="eda97-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="eda97-398">La conséquence est un comportement de basculement rapide lorsque les cibles d’un projet ne peuvent pas être importées.</span><span class="sxs-lookup"><span data-stu-id="eda97-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="eda97-399">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="eda97-399">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="eda97-400">Dossier de sortie, avec `BaseIntermediateOutputPath` comme valeur par défaut et le `obj` dossier.</span><span class="sxs-lookup"><span data-stu-id="eda97-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="eda97-401">Exemples</span><span class="sxs-lookup"><span data-stu-id="eda97-401">Examples</span></span>

<span data-ttu-id="eda97-402">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="eda97-402">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="eda97-403">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="eda97-403">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="eda97-404">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="eda97-404">Restore outputs</span></span>

<span data-ttu-id="eda97-405">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="eda97-405">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="eda97-406">Fichier</span><span class="sxs-lookup"><span data-stu-id="eda97-406">File</span></span> | <span data-ttu-id="eda97-407">Description</span><span class="sxs-lookup"><span data-stu-id="eda97-407">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="eda97-408">Contient le graphique de dépendance de toutes les références de package.</span><span class="sxs-lookup"><span data-stu-id="eda97-408">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="eda97-409">Références à des propriétés MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="eda97-409">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="eda97-410">Références à des cibles MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="eda97-410">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="eda97-411">Restauration et génération à l’aide d’une commande MSBuild</span><span class="sxs-lookup"><span data-stu-id="eda97-411">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="eda97-412">En raison du fait que NuGet peut restaurer des packages qui déplacent des cibles et des props MSBuild, les évaluations de la restauration et de la build sont exécutées avec des propriétés globales différentes.</span><span class="sxs-lookup"><span data-stu-id="eda97-412">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="eda97-413">Cela signifie que les éléments suivants auront un comportement imprévisible et souvent incorrect.</span><span class="sxs-lookup"><span data-stu-id="eda97-413">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="eda97-414">Au lieu de cela, l’approche recommandée est la suivante :</span><span class="sxs-lookup"><span data-stu-id="eda97-414">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="eda97-415">La même logique s’applique à d’autres cibles `build`similaires à celles de.</span><span class="sxs-lookup"><span data-stu-id="eda97-415">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="eda97-416">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="eda97-416">PackageTargetFallback</span></span>

<span data-ttu-id="eda97-417">L’élément `PackageTargetFallback` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="eda97-417">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="eda97-418">Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../reference/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="eda97-418">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="eda97-419">Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.</span><span class="sxs-lookup"><span data-stu-id="eda97-419">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="eda97-420">Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue.</span><span class="sxs-lookup"><span data-stu-id="eda97-420">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="eda97-421">Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :</span><span class="sxs-lookup"><span data-stu-id="eda97-421">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="eda97-422">Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="eda97-422">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="eda97-423">Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="eda97-423">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="eda97-424">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="eda97-424">Replacing one library from a restore graph</span></span>

<span data-ttu-id="eda97-425">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="eda97-425">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="eda97-426">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="eda97-426">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="eda97-427">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="eda97-427">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
