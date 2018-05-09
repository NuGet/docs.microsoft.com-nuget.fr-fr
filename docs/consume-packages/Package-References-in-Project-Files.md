---
title: Format PackageReference NuGet (références de package dans des fichiers projet)
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="f9090-103">Références de package (PackageReference) dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="f9090-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="f9090-104">Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé.</span><span class="sxs-lookup"><span data-stu-id="f9090-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="f9090-105">L’utilisation de PackageReference n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.Config` (notamment les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f9090-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="f9090-106">Avec PackageReference, vous pouvez aussi utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework, configuration, plateforme ou autre type de regroupement.</span><span class="sxs-lookup"><span data-stu-id="f9090-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="f9090-107">Elle permet également de mieux contrôler les dépendances et les flux de contenu.</span><span class="sxs-lookup"><span data-stu-id="f9090-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="f9090-108">Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="f9090-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="f9090-109">Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="f9090-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="f9090-110">Les projets .NET Framework Full prennent en charge PackageReference, mais utilisent par défaut `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f9090-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="f9090-111">Pour utiliser PackageReference, migrez les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.</span><span class="sxs-lookup"><span data-stu-id="f9090-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="f9090-112">Ajout d’un PackageReference</span><span class="sxs-lookup"><span data-stu-id="f9090-112">Adding a PackageReference</span></span>

<span data-ttu-id="f9090-113">Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="f9090-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="f9090-114">Contrôle des versions des dépendances</span><span class="sxs-lookup"><span data-stu-id="f9090-114">Controlling dependency version</span></span>

<span data-ttu-id="f9090-115">Pour spécifier la version d’un package, la convention est la même que pour `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="f9090-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f9090-116">Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="f9090-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="f9090-117">Versions flottantes</span><span class="sxs-lookup"><span data-stu-id="f9090-117">Floating Versions</span></span>

<span data-ttu-id="f9090-118">Les [versions flottantes](../consume-packages/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="f9090-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="f9090-119">Contrôle des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="f9090-119">Controlling dependency assets</span></span>

<span data-ttu-id="f9090-120">Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package.</span><span class="sxs-lookup"><span data-stu-id="f9090-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="f9090-121">Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.</span><span class="sxs-lookup"><span data-stu-id="f9090-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f9090-122">Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :</span><span class="sxs-lookup"><span data-stu-id="f9090-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="f9090-123">Balise</span><span class="sxs-lookup"><span data-stu-id="f9090-123">Tag</span></span> | <span data-ttu-id="f9090-124">Description</span><span class="sxs-lookup"><span data-stu-id="f9090-124">Description</span></span> | <span data-ttu-id="f9090-125">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="f9090-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9090-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="f9090-126">IncludeAssets</span></span> | <span data-ttu-id="f9090-127">Ces ressources sont consommées.</span><span class="sxs-lookup"><span data-stu-id="f9090-127">These assets will be consumed</span></span> | <span data-ttu-id="f9090-128">toutes les</span><span class="sxs-lookup"><span data-stu-id="f9090-128">all</span></span> |
| <span data-ttu-id="f9090-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="f9090-129">ExcludeAssets</span></span> | <span data-ttu-id="f9090-130">Ces ressources ne sont pas consommées.</span><span class="sxs-lookup"><span data-stu-id="f9090-130">These assets will not be consumed</span></span> | <span data-ttu-id="f9090-131">aucun</span><span class="sxs-lookup"><span data-stu-id="f9090-131">none</span></span> |
| <span data-ttu-id="f9090-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="f9090-132">PrivateAssets</span></span> | <span data-ttu-id="f9090-133">Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="f9090-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="f9090-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="f9090-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="f9090-135">Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :</span><span class="sxs-lookup"><span data-stu-id="f9090-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="f9090-136">Value</span><span class="sxs-lookup"><span data-stu-id="f9090-136">Value</span></span> | <span data-ttu-id="f9090-137">Description</span><span class="sxs-lookup"><span data-stu-id="f9090-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="f9090-138">compile</span><span class="sxs-lookup"><span data-stu-id="f9090-138">compile</span></span> | <span data-ttu-id="f9090-139">Contenu du dossier `lib` et contrôles permettant de déterminer si votre projet peut être compilé avec les assemblys dans le dossier</span><span class="sxs-lookup"><span data-stu-id="f9090-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="f9090-140">runtime</span><span class="sxs-lookup"><span data-stu-id="f9090-140">runtime</span></span> | <span data-ttu-id="f9090-141">Contenu des dossiers `lib` et `runtimes` contrôles permettant de déterminer si ces assemblys seront copiés vers le répertoire de sortie de build</span><span class="sxs-lookup"><span data-stu-id="f9090-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="f9090-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f9090-142">contentFiles</span></span> | <span data-ttu-id="f9090-143">Contenu du dossier `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="f9090-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="f9090-144">build</span><span class="sxs-lookup"><span data-stu-id="f9090-144">build</span></span> | <span data-ttu-id="f9090-145">Propriétés et cibles du dossier `build`</span><span class="sxs-lookup"><span data-stu-id="f9090-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="f9090-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="f9090-146">analyzers</span></span> | <span data-ttu-id="f9090-147">Analyseurs .NET</span><span class="sxs-lookup"><span data-stu-id="f9090-147">.NET analyzers</span></span> |
| <span data-ttu-id="f9090-148">natifs</span><span class="sxs-lookup"><span data-stu-id="f9090-148">native</span></span> | <span data-ttu-id="f9090-149">Contenu du dossier `native`</span><span class="sxs-lookup"><span data-stu-id="f9090-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="f9090-150">aucun</span><span class="sxs-lookup"><span data-stu-id="f9090-150">none</span></span> | <span data-ttu-id="f9090-151">Aucune des valeurs ci-dessus n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="f9090-151">None of the above are used.</span></span> |
| <span data-ttu-id="f9090-152">toutes les</span><span class="sxs-lookup"><span data-stu-id="f9090-152">all</span></span> | <span data-ttu-id="f9090-153">Toutes les valeurs ci-dessus sont utilisées (sauf `none`)</span><span class="sxs-lookup"><span data-stu-id="f9090-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="f9090-154">Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="f9090-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="f9090-155">Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="f9090-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="f9090-156">Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger.</span><span class="sxs-lookup"><span data-stu-id="f9090-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="f9090-157">AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.</span><span class="sxs-lookup"><span data-stu-id="f9090-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="f9090-158">Ajout d’une condition PackageReference</span><span class="sxs-lookup"><span data-stu-id="f9090-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="f9090-159">Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="f9090-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="f9090-160">Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f9090-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="f9090-161">Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`.</span><span class="sxs-lookup"><span data-stu-id="f9090-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="f9090-162">Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="f9090-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="f9090-163">Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="f9090-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f9090-164">Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.json est inclus en tant que dépendance uniquement pour une cible `net452` :</span><span class="sxs-lookup"><span data-stu-id="f9090-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="f9090-166">Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="f9090-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
