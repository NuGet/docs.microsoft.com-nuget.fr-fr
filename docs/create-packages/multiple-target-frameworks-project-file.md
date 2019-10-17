---
title: Multiciblage pour les packages NuGet dans votre fichier projet
description: Description des différentes méthodes pour cibler plusieurs versions de .NET Framework à partir d’un seul package NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380686"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="4554a-103">Prendre en charge plusieurs versions de .NET Framework dans votre fichier projet</span><span class="sxs-lookup"><span data-stu-id="4554a-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="4554a-104">Lorsque vous créez un projet, nous recommandons de créer une bibliothèque de classes .NET Standard, car elle est compatible avec la plus large gamme de projets consommateurs.</span><span class="sxs-lookup"><span data-stu-id="4554a-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="4554a-105">En utilisant .NET Standard, vous ajoutez une [prise en charge multiplateforme](/dotnet/standard/library-guidance/cross-platform-targeting) à une bibliothèque .NET par défaut.</span><span class="sxs-lookup"><span data-stu-id="4554a-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="4554a-106">Toutefois, dans certains scénarios, vous devrez peut-être également inclure du code ciblant un framework particulier.</span><span class="sxs-lookup"><span data-stu-id="4554a-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="4554a-107">Cet article vous explique comment procéder pour les projets [SDK-style](../resources/check-project-format.md).</span><span class="sxs-lookup"><span data-stu-id="4554a-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="4554a-108">Pour les projets SDK-style, vous pouvez configurer la prise en charge de plusieurs [frameworks de cibles (TFM](/dotnet/standard/frameworks)) dans votre `dotnet pack` fichier `msbuild /t:pack` projet, puis utiliser ou pour créer le package.</span><span class="sxs-lookup"><span data-stu-id="4554a-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="4554a-109">L’interface CLI nuget.exe ne prend pas en charge la compression de projets SDK-style. Vous devez donc utiliser uniquement `dotnet pack` ou `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="4554a-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="4554a-110">Nous recommandons d’[inclure toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se trouvent habituellement dans le fichier `.nuspec` du fichier projet à la place.</span><span class="sxs-lookup"><span data-stu-id="4554a-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="4554a-111">Pour cibler plusieurs versions de .NET Framework dans un projet non-SDK-style, consultez [Prise en charge de plusieurs versions de .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="4554a-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="4554a-112">Créer un projet qui prend en charge plusieurs versions de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4554a-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="4554a-113">Créez une nouvelle bibliothèque de classes .NET Standard dans Visual Studio ou utilisez `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="4554a-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="4554a-114">Nous vous recommandons de créer une bibliothèque de classes .NET Standard pour une meilleure compatibilité.</span><span class="sxs-lookup"><span data-stu-id="4554a-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="4554a-115">Modifiez le fichier *.csproj* pour prendre en charge les frameworks cibles.</span><span class="sxs-lookup"><span data-stu-id="4554a-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="4554a-116">Par exemple, changez</span><span class="sxs-lookup"><span data-stu-id="4554a-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="4554a-117">à :</span><span class="sxs-lookup"><span data-stu-id="4554a-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="4554a-118">Veillez à modifier l’élément XML mis au pluriel (ajoutez des «s» aux balises d’ouverture et de fermeture).</span><span class="sxs-lookup"><span data-stu-id="4554a-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="4554a-119">Si vous avez du code qui ne fonctionne que dans un TFM, vous pouvez utiliser `#if NET45` ou `#if NETSTANDARD2_0` pour séparer du code dépendant du TFM.</span><span class="sxs-lookup"><span data-stu-id="4554a-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="4554a-120">(Pour plus d’informations, consultez [la rubrique Comment effectuer une MULTICIBLAGE](/dotnet/core/tutorials/libraries#how-to-multitarget).) Par exemple, vous pouvez utiliser le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4554a-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="4554a-121">Ajoutez toutes les métadonnées NuGet que vous souhaitez au fichier *.csproj* en tant que propriétés MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4554a-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="4554a-122">Pour obtenir la liste des métadonnées de package disponibles et les noms de propriétés MSBuild, consultez [Pack Target](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="4554a-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="4554a-123">Consultez également [Contrôle des ressources de dépendance](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="4554a-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="4554a-124">Si vous souhaitez séparer les propriétés liées à la création de builds des métadonnées NuGet, vous pouvez utiliser un `PropertyGroup` différent, ou placer les propriétés NuGet dans un autre fichier et utiliser la directive `Import` de MSBuild pour l’inclure.</span><span class="sxs-lookup"><span data-stu-id="4554a-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="4554a-125">À compter de MSBuild 15.0, `Directory.Build.Props` et `Directory.Build.Targets` sont également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4554a-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="4554a-126">À présent, utilisez `dotnet pack` et les cibles *.nupkg*. qui en résultent, .NET standard 2.0 et .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4554a-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="4554a-127">Voici le fichier *.csproj* généré à l’aide des étapes précédentes et de .NET Core SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="4554a-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="4554a-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4554a-128">See also</span></span>

* [<span data-ttu-id="4554a-129">Guide pratique pour spécifier des frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="4554a-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="4554a-130">Ciblage multiplateforme</span><span class="sxs-lookup"><span data-stu-id="4554a-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
