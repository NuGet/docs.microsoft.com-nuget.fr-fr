---
title: Commandes pack et restore NuGet comme cibles MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+."
keywords: NuGet et MSBuild, cible pack NuGet, cible restore NuGet
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="e644e-104">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="e644e-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="e644e-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="e644e-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="e644e-106">Avec le format PackageReference, NuGet 4.0 + peut stocker des métadonnées du manifeste tout directement dans un fichier projet au lieu d’utiliser un distinct `.nuspec` fichier.</span><span class="sxs-lookup"><span data-stu-id="e644e-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="e644e-107">Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e644e-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="e644e-108">Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e644e-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="e644e-109">(Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../tools/cli-ref-pack.md) et [restore](../tools/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)</span><span class="sxs-lookup"><span data-stu-id="e644e-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="e644e-110">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="e644e-110">Target build order</span></span>

<span data-ttu-id="e644e-111">Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="e644e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="e644e-112">Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression.</span><span class="sxs-lookup"><span data-stu-id="e644e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="e644e-113">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="e644e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="e644e-114">De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e644e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="e644e-115">Cible pack</span><span class="sxs-lookup"><span data-stu-id="e644e-115">pack target</span></span>

<span data-ttu-id="e644e-116">Lors de l’utilisation de la cible de pack, autrement dit, `msbuild /t:pack`, MSBuild dessine ses entrées dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="e644e-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="e644e-117">Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier de projet dans le premier `<PropertyGroup>` nœud.</span><span class="sxs-lookup"><span data-stu-id="e644e-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="e644e-118">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="e644e-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="e644e-119">Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e644e-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="e644e-120">Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e644e-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="e644e-121">Valeur d’attribut/NuSpec</span><span class="sxs-lookup"><span data-stu-id="e644e-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="e644e-122">Propriété MSBuild</span><span class="sxs-lookup"><span data-stu-id="e644e-122">MSBuild Property</span></span> | <span data-ttu-id="e644e-123">Par défaut</span><span class="sxs-lookup"><span data-stu-id="e644e-123">Default</span></span> | <span data-ttu-id="e644e-124">Notes</span><span class="sxs-lookup"><span data-stu-id="e644e-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="e644e-125">Id</span><span class="sxs-lookup"><span data-stu-id="e644e-125">Id</span></span> | <span data-ttu-id="e644e-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="e644e-126">PackageId</span></span> | <span data-ttu-id="e644e-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="e644e-127">AssemblyName</span></span> | <span data-ttu-id="e644e-128">$(AssemblyName) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="e644e-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="e644e-129">Version</span><span class="sxs-lookup"><span data-stu-id="e644e-129">Version</span></span> | <span data-ttu-id="e644e-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="e644e-130">PackageVersion</span></span> | <span data-ttu-id="e644e-131">Version</span><span class="sxs-lookup"><span data-stu-id="e644e-131">Version</span></span> | <span data-ttu-id="e644e-132">Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 »</span><span class="sxs-lookup"><span data-stu-id="e644e-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="e644e-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e644e-133">VersionPrefix</span></span> | <span data-ttu-id="e644e-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e644e-134">PackageVersionPrefix</span></span> | <span data-ttu-id="e644e-135">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-135">empty</span></span> | <span data-ttu-id="e644e-136">La définition de PackageVersion remplace PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e644e-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="e644e-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e644e-137">VersionSuffix</span></span> | <span data-ttu-id="e644e-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e644e-138">PackageVersionSuffix</span></span> | <span data-ttu-id="e644e-139">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-139">empty</span></span> | <span data-ttu-id="e644e-140">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e644e-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="e644e-141">La définition de PackageVersion remplace PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e644e-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="e644e-142">Auteurs</span><span class="sxs-lookup"><span data-stu-id="e644e-142">Authors</span></span> | <span data-ttu-id="e644e-143">Auteurs</span><span class="sxs-lookup"><span data-stu-id="e644e-143">Authors</span></span> | <span data-ttu-id="e644e-144">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="e644e-144">Username of the current user</span></span> | |
| <span data-ttu-id="e644e-145">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="e644e-145">Owners</span></span> | <span data-ttu-id="e644e-146">N/A</span><span class="sxs-lookup"><span data-stu-id="e644e-146">N/A</span></span> | <span data-ttu-id="e644e-147">Ne figure pas dans NuSpec</span><span class="sxs-lookup"><span data-stu-id="e644e-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="e644e-148">Titre</span><span class="sxs-lookup"><span data-stu-id="e644e-148">Title</span></span> | <span data-ttu-id="e644e-149">Titre</span><span class="sxs-lookup"><span data-stu-id="e644e-149">Title</span></span> | <span data-ttu-id="e644e-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="e644e-150">The PackageId</span></span>| |
| <span data-ttu-id="e644e-151">Description</span><span class="sxs-lookup"><span data-stu-id="e644e-151">Description</span></span> | <span data-ttu-id="e644e-152">Description</span><span class="sxs-lookup"><span data-stu-id="e644e-152">Description</span></span> | <span data-ttu-id="e644e-153">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="e644e-153">"Package Description"</span></span> | |
| <span data-ttu-id="e644e-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="e644e-154">Copyright</span></span> | <span data-ttu-id="e644e-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="e644e-155">Copyright</span></span> | <span data-ttu-id="e644e-156">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-156">empty</span></span> | |
| <span data-ttu-id="e644e-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e644e-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="e644e-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e644e-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="e644e-159">False</span><span class="sxs-lookup"><span data-stu-id="e644e-159">false</span></span> | |
| <span data-ttu-id="e644e-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-160">LicenseUrl</span></span> | <span data-ttu-id="e644e-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-161">PackageLicenseUrl</span></span> | <span data-ttu-id="e644e-162">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-162">empty</span></span> | |
| <span data-ttu-id="e644e-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-163">ProjectUrl</span></span> | <span data-ttu-id="e644e-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-164">PackageProjectUrl</span></span> | <span data-ttu-id="e644e-165">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-165">empty</span></span> | |
| <span data-ttu-id="e644e-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-166">IconUrl</span></span> | <span data-ttu-id="e644e-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-167">PackageIconUrl</span></span> | <span data-ttu-id="e644e-168">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-168">empty</span></span> | |
| <span data-ttu-id="e644e-169">Balises</span><span class="sxs-lookup"><span data-stu-id="e644e-169">Tags</span></span> | <span data-ttu-id="e644e-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="e644e-170">PackageTags</span></span> | <span data-ttu-id="e644e-171">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-171">empty</span></span> | <span data-ttu-id="e644e-172">Les balises sont séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="e644e-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="e644e-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e644e-173">ReleaseNotes</span></span> | <span data-ttu-id="e644e-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e644e-174">PackageReleaseNotes</span></span> | <span data-ttu-id="e644e-175">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-175">empty</span></span> | |
| <span data-ttu-id="e644e-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-176">RepositoryUrl</span></span> | <span data-ttu-id="e644e-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-177">RepositoryUrl</span></span> | <span data-ttu-id="e644e-178">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-178">empty</span></span> | |
| <span data-ttu-id="e644e-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e644e-179">RepositoryType</span></span> | <span data-ttu-id="e644e-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e644e-180">RepositoryType</span></span> | <span data-ttu-id="e644e-181">vide</span><span class="sxs-lookup"><span data-stu-id="e644e-181">empty</span></span> | |
| <span data-ttu-id="e644e-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="e644e-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="e644e-183">Récapitulatif</span><span class="sxs-lookup"><span data-stu-id="e644e-183">Summary</span></span> | <span data-ttu-id="e644e-184">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="e644e-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="e644e-185">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="e644e-185">pack target inputs</span></span>

- <span data-ttu-id="e644e-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="e644e-186">IsPackable</span></span>
- <span data-ttu-id="e644e-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="e644e-187">PackageVersion</span></span>
- <span data-ttu-id="e644e-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="e644e-188">PackageId</span></span>
- <span data-ttu-id="e644e-189">Auteurs</span><span class="sxs-lookup"><span data-stu-id="e644e-189">Authors</span></span>
- <span data-ttu-id="e644e-190">Description</span><span class="sxs-lookup"><span data-stu-id="e644e-190">Description</span></span>
- <span data-ttu-id="e644e-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="e644e-191">Copyright</span></span>
- <span data-ttu-id="e644e-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e644e-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="e644e-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="e644e-193">DevelopmentDependency</span></span>
- <span data-ttu-id="e644e-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="e644e-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-195">PackageProjectUrl</span></span>
- <span data-ttu-id="e644e-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-196">PackageIconUrl</span></span>
- <span data-ttu-id="e644e-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e644e-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="e644e-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="e644e-198">PackageTags</span></span>
- <span data-ttu-id="e644e-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="e644e-199">PackageOutputPath</span></span>
- <span data-ttu-id="e644e-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e644e-200">IncludeSymbols</span></span>
- <span data-ttu-id="e644e-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e644e-201">IncludeSource</span></span>
- <span data-ttu-id="e644e-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="e644e-202">PackageTypes</span></span>
- <span data-ttu-id="e644e-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="e644e-203">IsTool</span></span>
- <span data-ttu-id="e644e-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-204">RepositoryUrl</span></span>
- <span data-ttu-id="e644e-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e644e-205">RepositoryType</span></span>
- <span data-ttu-id="e644e-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="e644e-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="e644e-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="e644e-207">MinClientVersion</span></span>
- <span data-ttu-id="e644e-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="e644e-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="e644e-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="e644e-209">IncludeContentInPack</span></span>
- <span data-ttu-id="e644e-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="e644e-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="e644e-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="e644e-211">ContentTargetFolders</span></span>
- <span data-ttu-id="e644e-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="e644e-212">NuspecFile</span></span>
- <span data-ttu-id="e644e-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="e644e-213">NuspecBasePath</span></span>
- <span data-ttu-id="e644e-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="e644e-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="e644e-215">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="e644e-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="e644e-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e644e-216">PackageIconUrl</span></span>

<span data-ttu-id="e644e-217">Dans le cadre du changement lié au [problème NuGet 2582](https://github.com/NuGet/Home/issues/2582), la propriété `PackageIconUrl` sera finalement remplacée par `PackageIconUri` et peut être un chemin relatif vers un fichier icône qui sera inclus à la racine du package obtenu.</span><span class="sxs-lookup"><span data-stu-id="e644e-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="e644e-218">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="e644e-218">Output assemblies</span></span>

<span data-ttu-id="e644e-219">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="e644e-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="e644e-220">Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="e644e-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="e644e-221">Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="e644e-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="e644e-222">`IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="e644e-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="e644e-223">`BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="e644e-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="e644e-224">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="e644e-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="e644e-225">Références de package</span><span class="sxs-lookup"><span data-stu-id="e644e-225">Package references</span></span>

<span data-ttu-id="e644e-226">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="e644e-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="e644e-227">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="e644e-227">Project to project references</span></span>

<span data-ttu-id="e644e-228">Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e644e-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="e644e-229">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="e644e-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="e644e-230">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="e644e-230">Including content in a package</span></span>

<span data-ttu-id="e644e-231">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="e644e-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="e644e-232">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e644e-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="e644e-233">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="e644e-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="e644e-234">Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="e644e-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="e644e-235">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="e644e-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="e644e-236">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="e644e-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="e644e-237">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="e644e-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="e644e-238">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="e644e-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="e644e-239">Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`.</span><span class="sxs-lookup"><span data-stu-id="e644e-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="e644e-240">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="e644e-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="e644e-241">D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.</span><span class="sxs-lookup"><span data-stu-id="e644e-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="e644e-242">Outre les éléments de contenu, le `<Pack>` et `<PackagePath>` métadonnées peuvent également être définies sur les fichiers avec une action de génération de la compilation, EmbeddedResource, ApplicationDefinition, Page, ressources, écran de démarrage, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="e644e-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="e644e-243">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="e644e-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="e644e-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e644e-244">IncludeSymbols</span></span>

<span data-ttu-id="e644e-245">Quand vous utilisez `MSBuild /t:pack /p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="e644e-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="e644e-246">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="e644e-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="e644e-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e644e-247">IncludeSource</span></span>

<span data-ttu-id="e644e-248">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="e644e-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="e644e-249">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="e644e-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="e644e-250">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="e644e-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="e644e-251">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="e644e-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="e644e-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="e644e-252">IsTool</span></span>

<span data-ttu-id="e644e-253">Lors de l’utilisation de `MSBuild /t:pack /p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="e644e-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="e644e-254">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="e644e-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="e644e-255">Compression à l’aide d’un fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="e644e-255">Packing using a .nuspec</span></span>

<span data-ttu-id="e644e-256">Vous pouvez utiliser un fichier `.nuspec` pour compresser votre projet à condition que vous ayez un fichier projet pour importer `NuGet.Build.Tasks.Pack.targets` afin que la tâche de compression puisse être exécutée.</span><span class="sxs-lookup"><span data-stu-id="e644e-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="e644e-257">Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="e644e-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="e644e-258">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="e644e-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="e644e-259">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="e644e-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="e644e-260">En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="e644e-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="e644e-261">`NuspecBasePath` : chemin de base pour le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e644e-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="e644e-262">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="e644e-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e644e-263">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="e644e-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="e644e-264">Cible restore</span><span class="sxs-lookup"><span data-stu-id="e644e-264">restore target</span></span>

<span data-ttu-id="e644e-265">`MSBuild /t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e644e-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="e644e-266">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="e644e-266">Read all project to project references</span></span>
1. <span data-ttu-id="e644e-267">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e644e-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="e644e-268">Passer des données msbuild à NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="e644e-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="e644e-269">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="e644e-269">Run restore</span></span>
1. <span data-ttu-id="e644e-270">Télécharger les packages</span><span class="sxs-lookup"><span data-stu-id="e644e-270">Download packages</span></span>
1. <span data-ttu-id="e644e-271">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="e644e-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="e644e-272">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="e644e-272">Restore properties</span></span>

<span data-ttu-id="e644e-273">Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="e644e-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="e644e-274">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `/p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="e644e-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="e644e-275">Propriété</span><span class="sxs-lookup"><span data-stu-id="e644e-275">Property</span></span> | <span data-ttu-id="e644e-276">Description</span><span class="sxs-lookup"><span data-stu-id="e644e-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="e644e-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="e644e-277">RestoreSources</span></span> | <span data-ttu-id="e644e-278">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="e644e-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="e644e-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="e644e-279">RestorePackagesPath</span></span> | <span data-ttu-id="e644e-280">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e644e-280">User packages folder path.</span></span> |
| <span data-ttu-id="e644e-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="e644e-281">RestoreDisableParallel</span></span> | <span data-ttu-id="e644e-282">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="e644e-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="e644e-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="e644e-283">RestoreConfigFile</span></span> | <span data-ttu-id="e644e-284">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="e644e-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="e644e-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="e644e-285">RestoreNoCache</span></span> | <span data-ttu-id="e644e-286">Si la valeur est true, permet d’éviter l’utilisation du cache web.</span><span class="sxs-lookup"><span data-stu-id="e644e-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="e644e-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="e644e-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="e644e-288">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="e644e-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="e644e-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="e644e-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="e644e-290">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="e644e-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="e644e-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="e644e-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="e644e-292">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="e644e-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="e644e-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="e644e-293">RestoreOutputPath</span></span> | <span data-ttu-id="e644e-294">Dossier de sortie qui est par défaut le dossier `obj`.</span><span class="sxs-lookup"><span data-stu-id="e644e-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="e644e-295">Exemples</span><span class="sxs-lookup"><span data-stu-id="e644e-295">Examples</span></span>

<span data-ttu-id="e644e-296">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="e644e-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="e644e-297">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="e644e-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="e644e-298">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="e644e-298">Restore outputs</span></span>

<span data-ttu-id="e644e-299">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="e644e-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="e644e-300">Fichier</span><span class="sxs-lookup"><span data-stu-id="e644e-300">File</span></span> | <span data-ttu-id="e644e-301">Description</span><span class="sxs-lookup"><span data-stu-id="e644e-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="e644e-302">Précédemment `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="e644e-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="e644e-303">Références à des propriétés MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="e644e-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="e644e-304">Références à des cibles MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="e644e-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="e644e-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="e644e-305">PackageTargetFallback</span></span>

<span data-ttu-id="e644e-306">L’élément `PackageTargetFallback` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages.</span><span class="sxs-lookup"><span data-stu-id="e644e-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="e644e-307">Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../reference/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="e644e-307">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="e644e-308">Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.</span><span class="sxs-lookup"><span data-stu-id="e644e-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="e644e-309">Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue.</span><span class="sxs-lookup"><span data-stu-id="e644e-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="e644e-310">Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :</span><span class="sxs-lookup"><span data-stu-id="e644e-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="e644e-311">Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="e644e-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="e644e-312">Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="e644e-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="e644e-313">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="e644e-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="e644e-314">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="e644e-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="e644e-315">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="e644e-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="e644e-316">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="e644e-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
