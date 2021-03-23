---
title: Format PackageReference NuGet (références de package dans des fichiers projet)
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: df7c793d115622f04a148cbbc3ebf396a3e4ab69
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859185"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="8574b-103">Références de package ( `PackageReference` ) dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="8574b-103">Package references (`PackageReference`) in project files</span></span>

<span data-ttu-id="8574b-104">Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé.</span><span class="sxs-lookup"><span data-stu-id="8574b-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="8574b-105">L’utilisation de PackageReference n’a pas d’impact sur les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.config` (notamment les sources de packages) continuent d’être appliqués, comme cela est expliqué dans [Configurations courantes de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8574b-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8574b-106">Avec PackageReference, vous pouvez également utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework ou d’autres regroupements.</span><span class="sxs-lookup"><span data-stu-id="8574b-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="8574b-107">Elle permet également de mieux contrôler les dépendances et les flux de contenu.</span><span class="sxs-lookup"><span data-stu-id="8574b-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="8574b-108">Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="8574b-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="8574b-109">Prise en charge de type de projet</span><span class="sxs-lookup"><span data-stu-id="8574b-109">Project type support</span></span>

<span data-ttu-id="8574b-110">Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="8574b-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="8574b-111">Les projets .NET Framework prennent en charge PackageReference, mais utilisent par défaut `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8574b-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="8574b-112">Pour utiliser PackageReference, [migrez](../consume-packages/migrate-packages-config-to-package-reference.md) les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.</span><span class="sxs-lookup"><span data-stu-id="8574b-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="8574b-113">Les applications ASP.NET ciblant le .NET Framework incluent uniquement une [prise en charge limitée](https://github.com/NuGet/Home/issues/5877) pour PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8574b-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="8574b-114">Les types de projets C++ et JavaScript ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8574b-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="8574b-115">Ajout d’un PackageReference</span><span class="sxs-lookup"><span data-stu-id="8574b-115">Adding a PackageReference</span></span>

<span data-ttu-id="8574b-116">Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="8574b-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="8574b-117">Contrôle des versions des dépendances</span><span class="sxs-lookup"><span data-stu-id="8574b-117">Controlling dependency version</span></span>

<span data-ttu-id="8574b-118">Pour spécifier la version d’un package, la convention est la même que pour `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="8574b-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8574b-119">Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="8574b-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="8574b-120">Utilisation de PackageReference pour un projet sans PackageReferences</span><span class="sxs-lookup"><span data-stu-id="8574b-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="8574b-121">Avancé : Si vous n’avez aucun package installé dans un projet (aucune PackageReferences dans le fichier projet et aucun fichier packages.config), mais que vous souhaitez restaurer le projet en tant que style PackageReference, vous pouvez définir une propriété de projet RestoreProjectStyle avec la valeur PackageReference dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="8574b-122">Cela peut être utile si vous référencez des projets qui sont de style PackageReference (projets csproj ou de style SDK existants).</span><span class="sxs-lookup"><span data-stu-id="8574b-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="8574b-123">Cela permet aux packages auxquels ces projets font référence d’être référencés « transitivement » par votre projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="8574b-124">PackageReference et sources</span><span class="sxs-lookup"><span data-stu-id="8574b-124">PackageReference and sources</span></span>

<span data-ttu-id="8574b-125">Dans les projets PackageReference, les versions de dépendances transitives sont résolues au moment de la restauration.</span><span class="sxs-lookup"><span data-stu-id="8574b-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="8574b-126">Par conséquent, dans les projets PackageReference, toutes les sources doivent être disponibles pour toutes les restaurations.</span><span class="sxs-lookup"><span data-stu-id="8574b-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="8574b-127">Versions flottantes</span><span class="sxs-lookup"><span data-stu-id="8574b-127">Floating Versions</span></span>

<span data-ttu-id="8574b-128">Les [versions flottantes](../concepts/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="8574b-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="8574b-129">Contrôle des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="8574b-129">Controlling dependency assets</span></span>

<span data-ttu-id="8574b-130">Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package.</span><span class="sxs-lookup"><span data-stu-id="8574b-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="8574b-131">Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.</span><span class="sxs-lookup"><span data-stu-id="8574b-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8574b-132">Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :</span><span class="sxs-lookup"><span data-stu-id="8574b-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="8574b-133">Tag</span><span class="sxs-lookup"><span data-stu-id="8574b-133">Tag</span></span> | <span data-ttu-id="8574b-134">Description</span><span class="sxs-lookup"><span data-stu-id="8574b-134">Description</span></span> | <span data-ttu-id="8574b-135">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="8574b-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8574b-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="8574b-136">IncludeAssets</span></span> | <span data-ttu-id="8574b-137">Ces ressources sont consommées.</span><span class="sxs-lookup"><span data-stu-id="8574b-137">These assets will be consumed</span></span> | <span data-ttu-id="8574b-138">all</span><span class="sxs-lookup"><span data-stu-id="8574b-138">all</span></span> |
| <span data-ttu-id="8574b-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="8574b-139">ExcludeAssets</span></span> | <span data-ttu-id="8574b-140">Ces ressources ne sont pas consommées.</span><span class="sxs-lookup"><span data-stu-id="8574b-140">These assets will not be consumed</span></span> | <span data-ttu-id="8574b-141">Aucun</span><span class="sxs-lookup"><span data-stu-id="8574b-141">none</span></span> |
| <span data-ttu-id="8574b-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="8574b-142">PrivateAssets</span></span> | <span data-ttu-id="8574b-143">Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="8574b-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="8574b-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="8574b-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="8574b-145">Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :</span><span class="sxs-lookup"><span data-stu-id="8574b-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="8574b-146">Valeur</span><span class="sxs-lookup"><span data-stu-id="8574b-146">Value</span></span> | <span data-ttu-id="8574b-147">Description</span><span class="sxs-lookup"><span data-stu-id="8574b-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="8574b-148">compile</span><span class="sxs-lookup"><span data-stu-id="8574b-148">compile</span></span> | <span data-ttu-id="8574b-149">Contenu du dossier `lib` et contrôles permettant de déterminer si votre projet peut être compilé avec les assemblys dans le dossier</span><span class="sxs-lookup"><span data-stu-id="8574b-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="8574b-150">runtime</span><span class="sxs-lookup"><span data-stu-id="8574b-150">runtime</span></span> | <span data-ttu-id="8574b-151">Contenu des dossiers `lib` et `runtimes` contrôles permettant de déterminer si ces assemblys seront copiés vers le répertoire de sortie de build</span><span class="sxs-lookup"><span data-stu-id="8574b-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="8574b-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8574b-152">contentFiles</span></span> | <span data-ttu-id="8574b-153">Contenu du dossier `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="8574b-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="8574b-154">build</span><span class="sxs-lookup"><span data-stu-id="8574b-154">build</span></span> | <span data-ttu-id="8574b-155">`.props` et `.targets` dans le dossier `build`</span><span class="sxs-lookup"><span data-stu-id="8574b-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="8574b-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="8574b-156">buildMultitargeting</span></span> | <span data-ttu-id="8574b-157">*(4.0)* `.props` et `.targets` dans le dossier `buildMultitargeting`, pour le ciblage multi-infrastructures</span><span class="sxs-lookup"><span data-stu-id="8574b-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="8574b-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="8574b-158">buildTransitive</span></span> | <span data-ttu-id="8574b-159">*(5.0 +)* `.props` et `.targets` dans le dossier `buildTransitive`, pour les ressources qui circulent de manière transitive vers n’importe quel projet consommateur.</span><span class="sxs-lookup"><span data-stu-id="8574b-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="8574b-160">Consultez la page [Fonctionnalité](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="8574b-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="8574b-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="8574b-161">analyzers</span></span> | <span data-ttu-id="8574b-162">Analyseurs .NET</span><span class="sxs-lookup"><span data-stu-id="8574b-162">.NET analyzers</span></span> |
| <span data-ttu-id="8574b-163">native</span><span class="sxs-lookup"><span data-stu-id="8574b-163">native</span></span> | <span data-ttu-id="8574b-164">Contenu du dossier `native`</span><span class="sxs-lookup"><span data-stu-id="8574b-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="8574b-165">Aucun</span><span class="sxs-lookup"><span data-stu-id="8574b-165">none</span></span> | <span data-ttu-id="8574b-166">Aucune des valeurs ci-dessus n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="8574b-166">None of the above are used.</span></span> |
| <span data-ttu-id="8574b-167">all</span><span class="sxs-lookup"><span data-stu-id="8574b-167">all</span></span> | <span data-ttu-id="8574b-168">Toutes les valeurs ci-dessus sont utilisées (sauf `none`)</span><span class="sxs-lookup"><span data-stu-id="8574b-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="8574b-169">Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="8574b-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8574b-170">Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="8574b-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="8574b-171">Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger.</span><span class="sxs-lookup"><span data-stu-id="8574b-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="8574b-172">AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.</span><span class="sxs-lookup"><span data-stu-id="8574b-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="8574b-173">Si la propriété `developmentDependency` est définie sur `true` dans un fichier `.nuspec`, elle marque un package comme dépendance de développement uniquement, ce qui l’empêche d’être inclus en tant que dépendance dans d’autres packages.</span><span class="sxs-lookup"><span data-stu-id="8574b-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="8574b-174">Avec PackageReference *(NuGet 4.8+)*, cet indicateur signifie également que la propriété exclura les ressources de la compilation.</span><span class="sxs-lookup"><span data-stu-id="8574b-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="8574b-175">Pour plus d'informations, voir [Prise en charge de DevelopmentDependency pour PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="8574b-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="8574b-176">Ajout d’une condition PackageReference</span><span class="sxs-lookup"><span data-stu-id="8574b-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="8574b-177">Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="8574b-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="8574b-178">Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="8574b-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="8574b-179">Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`.</span><span class="sxs-lookup"><span data-stu-id="8574b-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="8574b-180">Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="8574b-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="8574b-181">Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="8574b-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8574b-182">Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.Json est inclus en tant que dépendance uniquement pour une cible `net452` :</span><span class="sxs-lookup"><span data-stu-id="8574b-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="8574b-184">Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="8574b-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="8574b-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="8574b-185">GeneratePathProperty</span></span>

<span data-ttu-id="8574b-186">Cette fonctionnalité est disponible avec NuGet **5,0** ou version ultérieure et avec Visual Studio 2019 **16,0** ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8574b-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="8574b-187">Il est parfois souhaitable de référencer des fichiers dans un package à partir d’une cible MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8574b-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="8574b-188">Dans `packages.config` les projets basés sur, les packages sont installés dans un dossier relatif au fichier projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="8574b-189">Toutefois, dans PackageReference, les packages sont [consommés](../concepts/package-installation-process.md) à partir du dossier *Global-packages* , qui peut varier d’un ordinateur à l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8574b-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="8574b-190">Pour combler ce fossé, NuGet a introduit une propriété qui pointe vers l’emplacement à partir duquel le package sera consommé.</span><span class="sxs-lookup"><span data-stu-id="8574b-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="8574b-191">Exemple :</span><span class="sxs-lookup"><span data-stu-id="8574b-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="8574b-192">En outre, NuGet génère automatiquement les propriétés des packages contenant un dossier Tools.</span><span class="sxs-lookup"><span data-stu-id="8574b-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="8574b-193">Les propriétés MSBuild et les identités de package n’ont pas les mêmes restrictions afin que l’identité du package doive être remplacée par un nom convivial MSBuild, préfixé par le mot `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="8574b-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="8574b-194">Pour vérifier le nom exact de la propriété générée, examinez le fichier [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) généré.</span><span class="sxs-lookup"><span data-stu-id="8574b-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="8574b-195">Alias PackageReference</span><span class="sxs-lookup"><span data-stu-id="8574b-195">PackageReference Aliases</span></span>

<span data-ttu-id="8574b-196">Dans certains cas rares, différents packages contiendront des classes dans le même espace de noms.</span><span class="sxs-lookup"><span data-stu-id="8574b-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="8574b-197">À compter de NuGet 5,7 & Visual Studio 2019 Update 7, équivalent à ProjectReference, PackageReference prend en charge [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="8574b-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="8574b-198">Par défaut, aucun alias n’est fourni.</span><span class="sxs-lookup"><span data-stu-id="8574b-198">By default no aliases are provided.</span></span> <span data-ttu-id="8574b-199">Lorsqu’un alias est spécifié, *tous les* assemblys provenant du package annoté doivent être référencés avec un alias.</span><span class="sxs-lookup"><span data-stu-id="8574b-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="8574b-200">Vous pouvez examiner l’utilisation de l’exemple sur [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span><span class="sxs-lookup"><span data-stu-id="8574b-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="8574b-201">Dans le fichier projet, spécifiez les alias comme suit :</span><span class="sxs-lookup"><span data-stu-id="8574b-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="8574b-202">et dans le code, utilisez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="8574b-202">and in the code use it as follows:</span></span>

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="8574b-203">Avertissements et erreurs NuGet</span><span class="sxs-lookup"><span data-stu-id="8574b-203">NuGet warnings and errors</span></span>

<span data-ttu-id="8574b-204">*Cette fonctionnalité est disponible avec NuGet **4,3** ou version ultérieure et avec Visual Studio 2017 **15,3** ou version ultérieure.*</span><span class="sxs-lookup"><span data-stu-id="8574b-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="8574b-205">Pour de nombreux scénarios de packs et de restaurations, tous les avertissements et erreurs NuGet sont codés, et commencent par `NU****` .</span><span class="sxs-lookup"><span data-stu-id="8574b-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="8574b-206">Toutes les erreurs et avertissements NuGet sont répertoriés dans la documentation de [référence](../reference/errors-and-warnings.md) .</span><span class="sxs-lookup"><span data-stu-id="8574b-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="8574b-207">NuGet observe les propriétés d’avertissement suivantes :</span><span class="sxs-lookup"><span data-stu-id="8574b-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="8574b-208">`TreatWarningsAsErrors`, considérer tous les avertissements comme des erreurs</span><span class="sxs-lookup"><span data-stu-id="8574b-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="8574b-209">`WarningsAsErrors`, traiter des avertissements spécifiques comme des erreurs</span><span class="sxs-lookup"><span data-stu-id="8574b-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="8574b-210">`NoWarn`, masquez des avertissements spécifiques, à l’ensemble du projet ou à l’ensemble du package.</span><span class="sxs-lookup"><span data-stu-id="8574b-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="8574b-211">Exemples :</span><span class="sxs-lookup"><span data-stu-id="8574b-211">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="8574b-212">Suppression des avertissements NuGet</span><span class="sxs-lookup"><span data-stu-id="8574b-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="8574b-213">Bien qu’il soit recommandé de résoudre tous les avertissements NuGet au cours de vos opérations de Pack et de restauration, il est justifié, dans certaines situations, de les supprimer.</span><span class="sxs-lookup"><span data-stu-id="8574b-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="8574b-214">Pour supprimer un projet d’avertissement en largeur, envisagez d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8574b-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="8574b-215">Parfois, les avertissements s’appliquent uniquement à un package donné du graphique.</span><span class="sxs-lookup"><span data-stu-id="8574b-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="8574b-216">Nous pouvons choisir de supprimer cet avertissement de manière plus sélective en ajoutant un `NoWarn` sur l’élément PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8574b-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="8574b-217">Suppression des avertissements du package NuGet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8574b-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="8574b-218">Dans Visual Studio, vous pouvez également [supprimer des avertissements](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) par le biais de l’IDE.</span><span class="sxs-lookup"><span data-stu-id="8574b-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="8574b-219">Verrouillage des dépendances</span><span class="sxs-lookup"><span data-stu-id="8574b-219">Locking dependencies</span></span>

<span data-ttu-id="8574b-220">*Cette fonctionnalité est disponible avec NuGet **4.9** ou ultérieur, et avec Visual Studio 2017 **15.9** ou ultérieur.*</span><span class="sxs-lookup"><span data-stu-id="8574b-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="8574b-221">L’entrée de la restauration NuGet est un ensemble de références de package provenant du fichier de projet (dépendances de niveau supérieur ou directes). La sortie est une fermeture complète de toutes les dépendances de package, notamment les dépendances transitives.</span><span class="sxs-lookup"><span data-stu-id="8574b-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="8574b-222">NuGet s’efforce toujours de produire la même fermeture complète des dépendances de package si la liste PackageReference d’entrée ne change pas.</span><span class="sxs-lookup"><span data-stu-id="8574b-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="8574b-223">Toutefois, tous les scénarios ne s’y prêtent pas.</span><span class="sxs-lookup"><span data-stu-id="8574b-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="8574b-224">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8574b-224">For example:</span></span>

* <span data-ttu-id="8574b-225">Quand vous utilisez des versions flottantes comme `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="8574b-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="8574b-226">L’intention ici est de flotter vers la dernière version à chaque restauration de package. Mais dans certains scénarios, les utilisateurs peuvent exiger le verrouillage du graphe à une version récente donnée et son flottement vers une version ultérieure, si celle-ci est disponible, à la suite d’un mouvement explicite.</span><span class="sxs-lookup"><span data-stu-id="8574b-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="8574b-227">Une version plus récente du package correspondant aux exigences de version de PackageReference est publiée.</span><span class="sxs-lookup"><span data-stu-id="8574b-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="8574b-228">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="8574b-228">E.g.</span></span> 

  * <span data-ttu-id="8574b-229">Premier jour : Vous spécifiez `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, mais les versions disponibles sur les dépôts NuGet sont 4.1.0, 4.2.0 et 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="8574b-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="8574b-230">Dans ce cas, NuGet résout la version en 4.1.0 (la plus proche de la version minimale).</span><span class="sxs-lookup"><span data-stu-id="8574b-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="8574b-231">Deuxième jour : La version 4.0.0 est publiée.</span><span class="sxs-lookup"><span data-stu-id="8574b-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="8574b-232">NuGet trouve désormais la correspondance exacte et commence à résoudre la version en 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="8574b-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="8574b-233">Une version de package donnée est supprimée du dépôt.</span><span class="sxs-lookup"><span data-stu-id="8574b-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="8574b-234">Bien que nuget.org n’autorise pas la suppression de packages, d’autres dépôts de packages n’ont pas cette contrainte.</span><span class="sxs-lookup"><span data-stu-id="8574b-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="8574b-235">NuGet trouve donc la meilleure correspondance quand la version supprimée rend impossible la résolution.</span><span class="sxs-lookup"><span data-stu-id="8574b-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="8574b-236">Activation du fichier de verrouillage</span><span class="sxs-lookup"><span data-stu-id="8574b-236">Enabling lock file</span></span>

<span data-ttu-id="8574b-237">Pour rendre persistante la fermeture complète des dépendances de package, vous pouvez choisir d’utiliser la fonctionnalité de fichier de verrouillage en définissant la propriété MSBuild `RestorePackagesWithLockFile` pour votre projet :</span><span class="sxs-lookup"><span data-stu-id="8574b-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="8574b-238">Si cette propriété est définie, la restauration NuGet génère un fichier de verrouillage (`packages.lock.json`) au niveau du répertoire racine du projet qui liste toutes les dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="8574b-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="8574b-239">Quand un projet a un fichier `packages.lock.json` dans son répertoire racine, le fichier de verrouillage est toujours utilisé avec la restauration, même si la propriété `RestorePackagesWithLockFile` n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="8574b-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="8574b-240">Une autre façon de choisir cette fonctionnalité consiste à créer un fichier `packages.lock.json` vide factice dans le répertoire racine du projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="8574b-241">Comportement de `restore` avec fichier de verrouillage</span><span class="sxs-lookup"><span data-stu-id="8574b-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="8574b-242">Si un fichier de verrouillage est présent pour le projet, NuGet utilise ce fichier de verrouillage pour exécuter `restore`.</span><span class="sxs-lookup"><span data-stu-id="8574b-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="8574b-243">NuGet effectue une vérification rapide pour voir si les dépendances de package ont changé, comme indiqué dans le fichier projet (ou les fichiers des projets dépendants). Si aucun changement n’est détecté, il restaure simplement les packages mentionnés dans le fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="8574b-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="8574b-244">Les dépendances de package ne sont pas réévaluées.</span><span class="sxs-lookup"><span data-stu-id="8574b-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="8574b-245">Si NuGet détecte un changement dans les dépendances définies indiquées dans le ou les fichiers projet, il réévalue le graphe du package et met à jour le fichier de verrouillage pour refléter la nouvelle fermeture de package du projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="8574b-246">Dans CI/CD et d’autres scénarios où vous ne voulez pas changer les dépendances de package à la volée, vous pouvez définir `lockedmode` avec la valeur `true` :</span><span class="sxs-lookup"><span data-stu-id="8574b-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="8574b-247">Pour dotnet.exe, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8574b-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="8574b-248">Pour msbuild.exe, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8574b-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="8574b-249">Vous pouvez également définir cette propriété MSBuild conditionnelle dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="8574b-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="8574b-250">Si le mode verrouillé est `true`, soit la restauration restaure les packages exacts figurant dans la liste du fichier de verrouillage, soit elle échoue si vous avez mis à jour les dépendances de package définies pour le projet une fois le fichier de verrouillage créé.</span><span class="sxs-lookup"><span data-stu-id="8574b-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="8574b-251">Intégrer le fichier de verrouillage dans votre dépôt source</span><span class="sxs-lookup"><span data-stu-id="8574b-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="8574b-252">Si vous générez un exécutable d’application et que le projet en question se trouve à la début de la chaîne de dépendance, archivez le fichier de verrouillage dans le dépôt de code source pour que NuGet puisse l’utiliser durant la restauration.</span><span class="sxs-lookup"><span data-stu-id="8574b-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="8574b-253">Toutefois, si votre projet est un projet de bibliothèque que vous ne prévoyez pas de distribuer ou un projet de code commun dont dépendent d’autres projets, **n’archivez pas** le fichier de verrouillage dans le cadre de votre code source.</span><span class="sxs-lookup"><span data-stu-id="8574b-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="8574b-254">Le fait de conserver le fichier de verrouillage ne pose aucun risque. Toutefois, vous ne pouvez pas utiliser les dépendances de package verrouillées pour le projet de code commun, qui figurent dans la liste du fichier de verrouillage, durant la restauration/génération d’un projet qui dépend de ce projet de code commun.</span><span class="sxs-lookup"><span data-stu-id="8574b-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="8574b-255">par exemple</span><span class="sxs-lookup"><span data-stu-id="8574b-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="8574b-256">Si `ProjectA` a une dépendance à un `PackageX` version `2.0.0` et qu’il référence également `ProjectB` qui dépend de `PackageX` version `1.0.0`, le fichier de verrouillage pour `ProjectB` liste une dépendance à `PackageX` version `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="8574b-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="8574b-257">Toutefois, lorsque `ProjectA` est généré, son fichier de verrouillage contient une dépendance sur `PackageX` **`2.0.0`** la version **et non** `1.0.0` dans le fichier de verrouillage pour `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="8574b-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="8574b-258">Le fichier de verrouillage d’un projet de code commun a donc peu de contrôle sur les packages résolus pour les projets qui en dépendent.</span><span class="sxs-lookup"><span data-stu-id="8574b-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="8574b-259">Extensibilité du fichier de verrouillage</span><span class="sxs-lookup"><span data-stu-id="8574b-259">Lock file extensibility</span></span>

<span data-ttu-id="8574b-260">Vous pouvez contrôler divers comportements de restauration avec un fichier de verrouillage, comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8574b-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="8574b-261">Option NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="8574b-261">NuGet.exe option</span></span> | <span data-ttu-id="8574b-262">option dotnet</span><span class="sxs-lookup"><span data-stu-id="8574b-262">dotnet option</span></span> | <span data-ttu-id="8574b-263">Option MSBuild équivalente</span><span class="sxs-lookup"><span data-stu-id="8574b-263">MSBuild equivalent option</span></span> | <span data-ttu-id="8574b-264">Description</span><span class="sxs-lookup"><span data-stu-id="8574b-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="8574b-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="8574b-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="8574b-266">Opte pour l’utilisation d’un fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="8574b-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="8574b-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="8574b-267">RestoreLockedMode</span></span> | <span data-ttu-id="8574b-268">Active le mode verrouillé pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="8574b-268">Enables locked mode for restore.</span></span> <span data-ttu-id="8574b-269">Cela est utile dans les scénarios d’intégration continue et de livraison continue dans lesquels vous souhaitez créer des builds reproductibles.</span><span class="sxs-lookup"><span data-stu-id="8574b-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="8574b-270">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="8574b-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="8574b-271">Cette option est utile avec des packages dont la version flottante est définie dans le projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="8574b-272">Par défaut, NuGet Restore ne met pas à jour automatiquement la version du package lors de chaque restauration, sauf si vous exécutez Restore avec cette option.</span><span class="sxs-lookup"><span data-stu-id="8574b-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="8574b-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="8574b-273">NuGetLockFilePath</span></span> | <span data-ttu-id="8574b-274">Définit un emplacement de fichier de verrouillage personnalisé pour un projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="8574b-275">Par défaut, NuGet prend en charge `packages.lock.json` au niveau du répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="8574b-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="8574b-276">Si vous avez plusieurs projets dans le même répertoire, NuGet prend en charge le fichier de verrouillage `packages.<project_name>.lock.json` spécifique au projet.</span><span class="sxs-lookup"><span data-stu-id="8574b-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="8574b-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="8574b-277">AssetTargetFallback</span></span>

<span data-ttu-id="8574b-278">La `AssetTargetFallback` propriété vous permet de spécifier des versions de Framework compatibles supplémentaires pour les projets que votre projet référence et les packages NuGet que votre projet utilise.</span><span class="sxs-lookup"><span data-stu-id="8574b-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="8574b-279">Si vous spécifiez une dépendance de package à l’aide de `PackageReference` , mais que ce package ne contient pas les ressources qui sont compatibles avec le Framework cible de votre projet, la `AssetTargetFallback` propriété entre en lecture.</span><span class="sxs-lookup"><span data-stu-id="8574b-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="8574b-280">La compatibilité du package référencé est revérifiée à l’aide de chaque version cible de .NET Framework spécifiée dans `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="8574b-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="8574b-281">Quand un `project` ou un `package` est référencé par le biais de `AssetTargetFallback` , l’avertissement [NU1701](../reference/errors-and-warnings/NU1701.md) est déclenché.</span><span class="sxs-lookup"><span data-stu-id="8574b-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="8574b-282">Reportez-vous au tableau ci-dessous pour obtenir des exemples d' `AssetTargetFallback` impact sur la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="8574b-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="8574b-283">Infrastructure de projet</span><span class="sxs-lookup"><span data-stu-id="8574b-283">Project framework</span></span> | <span data-ttu-id="8574b-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="8574b-284">AssetTargetFallback</span></span> | <span data-ttu-id="8574b-285">Infrastructures de package</span><span class="sxs-lookup"><span data-stu-id="8574b-285">Package frameworks</span></span> | <span data-ttu-id="8574b-286">Résultats</span><span class="sxs-lookup"><span data-stu-id="8574b-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="8574b-287">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8574b-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="8574b-288">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="8574b-288">.NET Standard 2.0</span></span> | <span data-ttu-id="8574b-289">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="8574b-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="8574b-290">Application .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="8574b-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="8574b-291">.NET Standard 2,0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8574b-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="8574b-292">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="8574b-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="8574b-293">Application .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="8574b-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="8574b-294">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8574b-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="8574b-295">Incompatible, échec avec [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="8574b-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="8574b-296">Application .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="8574b-296">.NET Core App 3.1</span></span> | <span data-ttu-id="8574b-297">net472;net471</span><span class="sxs-lookup"><span data-stu-id="8574b-297">net472;net471</span></span> | <span data-ttu-id="8574b-298">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="8574b-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="8574b-299">.NET Framework 4.7.2 avec [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="8574b-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="8574b-300">Plusieurs infrastructures peuvent être spécifiées à l’aide de `;` comme délimiteur.</span><span class="sxs-lookup"><span data-stu-id="8574b-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="8574b-301">Pour ajouter une infrastructure de secours, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8574b-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="8574b-302">Vous pouvez abandonner `$(AssetTargetFallback)` si vous souhaitez remplacer les valeurs existantes au lieu de les ajouter `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="8574b-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="8574b-303">Si vous utilisez un [projet basé sur le kit de développement logiciel (SDK) .net](/dotnet/core/sdk), les `$(AssetTargetFallback)` valeurs appropriées sont configurées et vous n’avez pas besoin de les définir manuellement.</span><span class="sxs-lookup"><span data-stu-id="8574b-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="8574b-304">`$(PackageTargetFallback)` était une fonctionnalité antérieure qui tentait de résoudre ce problème, mais elle est radicalement rompue et ne *doit* pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="8574b-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="8574b-305">Pour migrer de `$(PackageTargetFallback)` vers `$(AssetTargetFallback)` , il vous suffit de modifier le nom de la propriété.</span><span class="sxs-lookup"><span data-stu-id="8574b-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
