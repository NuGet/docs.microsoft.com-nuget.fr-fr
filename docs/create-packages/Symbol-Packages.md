---
title: Création de packages de symboles hérités (. Symbols. nupkg)
description: Comment créer des packages NuGet qui contiennent uniquement des symboles pour prendre en charge le débogage d’autres packages NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476267"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="4b992-103">Création de packages de symboles hérités (. Symbols. nupkg)</span><span class="sxs-lookup"><span data-stu-id="4b992-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="4b992-104">Le nouveau format recommandé pour les packages de symboles est .snupkg.</span><span class="sxs-lookup"><span data-stu-id="4b992-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="4b992-105">Consultez [Création de packages de symboles (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="4b992-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="4b992-106">.symbols.nupkg est toujours pris en charge, mais uniquement pour des raisons de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="4b992-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="4b992-107">En plus de créer des packages pour nuget.org ou d’autres sources, NuGet prend également en charge la création de packages de symboles associés qui peuvent être publiés sur des serveurs de symboles.</span><span class="sxs-lookup"><span data-stu-id="4b992-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="4b992-108">Le format de package de symboles hérité,. Symbols. nupkg, peut faire l’objet d’un push vers le référentiel SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="4b992-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="4b992-109">Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b992-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="4b992-110">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="4b992-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="4b992-111">Création d’un package de symboles hérité</span><span class="sxs-lookup"><span data-stu-id="4b992-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="4b992-112">Pour créer un package de symboles hérité, respectez les conventions suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b992-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="4b992-113">Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="4b992-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="4b992-114">Nommez le package de symboles hérité `{identifier}.symbols.nupkg` et incluez votre DLL d’assembly, les fichiers de `.pdb`, les fichiers XMLDOC, les fichiers sources (voir les sections qui suivent).</span><span class="sxs-lookup"><span data-stu-id="4b992-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="4b992-115">Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :</span><span class="sxs-lookup"><span data-stu-id="4b992-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="4b992-116">Notez que `pack` requiert Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="4b992-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="4b992-117">Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.</span><span class="sxs-lookup"><span data-stu-id="4b992-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="4b992-118">Structure de package de symboles héritée</span><span class="sxs-lookup"><span data-stu-id="4b992-118">Legacy symbol package structure</span></span>

<span data-ttu-id="4b992-119">Un package de symboles hérité peut cibler plusieurs frameworks cibles de la même manière qu’un package de bibliothèque, de sorte que la structure du dossier `lib` doit être exactement la même que celle du package principal, y compris les fichiers `.pdb` avec la DLL.</span><span class="sxs-lookup"><span data-stu-id="4b992-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="4b992-120">Par exemple, un package de symboles hérité qui cible .NET 4,0 et Silverlight 4 aura cette disposition :</span><span class="sxs-lookup"><span data-stu-id="4b992-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="4b992-121">Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source.</span><span class="sxs-lookup"><span data-stu-id="4b992-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="4b992-122">En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="4b992-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="4b992-123">Un chemin d’accès de base (préfixe de chemin d’accès commun) peut être supprimé. Prenons l’exemple d’une bibliothèque générée à partir de ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="4b992-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="4b992-124">En dehors du dossier `lib`, un package de symboles hérité doit contenir cette disposition :</span><span class="sxs-lookup"><span data-stu-id="4b992-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="4b992-125">Référence à des fichiers dans le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="4b992-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="4b992-126">Un package de symboles hérité peut être généré par des conventions, à partir d’une structure de dossiers comme décrit dans la section précédente, ou en spécifiant son contenu dans la section `files` du manifeste.</span><span class="sxs-lookup"><span data-stu-id="4b992-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="4b992-127">Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="4b992-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="4b992-128">Publication d’un package de symboles hérité</span><span class="sxs-lookup"><span data-stu-id="4b992-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="4b992-129">Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.9.1 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.</span><span class="sxs-lookup"><span data-stu-id="4b992-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="4b992-130">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).</span><span class="sxs-lookup"><span data-stu-id="4b992-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="4b992-131">Après la publication de votre package principal sur nuget.org, envoyez le package de symboles hérités comme suit, qui utilisera automatiquement symbolsource.org en tant que cible en raison de l' `.symbols` dans le nom de fichier :</span><span class="sxs-lookup"><span data-stu-id="4b992-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="4b992-132">Pour publier dans un autre référentiel de symboles ou pour pousser un package de symboles hérité qui ne respecte pas la Convention d’affectation de noms, utilisez l’option `-Source` :</span><span class="sxs-lookup"><span data-stu-id="4b992-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="4b992-133">Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4b992-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="4b992-134">Avec NuGet. exe 4.5.0 ou version ultérieure, les packages de symboles ne sont pas automatiquement envoyés à symbolsource.org. Vous devez envoyer les packages de symboles séparément, comme expliqué dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="4b992-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="4b992-135">Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4b992-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="4b992-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4b992-136">See also</span></span>

* <span data-ttu-id="4b992-137">[Création de packages de symboles (. snupkg)](Symbol-Packages-snupkg.md) -nouveau format recommandé pour les packages de symboles</span><span class="sxs-lookup"><span data-stu-id="4b992-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="4b992-138">[Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="4b992-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
