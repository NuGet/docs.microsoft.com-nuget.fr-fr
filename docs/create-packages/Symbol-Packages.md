---
title: Guide pratique pour créer des packages de symboles NuGet
description: Comment créer des packages NuGet qui contiennent uniquement des symboles pour prendre en charge le débogage d’autres packages NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 8d2ff4d414e496d4a57755637cbbe05f4a8408e3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816889"
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="e7db8-103">Création de packages de symboles</span><span class="sxs-lookup"><span data-stu-id="e7db8-103">Creating symbol packages</span></span>

<span data-ttu-id="e7db8-104">En plus de générer des packages pour nuget.org et d’autres sources, NuGet prend en charge la création de packages de symboles associés et leur publication dans le référentiel SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="e7db8-104">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="e7db8-105">Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e7db8-105">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="e7db8-106">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="e7db8-106">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="e7db8-107">Création d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="e7db8-107">Creating a symbol package</span></span>

<span data-ttu-id="e7db8-108">Pour créer un package de symboles, respectez les conventions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7db8-108">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="e7db8-109">Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="e7db8-109">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="e7db8-110">Nommez le package de symboles `{identifier}.symbols.nupkg` et incluez la DLL de votre assembly, vos fichiers `.pdb`, vos fichiers XMLDOC, vos fichiers sources (consultez les sections qui suivent).</span><span class="sxs-lookup"><span data-stu-id="e7db8-110">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="e7db8-111">Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :</span><span class="sxs-lookup"><span data-stu-id="e7db8-111">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="e7db8-112">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="e7db8-112">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="e7db8-113">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="e7db8-113">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="e7db8-114">Structure des packages de symboles</span><span class="sxs-lookup"><span data-stu-id="e7db8-114">Symbol package structure</span></span>

<span data-ttu-id="e7db8-115">Un package de symboles peut cibler plusieurs versions cibles du .Net Framework de la même façon qu’un package de bibliothèque, si bien que la structure du dossier `lib` doit être exactement la même que celle du package principal, en incluant uniquement les fichiers `.pdb` avec la DLL.</span><span class="sxs-lookup"><span data-stu-id="e7db8-115">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="e7db8-116">Par exemple, un package de symboles ciblant le .NET 4.0 et Silverlight 4 aurait cette disposition :</span><span class="sxs-lookup"><span data-stu-id="e7db8-116">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="e7db8-117">Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source.</span><span class="sxs-lookup"><span data-stu-id="e7db8-117">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="e7db8-118">En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="e7db8-118">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="e7db8-119">Un chemin de base (préfixe de chemin commun) peut être supprimé. Par exemple, considérez une bibliothèque créée à partir de ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="e7db8-119">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="e7db8-120">À part le dossier `lib`, un package de symboles doit contenir cette disposition :</span><span class="sxs-lookup"><span data-stu-id="e7db8-120">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="e7db8-121">Référence à des fichiers dans le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="e7db8-121">Referring to files in the nuspec</span></span>

<span data-ttu-id="e7db8-122">Un package de symboles peut être généré par des conventions, à partir d’une structure de dossiers comme décrit dans la section précédente, ou en spécifiant son contenu dans la section `files` du manifeste.</span><span class="sxs-lookup"><span data-stu-id="e7db8-122">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="e7db8-123">Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="e7db8-123">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="e7db8-124">Publication d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="e7db8-124">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="e7db8-125">Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.1.0 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.</span><span class="sxs-lookup"><span data-stu-id="e7db8-125">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="e7db8-126">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../create-packages/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).</span><span class="sxs-lookup"><span data-stu-id="e7db8-126">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="e7db8-127">Après avoir publié votre package principal sur nuget.org, envoyez le package de symboles de la manière suivante, ce qui permet d’utiliser automatiquement symbolsource.org en tant que cible puisque le nom de fichier contient `.symbols` :</span><span class="sxs-lookup"><span data-stu-id="e7db8-127">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="e7db8-128">Avec nuget.exe 4.5.0 ou ultérieur, les packages de symboles ne sont pas automatiquement envoyés à symbolsource.org. Vous devez envoyer les packages de symboles séparément, comme expliqué dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="e7db8-128">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

3. <span data-ttu-id="e7db8-129">Pour publier sur un dépôt de symboles différent ou envoyer un package de symboles qui ne respecte pas les conventions de nommage, utilisez l’option `-Source` :</span><span class="sxs-lookup"><span data-stu-id="e7db8-129">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="e7db8-130">Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e7db8-130">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="e7db8-131">Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e7db8-131">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7db8-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e7db8-132">See Also</span></span>

<span data-ttu-id="e7db8-133">[Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="e7db8-133">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
