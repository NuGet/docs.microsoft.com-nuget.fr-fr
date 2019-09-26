---
title: Guide pratique pour publier des packages de symboles NuGet à l’aide du nouveau format de package de symboles « .snupkg »| Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Guide pratique pour créer des packages de symboles NuGet (snupkg).
keywords: Packages de symboles NuGet, débogage de packages NuGet, prise en charge du débogage NuGet, symboles de packages, conventions des packages de symboles
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 0197902e4dbc18893d68833fbcfe4263f185a594
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307183"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="6feff-104">Création de packages de symboles (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="6feff-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="6feff-105">Les packages de symboles vous permettent d’améliorer le débogage de vos packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="6feff-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6feff-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="6feff-106">Prerequisites</span></span>

<span data-ttu-id="6feff-107">[nuget.exe v4.9.0 ou version ultérieure](https://www.nuget.org/downloads), ou [dotnet.exe v2.2.0 ou version ultérieure](https://www.microsoft.com/net/download/dotnet-core/2.2), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) nécessaires.</span><span class="sxs-lookup"><span data-stu-id="6feff-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="6feff-108">Création d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="6feff-108">Creating a symbol package</span></span>

<span data-ttu-id="6feff-109">Si vous utilisez dotnet. exe ou MSBuild, vous devez définir les `IncludeSymbols` propriétés et `SymbolPackageFormat` pour créer un fichier. snupkg en plus du fichier. nupkg.</span><span class="sxs-lookup"><span data-stu-id="6feff-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="6feff-110">Ajoutez les propriétés suivantes à votre fichier. csproj :</span><span class="sxs-lookup"><span data-stu-id="6feff-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="6feff-111">Ou spécifiez ces propriétés sur la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="6feff-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="6feff-112">ou</span><span class="sxs-lookup"><span data-stu-id="6feff-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="6feff-113">Si vous choisissez NuGet.exe, vous pouvez utiliser les commandes suivantes pour créer un fichier .snupkg, en plus du fichier .nupkg :</span><span class="sxs-lookup"><span data-stu-id="6feff-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="6feff-114">La propriété [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) peut avoir l’une des deux valeurs suivantes : `symbols.nupkg` (valeur par défaut) ou `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6feff-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="6feff-115">Si cette propriété n’est pas spécifiée, un package de symboles hérité sera créé.</span><span class="sxs-lookup"><span data-stu-id="6feff-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="6feff-116">Le format hérité `.symbols.nupkg` est toujours pris en charge, mais uniquement pour des raisons de compatibilité (consultez [Packages de symboles hérités](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="6feff-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="6feff-117">Le serveur de symboles NuGet.org accepte uniquement le nouveau format de package de symboles - `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6feff-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="6feff-118">Publication d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="6feff-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="6feff-119">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="6feff-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="6feff-120">Après avoir publié votre package principal sur nuget.org, envoyez (push) le package de symboles comme suit.</span><span class="sxs-lookup"><span data-stu-id="6feff-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="6feff-121">Vous pouvez également envoyer simultanément le package principal et le package de symboles à l’aide de la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6feff-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="6feff-122">Les fichiers .nupkg et .snupkg doivent être présents dans le dossier actuel.</span><span class="sxs-lookup"><span data-stu-id="6feff-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="6feff-123">NuGet publie les deux packages sur nuget.org. `MyPackage.nupkg` sera publié en premier, suivi de `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6feff-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="6feff-124">Si le package de symboles n’est pas publié, vérifiez que vous avez configuré la source NuGet.org comme `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6feff-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="6feff-125">La publication du package de symboles est uniquement prise en charge par [l’API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="6feff-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="6feff-126">Serveur de symboles NuGet.org</span><span class="sxs-lookup"><span data-stu-id="6feff-126">NuGet.org symbol server</span></span>

<span data-ttu-id="6feff-127">NuGet.org prend en charge son propre dépôt de serveur de symboles et accepte uniquement le nouveau format de package de symboles - `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6feff-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="6feff-128">Les consommateurs de package peuvent utiliser les symboles publiés sur le serveur de symboles nuget.org en ajoutant `https://symbols.nuget.org/download/symbols` à leurs sources de symboles dans Visual Studio, ce qui permet d’effectuer un pas à pas détaillé du code de package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6feff-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="6feff-129">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="6feff-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="6feff-130">Contraintes du package de symboles NuGet.org</span><span class="sxs-lookup"><span data-stu-id="6feff-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="6feff-131">NuGet.org présente les contraintes suivantes pour les packages de symboles :</span><span class="sxs-lookup"><span data-stu-id="6feff-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="6feff-132">Seules les extensions de fichier suivantes sont autorisées dans les packages `.pdb`de `.nuspec`symboles : `.psmdcp`, `.rels`, `.xml`,,,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="6feff-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="6feff-133">Seuls les fichiers [PDB portables](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gérés sont pris en charge sur le serveur de symboles NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="6feff-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="6feff-134">Les fichiers PDB et leurs dll. nupkg associés doivent être générés avec le compilateur dans Visual Studio version 15,9 ou ultérieure (voir [PDB crypto Hash](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="6feff-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="6feff-135">Les packages de symboles publiés sur NuGet.org ne seront pas validés si ces contraintes ne sont pas satisfaites.</span><span class="sxs-lookup"><span data-stu-id="6feff-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="6feff-136">Validation et indexation du package de symboles</span><span class="sxs-lookup"><span data-stu-id="6feff-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="6feff-137">Les packages de symboles publiés dans [NuGet.org](https://www.nuget.org/) subissent plusieurs validations, y compris l’analyse des logiciels malveillants.</span><span class="sxs-lookup"><span data-stu-id="6feff-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="6feff-138">Si un package ne parvient pas à effectuer une vérification de validation, sa page Détails du package affiche un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="6feff-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="6feff-139">En outre, les propriétaires du package recevront un message électronique contenant des instructions sur la façon de résoudre les problèmes identifiés.</span><span class="sxs-lookup"><span data-stu-id="6feff-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="6feff-140">Quand le package de symboles a passé toutes les validations, les symboles sont indexés par les serveurs de symboles NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="6feff-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="6feff-141">Une fois indexés, le symbole sera disponible à la consommation à partir des serveurs de symboles NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="6feff-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="6feff-142">La validation et l’indexation du package prend généralement moins de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="6feff-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="6feff-143">Si la publication du package prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si NuGet.org rencontre des interruptions.</span><span class="sxs-lookup"><span data-stu-id="6feff-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="6feff-144">Si tous les systèmes sont opérationnels et si le package n’est pas correctement publié en moins d’une heure, connectez-vous à nuget.org et contactez-nous via le lien permettant de contacter le support dans la page des détails du package.</span><span class="sxs-lookup"><span data-stu-id="6feff-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="6feff-145">Structure des packages de symboles</span><span class="sxs-lookup"><span data-stu-id="6feff-145">Symbol package structure</span></span>

<span data-ttu-id="6feff-146">Le fichier .nupkg est exactement le même qu’aujourd’hui. Toutefois, le fichier .snupkg présente les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="6feff-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="6feff-147">Le fichier .snupkg a le même ID et la même version que le fichier .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="6feff-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="6feff-148">Le fichier .snupkg comporte la même structure de dossiers que le fichier .nupkg pour tous les fichiers DLL ou EXE, à la différence qu’au lieu de fichiers DLL/EXE, les fichiers PDB correspondants sont inclus dans la même hiérarchie de dossiers.</span><span class="sxs-lookup"><span data-stu-id="6feff-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="6feff-149">Les fichiers et dossiers ayant d’autres extensions que PDB ne sont pas inclus dans le fichier .snupkg.</span><span class="sxs-lookup"><span data-stu-id="6feff-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="6feff-150">Le fichier .nuspec dans le fichier .snupkg spécifie également un nouveau PackageType, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6feff-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="6feff-151">Il doit s’agir du seul PackageType spécifié.</span><span class="sxs-lookup"><span data-stu-id="6feff-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="6feff-152">Si un auteur décide d’utiliser un nuspec personnalisé pour générer ses nupkg et snupkg, le snupkg doit avoir la même hiérarchie de dossiers et les mêmes fichiers que ceux décrits dans 2).</span><span class="sxs-lookup"><span data-stu-id="6feff-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="6feff-153">Les champs ```authors``` et ```owners``` sont exclus du nuspec de snupkg.</span><span class="sxs-lookup"><span data-stu-id="6feff-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="6feff-154">N'utilisez pas l’élément ```<license>``` .</span><span class="sxs-lookup"><span data-stu-id="6feff-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="6feff-155">Un fichier .snupkg est couvert par la même licence que le fichier .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="6feff-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="6feff-156">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6feff-156">See Also</span></span>

<span data-ttu-id="6feff-157">Envisagez d’utiliser le lien source pour activer le débogage du code source des assemblys .NET.</span><span class="sxs-lookup"><span data-stu-id="6feff-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="6feff-158">Pour plus d’informations, reportez-vous à l’aide sur les [liens source](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="6feff-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="6feff-159">Pour plus d’informations sur les packages de symboles, reportez-vous à la spécification du [débogage du package NuGet & les améliorations des symboles](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) .</span><span class="sxs-lookup"><span data-stu-id="6feff-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
