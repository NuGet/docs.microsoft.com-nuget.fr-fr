---
title: "Guide pratique pour créer des packages de symboles NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "Comment créer des packages NuGet qui contiennent uniquement des symboles pour prendre en charge le débogage d’autres packages NuGet dans Visual Studio."
keywords: "Packages de symboles NuGet, débogage de packages NuGet, prise en charge du débogage NuGet, symboles de packages, conventions des packages de symboles"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1a29fe6e9a3dec6847dbed07761e28fb8eb9b19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="42bc8-104">Création de packages de symboles</span><span class="sxs-lookup"><span data-stu-id="42bc8-104">Creating symbol packages</span></span>

<span data-ttu-id="42bc8-105">En plus de générer des packages pour nuget.org ou d’autres sources, NuGet prend également en charge la création de packages de symboles associés et leur publication dans le [dépôt SymbolSource](http://www.symbolsource.org/Public).</span><span class="sxs-lookup"><span data-stu-id="42bc8-105">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the [SymbolSource repository](http://www.symbolsource.org/Public).</span></span>

<span data-ttu-id="42bc8-106">Les consommateurs de packages peuvent alors ajouter `http://srv.symbolsource.org/pdb/Public` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42bc8-106">Package consumers can then add `http://srv.symbolsource.org/pdb/Public` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="42bc8-107">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="42bc8-107">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>


## <a name="creating-a-symbol-package"></a><span data-ttu-id="42bc8-108">Création d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="42bc8-108">Creating a symbol package</span></span>

<span data-ttu-id="42bc8-109">Pour créer un package de symboles, respectez les conventions suivantes :</span><span class="sxs-lookup"><span data-stu-id="42bc8-109">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="42bc8-110">Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="42bc8-110">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="42bc8-111">Nommez le package de symboles `{identifier}.symbols.nupkg` et incluez la DLL de votre assembly, vos fichiers `.pdb`, vos fichiers XMLDOC, vos fichiers sources (consultez les sections qui suivent).</span><span class="sxs-lookup"><span data-stu-id="42bc8-111">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="42bc8-112">Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :</span><span class="sxs-lookup"><span data-stu-id="42bc8-112">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="42bc8-113">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="42bc8-113">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="42bc8-114">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="42bc8-114">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="42bc8-115">Structure des packages de symboles</span><span class="sxs-lookup"><span data-stu-id="42bc8-115">Symbol package structure</span></span>

<span data-ttu-id="42bc8-116">Un package de symboles peut cibler plusieurs versions cibles du .Net Framework de la même façon qu’un package de bibliothèque, si bien que la structure du dossier `lib` doit être exactement la même que celle du package principal, en incluant uniquement les fichiers `.pdb` avec la DLL.</span><span class="sxs-lookup"><span data-stu-id="42bc8-116">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="42bc8-117">Par exemple, un package de symboles ciblant le .NET 4.0 et Silverlight 4 aurait cette disposition :</span><span class="sxs-lookup"><span data-stu-id="42bc8-117">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="42bc8-118">Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source.</span><span class="sxs-lookup"><span data-stu-id="42bc8-118">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="42bc8-119">En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="42bc8-119">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="42bc8-120">Un chemin de base (préfixe de chemin commun) peut être supprimé. Par exemple, considérez une bibliothèque créée à partir de ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="42bc8-120">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="42bc8-121">À part le dossier `lib`, un package de symboles doit contenir cette disposition :</span><span class="sxs-lookup"><span data-stu-id="42bc8-121">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="42bc8-122">Référence à des fichiers dans le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="42bc8-122">Referring to files in the nuspec</span></span>

<span data-ttu-id="42bc8-123">Un package de symboles peut être généré par des conventions, à partir d’une structure de dossiers comme décrit dans la section précédente, ou en spécifiant son contenu dans la section `files` du manifeste.</span><span class="sxs-lookup"><span data-stu-id="42bc8-123">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="42bc8-124">Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="42bc8-124">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="42bc8-125">Publication d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="42bc8-125">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="42bc8-126">Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.1.0 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.</span><span class="sxs-lookup"><span data-stu-id="42bc8-126">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="42bc8-127">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../create-packages/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).</span><span class="sxs-lookup"><span data-stu-id="42bc8-127">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="42bc8-128">Après avoir publié votre package principal sur nuget.org, envoyez le package de symboles de la manière suivante, ce qui permet d’utiliser automatiquement symbolsource.org en tant que cible puisque le nom de fichier contient `.symbols` :</span><span class="sxs-lookup"><span data-stu-id="42bc8-128">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> <span data-ttu-id="42bc8-129">Avec nuget.exe 4.5.0 ou ultérieur, les packages de symboles ne sont pas automatiquement envoyés à symbolsource.org. Vous devez envoyer les packages de symboles séparément, comme expliqué dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="42bc8-129">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

1. <span data-ttu-id="42bc8-130">Pour publier sur un dépôt de symboles différent ou envoyer un package de symboles qui ne respecte pas les conventions de nommage, utilisez l’option `-Source` :</span><span class="sxs-lookup"><span data-stu-id="42bc8-130">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. <span data-ttu-id="42bc8-131">Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="42bc8-131">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="42bc8-132">Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), une fois qu’il a publié le package principal sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="42bc8-132">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="42bc8-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="42bc8-133">See Also</span></span>

 - <span data-ttu-id="42bc8-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Utilisation de SymbolSource</a> (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="42bc8-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Using SymbolSource</a> (symbolsource.org)</span></span>
