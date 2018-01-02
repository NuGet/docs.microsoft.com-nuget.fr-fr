---
title: "Références de package (PackageReference) NuGet dans les fichiers projet Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Informations détaillées sur les références de package (PackageReference) NuGet dans les fichiers projet pris en charge par NuGet 4.0+ et Visual Studio 2017"
keywords: "Dépendances de package NuGet, références de package, fichiers projet, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="c8c61-104">Références de package (PackageReference) dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="c8c61-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="c8c61-105">En utilisant le nœud `PackageReference`, les références de package permettent de gérer les dépendances NuGet directement dans les fichiers projet, ce qui évite d’avoir à utiliser un fichier `packages.config` ou `project.json` séparé.</span><span class="sxs-lookup"><span data-stu-id="c8c61-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="c8c61-106">Cette méthode n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.Config` (y compris les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c8c61-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="c8c61-107">Actuellement, les références de package sont prises en charge uniquement dans Visual Studio 2017 pour les projets .NET Core, .NET Standard et UWP qui ciblent Windows 10 build 15063 (Creators Update).</span><span class="sxs-lookup"><span data-stu-id="c8c61-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="c8c61-108">L’approche `PackageReference` vous permet d’utiliser des conditions MSBuild pour choisir des références de package par version cible du .NET Framework, par configuration, par plateforme ou autre type de regroupement.</span><span class="sxs-lookup"><span data-stu-id="c8c61-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="c8c61-109">Elle permet également de mieux contrôler les dépendances et les flux de contenu.</span><span class="sxs-lookup"><span data-stu-id="c8c61-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="c8c61-110">Au niveau du comportement et de la [résolution des dépendances](Dependency-Resolution.md), cela revient à utiliser `project.json`.</span><span class="sxs-lookup"><span data-stu-id="c8c61-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it is the same as using `project.json`.</span></span>

<span data-ttu-id="c8c61-111">Pour plus d’informations sur l’intégration de MSBuild aux références de package des fichiers projet, consultez [Commandes pack et restore NuGet en tant que cibles MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="c8c61-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="c8c61-112">Ajout d’un PackageReference</span><span class="sxs-lookup"><span data-stu-id="c8c61-112">Adding a PackageReference</span></span>

<span data-ttu-id="c8c61-113">Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="c8c61-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="c8c61-114">Contrôle des versions des dépendances</span><span class="sxs-lookup"><span data-stu-id="c8c61-114">Controlling dependency version</span></span>

<span data-ttu-id="c8c61-115">Pour spécifier la version d’un package, la convention est la même que celle utilisée pour `packages.config` ou `project.json` :</span><span class="sxs-lookup"><span data-stu-id="c8c61-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c8c61-116">Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="c8c61-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="c8c61-117">Versions flottantes</span><span class="sxs-lookup"><span data-stu-id="c8c61-117">Floating Versions</span></span>

<span data-ttu-id="c8c61-118">Les [versions flottantes](../consume-packages/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="c8c61-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="c8c61-119">Contrôle des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="c8c61-119">Controlling dependency assets</span></span>

<span data-ttu-id="c8c61-120">Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package.</span><span class="sxs-lookup"><span data-stu-id="c8c61-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="c8c61-121">Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.</span><span class="sxs-lookup"><span data-stu-id="c8c61-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c8c61-122">Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :</span><span class="sxs-lookup"><span data-stu-id="c8c61-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="c8c61-123">Balise</span><span class="sxs-lookup"><span data-stu-id="c8c61-123">Tag</span></span> | <span data-ttu-id="c8c61-124">Description</span><span class="sxs-lookup"><span data-stu-id="c8c61-124">Description</span></span> | <span data-ttu-id="c8c61-125">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="c8c61-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8c61-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="c8c61-126">IncludeAssets</span></span> | <span data-ttu-id="c8c61-127">Ces ressources sont consommées.</span><span class="sxs-lookup"><span data-stu-id="c8c61-127">These assets will be consumed</span></span> | <span data-ttu-id="c8c61-128">all</span><span class="sxs-lookup"><span data-stu-id="c8c61-128">all</span></span> |
| <span data-ttu-id="c8c61-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="c8c61-129">ExcludeAssets</span></span> | <span data-ttu-id="c8c61-130">Ces ressources ne sont pas consommées.</span><span class="sxs-lookup"><span data-stu-id="c8c61-130">These assets will not be consumed</span></span> | <span data-ttu-id="c8c61-131">none</span><span class="sxs-lookup"><span data-stu-id="c8c61-131">none</span></span> | 
| <span data-ttu-id="c8c61-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="c8c61-132">PrivateAssets</span></span> | <span data-ttu-id="c8c61-133">Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="c8c61-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="c8c61-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="c8c61-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="c8c61-135">Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :</span><span class="sxs-lookup"><span data-stu-id="c8c61-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="c8c61-136">Valeur</span><span class="sxs-lookup"><span data-stu-id="c8c61-136">Value</span></span> | <span data-ttu-id="c8c61-137">Description</span><span class="sxs-lookup"><span data-stu-id="c8c61-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="c8c61-138">compile</span><span class="sxs-lookup"><span data-stu-id="c8c61-138">compile</span></span> | <span data-ttu-id="c8c61-139">Contenu du dossier `lib`</span><span class="sxs-lookup"><span data-stu-id="c8c61-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="c8c61-140">runtime</span><span class="sxs-lookup"><span data-stu-id="c8c61-140">runtime</span></span> | <span data-ttu-id="c8c61-141">Contenu du dossier `runtime`</span><span class="sxs-lookup"><span data-stu-id="c8c61-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="c8c61-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c8c61-142">contentFiles</span></span> | <span data-ttu-id="c8c61-143">Contenu du dossier `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="c8c61-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="c8c61-144">build</span><span class="sxs-lookup"><span data-stu-id="c8c61-144">build</span></span> | <span data-ttu-id="c8c61-145">Propriétés et cibles du dossier `build`</span><span class="sxs-lookup"><span data-stu-id="c8c61-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="c8c61-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="c8c61-146">analyzers</span></span> | <span data-ttu-id="c8c61-147">Analyseurs .NET</span><span class="sxs-lookup"><span data-stu-id="c8c61-147">.NET analyzers</span></span> |
| <span data-ttu-id="c8c61-148">native</span><span class="sxs-lookup"><span data-stu-id="c8c61-148">native</span></span> | <span data-ttu-id="c8c61-149">Contenu du dossier `native`</span><span class="sxs-lookup"><span data-stu-id="c8c61-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="c8c61-150">none</span><span class="sxs-lookup"><span data-stu-id="c8c61-150">none</span></span> | <span data-ttu-id="c8c61-151">Aucune des valeurs ci-dessus n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="c8c61-151">None of the above are used.</span></span> |
| <span data-ttu-id="c8c61-152">all</span><span class="sxs-lookup"><span data-stu-id="c8c61-152">all</span></span> | <span data-ttu-id="c8c61-153">Toutes les valeurs ci-dessus sont utilisées (sauf `none`)</span><span class="sxs-lookup"><span data-stu-id="c8c61-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="c8c61-154">Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="c8c61-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="c8c61-155">Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="c8c61-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="c8c61-156">Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger.</span><span class="sxs-lookup"><span data-stu-id="c8c61-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="c8c61-157">AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.</span><span class="sxs-lookup"><span data-stu-id="c8c61-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="c8c61-158">Ajout d’une condition PackageReference</span><span class="sxs-lookup"><span data-stu-id="c8c61-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="c8c61-159">Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="c8c61-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="c8c61-160">Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c8c61-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="c8c61-161">Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`.</span><span class="sxs-lookup"><span data-stu-id="c8c61-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="c8c61-162">Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="c8c61-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="c8c61-163">Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="c8c61-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c8c61-164">Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.json est inclus en tant que dépendance uniquement pour une cible `net452` :</span><span class="sxs-lookup"><span data-stu-id="c8c61-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="c8c61-166">Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="c8c61-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
