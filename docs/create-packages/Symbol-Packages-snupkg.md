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
ms.openlocfilehash: de37cbf1f63da3de07774281eceef99c51abdaa5
ms.sourcegitcommit: 96aab8a1ad35eca0c029679d0158d9cc93d66009
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/06/2020
ms.locfileid: "75676378"
---
# <a name="creating-symbol-packages-snupkg"></a>Création de packages de symboles (.snupkg)

Les packages de symboles vous permettent d’améliorer le débogage de vos packages NuGet.

## <a name="prerequisites"></a>Configuration requise

[nuget.exe v4.9.0 ou version ultérieure](https://www.nuget.org/downloads), ou [dotnet.exe v2.2.0 ou version ultérieure](https://www.microsoft.com/net/download/dotnet-core/2.2), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) nécessaires.

## <a name="creating-a-symbol-package"></a>Création d’un package de symboles

Si vous utilisez dotnet. exe ou MSBuild, vous devez définir les propriétés `IncludeSymbols` et `SymbolPackageFormat` pour créer un fichier. snupkg en plus du fichier. nupkg.

* Ajoutez les propriétés suivantes à votre fichier. csproj :

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Ou spécifiez ces propriétés sur la ligne de commande :

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  ou

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Si vous choisissez NuGet.exe, vous pouvez utiliser les commandes suivantes pour créer un fichier .snupkg, en plus du fichier .nupkg :

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

La propriété [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) peut avoir l’une des deux valeurs suivantes : `symbols.nupkg` (valeur par défaut) ou `snupkg`. Si cette propriété n’est pas spécifiée, un package de symboles hérité sera créé.

> [!Note]
> Le format hérité `.symbols.nupkg` est toujours pris en charge, mais uniquement pour des raisons de compatibilité (consultez [Packages de symboles hérités](Symbol-Packages.md)). Le serveur de symboles NuGet.org accepte uniquement le nouveau format de package de symboles - `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publication d’un package de symboles

1. Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Après avoir publié votre package principal sur nuget.org, envoyez (push) le package de symboles comme suit.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Vous pouvez également envoyer simultanément le package principal et le package de symboles à l’aide de la commande ci-dessous. Les fichiers .nupkg et .snupkg doivent être présents dans le dossier actuel.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet publie les deux packages sur nuget.org. `MyPackage.nupkg` sera publié en premier, suivi de `MyPackage.snupkg`.

> [!Note]
> Si le package de symboles n’est pas publié, vérifiez que vous avez configuré la source NuGet.org comme `https://api.nuget.org/v3/index.json`. La publication du package de symboles est uniquement prise en charge par [l’API NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Serveur de symboles NuGet.org

NuGet.org prend en charge son propre dépôt de serveur de symboles et accepte uniquement le nouveau format de package de symboles - `.snupkg`. Les consommateurs de package peuvent utiliser les symboles publiés sur le serveur de symboles nuget.org en ajoutant `https://symbols.nuget.org/download/symbols` à leurs sources de symboles dans Visual Studio, ce qui permet d’effectuer un pas à pas détaillé du code de package dans le débogueur Visual Studio. Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

### <a name="nugetorg-symbol-package-constraints"></a>Contraintes du package de symboles NuGet.org

NuGet.org présente les contraintes suivantes pour les packages de symboles :

- Seules les extensions de fichier suivantes sont autorisées dans les packages de symboles : `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- Seuls les fichiers [PDB portables](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gérés sont pris en charge sur le serveur de symboles NuGet. org.
- Les fichiers PDB et leurs dll. nupkg associés doivent être générés avec le compilateur dans Visual Studio version 15,9 ou ultérieure (voir [PDB crypto Hash](https://github.com/dotnet/roslyn/issues/24429))

Les packages de symboles publiés sur NuGet.org ne seront pas validés si ces contraintes ne sont pas satisfaites. 

### <a name="symbol-package-validation-and-indexing"></a>Validation et indexation du package de symboles

Les packages de symboles publiés dans [NuGet.org](https://www.nuget.org/) subissent plusieurs validations, y compris l’analyse des logiciels malveillants. Si un package ne parvient pas à effectuer une vérification de validation, sa page Détails du package affiche un message d’erreur. En outre, les propriétaires du package recevront un message électronique contenant des instructions sur la façon de résoudre les problèmes identifiés.

Quand le package de symboles a passé toutes les validations, les symboles sont indexés par les serveurs de symboles NuGet. org. Une fois indexés, le symbole sera disponible à la consommation à partir des serveurs de symboles NuGet.org.

La validation et l’indexation du package prend généralement moins de 15 minutes. Si la publication du package prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si NuGet.org rencontre des interruptions. Si tous les systèmes sont opérationnels et si le package n’est pas correctement publié en moins d’une heure, connectez-vous à nuget.org et contactez-nous via le lien permettant de contacter le support dans la page des détails du package.

## <a name="symbol-package-structure"></a>Structure des packages de symboles

Le fichier .nupkg est exactement le même qu’aujourd’hui. Toutefois, le fichier .snupkg présente les caractéristiques suivantes :

1) Le fichier .snupkg a le même ID et la même version que le fichier .nupkg correspondant.
2) Le fichier .snupkg comporte la même structure de dossiers que le fichier .nupkg pour tous les fichiers DLL ou EXE, à la différence qu’au lieu de fichiers DLL/EXE, les fichiers PDB correspondants sont inclus dans la même hiérarchie de dossiers. Les fichiers et dossiers ayant d’autres extensions que PDB ne sont pas inclus dans le fichier .snupkg.
3) Le fichier .nuspec dans le fichier .snupkg spécifie également un nouveau PackageType, comme indiqué ci-dessous. Il doit s’agir du seul PackageType spécifié.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Si un auteur décide d’utiliser un nuspec personnalisé pour générer ses nupkg et snupkg, le snupkg doit avoir la même hiérarchie de dossiers et les mêmes fichiers que ceux décrits dans 2).
5) Les champs ```authors``` et ```owners``` sont exclus du nuspec de snupkg.
6) N'utilisez pas l’élément ```<license>``` . Un fichier .snupkg est couvert par la même licence que le fichier .nupkg correspondant.

## <a name="see-also"></a>Voir aussi

Envisagez d’utiliser le lien source pour activer le débogage du code source des assemblys .NET. Pour plus d’informations, reportez-vous à l’aide sur les [liens source](/dotnet/standard/library-guidance/sourcelink).

Pour plus d’informations sur les packages de symboles, reportez-vous à la spécification du [débogage du package NuGet & les améliorations des symboles](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) .
