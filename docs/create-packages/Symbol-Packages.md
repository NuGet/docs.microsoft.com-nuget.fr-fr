---
title: Guide pratique pour créer des packages de symboles NuGet
description: Comment créer des packages NuGet qui contiennent uniquement des symboles pour prendre en charge le débogage d’autres packages NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3321cba9082eb35b53ba693e246db18e5d8e187b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580257"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="62037-103">Création de packages de symboles (hérité)</span><span class="sxs-lookup"><span data-stu-id="62037-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="62037-104">Le nouveau format recommandé pour les packages de symboles est .snupkg.</span><span class="sxs-lookup"><span data-stu-id="62037-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="62037-105">Consultez [Création de packages de symboles (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="62037-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="62037-106">.symbols.nupkg est toujours pris en charge, mais uniquement pour des raisons de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="62037-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="62037-107">En plus de générer des packages pour nuget.org et d’autres sources, NuGet prend en charge la création de packages de symboles associés et leur publication dans le référentiel SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="62037-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="62037-108">Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62037-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="62037-109">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="62037-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="62037-110">Création d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="62037-110">Creating a symbol package</span></span>

<span data-ttu-id="62037-111">Pour créer un package de symboles, respectez les conventions suivantes :</span><span class="sxs-lookup"><span data-stu-id="62037-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="62037-112">Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="62037-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="62037-113">Nommez le package de symboles `{identifier}.symbols.nupkg` et incluez la DLL de votre assembly, vos fichiers `.pdb`, vos fichiers XMLDOC, vos fichiers sources (consultez les sections qui suivent).</span><span class="sxs-lookup"><span data-stu-id="62037-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="62037-114">Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :</span><span class="sxs-lookup"><span data-stu-id="62037-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="62037-115">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="62037-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="62037-116">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="62037-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="62037-117">Structure des packages de symboles</span><span class="sxs-lookup"><span data-stu-id="62037-117">Symbol package structure</span></span>

<span data-ttu-id="62037-118">Un package de symboles peut cibler plusieurs versions cibles du .Net Framework de la même façon qu’un package de bibliothèque, si bien que la structure du dossier `lib` doit être exactement la même que celle du package principal, en incluant uniquement les fichiers `.pdb` avec la DLL.</span><span class="sxs-lookup"><span data-stu-id="62037-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="62037-119">Par exemple, un package de symboles ciblant le .NET 4.0 et Silverlight 4 aurait cette disposition :</span><span class="sxs-lookup"><span data-stu-id="62037-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="62037-120">Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source.</span><span class="sxs-lookup"><span data-stu-id="62037-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="62037-121">En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="62037-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="62037-122">Un chemin de base (préfixe de chemin commun) peut être supprimé. Par exemple, considérez une bibliothèque créée à partir de ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="62037-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="62037-123">À part le dossier `lib`, un package de symboles doit contenir cette disposition :</span><span class="sxs-lookup"><span data-stu-id="62037-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="62037-124">Référence à des fichiers dans le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="62037-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="62037-125">Un package de symboles peut être généré par des conventions, à partir d’une structure de dossiers comme décrit dans la section précédente, ou en spécifiant son contenu dans la section `files` du manifeste.</span><span class="sxs-lookup"><span data-stu-id="62037-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="62037-126">Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="62037-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="62037-127">Publication d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="62037-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="62037-128">Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.1.0 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.</span><span class="sxs-lookup"><span data-stu-id="62037-128">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="62037-129">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../create-packages/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).</span><span class="sxs-lookup"><span data-stu-id="62037-129">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="62037-130">Après avoir publié votre package principal sur nuget.org, envoyez le package de symboles de la manière suivante, ce qui permet d’utiliser automatiquement symbolsource.org en tant que cible puisque le nom de fichier contient `.symbols` :</span><span class="sxs-lookup"><span data-stu-id="62037-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="62037-131">Pour publier sur un dépôt de symboles différent ou envoyer un package de symboles qui ne respecte pas les conventions de nommage, utilisez l’option `-Source` :</span><span class="sxs-lookup"><span data-stu-id="62037-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="62037-132">Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="62037-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="62037-133">Avec nuget.exe 4.5.0 ou ultérieur, les packages de symboles ne sont pas automatiquement envoyés à symbolsource.org. Vous devez envoyer les packages de symboles séparément, comme expliqué dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="62037-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="62037-134">Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62037-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="62037-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="62037-135">See Also</span></span>

<span data-ttu-id="62037-136">[Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="62037-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
