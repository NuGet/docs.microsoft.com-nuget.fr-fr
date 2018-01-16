---
title: Commandes pack et restore NuGet comme cibles MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "Les commandes pack et restore NuGet peuvent être utilisées directement comme cibles MSBuild avec NuGet 4.0+."
keywords: NuGet et MSBuild, cible pack NuGet, cible restore NuGet
ms.reviewer: karann-msft
ms.openlocfilehash: d4778a21a96de6d76d7a20ff9a305960dd6c2bf1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5e860-104">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="5e860-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5e860-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="5e860-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="5e860-106">NuGet 4.0+ peut fonctionner directement avec les informations contenues dans un fichier `.csproj` sans nécessiter de fichier `.nuspec` ou `project.json` distinct.</span><span class="sxs-lookup"><span data-stu-id="5e860-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="5e860-107">Toutes les métadonnées précédemment stockées dans ces fichiers de configuration peuvent être à la place stockées directement dans le fichier `.csproj`, comme décrit ici.</span><span class="sxs-lookup"><span data-stu-id="5e860-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="5e860-108">Avec MSBuild 15.1+, NuGet est également un citoyen MSBuild de première classe avec les cibles `pack` et `restore` comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5e860-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5e860-109">Ces cibles vous permettent d’utiliser NuGet comme vous utiliseriez toute autre tâche ou cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5e860-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5e860-110">(Pour NuGet 3.x et versions antérieures, vous utilisez les commandes [pack](../tools/cli-ref-pack.md) et [restore](../tools/cli-ref-restore.md) via l’interface de ligne de commande NuGet à la place.)</span><span class="sxs-lookup"><span data-stu-id="5e860-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="5e860-111">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="5e860-111">In this topic:</span></span>

- [<span data-ttu-id="5e860-112">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="5e860-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="5e860-113">Cible pack</span><span class="sxs-lookup"><span data-stu-id="5e860-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="5e860-114">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="5e860-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="5e860-115">Cible restore</span><span class="sxs-lookup"><span data-stu-id="5e860-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="5e860-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5e860-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="5e860-117">Ordre de génération des cibles</span><span class="sxs-lookup"><span data-stu-id="5e860-117">Target build order</span></span>

<span data-ttu-id="5e860-118">Étant donné que `pack` et `restore` sont des cibles MSBuild, vous pouvez y accéder pour améliorer votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="5e860-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5e860-119">Par exemple, supposons que vous souhaitez copier votre package sur un partage réseau après compression.</span><span class="sxs-lookup"><span data-stu-id="5e860-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5e860-120">Pour ce faire, ajoutez le code suivant dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="5e860-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="5e860-121">De même, vous pouvez écrire une tâche MSBuild, écrire votre propre cible et consommer des propriétés NuGet dans la tâche MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5e860-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5e860-122">Cible pack</span><span class="sxs-lookup"><span data-stu-id="5e860-122">pack target</span></span>

<span data-ttu-id="5e860-123">Lors de l’utilisation de la cible pack, autrement dit `msbuild /t:pack`, MSBuild obtient ses entrées du fichier `.csproj` plutôt que des fichiers `project.json` ou `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5e860-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="5e860-124">Le tableau ci-dessous décrit les propriétés MSBuild qui peuvent être ajoutées à un fichier `.csproj` au sein du premier nœud `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="5e860-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5e860-125">Vous pouvez effectuer ces modifications facilement dans Visual Studio 2017 et versions ultérieures en cliquant avec le bouton droit sur le projet et en sélectionnant **Modifier {nom_projet}** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="5e860-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5e860-126">Pour des raisons pratiques, le tableau est organisé selon la propriété équivalente dans un [fichier `.nuspec`](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5e860-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="5e860-127">Notez que les propriétés `Owners` et `Summary` de `.nuspec` ne sont pas prises en charge avec MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5e860-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="5e860-128">Valeur d’attribut/NuSpec</span><span class="sxs-lookup"><span data-stu-id="5e860-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5e860-129">Propriété MSBuild</span><span class="sxs-lookup"><span data-stu-id="5e860-129">MSBuild Property</span></span> | <span data-ttu-id="5e860-130">Par défaut</span><span class="sxs-lookup"><span data-stu-id="5e860-130">Default</span></span> | <span data-ttu-id="5e860-131">Notes</span><span class="sxs-lookup"><span data-stu-id="5e860-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5e860-132">Id</span><span class="sxs-lookup"><span data-stu-id="5e860-132">Id</span></span> | <span data-ttu-id="5e860-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="5e860-133">PackageId</span></span> | <span data-ttu-id="5e860-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5e860-134">AssemblyName</span></span> | <span data-ttu-id="5e860-135">$(AssemblyName) de MSBuild</span><span class="sxs-lookup"><span data-stu-id="5e860-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5e860-136">Version</span><span class="sxs-lookup"><span data-stu-id="5e860-136">Version</span></span> | <span data-ttu-id="5e860-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5e860-137">PackageVersion</span></span> | <span data-ttu-id="5e860-138">Version</span><span class="sxs-lookup"><span data-stu-id="5e860-138">Version</span></span> | <span data-ttu-id="5e860-139">Compatible avec SemVer, par exemple « 1.0.0 », « version bêta 1.0.0 » ou « version bêta-1.0.0-00345 »</span><span class="sxs-lookup"><span data-stu-id="5e860-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5e860-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5e860-140">VersionPrefix</span></span> | <span data-ttu-id="5e860-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5e860-141">PackageVersionPrefix</span></span> | <span data-ttu-id="5e860-142">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-142">empty</span></span> | <span data-ttu-id="5e860-143">La définition de PackageVersion remplace PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5e860-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="5e860-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5e860-144">VersionSuffix</span></span> | <span data-ttu-id="5e860-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5e860-145">PackageVersionSuffix</span></span> | <span data-ttu-id="5e860-146">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-146">empty</span></span> | <span data-ttu-id="5e860-147">$(VersionSuffix) de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5e860-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5e860-148">La définition de PackageVersion remplace PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5e860-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="5e860-149">Auteurs</span><span class="sxs-lookup"><span data-stu-id="5e860-149">Authors</span></span> | <span data-ttu-id="5e860-150">Auteurs</span><span class="sxs-lookup"><span data-stu-id="5e860-150">Authors</span></span> | <span data-ttu-id="5e860-151">Nom de l’utilisateur actuel</span><span class="sxs-lookup"><span data-stu-id="5e860-151">Username of the current user</span></span> | |
| <span data-ttu-id="5e860-152">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="5e860-152">Owners</span></span> | <span data-ttu-id="5e860-153">N/A</span><span class="sxs-lookup"><span data-stu-id="5e860-153">N/A</span></span> | <span data-ttu-id="5e860-154">Ne figure pas dans NuSpec</span><span class="sxs-lookup"><span data-stu-id="5e860-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5e860-155">Titre</span><span class="sxs-lookup"><span data-stu-id="5e860-155">Title</span></span> | <span data-ttu-id="5e860-156">Titre</span><span class="sxs-lookup"><span data-stu-id="5e860-156">Title</span></span> | <span data-ttu-id="5e860-157">PackageId</span><span class="sxs-lookup"><span data-stu-id="5e860-157">The PackageId</span></span>| |
| <span data-ttu-id="5e860-158">Description</span><span class="sxs-lookup"><span data-stu-id="5e860-158">Description</span></span> | <span data-ttu-id="5e860-159">Description</span><span class="sxs-lookup"><span data-stu-id="5e860-159">Description</span></span> | <span data-ttu-id="5e860-160">« Description du package »</span><span class="sxs-lookup"><span data-stu-id="5e860-160">"Package Description"</span></span> | |
| <span data-ttu-id="5e860-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="5e860-161">Copyright</span></span> | <span data-ttu-id="5e860-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="5e860-162">Copyright</span></span> | <span data-ttu-id="5e860-163">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-163">empty</span></span> | |
| <span data-ttu-id="5e860-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5e860-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5e860-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5e860-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5e860-166">False</span><span class="sxs-lookup"><span data-stu-id="5e860-166">false</span></span> | |
| <span data-ttu-id="5e860-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-167">LicenseUrl</span></span> | <span data-ttu-id="5e860-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-168">PackageLicenseUrl</span></span> | <span data-ttu-id="5e860-169">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-169">empty</span></span> | |
| <span data-ttu-id="5e860-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-170">ProjectUrl</span></span> | <span data-ttu-id="5e860-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-171">PackageProjectUrl</span></span> | <span data-ttu-id="5e860-172">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-172">empty</span></span> | |
| <span data-ttu-id="5e860-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-173">IconUrl</span></span> | <span data-ttu-id="5e860-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-174">PackageIconUrl</span></span> | <span data-ttu-id="5e860-175">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-175">empty</span></span> | |
| <span data-ttu-id="5e860-176">Balises</span><span class="sxs-lookup"><span data-stu-id="5e860-176">Tags</span></span> | <span data-ttu-id="5e860-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5e860-177">PackageTags</span></span> | <span data-ttu-id="5e860-178">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-178">empty</span></span> | <span data-ttu-id="5e860-179">Les balises sont séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5e860-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5e860-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5e860-180">ReleaseNotes</span></span> | <span data-ttu-id="5e860-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5e860-181">PackageReleaseNotes</span></span> | <span data-ttu-id="5e860-182">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-182">empty</span></span> | |
| <span data-ttu-id="5e860-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-183">RepositoryUrl</span></span> | <span data-ttu-id="5e860-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-184">RepositoryUrl</span></span> | <span data-ttu-id="5e860-185">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-185">empty</span></span> | |
| <span data-ttu-id="5e860-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5e860-186">RepositoryType</span></span> | <span data-ttu-id="5e860-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5e860-187">RepositoryType</span></span> | <span data-ttu-id="5e860-188">vide</span><span class="sxs-lookup"><span data-stu-id="5e860-188">empty</span></span> | |
| <span data-ttu-id="5e860-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="5e860-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5e860-190">Récapitulatif</span><span class="sxs-lookup"><span data-stu-id="5e860-190">Summary</span></span> | <span data-ttu-id="5e860-191">Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="5e860-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="5e860-192">entrées de cible pack</span><span class="sxs-lookup"><span data-stu-id="5e860-192">pack target inputs</span></span>

- <span data-ttu-id="5e860-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5e860-193">IsPackable</span></span>
- <span data-ttu-id="5e860-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5e860-194">PackageVersion</span></span>
- <span data-ttu-id="5e860-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="5e860-195">PackageId</span></span>
- <span data-ttu-id="5e860-196">Auteurs</span><span class="sxs-lookup"><span data-stu-id="5e860-196">Authors</span></span>
- <span data-ttu-id="5e860-197">Description</span><span class="sxs-lookup"><span data-stu-id="5e860-197">Description</span></span>
- <span data-ttu-id="5e860-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="5e860-198">Copyright</span></span>
- <span data-ttu-id="5e860-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5e860-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5e860-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5e860-200">DevelopmentDependency</span></span>
- <span data-ttu-id="5e860-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="5e860-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-202">PackageProjectUrl</span></span>
- <span data-ttu-id="5e860-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-203">PackageIconUrl</span></span>
- <span data-ttu-id="5e860-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5e860-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="5e860-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5e860-205">PackageTags</span></span>
- <span data-ttu-id="5e860-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5e860-206">PackageOutputPath</span></span>
- <span data-ttu-id="5e860-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5e860-207">IncludeSymbols</span></span>
- <span data-ttu-id="5e860-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5e860-208">IncludeSource</span></span>
- <span data-ttu-id="5e860-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5e860-209">PackageTypes</span></span>
- <span data-ttu-id="5e860-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="5e860-210">IsTool</span></span>
- <span data-ttu-id="5e860-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-211">RepositoryUrl</span></span>
- <span data-ttu-id="5e860-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5e860-212">RepositoryType</span></span>
- <span data-ttu-id="5e860-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5e860-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="5e860-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5e860-214">MinClientVersion</span></span>
- <span data-ttu-id="5e860-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5e860-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="5e860-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5e860-216">IncludeContentInPack</span></span>
- <span data-ttu-id="5e860-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5e860-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5e860-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5e860-218">ContentTargetFolders</span></span>
- <span data-ttu-id="5e860-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5e860-219">NuspecFile</span></span>
- <span data-ttu-id="5e860-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5e860-220">NuspecBasePath</span></span>
- <span data-ttu-id="5e860-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5e860-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5e860-222">Scénarios avec pack</span><span class="sxs-lookup"><span data-stu-id="5e860-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5e860-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5e860-223">PackageIconUrl</span></span>

<span data-ttu-id="5e860-224">Dans le cadre du changement lié au [problème NuGet 2582](https://github.com/NuGet/Home/issues/2582), la propriété `PackageIconUrl` sera finalement remplacée par `PackageIconUri` et peut être un chemin relatif vers un fichier icône qui sera inclus à la racine du package obtenu.</span><span class="sxs-lookup"><span data-stu-id="5e860-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5e860-225">Assemblys de sortie</span><span class="sxs-lookup"><span data-stu-id="5e860-225">Output assemblies</span></span>

<span data-ttu-id="5e860-226">`nuget pack` copie les fichiers de sortie avec les extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json` et `.pri`.</span><span class="sxs-lookup"><span data-stu-id="5e860-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5e860-227">Les fichiers de sortie qui sont copiés dépendent de ce que fournit MSBuild à partir de la cible `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="5e860-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5e860-228">Il existe deux propriétés MSBuild que vous pouvez utiliser dans votre fichier projet ou ligne de commande pour contrôler la destination des assemblys de sortie :</span><span class="sxs-lookup"><span data-stu-id="5e860-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5e860-229">`IncludeBuildOutput` : valeur booléenne qui détermine si les assemblys de sortie de génération doivent être inclus dans le package.</span><span class="sxs-lookup"><span data-stu-id="5e860-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5e860-230">`BuildOutputTargetFolder` : spécifie le dossier dans lequel les assemblys de sortie doivent être placés.</span><span class="sxs-lookup"><span data-stu-id="5e860-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5e860-231">Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.</span><span class="sxs-lookup"><span data-stu-id="5e860-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5e860-232">Références de package</span><span class="sxs-lookup"><span data-stu-id="5e860-232">Package references</span></span>

<span data-ttu-id="5e860-233">Consultez [Références de package dans les fichiers projet](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="5e860-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5e860-234">Références entre projets</span><span class="sxs-lookup"><span data-stu-id="5e860-234">Project to project references</span></span>

<span data-ttu-id="5e860-235">Les références entre projets sont considérées par défaut comme des références de package nuget, par exemple :</span><span class="sxs-lookup"><span data-stu-id="5e860-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5e860-236">Vous pouvez également ajouter les métadonnées suivantes à votre référence de projet :</span><span class="sxs-lookup"><span data-stu-id="5e860-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5e860-237">Ajout de contenu dans un package</span><span class="sxs-lookup"><span data-stu-id="5e860-237">Including content in a package</span></span>

<span data-ttu-id="5e860-238">Pour inclure du contenu, ajoutez des métadonnées supplémentaires à l’élément `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="5e860-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5e860-239">Par défaut, tous les éléments de type « Contenu » sont inclus dans le package, sauf si vous procédez à un remplacement avec des entrées telles que les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e860-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="5e860-240">Par défaut, tous les éléments sont ajoutés à la racine de `content` et du dossier `contentFiles\any\<target_framework>` au sein d’un package et la structure de dossier relatif est conservée, sauf si vous spécifiez un chemin de package :</span><span class="sxs-lookup"><span data-stu-id="5e860-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5e860-241">Si vous souhaitez copier tout le contenu uniquement vers des dossiers racines spécifiques (et non vers `content` et `contentFiles`), vous pouvez utiliser la propriété MSBuild `ContentTargetFolders` qui a pour valeur par défaut « content;contentFiles », mais peut être définie sur tout autre nom de dossier.</span><span class="sxs-lookup"><span data-stu-id="5e860-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5e860-242">Notez que le fait de spécifier uniquement « contentFiles » dans `ContentTargetFolders` place les fichiers sous `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` selon `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="5e860-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5e860-243">`PackagePath` peut être un ensemble de chemins cibles séparés par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5e860-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5e860-244">La spécification d’un chemin de package vide permet d’ajouter le fichier à la racine du package.</span><span class="sxs-lookup"><span data-stu-id="5e860-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5e860-245">Par exemple, le code suivant ajoute `libuv.txt` à `content\myfiles`, `content\samples` et la racine du package :</span><span class="sxs-lookup"><span data-stu-id="5e860-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5e860-246">Il existe également une propriété MSBuild `$(IncludeContentInPack)` qui a pour valeur par défaut `true`.</span><span class="sxs-lookup"><span data-stu-id="5e860-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5e860-247">Si sa valeur est `false` sur un projet, le contenu de ce projet ne figure pas dans le package nuget.</span><span class="sxs-lookup"><span data-stu-id="5e860-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5e860-248">D’autres métadonnées spécifiques à pack que vous pouvez définir sur l’un des éléments ci-dessus incluent ```<PackageCopyToOutput>``` et ```<PackageFlatten>``` qui définissent les valeurs ```CopyToOutput``` et ```Flatten``` sur l’entrée ```contentFiles``` dans le fichier nuspec de sortie.</span><span class="sxs-lookup"><span data-stu-id="5e860-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="5e860-249">Outre les éléments de contenu, les métadonnées `<Pack>` et `<PackagePath>` peuvent aussi être définies sur des fichiers avec l’action de génération Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="5e860-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5e860-250">Pour que la commande pack ajoute le nom de fichier à votre chemin de package lors de l’utilisation de modèles de globbing, votre chemin doit se terminer par le caractère de séparation de dossier, sinon il est traité comme le chemin complet avec le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="5e860-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5e860-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5e860-251">IncludeSymbols</span></span>

<span data-ttu-id="5e860-252">Quand vous utilisez `MSBuild /t:pack /p:IncludeSymbols=true`, les fichiers `.pdb` correspondants sont copiés avec d’autres fichiers de sortie (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="5e860-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5e860-253">Notez que la définition `IncludeSymbols=true` crée un package standard *et* un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="5e860-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5e860-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5e860-254">IncludeSource</span></span>

<span data-ttu-id="5e860-255">Propriété identique à `IncludeSymbols`, sauf qu’elle copie également les fichiers sources avec les fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="5e860-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5e860-256">Tous les fichiers de type `Compile` sont copiés vers `src\<ProjectName>\` en conservant la structure de dossiers de chemin relatif dans le package obtenu.</span><span class="sxs-lookup"><span data-stu-id="5e860-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5e860-257">La même situation se produit également pour les fichiers sources de n’importe quel `ProjectReference` dont `TreatAsPackageReference` a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="5e860-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5e860-258">Si un fichier de type Compile est en dehors du dossier de projet, il est simplement ajouté à `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="5e860-258">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="5e860-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="5e860-259">IsTool</span></span>

<span data-ttu-id="5e860-260">Lors de l’utilisation de `MSBuild /t:pack /p:IsTool=true`, tous les fichiers de sortie, comme spécifié dans le scénario [Assemblys de sortie](#output-assemblies), sont copiés dans le dossier `tools` au lieu du dossier `lib`.</span><span class="sxs-lookup"><span data-stu-id="5e860-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5e860-261">Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="5e860-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5e860-262">Compression à l’aide d’un fichier .nuspec</span><span class="sxs-lookup"><span data-stu-id="5e860-262">Packing using a .nuspec</span></span>

<span data-ttu-id="5e860-263">Vous pouvez utiliser un fichier `.nuspec` pour compresser votre projet à condition que vous ayez un fichier projet pour importer `NuGet.Build.Tasks.Pack.targets` afin que la tâche de compression puisse être exécutée.</span><span class="sxs-lookup"><span data-stu-id="5e860-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5e860-264">Les trois propriétés MSBuild suivantes sont pertinentes lors de la compression à l’aide d’un fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="5e860-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5e860-265">`NuspecFile` : chemin relatif ou absolu du fichier `.nuspec` utilisé pour la compression.</span><span class="sxs-lookup"><span data-stu-id="5e860-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5e860-266">`NuspecProperties` : liste de paires clé=valeur séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5e860-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5e860-267">En raison du mode de fonctionnement de l’analyse de ligne de commande MSBuild, plusieurs propriétés doivent être spécifiées comme suit : `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="5e860-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5e860-268">`NuspecBasePath` : chemin de base pour le fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5e860-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5e860-269">Si vous utilisez `dotnet.exe` pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="5e860-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5e860-270">Si vous utilisez MSBuild pour compresser votre projet, utilisez une commande semblable à la suivante :</span><span class="sxs-lookup"><span data-stu-id="5e860-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="5e860-271">Cible restore</span><span class="sxs-lookup"><span data-stu-id="5e860-271">restore target</span></span>

<span data-ttu-id="5e860-272">`MSBuild /t:restore` (que `nuget restore` et `dotnet restore` utilisent avec les projets .NET Core) restaure les packages référencés dans le fichier projet en effectuant les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e860-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5e860-273">Lire toutes les références entre projets</span><span class="sxs-lookup"><span data-stu-id="5e860-273">Read all project to project references</span></span>
1. <span data-ttu-id="5e860-274">Lire les propriétés du projet pour trouver le dossier intermédiaire et les versions cibles de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="5e860-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5e860-275">Passer des données msbuild à NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="5e860-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5e860-276">Exécuter la restauration</span><span class="sxs-lookup"><span data-stu-id="5e860-276">Run restore</span></span>
1. <span data-ttu-id="5e860-277">Télécharger les packages</span><span class="sxs-lookup"><span data-stu-id="5e860-277">Download packages</span></span>
1. <span data-ttu-id="5e860-278">Écrire le fichier de ressources, les cibles et les propriétés</span><span class="sxs-lookup"><span data-stu-id="5e860-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="5e860-279">Propriétés de restauration</span><span class="sxs-lookup"><span data-stu-id="5e860-279">Restore properties</span></span>

<span data-ttu-id="5e860-280">Des paramètres de restauration supplémentaires peuvent provenir de propriétés MSBuild dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="5e860-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5e860-281">Des valeurs peuvent également être définies à partir de la ligne de commande à l’aide du commutateur `/p:` (consultez Exemples ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="5e860-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5e860-282">Propriété</span><span class="sxs-lookup"><span data-stu-id="5e860-282">Property</span></span> | <span data-ttu-id="5e860-283">Description</span><span class="sxs-lookup"><span data-stu-id="5e860-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5e860-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5e860-284">RestoreSources</span></span> | <span data-ttu-id="5e860-285">Liste de sources de packages séparées par un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="5e860-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5e860-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5e860-286">RestorePackagesPath</span></span> | <span data-ttu-id="5e860-287">Chemin du dossier de packages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5e860-287">User packages folder path.</span></span> |
| <span data-ttu-id="5e860-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5e860-288">RestoreDisableParallel</span></span> | <span data-ttu-id="5e860-289">Limite les téléchargements à un à la fois.</span><span class="sxs-lookup"><span data-stu-id="5e860-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5e860-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5e860-290">RestoreConfigFile</span></span> | <span data-ttu-id="5e860-291">Chemin à un fichier `Nuget.Config` à appliquer.</span><span class="sxs-lookup"><span data-stu-id="5e860-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5e860-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5e860-292">RestoreNoCache</span></span> | <span data-ttu-id="5e860-293">Si la valeur est true, permet d’éviter l’utilisation du cache web.</span><span class="sxs-lookup"><span data-stu-id="5e860-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="5e860-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5e860-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5e860-295">Si la valeur est true, ignore les sources de packages défectueuses ou manquantes.</span><span class="sxs-lookup"><span data-stu-id="5e860-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5e860-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5e860-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5e860-297">Chemin d’accès à `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="5e860-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5e860-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5e860-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5e860-299">Liste de projets à restaurer séparés par un point-virgule, qui doit contenir des chemins absolus.</span><span class="sxs-lookup"><span data-stu-id="5e860-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5e860-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="5e860-300">RestoreOutputPath</span></span> | <span data-ttu-id="5e860-301">Dossier de sortie qui est par défaut le dossier `obj`.</span><span class="sxs-lookup"><span data-stu-id="5e860-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="5e860-302">**Exemples**</span><span class="sxs-lookup"><span data-stu-id="5e860-302">**Examples**</span></span>

<span data-ttu-id="5e860-303">Ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="5e860-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="5e860-304">Fichier projet :</span><span class="sxs-lookup"><span data-stu-id="5e860-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5e860-305">Sorties de restauration</span><span class="sxs-lookup"><span data-stu-id="5e860-305">Restore outputs</span></span>

<span data-ttu-id="5e860-306">La restauration crée les fichiers suivants dans le dossier `obj` de build :</span><span class="sxs-lookup"><span data-stu-id="5e860-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5e860-307">Fichier</span><span class="sxs-lookup"><span data-stu-id="5e860-307">File</span></span> | <span data-ttu-id="5e860-308">Description</span><span class="sxs-lookup"><span data-stu-id="5e860-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5e860-309">Précédemment `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="5e860-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5e860-310">Références à des propriétés MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="5e860-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5e860-311">Références à des cibles MSBuild contenues dans des packages</span><span class="sxs-lookup"><span data-stu-id="5e860-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="5e860-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5e860-312">PackageTargetFallback</span></span> 

<span data-ttu-id="5e860-313">L’élément `PackageTargetFallback` vous permet de spécifier un ensemble de cibles compatibles à utiliser lors de la restauration des packages (équivalent de [`imports` dans `project.json`](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="5e860-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="5e860-314">Il est conçu pour permettre aux packages qui utilisent un [moniker du Framework cible](../schema/target-frameworks.md) dotnet de fonctionner avec des packages compatibles qui ne déclarent pas de moniker du Framework cible dotnet.</span><span class="sxs-lookup"><span data-stu-id="5e860-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5e860-315">Autrement dit, si votre projet utilise le moniker du Framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du Framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet.</span><span class="sxs-lookup"><span data-stu-id="5e860-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="5e860-316">Par exemple, si le projet utilise le moniker du Framework cible `netstandard1.6` et qu’un package dépendant ne contient que `lib/net45/a.dll` et `lib/portable-net45+win81/a.dll`, la génération du projet échoue.</span><span class="sxs-lookup"><span data-stu-id="5e860-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5e860-317">Si vous souhaitez présenter la dernière DLL, vous pouvez ajouter un `PackageTargetFallback` comme suit pour dire que la DLL `portable-net45+win81` est compatible :</span><span class="sxs-lookup"><span data-stu-id="5e860-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5e860-318">Pour déclarer une solution de secours pour toutes les cibles de votre projet, omettez l’attribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="5e860-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5e860-319">Vous pouvez également étendre tout `PackageTargetFallback` en incluant `$(PackageTargetFallback)` comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="5e860-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5e860-320">Remplacement d’une bibliothèque à partir d’un graphique de restauration</span><span class="sxs-lookup"><span data-stu-id="5e860-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5e860-321">Si une restauration présente un assembly incorrect, il est possible d’exclure cette option par défaut de package et de la remplacer par votre propre choix.</span><span class="sxs-lookup"><span data-stu-id="5e860-321">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5e860-322">Commencez par exclure toutes les ressources avec un `PackageReference` de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="5e860-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5e860-323">Ajoutez ensuite votre propre référence à la copie locale appropriée de la DLL :</span><span class="sxs-lookup"><span data-stu-id="5e860-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
