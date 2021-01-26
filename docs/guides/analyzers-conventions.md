---
title: Formats des analyseurs .NET Compiler Platform pour NuGet
description: Conventions pour les analyseurs .NET qui sont empaquetés et distribués avec les packages NuGet qui implémentent une API ou une bibliothèque.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 63880b6b9bbfe6aac9cc6419d6a972062eea3495
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774135"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="369e0-103">Formats NuGet des analyseurs</span><span class="sxs-lookup"><span data-stu-id="369e0-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="369e0-104">.NET Compiler Platform (ou « Roslyn ») permet aux développeurs de créer des [analyseurs](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) qui examinent la sémantique et l’arborescence de syntaxe du code à mesure qu’il est écrit.</span><span class="sxs-lookup"><span data-stu-id="369e0-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="369e0-105">Les développeurs ont ainsi un moyen de créer des outils d’analyse spécifiques au domaine, tels que ceux qui peuvent vous aider à utiliser une API ou une bibliothèque particulière.</span><span class="sxs-lookup"><span data-stu-id="369e0-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="369e0-106">Vous trouverez plus d’informations sur le Wiki GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="369e0-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="369e0-107">Consultez également l’article [Utilisez Roslyn pour développer un analyseur de code dynamique pour votre API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) dans MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="369e0-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) in MSDN Magazine.</span></span>

<span data-ttu-id="369e0-108">Les analyseurs proprement dits sont généralement empaquetés et distribués en tant que partie des packages NuGet qui implémentent l’API ou la bibliothèque en question.</span><span class="sxs-lookup"><span data-stu-id="369e0-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="369e0-109">Pour obtenir un exemple intéressant, consultez le package [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), qui présente le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="369e0-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="369e0-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="369e0-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="369e0-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="369e0-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="369e0-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="369e0-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="369e0-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="369e0-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="369e0-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="369e0-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="369e0-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="369e0-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="369e0-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="369e0-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="369e0-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="369e0-117">tools\install.ps1</span></span>
- <span data-ttu-id="369e0-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="369e0-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="369e0-119">Comme vous pouvez le voir, vous placez les DLL de l’analyseur dans un dossier `analyzers` dans le package.</span><span class="sxs-lookup"><span data-stu-id="369e0-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="369e0-120">Les fichiers de propriétés, qui sont inclus pour désactiver les règles FxCop héritées au profit de l’implémentation de l’analyseur, sont placés dans le dossier `build`.</span><span class="sxs-lookup"><span data-stu-id="369e0-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="369e0-121">Les scripts d’installation et de désinstallation qui prennent en charge des projets avec `packages.config` sont placés dans `tools`.</span><span class="sxs-lookup"><span data-stu-id="369e0-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="369e0-122">Notez également que le dossier `platform` est omis, car ce package n’exige aucune plateforme en particulier.</span><span class="sxs-lookup"><span data-stu-id="369e0-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="369e0-123">Format du chemin des analyseurs</span><span class="sxs-lookup"><span data-stu-id="369e0-123">Analyzers path format</span></span>

<span data-ttu-id="369e0-124">L’emploi du dossier `analyzers` est similaire à celui utilisé pour les [versions cibles de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md), sauf que les spécificateurs dans le chemin décrivent des dépendances de l’hôte de développement au lieu du temps de génération.</span><span class="sxs-lookup"><span data-stu-id="369e0-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="369e0-125">Le format général est le suivant :</span><span class="sxs-lookup"><span data-stu-id="369e0-125">The general format is as follows:</span></span>

```
$/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll
```

- <span data-ttu-id="369e0-126">**framework_name** et **version**: la surface d’exposition *facultative* de l’API du .NET Framework que les dll contenues doivent s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="369e0-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="369e0-127">`dotnet` est actuellement la seule valeur valide, car Roslyn est le seul hôte qui peut exécuter des analyseurs.</span><span class="sxs-lookup"><span data-stu-id="369e0-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="369e0-128">Si aucune cible n’est spécifiée, les DLL sont censées s’appliquer à *toutes* les cibles.</span><span class="sxs-lookup"><span data-stu-id="369e0-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="369e0-129">**langage_pris_en_charge** : langage pour lequel la DLL s’applique, entre `cs` (C#) et `vb` (Visual Basic), et `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="369e0-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="369e0-130">Le langage indique que l’analyseur doit être chargé uniquement pour un projet utilisant ce langage.</span><span class="sxs-lookup"><span data-stu-id="369e0-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="369e0-131">Si aucun langage n’est spécifié, la DLL est censée s’appliquer à *tous* les langages qui prennent en charge des analyseurs.</span><span class="sxs-lookup"><span data-stu-id="369e0-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="369e0-132">**nom_analyseur** : spécifie les DLL de l’analyseur.</span><span class="sxs-lookup"><span data-stu-id="369e0-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="369e0-133">Si vous avez besoin de fichiers supplémentaires en plus des DLL, ils doivent être inclus via des fichiers de propriétés ou de cibles.</span><span class="sxs-lookup"><span data-stu-id="369e0-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="369e0-134">Scripts d’installation et de désinstallation</span><span class="sxs-lookup"><span data-stu-id="369e0-134">Install and uninstall scripts</span></span>

<span data-ttu-id="369e0-135">Si le projet de l’utilisateur utilise `packages.config`, le script MSBuild qui récupère l’analyseur n’intervient pas et vous devez donc placer `install.ps1` et `uninstall.ps1` dans le dossier `tools` avec le contenu qui est décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="369e0-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="369e0-136">**contenu du fichier install.ps1**</span><span class="sxs-lookup"><span data-stu-id="369e0-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="369e0-137">**contenu du fichier uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="369e0-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
