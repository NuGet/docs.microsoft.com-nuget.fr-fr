---
title: Formats des analyseurs .NET Compiler Platform pour NuGet
description: Conventions pour les analyseurs .NET qui sont empaquetés et distribués avec les packages NuGet qui implémentent une API ou une bibliothèque.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 9de890d14747a74a13a660109a3b6812a5e08acc
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237917"
---
# <a name="analyzer-nuget-formats"></a>Formats NuGet des analyseurs

.NET Compiler Platform (ou « Roslyn ») permet aux développeurs de créer des [analyseurs](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) qui examinent la sémantique et l’arborescence de syntaxe du code à mesure qu’il est écrit. Les développeurs ont ainsi un moyen de créer des outils d’analyse spécifiques au domaine, tels que ceux qui peuvent vous aider à utiliser une API ou une bibliothèque particulière. Vous trouverez plus d’informations sur le Wiki GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Consultez également l’article [Utilisez Roslyn pour développer un analyseur de code dynamique pour votre API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) dans MSDN Magazine.

Les analyseurs proprement dits sont généralement empaquetés et distribués en tant que partie des packages NuGet qui implémentent l’API ou la bibliothèque en question.

Pour obtenir un exemple intéressant, consultez le package [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), qui présente le contenu suivant :

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Comme vous pouvez le voir, vous placez les DLL de l’analyseur dans un dossier `analyzers` dans le package.

Les fichiers de propriétés, qui sont inclus pour désactiver les règles FxCop héritées au profit de l’implémentation de l’analyseur, sont placés dans le dossier `build`.

Les scripts d’installation et de désinstallation qui prennent en charge des projets avec `packages.config` sont placés dans `tools`.

Notez également que le dossier `platform` est omis, car ce package n’exige aucune plateforme en particulier.


## <a name="analyzers-path-format"></a>Format du chemin des analyseurs

L’emploi du dossier `analyzers` est similaire à celui utilisé pour les [versions cibles de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md), sauf que les spécificateurs dans le chemin décrivent des dépendances de l’hôte de développement au lieu du temps de génération. Le format général est le suivant :

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name** et **version** : la surface d’exposition *facultative* de l’API du .NET Framework que les dll contenues doivent s’exécuter. `dotnet` est actuellement la seule valeur valide, car Roslyn est le seul hôte qui peut exécuter des analyseurs. Si aucune cible n’est spécifiée, les DLL sont censées s’appliquer à *toutes* les cibles.
- **langage_pris_en_charge** : langage pour lequel la DLL s’applique, entre `cs` (C#) et `vb` (Visual Basic), et `fs` (F#). Le langage indique que l’analyseur doit être chargé uniquement pour un projet utilisant ce langage. Si aucun langage n’est spécifié, la DLL est censée s’appliquer à *tous* les langages qui prennent en charge des analyseurs.
- **nom_analyseur** : spécifie les DLL de l’analyseur. Si vous avez besoin de fichiers supplémentaires en plus des DLL, ils doivent être inclus via des fichiers de propriétés ou de cibles.


## <a name="install-and-uninstall-scripts"></a>Scripts d’installation et de désinstallation

Si le projet de l’utilisateur utilise `packages.config`, le script MSBuild qui récupère l’analyseur n’intervient pas et vous devez donc placer `install.ps1` et `uninstall.ps1` dans le dossier `tools` avec le contenu qui est décrit ci-dessous.

**contenu du fichier install.ps1**

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


**contenu du fichier uninstall.ps1**

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