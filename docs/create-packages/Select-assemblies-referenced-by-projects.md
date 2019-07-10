---
title: Sélectionner des assemblys référencés par les projets
description: Mettez un sous-ensemble d’assemblys dans le package à la disposition du compilateur, alors que tous les assemblys sont disponibles au moment de l’exécution.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427474"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="44caa-103">Sélectionner des assemblys référencés par les projets</span><span class="sxs-lookup"><span data-stu-id="44caa-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="44caa-104">Avec les références d’assembly explicites, vous pouvez utiliser un sous-ensemble d’assemblys pour IntelliSense et la compilation, alors que tous les assemblys sont disponibles au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="44caa-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="44caa-105">Étant donné que `PackageReference` et `packages.config` fonctionnent différemment, les auteurs de packages doivent s’assurer de créer des packages compatibles avec les deux types de projets.</span><span class="sxs-lookup"><span data-stu-id="44caa-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="44caa-106">Les références d’assembly explicites s’appliquent aux assemblys .NET.</span><span class="sxs-lookup"><span data-stu-id="44caa-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="44caa-107">Ce n’est pas une méthode permettant de distribuer les assemblys natifs qui sont appelés (P/Invoke) par un assembly managé.</span><span class="sxs-lookup"><span data-stu-id="44caa-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="44caa-108">Prise en charge de `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="44caa-108">`PackageReference` support</span></span>

<span data-ttu-id="44caa-109">Quand un projet utilise un package avec `PackageReference` et que ce package contient un répertoire `ref\<tfm>\`, NuGet classe ces assemblys en tant que ressources de compilation, alors que les assemblys `lib\<tfm>\` sont classés en tant que ressources d’exécution.</span><span class="sxs-lookup"><span data-stu-id="44caa-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="44caa-110">Les assemblys dans `ref\<tfm>\` ne sont pas utilisés au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="44caa-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="44caa-111">Cela implique que chaque assembly dans `ref\<tfm>\` ait un assembly correspondant dans `lib\<tfm>\` ou dans un répertoire `runtime\` correspondant. Sinon, des erreurs d’exécution se produiront certainement.</span><span class="sxs-lookup"><span data-stu-id="44caa-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="44caa-112">Du fait que les assemblys dans `ref\<tfm>\` ne sont pas utilisés au moment de l’exécution, vous pouvez utiliser des [assemblys de métadonnées uniquement](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) afin de réduire la taille du package.</span><span class="sxs-lookup"><span data-stu-id="44caa-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="44caa-113">Si un package contient l’élément nuspec `<references>` (utilisé par `packages.config`, comme décrit ci-dessous) et ne contient pas d’assemblys dans `ref\<tfm>\`, NuGet publie les assemblys listés dans l’élément nuspec `<references>` à la fois comme ressources de compilation et ressources d’exécution.</span><span class="sxs-lookup"><span data-stu-id="44caa-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="44caa-114">Cela signifie qu’il y aura des exceptions de runtime si les assemblys référencés doivent charger un autre assembly dans le répertoire `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="44caa-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="44caa-115">Si le package contient un répertoire `runtime\`, NuGet n’utilise pas les ressources contenues dans le répertoire `lib\`.</span><span class="sxs-lookup"><span data-stu-id="44caa-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="44caa-116">Prise en charge de `packages.config`</span><span class="sxs-lookup"><span data-stu-id="44caa-116">`packages.config` support</span></span>

<span data-ttu-id="44caa-117">Les projets qui utilisent `packages.config` pour gérer les packages NuGet ajoutent normalement des références à tous les assemblys listés dans le répertoire `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="44caa-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="44caa-118">Le répertoire `ref\` ayant été ajouté pour prendre en charge `PackageReference`, il est ignoré quand `packages.config` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="44caa-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="44caa-119">Pour définir explicitement quels assemblys sont référencés dans les projets utilisant `packages.config`, le package doit utiliser l’[élément `<references>` dans le fichier nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="44caa-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="44caa-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="44caa-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="44caa-121">Le projet `packages.config` utilise un processus appelé [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) pour copier les assemblys dans le répertoire de sortie `bin\<configuration>\`.</span><span class="sxs-lookup"><span data-stu-id="44caa-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="44caa-122">L’assembly du projet est copié, après quoi le système de build recherche les assemblys référencés dans le manifeste de l’assembly, puis copie ces assemblys, et répète cette séquence de manière récursive pour tous les assemblys.</span><span class="sxs-lookup"><span data-stu-id="44caa-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="44caa-123">Cela signifie que si un des assemblys du répertoire `lib\<tfm>\` n’est pas référencé dans le manifeste d’aucun autre assembly en tant que dépendance (si l’assembly est chargé au moment de l’exécution avec `Assembly.Load`, MEF ou tout autre framework d’injection de dépendance), il risque de ne pas être copié dans le répertoire de sortie `bin\<configuration>\` de votre projet, même s’il est bien dans `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="44caa-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="44caa-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="44caa-124">Example</span></span>

<span data-ttu-id="44caa-125">Mon package doit contenir trois assemblys, `MyLib.dll`, `MyHelpers.dll` et `MyUtilities.dll`, qui ciblent .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="44caa-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="44caa-126">`MyUtilities.dll` contient des classes destinées à être utilisées uniquement par les deux autres assemblys. Je ne veux donc pas que ces classes soient disponibles dans IntelliSense ou au moment de la compilation pour les projets qui utilisent mon package.</span><span class="sxs-lookup"><span data-stu-id="44caa-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="44caa-127">Mon fichier `nuspec` doit contenir les éléments XML suivants :</span><span class="sxs-lookup"><span data-stu-id="44caa-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="44caa-128">Le package doit contenir ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="44caa-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
