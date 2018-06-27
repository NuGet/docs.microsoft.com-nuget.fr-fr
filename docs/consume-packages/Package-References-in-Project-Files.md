---
title: Format PackageReference NuGet (références de package dans des fichiers projet)
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817669"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="c2ce3-103">Références de package (PackageReference) dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="c2ce3-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="c2ce3-104">Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="c2ce3-105">L’utilisation de PackageReference n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.Config` (notamment les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c2ce3-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="c2ce3-106">Avec PackageReference, vous pouvez aussi utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework, configuration, plateforme ou autre type de regroupement.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="c2ce3-107">Elle permet également de mieux contrôler les dépendances et les flux de contenu.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="c2ce3-108">Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="c2ce3-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="c2ce3-109">Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="c2ce3-110">Les projets .NET Framework Full prennent en charge PackageReference, mais utilisent par défaut `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="c2ce3-111">Pour utiliser PackageReference, migrez les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="c2ce3-112">Ajout d’un PackageReference</span><span class="sxs-lookup"><span data-stu-id="c2ce3-112">Adding a PackageReference</span></span>

<span data-ttu-id="c2ce3-113">Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="c2ce3-114">Contrôle des versions des dépendances</span><span class="sxs-lookup"><span data-stu-id="c2ce3-114">Controlling dependency version</span></span>

<span data-ttu-id="c2ce3-115">Pour spécifier la version d’un package, la convention est la même que pour `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c2ce3-116">Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="c2ce3-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="c2ce3-117">Utilisation de PackageReference pour un projet sans PackageReferences</span><span class="sxs-lookup"><span data-stu-id="c2ce3-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="c2ce3-118">Avancé : Si vous n’avez aucun package installé dans un projet (aucune PackageReferences dans le fichier projet et aucun fichier packages.config), mais que vous souhaitez restaurer le projet en tant que style PackageReference, vous pouvez définir une propriété de projet RestoreProjectStyle avec la valeur PackageReference dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="c2ce3-119">Cela peut être utile si vous référencez des projets qui sont de style PackageReference (projets csproj ou de style SDK existants).</span><span class="sxs-lookup"><span data-stu-id="c2ce3-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="c2ce3-120">Cela permet aux packages auxquels ces projets font référence d’être référencés « transitivement » par votre projet.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="c2ce3-121">Versions flottantes</span><span class="sxs-lookup"><span data-stu-id="c2ce3-121">Floating Versions</span></span>

<span data-ttu-id="c2ce3-122">Les [versions flottantes](../consume-packages/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="c2ce3-123">Contrôle des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="c2ce3-123">Controlling dependency assets</span></span>

<span data-ttu-id="c2ce3-124">Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="c2ce3-125">Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c2ce3-126">Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="c2ce3-127">Balise</span><span class="sxs-lookup"><span data-stu-id="c2ce3-127">Tag</span></span> | <span data-ttu-id="c2ce3-128">Description</span><span class="sxs-lookup"><span data-stu-id="c2ce3-128">Description</span></span> | <span data-ttu-id="c2ce3-129">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="c2ce3-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2ce3-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="c2ce3-130">IncludeAssets</span></span> | <span data-ttu-id="c2ce3-131">Ces ressources sont consommées.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-131">These assets will be consumed</span></span> | <span data-ttu-id="c2ce3-132">toutes les</span><span class="sxs-lookup"><span data-stu-id="c2ce3-132">all</span></span> |
| <span data-ttu-id="c2ce3-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="c2ce3-133">ExcludeAssets</span></span> | <span data-ttu-id="c2ce3-134">Ces ressources ne sont pas consommées.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-134">These assets will not be consumed</span></span> | <span data-ttu-id="c2ce3-135">aucun</span><span class="sxs-lookup"><span data-stu-id="c2ce3-135">none</span></span> |
| <span data-ttu-id="c2ce3-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="c2ce3-136">PrivateAssets</span></span> | <span data-ttu-id="c2ce3-137">Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="c2ce3-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="c2ce3-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="c2ce3-139">Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="c2ce3-140">Value</span><span class="sxs-lookup"><span data-stu-id="c2ce3-140">Value</span></span> | <span data-ttu-id="c2ce3-141">Description</span><span class="sxs-lookup"><span data-stu-id="c2ce3-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="c2ce3-142">compile</span><span class="sxs-lookup"><span data-stu-id="c2ce3-142">compile</span></span> | <span data-ttu-id="c2ce3-143">Contenu du dossier `lib` et contrôles permettant de déterminer si votre projet peut être compilé avec les assemblys dans le dossier</span><span class="sxs-lookup"><span data-stu-id="c2ce3-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="c2ce3-144">runtime</span><span class="sxs-lookup"><span data-stu-id="c2ce3-144">runtime</span></span> | <span data-ttu-id="c2ce3-145">Contenu des dossiers `lib` et `runtimes` contrôles permettant de déterminer si ces assemblys seront copiés vers le répertoire de sortie de build</span><span class="sxs-lookup"><span data-stu-id="c2ce3-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="c2ce3-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c2ce3-146">contentFiles</span></span> | <span data-ttu-id="c2ce3-147">Contenu du dossier `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="c2ce3-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="c2ce3-148">build</span><span class="sxs-lookup"><span data-stu-id="c2ce3-148">build</span></span> | <span data-ttu-id="c2ce3-149">Propriétés et cibles du dossier `build`</span><span class="sxs-lookup"><span data-stu-id="c2ce3-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="c2ce3-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="c2ce3-150">analyzers</span></span> | <span data-ttu-id="c2ce3-151">Analyseurs .NET</span><span class="sxs-lookup"><span data-stu-id="c2ce3-151">.NET analyzers</span></span> |
| <span data-ttu-id="c2ce3-152">natifs</span><span class="sxs-lookup"><span data-stu-id="c2ce3-152">native</span></span> | <span data-ttu-id="c2ce3-153">Contenu du dossier `native`</span><span class="sxs-lookup"><span data-stu-id="c2ce3-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="c2ce3-154">aucun</span><span class="sxs-lookup"><span data-stu-id="c2ce3-154">none</span></span> | <span data-ttu-id="c2ce3-155">Aucune des valeurs ci-dessus n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-155">None of the above are used.</span></span> |
| <span data-ttu-id="c2ce3-156">toutes les</span><span class="sxs-lookup"><span data-stu-id="c2ce3-156">all</span></span> | <span data-ttu-id="c2ce3-157">Toutes les valeurs ci-dessus sont utilisées (sauf `none`)</span><span class="sxs-lookup"><span data-stu-id="c2ce3-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="c2ce3-158">Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="c2ce3-159">Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="c2ce3-160">Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="c2ce3-161">AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="c2ce3-162">Ajout d’une condition PackageReference</span><span class="sxs-lookup"><span data-stu-id="c2ce3-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="c2ce3-163">Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="c2ce3-164">Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="c2ce3-165">Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="c2ce3-166">Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="c2ce3-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="c2ce3-167">Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c2ce3-168">Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.json est inclus en tant que dépendance uniquement pour une cible `net452` :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-168">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="c2ce3-170">Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="c2ce3-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
