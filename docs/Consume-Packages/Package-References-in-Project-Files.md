---
title: Format PackageReference NuGet (références de package dans des fichiers projet) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
keywords: Dépendances de package NuGet, références de package, fichiers projet, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e1880c9b294e19ef1b71c7b17b02df8ff1cf1b73
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="6ba7c-104">Références de package (PackageReference) dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="6ba7c-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="6ba7c-105">Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="6ba7c-106">L’utilisation de PackageReference n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.Config` (notamment les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6ba7c-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6ba7c-107">Avec PackageReference, vous pouvez aussi utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework, configuration, plateforme ou autre type de regroupement.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="6ba7c-108">Elle permet également de mieux contrôler les dépendances et les flux de contenu.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="6ba7c-109">Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="6ba7c-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="6ba7c-110">Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="6ba7c-111">Les projets .NET Framework Full prennent en charge PackageReference, mais utilisent par défaut `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="6ba7c-112">Pour utiliser PackageReference, migrez les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="6ba7c-113">Ajout d’un PackageReference</span><span class="sxs-lookup"><span data-stu-id="6ba7c-113">Adding a PackageReference</span></span>

<span data-ttu-id="6ba7c-114">Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="6ba7c-115">Contrôle des versions des dépendances</span><span class="sxs-lookup"><span data-stu-id="6ba7c-115">Controlling dependency version</span></span>

<span data-ttu-id="6ba7c-116">Pour spécifier la version d’un package, la convention est la même que pour `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="6ba7c-117">Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="6ba7c-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="6ba7c-118">Versions flottantes</span><span class="sxs-lookup"><span data-stu-id="6ba7c-118">Floating Versions</span></span>

<span data-ttu-id="6ba7c-119">Les [versions flottantes](../consume-packages/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="6ba7c-120">Contrôle des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="6ba7c-120">Controlling dependency assets</span></span>

<span data-ttu-id="6ba7c-121">Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="6ba7c-122">Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="6ba7c-123">Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="6ba7c-124">Balise</span><span class="sxs-lookup"><span data-stu-id="6ba7c-124">Tag</span></span> | <span data-ttu-id="6ba7c-125">Description</span><span class="sxs-lookup"><span data-stu-id="6ba7c-125">Description</span></span> | <span data-ttu-id="6ba7c-126">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="6ba7c-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ba7c-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="6ba7c-127">IncludeAssets</span></span> | <span data-ttu-id="6ba7c-128">Ces ressources sont consommées.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-128">These assets will be consumed</span></span> | <span data-ttu-id="6ba7c-129">toutes les</span><span class="sxs-lookup"><span data-stu-id="6ba7c-129">all</span></span> |
| <span data-ttu-id="6ba7c-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="6ba7c-130">ExcludeAssets</span></span> | <span data-ttu-id="6ba7c-131">Ces ressources ne sont pas consommées.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-131">These assets will not be consumed</span></span> | <span data-ttu-id="6ba7c-132">aucun</span><span class="sxs-lookup"><span data-stu-id="6ba7c-132">none</span></span> |
| <span data-ttu-id="6ba7c-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="6ba7c-133">PrivateAssets</span></span> | <span data-ttu-id="6ba7c-134">Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="6ba7c-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="6ba7c-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="6ba7c-136">Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="6ba7c-137">Value</span><span class="sxs-lookup"><span data-stu-id="6ba7c-137">Value</span></span> | <span data-ttu-id="6ba7c-138">Description</span><span class="sxs-lookup"><span data-stu-id="6ba7c-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="6ba7c-139">compile</span><span class="sxs-lookup"><span data-stu-id="6ba7c-139">compile</span></span> | <span data-ttu-id="6ba7c-140">Contenu du dossier `lib`</span><span class="sxs-lookup"><span data-stu-id="6ba7c-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="6ba7c-141">runtime</span><span class="sxs-lookup"><span data-stu-id="6ba7c-141">runtime</span></span> | <span data-ttu-id="6ba7c-142">Contenu du dossier `runtimes`</span><span class="sxs-lookup"><span data-stu-id="6ba7c-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="6ba7c-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="6ba7c-143">contentFiles</span></span> | <span data-ttu-id="6ba7c-144">Contenu du dossier `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="6ba7c-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="6ba7c-145">build</span><span class="sxs-lookup"><span data-stu-id="6ba7c-145">build</span></span> | <span data-ttu-id="6ba7c-146">Propriétés et cibles du dossier `build`</span><span class="sxs-lookup"><span data-stu-id="6ba7c-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="6ba7c-147">analyzers</span><span class="sxs-lookup"><span data-stu-id="6ba7c-147">analyzers</span></span> | <span data-ttu-id="6ba7c-148">Analyseurs .NET</span><span class="sxs-lookup"><span data-stu-id="6ba7c-148">.NET analyzers</span></span> |
| <span data-ttu-id="6ba7c-149">natifs</span><span class="sxs-lookup"><span data-stu-id="6ba7c-149">native</span></span> | <span data-ttu-id="6ba7c-150">Contenu du dossier `native`</span><span class="sxs-lookup"><span data-stu-id="6ba7c-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="6ba7c-151">aucun</span><span class="sxs-lookup"><span data-stu-id="6ba7c-151">none</span></span> | <span data-ttu-id="6ba7c-152">Aucune des valeurs ci-dessus n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-152">None of the above are used.</span></span> |
| <span data-ttu-id="6ba7c-153">toutes les</span><span class="sxs-lookup"><span data-stu-id="6ba7c-153">all</span></span> | <span data-ttu-id="6ba7c-154">Toutes les valeurs ci-dessus sont utilisées (sauf `none`)</span><span class="sxs-lookup"><span data-stu-id="6ba7c-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="6ba7c-155">Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="6ba7c-156">Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="6ba7c-157">Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="6ba7c-158">AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="6ba7c-159">Ajout d’une condition PackageReference</span><span class="sxs-lookup"><span data-stu-id="6ba7c-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="6ba7c-160">Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="6ba7c-161">Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="6ba7c-162">Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="6ba7c-163">Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="6ba7c-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="6ba7c-164">Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="6ba7c-165">Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.json est inclus en tant que dépendance uniquement pour une cible `net452` :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="6ba7c-167">Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="6ba7c-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
