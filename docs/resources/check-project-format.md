---
title: Identifier le format du projet
description: Décrit comment identifier le format de votre projet
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843441"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="824a4-103">Identifier le format du projet</span><span class="sxs-lookup"><span data-stu-id="824a4-103">Identify the project format</span></span>

<span data-ttu-id="824a4-104">NuGet fonctionne avec tous les projets .NET.</span><span class="sxs-lookup"><span data-stu-id="824a4-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="824a4-105">Toutefois, le format de projet (de type SDK ou non SDK) détermine certains des outils et méthodes que vous devez utiliser pour consommer et créer des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="824a4-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="824a4-106">Les projets de style SDK utilisent [l’attribut SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="824a4-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="824a4-107">Il est important d’identifier votre type de projet, car les méthodes et les outils que vous utilisez pour utiliser et créer des packages NuGet dépendent du format du projet.</span><span class="sxs-lookup"><span data-stu-id="824a4-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="824a4-108">Pour les projets qui ne sont pas de type SDK, les méthodes et les outils dépendent également du fait que le projet a été migré vers le format `PackageReference` ou pas.</span><span class="sxs-lookup"><span data-stu-id="824a4-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="824a4-109">La méthode utilisée pour créer le projet détermine si votre projet est de style SDK ou pas.</span><span class="sxs-lookup"><span data-stu-id="824a4-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="824a4-110">Le tableau suivant indique le format de projet par défaut et l’outil CLI associé à votre projet lorsque vous le créez à l’aide de Visual Studio 2017 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="824a4-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="824a4-111">Projet&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="824a4-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="824a4-112">Format de projet par défaut</span><span class="sxs-lookup"><span data-stu-id="824a4-112">Default project format</span></span> | <span data-ttu-id="824a4-113">Outil CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="824a4-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="824a4-114">Notes</span><span class="sxs-lookup"><span data-stu-id="824a4-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="824a4-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="824a4-115">.NET Standard</span></span> | <span data-ttu-id="824a4-116">Style SDK</span><span class="sxs-lookup"><span data-stu-id="824a4-116">SDK-style</span></span> | [<span data-ttu-id="824a4-117">Interface CLI .NET</span><span class="sxs-lookup"><span data-stu-id="824a4-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="824a4-118">Les projets créés avant Visual Studio 2017 ne sont pas de type SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="824a4-119">Utilisez la CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="824a4-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="824a4-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="824a4-120">.NET Core</span></span> | <span data-ttu-id="824a4-121">Style SDK</span><span class="sxs-lookup"><span data-stu-id="824a4-121">SDK-style</span></span> | [<span data-ttu-id="824a4-122">Interface CLI .NET</span><span class="sxs-lookup"><span data-stu-id="824a4-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="824a4-123">Les projets créés avant Visual Studio 2017 ne sont pas de type SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="824a4-124">Utilisez la CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="824a4-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="824a4-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="824a4-125">.NET Framework</span></span> | <span data-ttu-id="824a4-126">Pas de style SDK</span><span class="sxs-lookup"><span data-stu-id="824a4-126">Non-SDK-style</span></span> | [<span data-ttu-id="824a4-127">Interface CLI de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="824a4-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="824a4-128">Les projets .NET Framework créés à l’aide d’autres méthodes peuvent être des projets de type SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="824a4-129">Pour ceux-ci, utilisez la [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli) à la place.</span><span class="sxs-lookup"><span data-stu-id="824a4-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="824a4-130">Projet .NET [migré](../reference/migrate-packages-config-to-package-reference.md)</span><span class="sxs-lookup"><span data-stu-id="824a4-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="824a4-131">Pas de style SDK</span><span class="sxs-lookup"><span data-stu-id="824a4-131">Non-SDK-style</span></span>| <span data-ttu-id="824a4-132">Pour créer des packages, utilisez [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) pour créer des packages.</span><span class="sxs-lookup"><span data-stu-id="824a4-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="824a4-133">Pour créer des packages, `msbuild -t:pack` est recommandé.</span><span class="sxs-lookup"><span data-stu-id="824a4-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="824a4-134">Sinon, utilisez la [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="824a4-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="824a4-135">Les projets migrés ne sont pas des projets de type SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="824a4-136">Vérifier le format du projet</span><span class="sxs-lookup"><span data-stu-id="824a4-136">Check the project format</span></span>

<span data-ttu-id="824a4-137">Si vous ne savez pas si le projet est au format de type SDK, recherchez l’attribut SDK dans l’élément `<Project>` du fichier projet (pour C#, il s’agit du fichier \*.csproj).</span><span class="sxs-lookup"><span data-stu-id="824a4-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="824a4-138">Si cet élément est présent, le projet est de type SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="824a4-139">Vérifier le format du projet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="824a4-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="824a4-140">Si vous travaillez dans Visual Studio, vous pouvez rapidement vérifier le format du projet à l’aide de l’une des méthodes suivantes:</span><span class="sxs-lookup"><span data-stu-id="824a4-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="824a4-141">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, puis sélectionnez **Modifier myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="824a4-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="824a4-142">Cette option n’est disponible qu’à partir de Visual Studio 2017 pour les projets qui utilisent l’attribut de style SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="824a4-143">Sinon, utilisez l’autre méthode.</span><span class="sxs-lookup"><span data-stu-id="824a4-143">Otherwise, use the other method.</span></span>

   ![Modifier le fichier projet](media/edit-project-file.png)

   <span data-ttu-id="824a4-145">Un projet de type SDK affiche [l’attribut SDK](/dotnet/core/tools/csproj#additions) dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="824a4-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="824a4-146">Dans le menu **Projet**, choisissez **Décharger le projet** (ou cliquez sur le projet avec le bouton droit et choisissez **Décharger le projet**).</span><span class="sxs-lookup"><span data-stu-id="824a4-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="824a4-147">Ce projet n’inclut pas l’attribut SDK dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="824a4-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="824a4-148">Il ne s’agit pas d’un projet de type SDK.</span><span class="sxs-lookup"><span data-stu-id="824a4-148">It is not an SDK-style project.</span></span>

   ![Décharger le projet](media/unload-project.png)

   <span data-ttu-id="824a4-150">Cliquez ensuite avec le bouton droit sur le projet déchargé et choisissez **Modifier myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="824a4-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="824a4-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="824a4-151">See also</span></span>

- [<span data-ttu-id="824a4-152">Créer des packages .NET Standard avec la CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="824a4-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="824a4-153">Créer des packages .NET Standard avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="824a4-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="824a4-154">Créer et publier un package .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="824a4-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="824a4-155">Commandes pack et restore NuGet comme cibles MSBuild</span><span class="sxs-lookup"><span data-stu-id="824a4-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
