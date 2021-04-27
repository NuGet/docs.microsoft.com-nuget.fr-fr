---
title: Définir un type de package NuGet
description: Décrit les types de packages pour indiquer l’utilisation prévue d’un package.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067274"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="43c62-103">Définir un type de package NuGet</span><span class="sxs-lookup"><span data-stu-id="43c62-103">Set a NuGet package type</span></span>

<span data-ttu-id="43c62-104">Les packages peuvent être marqués avec un plus grand nombre de *types* de packages pour indiquer l’utilisation prévue.</span><span class="sxs-lookup"><span data-stu-id="43c62-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="43c62-105">Types de packages connus</span><span class="sxs-lookup"><span data-stu-id="43c62-105">Known package types</span></span>

- <span data-ttu-id="43c62-106">Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).</span><span class="sxs-lookup"><span data-stu-id="43c62-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="43c62-107">`DotnetTool` les packages de type sont des outils .NET qui peuvent être installés par l' [interface CLI dotnet](/dotnet/articles/core/tools/index).</span><span class="sxs-lookup"><span data-stu-id="43c62-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="43c62-108">`Template` les packages de type fournissent des [modèles personnalisés](/dotnet/core/tools/custom-templates) qui peuvent être utilisés pour créer des fichiers ou des projets comme une application, un service, un outil ou une bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="43c62-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="43c62-109">Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.</span><span class="sxs-lookup"><span data-stu-id="43c62-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="43c62-110">La prise en charge des types de packages a été ajoutée dans NuGet 3,5.</span><span class="sxs-lookup"><span data-stu-id="43c62-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="43c62-111">Si vous n’avez pas besoin d’un type de package personnalisé, il est préférable de *ne pas* définir explicitement le type de package.</span><span class="sxs-lookup"><span data-stu-id="43c62-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="43c62-112">La valeur par défaut de NuGet `Dependency` est le type quand aucun type n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="43c62-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="43c62-113">Types de packages personnalisés</span><span class="sxs-lookup"><span data-stu-id="43c62-113">Custom package types</span></span>

<span data-ttu-id="43c62-114">Vous pouvez marquer votre package avec un ou plusieurs types de packages personnalisés si son utilisation ne correspond pas aux [types de packages connus](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="43c62-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="43c62-115">Par exemple, imaginez que les clients de l' `Contoso` application peuvent installer des extensions.</span><span class="sxs-lookup"><span data-stu-id="43c62-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="43c62-116">L’application peut exiger que les auteurs d’extension utilisent le type de package personnalisé `ContosoExtension` pour identifier leurs packages comme des extensions appropriées qui suivent les conventions requises.</span><span class="sxs-lookup"><span data-stu-id="43c62-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="43c62-117">Un package avec un type de package personnalisé ne peut pas être installé par Visual Studio ou nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="43c62-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="43c62-118">Pour plus d’informations, consultez [NuGet/page de démarrage # 10468](https://github.com/NuGet/Home/issues/10468) .</span><span class="sxs-lookup"><span data-stu-id="43c62-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="43c62-119">Utilisation de l’interface CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="43c62-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="43c62-120">Les types de packages peuvent être définis dans le fichier projet ( `.csproj` ) :</span><span class="sxs-lookup"><span data-stu-id="43c62-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="43c62-121">Les packages avec plusieurs utilisations prévues peuvent être marqués avec plusieurs types de packages à l’aide du `;` délimiteur :</span><span class="sxs-lookup"><span data-stu-id="43c62-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="43c62-122">La gestion des versions des types de package peut se faire à l’aide d’un `,` délimiteur entre le type de package et sa [`Version`](/dotnet/api/system.version) chaîne :</span><span class="sxs-lookup"><span data-stu-id="43c62-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="43c62-123">Utilisation de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="43c62-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="43c62-124">Les types de package sont définis dans le `.nuspec` fichier au sein d’un `packageTypes\packageType` nœud sous l' `<metadata>` élément :</span><span class="sxs-lookup"><span data-stu-id="43c62-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="43c62-125">Les packages avec plusieurs utilisations prévues peuvent être marqués avec plusieurs types de packages :</span><span class="sxs-lookup"><span data-stu-id="43c62-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="43c62-126">Les types de package peuvent être avec version à l’aide d’une [`Version`](/dotnet/api/system.version) chaîne :</span><span class="sxs-lookup"><span data-stu-id="43c62-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="43c62-127">Le format d’une chaîne de type de package est exactement comme un ID de package.</span><span class="sxs-lookup"><span data-stu-id="43c62-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="43c62-128">Autrement dit, un type de package est une chaîne ne respectant pas la casse qui correspond à l’expression régulière `^\w+([_.-]\w+)*$` contenant au moins un caractère et au plus 100 caractères.</span><span class="sxs-lookup"><span data-stu-id="43c62-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="43c62-129">Si elle est fournie, la version du type de package est une [`Version`](/dotnet/api/system.version) chaîne.</span><span class="sxs-lookup"><span data-stu-id="43c62-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="43c62-130">La version du type de package est facultative et prend par défaut la valeur `0.0` .</span><span class="sxs-lookup"><span data-stu-id="43c62-130">The package type version is optional and defaults to `0.0`.</span></span>
