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
ms.openlocfilehash: 109df18bcfd3e6a3fbd3ef3da1707ffada585140
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70749029"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="d8ea0-104">Création de packages de symboles (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="d8ea0-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="d8ea0-105">Les packages de symboles vous permettent d’améliorer le débogage de vos packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8ea0-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d8ea0-106">Prerequisites</span></span>

<span data-ttu-id="d8ea0-107">[nuget.exe v4.9.0 ou version ultérieure](https://www.nuget.org/downloads), ou [dotnet.exe v2.2.0 ou version ultérieure](https://www.microsoft.com/net/download/dotnet-core/2.2), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) nécessaires.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="d8ea0-108">Création d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="d8ea0-108">Creating a symbol package</span></span>

<span data-ttu-id="d8ea0-109">Si vous utilisez dotnet. exe ou MSBuild, vous devez définir les `IncludeSymbols` propriétés et `SymbolPackageFormat` pour créer un fichier. snupkg en plus du fichier. nupkg.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="d8ea0-110">Ajoutez les propriétés suivantes à votre fichier. csproj :</span><span class="sxs-lookup"><span data-stu-id="d8ea0-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="d8ea0-111">Ou spécifiez ces propriétés sur la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="d8ea0-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="d8ea0-112">ou Gestionnaire de configuration</span><span class="sxs-lookup"><span data-stu-id="d8ea0-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="d8ea0-113">Si vous choisissez NuGet.exe, vous pouvez utiliser les commandes suivantes pour créer un fichier .snupkg, en plus du fichier .nupkg :</span><span class="sxs-lookup"><span data-stu-id="d8ea0-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="d8ea0-114">La propriété [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) peut avoir l’une des deux valeurs suivantes : `symbols.nupkg` (valeur par défaut) ou `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="d8ea0-115">Si cette propriété n’est pas spécifiée, un package de symboles hérité sera créé.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="d8ea0-116">Le format hérité `.symbols.nupkg` est toujours pris en charge, mais uniquement pour des raisons de compatibilité (consultez [Packages de symboles hérités](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="d8ea0-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="d8ea0-117">Le serveur de symboles NuGet.org accepte uniquement le nouveau format de package de symboles - `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="d8ea0-118">Publication d’un package de symboles</span><span class="sxs-lookup"><span data-stu-id="d8ea0-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="d8ea0-119">Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="d8ea0-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="d8ea0-120">Après avoir publié votre package principal sur nuget.org, envoyez (push) le package de symboles comme suit.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="d8ea0-121">Vous pouvez également envoyer simultanément le package principal et le package de symboles à l’aide de la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="d8ea0-122">Les fichiers .nupkg et .snupkg doivent être présents dans le dossier actuel.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="d8ea0-123">NuGet publie les deux packages sur nuget.org. `MyPackage.nupkg` sera publié en premier, suivi de `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="d8ea0-124">Si le package de symboles n’est pas publié, vérifiez que vous avez configuré la source NuGet.org comme `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d8ea0-125">La publication du package de symboles est uniquement prise en charge par [l’API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="d8ea0-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="d8ea0-126">Serveur de symboles NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d8ea0-126">NuGet.org symbol server</span></span>

<span data-ttu-id="d8ea0-127">NuGet.org prend en charge son propre dépôt de serveur de symboles et accepte uniquement le nouveau format de package de symboles - `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="d8ea0-128">Les consommateurs de package peuvent utiliser les symboles publiés sur le serveur de symboles nuget.org en ajoutant `https://symbols.nuget.org/download/symbols` à leurs sources de symboles dans Visual Studio, ce qui permet d’effectuer un pas à pas détaillé du code de package dans le débogueur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="d8ea0-129">Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017).</span><span class="sxs-lookup"><span data-stu-id="d8ea0-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="d8ea0-130">Contraintes liées au package de symboles Nuget.org</span><span class="sxs-lookup"><span data-stu-id="d8ea0-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="d8ea0-131">Les packages de symboles pris en charge sur nuget.org ont les contraintes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8ea0-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="d8ea0-132">Seules les extensions de fichier suivantes peuvent être ajoutées à un package de symboles.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="d8ea0-133">Seuls les fichiers [pdb portables](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) managés sont pris en charge sur le serveur de symboles nuget.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="d8ea0-134">Les fichiers pdb et les fichiers dll associés de nupkg doivent être générés avec le compilateur de Visual Studio version 15.9 ou version ultérieure (consultez [code de hachage de chiffrement de fichier pdb](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="d8ea0-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="d8ea0-135">La publication du package de symboles sur nuget.org ne peut pas s’effectuer correctement si d’autres types de fichier sont inclus dans le fichier .snupkg.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="d8ea0-136">Validation et indexation du package de symboles</span><span class="sxs-lookup"><span data-stu-id="d8ea0-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="d8ea0-137">Les packages de symboles publiés sur [NuGet.org](https://www.nuget.org/) sont soumis à plusieurs validations, par exemple des contrôles antivirus.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="d8ea0-138">Une fois que tous les contrôles de validation du package ont réussi, il est parfois nécessaire d’attendre un certain temps avant que les symboles ne soient indexés et disponibles pour être consommés à partir des serveurs de symboles NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="d8ea0-139">En cas d’échec d’un contrôle de validation du package, la page des détails de package du fichier .nupkg se met à jour pour afficher l’erreur associée. De plus, vous recevez un e-mail de notification.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="d8ea0-140">La validation et l’indexation du package prend généralement moins de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="d8ea0-141">Si la publication du package prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si nuget.org rencontre des interruptions.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="d8ea0-142">Si tous les systèmes sont opérationnels et si le package n’est pas correctement publié en moins d’une heure, connectez-vous à nuget.org et contactez-nous via le lien permettant de contacter le support dans la page des détails du package.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="d8ea0-143">Structure des packages de symboles</span><span class="sxs-lookup"><span data-stu-id="d8ea0-143">Symbol package structure</span></span>

<span data-ttu-id="d8ea0-144">Le fichier .nupkg est exactement le même qu’aujourd’hui. Toutefois, le fichier .snupkg présente les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="d8ea0-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="d8ea0-145">Le fichier .snupkg a le même ID et la même version que le fichier .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="d8ea0-146">Le fichier .snupkg comporte la même structure de dossiers que le fichier .nupkg pour tous les fichiers DLL ou EXE, à la différence qu’au lieu de fichiers DLL/EXE, les fichiers PDB correspondants sont inclus dans la même hiérarchie de dossiers.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="d8ea0-147">Les fichiers et dossiers ayant d’autres extensions que PDB ne sont pas inclus dans le fichier .snupkg.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="d8ea0-148">Le fichier .nuspec dans le fichier .snupkg spécifie également un nouveau PackageType, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="d8ea0-149">Il doit s’agir du seul PackageType spécifié.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="d8ea0-150">Si un auteur décide d’utiliser un nuspec personnalisé pour générer ses nupkg et snupkg, le snupkg doit avoir la même hiérarchie de dossiers et les mêmes fichiers que ceux décrits dans 2).</span><span class="sxs-lookup"><span data-stu-id="d8ea0-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="d8ea0-151">Les champs ```authors``` et ```owners``` sont exclus du nuspec de snupkg.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="d8ea0-152">N'utilisez pas l’élément ```<license>``` .</span><span class="sxs-lookup"><span data-stu-id="d8ea0-152">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="d8ea0-153">Un fichier .snupkg est couvert par la même licence que le fichier .nupkg correspondant.</span><span class="sxs-lookup"><span data-stu-id="d8ea0-153">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8ea0-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d8ea0-154">See Also</span></span>

[<span data-ttu-id="d8ea0-155">Améliorations du débogage des packages NuGet & symboles</span><span class="sxs-lookup"><span data-stu-id="d8ea0-155">NuGet Package Debugging & Symbols Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
