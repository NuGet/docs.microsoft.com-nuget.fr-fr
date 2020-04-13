---
title: Créer des packages avec des assemblys COM Interop
description: Décrit comment créer des packages contenant des assemblys COM Interop
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385570"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="3f95c-103">Créer des packages NuGet contenant des assemblys COM Interop</span><span class="sxs-lookup"><span data-stu-id="3f95c-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="3f95c-104">Les packages qui contiennent des assemblys COM Interop doivent inclure un [fichier de cibles](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) approprié afin que les bonnes métadonnées `EmbedInteropTypes` soient ajoutées aux projets en utilisant le format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3f95c-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="3f95c-105">Par défaut, les métadonnées `EmbedInteropTypes` sont toujours fausses pour tous les assemblys lorsque PackageReference est utilisé, si bien que le fichier de cibles ajoute ces métadonnées explicitement.</span><span class="sxs-lookup"><span data-stu-id="3f95c-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="3f95c-106">Pour éviter les conflits, le nom de la cible doit être unique ; dans l’idéal, utilisez une combinaison du nom de votre package et de l’assembly incorporé, en remplaçant `{InteropAssemblyName}` dans l’exemple ci-dessous par cette valeur.</span><span class="sxs-lookup"><span data-stu-id="3f95c-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="3f95c-107">(Consultez également [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) pour obtenir un exemple.)</span><span class="sxs-lookup"><span data-stu-id="3f95c-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="3f95c-108">Notez que, si le format de gestion `packages.config` est utilisé, l’ajout de références aux assemblys à partir des packages amène NuGet et Visual Studio à rechercher des assemblys COM Interop et à affecter à `EmbedInteropTypes` la valeur true dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="3f95c-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="3f95c-109">Dans ce cas, les cibles sont dépassées.</span><span class="sxs-lookup"><span data-stu-id="3f95c-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="3f95c-110">De plus, [les ressources de build ne circulent pas de manière transitive](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) par défaut.</span><span class="sxs-lookup"><span data-stu-id="3f95c-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="3f95c-111">Les packages créés comme décrit ici fonctionnent différemment quand ils sont extraits en tant que dépendance transitive d’un projet vers une référence de projet.</span><span class="sxs-lookup"><span data-stu-id="3f95c-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="3f95c-112">Le consommateur du package peut les autoriser à circuler en modifiant la valeur par défaut PrivateAssets de sorte à ce qu’elle n’inclue pas de build.</span><span class="sxs-lookup"><span data-stu-id="3f95c-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>