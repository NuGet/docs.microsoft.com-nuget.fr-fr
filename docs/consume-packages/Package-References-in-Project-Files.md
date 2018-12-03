---
title: Format PackageReference NuGet (références de package dans des fichiers projet)
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: d4f0177183ee3edf595c4ce10d1f26cbaca5755d
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453570"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="2e5d1-103">Références de package (PackageReference) dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="2e5d1-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="2e5d1-104">Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="2e5d1-105">L’utilisation de PackageReference n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.config` (notamment les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2e5d1-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="2e5d1-106">Avec PackageReference, vous pouvez aussi utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework, configuration, plateforme ou autre type de regroupement.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="2e5d1-107">Elle permet également de mieux contrôler les dépendances et les flux de contenu.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="2e5d1-108">Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="2e5d1-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="2e5d1-109">Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="2e5d1-110">Les projets .NET Framework prennent en charge PackageReference, mais utilisent par défaut `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="2e5d1-111">Pour utiliser PackageReference, migrez les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="2e5d1-112">Ajout d’un PackageReference</span><span class="sxs-lookup"><span data-stu-id="2e5d1-112">Adding a PackageReference</span></span>

<span data-ttu-id="2e5d1-113">Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="2e5d1-114">Contrôle des versions des dépendances</span><span class="sxs-lookup"><span data-stu-id="2e5d1-114">Controlling dependency version</span></span>

<span data-ttu-id="2e5d1-115">Pour spécifier la version d’un package, la convention est la même que pour `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2e5d1-116">Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="2e5d1-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="2e5d1-117">Utilisation de PackageReference pour un projet sans PackageReferences</span><span class="sxs-lookup"><span data-stu-id="2e5d1-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="2e5d1-118">Avancé : Si vous n’avez aucun package installé dans un projet (aucune PackageReferences dans le fichier projet et aucun fichier packages.config), mais que vous souhaitez restaurer le projet en tant que style PackageReference, vous pouvez définir une propriété de projet RestoreProjectStyle avec la valeur PackageReference dans votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="2e5d1-119">Cela peut être utile si vous référencez des projets qui sont de style PackageReference (projets csproj ou de style SDK existants).</span><span class="sxs-lookup"><span data-stu-id="2e5d1-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="2e5d1-120">Cela permet aux packages auxquels ces projets font référence d’être référencés « transitivement » par votre projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="2e5d1-121">Versions flottantes</span><span class="sxs-lookup"><span data-stu-id="2e5d1-121">Floating Versions</span></span>

<span data-ttu-id="2e5d1-122">Les [versions flottantes](../consume-packages/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="2e5d1-123">Contrôle des ressources de dépendance</span><span class="sxs-lookup"><span data-stu-id="2e5d1-123">Controlling dependency assets</span></span>

<span data-ttu-id="2e5d1-124">Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="2e5d1-125">Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2e5d1-126">Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="2e5d1-127">Balise</span><span class="sxs-lookup"><span data-stu-id="2e5d1-127">Tag</span></span> | <span data-ttu-id="2e5d1-128">Description</span><span class="sxs-lookup"><span data-stu-id="2e5d1-128">Description</span></span> | <span data-ttu-id="2e5d1-129">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="2e5d1-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e5d1-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="2e5d1-130">IncludeAssets</span></span> | <span data-ttu-id="2e5d1-131">Ces ressources sont consommées.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-131">These assets will be consumed</span></span> | <span data-ttu-id="2e5d1-132">all</span><span class="sxs-lookup"><span data-stu-id="2e5d1-132">all</span></span> |
| <span data-ttu-id="2e5d1-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="2e5d1-133">ExcludeAssets</span></span> | <span data-ttu-id="2e5d1-134">Ces ressources ne sont pas consommées.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-134">These assets will not be consumed</span></span> | <span data-ttu-id="2e5d1-135">none</span><span class="sxs-lookup"><span data-stu-id="2e5d1-135">none</span></span> |
| <span data-ttu-id="2e5d1-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="2e5d1-136">PrivateAssets</span></span> | <span data-ttu-id="2e5d1-137">Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="2e5d1-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="2e5d1-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="2e5d1-139">Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="2e5d1-140">Value</span><span class="sxs-lookup"><span data-stu-id="2e5d1-140">Value</span></span> | <span data-ttu-id="2e5d1-141">Description</span><span class="sxs-lookup"><span data-stu-id="2e5d1-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="2e5d1-142">compile</span><span class="sxs-lookup"><span data-stu-id="2e5d1-142">compile</span></span> | <span data-ttu-id="2e5d1-143">Contenu du dossier `lib` et contrôles permettant de déterminer si votre projet peut être compilé avec les assemblys dans le dossier</span><span class="sxs-lookup"><span data-stu-id="2e5d1-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="2e5d1-144">runtime</span><span class="sxs-lookup"><span data-stu-id="2e5d1-144">runtime</span></span> | <span data-ttu-id="2e5d1-145">Contenu des dossiers `lib` et `runtimes` contrôles permettant de déterminer si ces assemblys seront copiés vers le répertoire de sortie de build</span><span class="sxs-lookup"><span data-stu-id="2e5d1-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="2e5d1-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="2e5d1-146">contentFiles</span></span> | <span data-ttu-id="2e5d1-147">Contenu du dossier `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="2e5d1-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="2e5d1-148">build</span><span class="sxs-lookup"><span data-stu-id="2e5d1-148">build</span></span> | <span data-ttu-id="2e5d1-149">Propriétés et cibles du dossier `build`</span><span class="sxs-lookup"><span data-stu-id="2e5d1-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="2e5d1-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="2e5d1-150">analyzers</span></span> | <span data-ttu-id="2e5d1-151">Analyseurs .NET</span><span class="sxs-lookup"><span data-stu-id="2e5d1-151">.NET analyzers</span></span> |
| <span data-ttu-id="2e5d1-152">native</span><span class="sxs-lookup"><span data-stu-id="2e5d1-152">native</span></span> | <span data-ttu-id="2e5d1-153">Contenu du dossier `native`</span><span class="sxs-lookup"><span data-stu-id="2e5d1-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="2e5d1-154">none</span><span class="sxs-lookup"><span data-stu-id="2e5d1-154">none</span></span> | <span data-ttu-id="2e5d1-155">Aucune des valeurs ci-dessus n’est utilisée.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-155">None of the above are used.</span></span> |
| <span data-ttu-id="2e5d1-156">all</span><span class="sxs-lookup"><span data-stu-id="2e5d1-156">all</span></span> | <span data-ttu-id="2e5d1-157">Toutes les valeurs ci-dessus sont utilisées (sauf `none`)</span><span class="sxs-lookup"><span data-stu-id="2e5d1-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="2e5d1-158">Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="2e5d1-159">Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="2e5d1-160">Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="2e5d1-161">AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="2e5d1-162">Ajout d’une condition PackageReference</span><span class="sxs-lookup"><span data-stu-id="2e5d1-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="2e5d1-163">Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="2e5d1-164">Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="2e5d1-165">Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="2e5d1-166">Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="2e5d1-167">Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2e5d1-168">Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.Json est inclus en tant que dépendance uniquement pour une cible `net452` :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="2e5d1-170">Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="2e5d1-171">Verrouillage des dépendances</span><span class="sxs-lookup"><span data-stu-id="2e5d1-171">Locking dependencies</span></span>
<span data-ttu-id="2e5d1-172">*Cette fonctionnalité est disponible avec NuGet **4.9** ou ultérieur, et avec Visual Studio 2017 **15.9 Preview 5** ou ultérieur.*</span><span class="sxs-lookup"><span data-stu-id="2e5d1-172">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9 Preview 5** or above.*</span></span>

<span data-ttu-id="2e5d1-173">L’entrée de la restauration NuGet est un ensemble de références de package provenant du fichier de projet (dépendances de niveau supérieur ou directes). La sortie est une fermeture complète de toutes les dépendances de package, notamment les dépendances transitives.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-173">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="2e5d1-174">NuGet s’efforce toujours de produire la même fermeture complète des dépendances de package si la liste PackageReference d’entrée ne change pas.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-174">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="2e5d1-175">Toutefois, tous les scénarios ne s’y prêtent pas.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-175">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="2e5d1-176">Exemple :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-176">For example:</span></span>

* <span data-ttu-id="2e5d1-177">Quand vous utilisez des versions flottantes comme `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-177">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="2e5d1-178">L’intention ici est de flotter vers la dernière version à chaque restauration de package. Mais dans certains scénarios, les utilisateurs peuvent exiger le verrouillage du graphe à une version récente donnée et son flottement vers une version ultérieure, si celle-ci est disponible, à la suite d’un mouvement explicite.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-178">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="2e5d1-179">Une version plus récente du package correspondant aux exigences de version de PackageReference est publiée.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-179">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="2e5d1-180">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="2e5d1-180">E.g.</span></span> 

  * <span data-ttu-id="2e5d1-181">Premier jour : Vous spécifiez `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, mais les versions disponibles sur les dépôts NuGet sont 4.1.0, 4.2.0 et 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-181">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="2e5d1-182">Dans ce cas, NuGet résout la version en 4.1.0 (la plus proche de la version minimale).</span><span class="sxs-lookup"><span data-stu-id="2e5d1-182">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="2e5d1-183">Deuxième jour : La version 4.0.0 est publiée.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-183">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="2e5d1-184">NuGet trouve désormais la correspondance exacte et commence à résoudre la version en 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-184">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="2e5d1-185">Une version de package donnée est supprimée du dépôt.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-185">A given package version is removed from the repository.</span></span> <span data-ttu-id="2e5d1-186">Bien que nuget.org n’autorise pas la suppression de packages, d’autres dépôts de packages n’ont pas cette contrainte.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-186">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="2e5d1-187">NuGet trouve donc la meilleure correspondance quand la version supprimée rend impossible la résolution.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-187">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="2e5d1-188">Activation du fichier de verrouillage</span><span class="sxs-lookup"><span data-stu-id="2e5d1-188">Enabling lock file</span></span>
<span data-ttu-id="2e5d1-189">Pour rendre persistante la fermeture complète des dépendances de package, vous pouvez choisir d’utiliser la fonctionnalité de fichier de verrouillage en définissant la propriété MSBuild `RestorePackagesWithLockFile` pour votre projet :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-189">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="2e5d1-190">Si cette propriété est définie, la restauration NuGet génère un fichier de verrouillage (`packages.lock.json`) au niveau du répertoire racine du projet qui liste toutes les dépendances du package.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-190">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="2e5d1-191">Quand un projet a un fichier `packages.lock.json` dans son répertoire racine, le fichier de verrouillage est toujours utilisé avec la restauration, même si la propriété `RestorePackagesWithLockFile` n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-191">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="2e5d1-192">Une autre façon de choisir cette fonctionnalité consiste à créer un fichier `packages.lock.json` vide factice dans le répertoire racine du projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-192">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="2e5d1-193">Comportement de `restore` avec fichier de verrouillage</span><span class="sxs-lookup"><span data-stu-id="2e5d1-193">`restore` behavior with lock file</span></span>
<span data-ttu-id="2e5d1-194">Si un fichier de verrouillage est présent pour le projet, NuGet utilise ce fichier de verrouillage pour exécuter `restore`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-194">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="2e5d1-195">NuGet effectue une vérification rapide pour voir si les dépendances de package ont changé, comme indiqué dans le fichier projet (ou les fichiers des projets dépendants). Si aucun changement n’est détecté, il restaure simplement les packages mentionnés dans le fichier de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-195">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="2e5d1-196">Les dépendances de package ne sont pas réévaluées.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-196">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="2e5d1-197">Si NuGet détecte un changement dans les dépendances définies indiquées dans le ou les fichiers projet, il réévalue le graphe du package et met à jour le fichier de verrouillage pour refléter la nouvelle fermeture de package du projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-197">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="2e5d1-198">Dans CI/CD et d’autres scénarios où vous ne voulez pas changer les dépendances de package à la volée, vous pouvez définir `lockedmode` avec la valeur `true` :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-198">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="2e5d1-199">Pour dotnet.exe, exécutez :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-199">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="2e5d1-200">Pour msbuild.exe, exécutez :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-200">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="2e5d1-201">Vous pouvez également définir cette propriété MSBuild conditionnelle dans votre fichier projet :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-201">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="2e5d1-202">Si le mode verrouillé est `true`, soit la restauration restaure les packages exacts figurant dans la liste du fichier de verrouillage, soit elle échoue si vous avez mis à jour les dépendances de package définies pour le projet une fois le fichier de verrouillage créé.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-202">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="2e5d1-203">Intégrer le fichier de verrouillage dans votre dépôt source</span><span class="sxs-lookup"><span data-stu-id="2e5d1-203">Make lock file part of your source repository</span></span>
<span data-ttu-id="2e5d1-204">Si vous générez un exécutable d’application et que le projet en question se trouve à la fin de la chaîne de dépendance, archivez le fichier de verrouillage dans le dépôt de code source pour que NuGet puisse l’utiliser durant la restauration.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-204">If you are building an application, an executable and the project in question is at the end of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="2e5d1-205">Toutefois, si votre projet est un projet de bibliothèque que vous ne prévoyez pas de distribuer ou un projet de code commun dont dépendent d’autres projets, **n’archivez pas** le fichier de verrouillage dans le cadre de votre code source.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-205">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="2e5d1-206">Le fait de conserver le fichier de verrouillage ne pose aucun risque. Toutefois, vous ne pouvez pas utiliser les dépendances de package verrouillées pour le projet de code commun, qui figurent dans la liste du fichier de verrouillage, durant la restauration/génération d’un projet qui dépend de ce projet de code commun.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-206">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="2e5d1-207">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-207">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="2e5d1-208">Si `ProjectA` a une dépendance à un `PackageX` version `2.0.0` et qu’il référence également `ProjectB` qui dépend de `PackageX` version `1.0.0`, le fichier de verrouillage pour `ProjectB` liste une dépendance à `PackageX` version `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-208">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="2e5d1-209">Toutefois, quand `ProjectA` est généré, son fichier de verrouillage contient une dépendance à `PackageX` version **`2.0.0`** et **non à** `1.0.0` (qui figure dans la liste du fichier de verrouillage pour `ProjectB`).</span><span class="sxs-lookup"><span data-stu-id="2e5d1-209">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="2e5d1-210">Le fichier de verrouillage d’un projet de code commun a donc peu de contrôle sur les packages résolus pour les projets qui en dépendent.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-210">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="2e5d1-211">Extensibilité du fichier de verrouillage</span><span class="sxs-lookup"><span data-stu-id="2e5d1-211">Lock file extensibility</span></span>
<span data-ttu-id="2e5d1-212">Vous pouvez contrôler divers comportements de restauration avec un fichier de verrouillage, comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2e5d1-212">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="2e5d1-213">Option</span><span class="sxs-lookup"><span data-stu-id="2e5d1-213">Option</span></span> | <span data-ttu-id="2e5d1-214">Option MSBuild équivalente</span><span class="sxs-lookup"><span data-stu-id="2e5d1-214">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="2e5d1-215">Utilisation par les démarrages d’un fichier de verrouillage pour un projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-215">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="2e5d1-216">Vous pouvez également définir la propriété `RestorePackagesWithLockFile` dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-216">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="2e5d1-217">Active le mode verrouillé pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-217">Enables locked mode for restore.</span></span> <span data-ttu-id="2e5d1-218">Ceci est utile dans les scénarios CI/CD dans lesquels vous souhaitez obtenir les builds renouvelables.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-218">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="2e5d1-219">Vous pouvez obtenir le même résultat en définissant la propriété MSBuild `RestoreLockedMode` avec la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-219">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="2e5d1-220">Cette option est utile avec des packages dont la version flottante est définie dans le projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-220">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="2e5d1-221">Par défaut, la restauration NuGet ne met pas automatiquement à jour la version du package à chaque restauration, sauf si vous exécutez la restauration avec l’option `--force-evaluate`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-221">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="2e5d1-222">Définit un emplacement de fichier de verrouillage personnalisé pour un projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-222">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="2e5d1-223">Vous pouvez obtenir le même résultat en définissant la propriété MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-223">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="2e5d1-224">Par défaut, NuGet prend en charge `packages.lock.json` au niveau du répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-224">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="2e5d1-225">Si vous avez plusieurs projets dans le même répertoire, NuGet prend en charge le fichier de verrouillage `packages.<project_name>.lock.json` spécifique au projet.</span><span class="sxs-lookup"><span data-stu-id="2e5d1-225">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
