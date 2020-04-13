---
title: Création de paquets de symboles hérités (.symbols.nupkg)
description: Comment créer des packages NuGet qui contiennent uniquement des symboles pour prendre en charge le débogage d’autres packages NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476267"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="89914-103">Création de paquets de symboles hérités (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="89914-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="89914-104">Le nouveau format recommandé pour les packages de symboles est .snupkg.</span><span class="sxs-lookup"><span data-stu-id="89914-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="89914-105">Consultez [Création de packages de symboles (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="89914-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="89914-106">.symbols.nupkg est toujours pris en charge, mais uniquement pour des raisons de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="89914-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="89914-107">En plus de construire des paquets pour nuget.org ou d’autres sources, NuGet prend également en charge la création de paquets de symboles associés qui peuvent être publiés sur des serveurs de symboles.</span><span class="sxs-lookup"><span data-stu-id="89914-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="89914-108">Le format de paquet de symbole hérité, .symbols.nupkg, peut être poussé au référentiel SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="89914-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="89914-109">Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89914-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="89914-110">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="89914-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="89914-111">Création d’un ensemble de symboles hérités</span><span class="sxs-lookup"><span data-stu-id="89914-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="89914-112">Pour créer un ensemble de symboles hérités, suivez ces conventions :</span><span class="sxs-lookup"><span data-stu-id="89914-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="89914-113">Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="89914-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="89914-114">Nommez le `{identifier}.symbols.nupkg` paquet de symboles `.pdb` hérités et incluez votre DLL d’assemblage, fichiers, fichiers XMLDOC, fichiers sources (voir les sections qui suivent).</span><span class="sxs-lookup"><span data-stu-id="89914-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="89914-115">Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :</span><span class="sxs-lookup"><span data-stu-id="89914-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="89914-116">Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="89914-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="89914-117">Sur un Mac, vous devez également convertir les chemins d’accès Windows dans le fichier `.nuspec` en chemins d’accès de style Unix.</span><span class="sxs-lookup"><span data-stu-id="89914-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="89914-118">Structure de paquet de symbole d’héritage</span><span class="sxs-lookup"><span data-stu-id="89914-118">Legacy symbol package structure</span></span>

<span data-ttu-id="89914-119">Un ensemble de symboles hérités peut cibler plusieurs cadres cibles de la `lib` même manière qu’un paquet de bibliothèque, de sorte que la structure du dossier doit être exactement la même que le paquet principal, seulement y compris `.pdb` les fichiers aux côtés de la DLL.</span><span class="sxs-lookup"><span data-stu-id="89914-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="89914-120">Par exemple, un ensemble de symboles hérités qui cible .NET 4.0 et Silverlight 4 aurait cette disposition :</span><span class="sxs-lookup"><span data-stu-id="89914-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="89914-121">Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source.</span><span class="sxs-lookup"><span data-stu-id="89914-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="89914-122">En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="89914-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="89914-123">Un chemin de base (préfixe de voie commune) peut être démonté. Par exemple, considérez une bibliothèque construite à partir de ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="89914-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="89914-124">En dehors `lib` du dossier, un paquet de symbole hérité devrait contenir cette mise en page:</span><span class="sxs-lookup"><span data-stu-id="89914-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="89914-125">Référence à des fichiers dans le fichier nuspec</span><span class="sxs-lookup"><span data-stu-id="89914-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="89914-126">Un ensemble de symboles hérités peut être construit par des conventions, à partir d’une structure de dossier comme décrit dans la section précédente, ou en spécifiant son contenu dans la `files` section du manifeste.</span><span class="sxs-lookup"><span data-stu-id="89914-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="89914-127">Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="89914-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="89914-128">Publication d’un paquet de symboles hérités</span><span class="sxs-lookup"><span data-stu-id="89914-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="89914-129">Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.9.1 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.</span><span class="sxs-lookup"><span data-stu-id="89914-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="89914-130">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).</span><span class="sxs-lookup"><span data-stu-id="89914-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="89914-131">Après la publication de votre colis principal pour nuget.org, poussez le paquet de symboles hérités comme suit, qui utilisera automatiquement symbolsource.org comme cible `.symbols` en raison du nom de fichier dans le nom de fichier:</span><span class="sxs-lookup"><span data-stu-id="89914-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="89914-132">Pour publier sur un autre référentiel de symboles, ou pour pousser un `-Source` paquet de symbole hérité qui ne suit pas la convention de nommage, utilisez l’option :</span><span class="sxs-lookup"><span data-stu-id="89914-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="89914-133">Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="89914-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="89914-134">Avec nuget.exe 4.5.0 ou plus, les paquets de symboles ne sont pas automatiquement poussés à symbolsource.org. Vous auriez besoin de pousser les paquets de symboles séparément comme expliqué dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="89914-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="89914-135">Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="89914-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="89914-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="89914-136">See also</span></span>

* <span data-ttu-id="89914-137">[Création de paquets de symboles (.snupkg)](Symbol-Packages-snupkg.md) - Le nouveau format recommandé pour les paquets de symboles</span><span class="sxs-lookup"><span data-stu-id="89914-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="89914-138">[Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="89914-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
