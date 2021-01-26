---
title: Guide pratique pour publier des packages de symboles NuGet à l’aide du nouveau format de package de symboles « .snupkg »| Microsoft Docs
author: JonDouglas
ms.author: jodou
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
ms.openlocfilehash: 001637348fdd435e4ffd3a5a55e8128d1eab453c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774567"
---
# <a name="creating-symbol-packages-snupkg"></a>Création de packages de symboles (.snupkg)

Une bonne expérience de débogage repose sur la présence de symboles de débogage, car ils fournissent des informations critiques telles que l’association entre le code compilé et le code source, les noms des variables locales, les traces de la pile, et bien plus encore. Vous pouvez utiliser des packages de symboles (. snupkg) pour distribuer ces symboles et améliorer l’expérience de débogage de vos packages NuGet.

> Notez que le package de symboles n’est pas la seule stratégie pour rendre les symboles de débogage disponibles pour les consommateurs de votre bibliothèque. Il est également [possible `embed` ](https://docs.microsoft.com/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) de les utiliser dans le `dll` ou `exe` avec la propriété de projet suivante :`<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Prérequis

[nuget.exe v 4.9.0 ou version ultérieure](https://www.nuget.org/downloads) ou [dotnet CLI v 2.2.0 ou version ultérieure](https://www.microsoft.com/net/download/dotnet-core/2.2), qui implémente les [protocoles NuGet](../api/nuget-protocols.md)requis.

## <a name="creating-a-symbol-package"></a>Création d’un package de symboles

Si vous utilisez l’interface CLI dotnet ou MSBuild, vous devez définir les `IncludeSymbols` `SymbolPackageFormat` Propriétés et pour créer un fichier. snupkg en plus du fichier. nupkg.

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

  or

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Si vous choisissez NuGet.exe, vous pouvez utiliser les commandes suivantes pour créer un fichier .snupkg, en plus du fichier .nupkg :

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) propriété peut avoir l’une des deux valeurs suivantes : `symbols.nupkg` (valeur par défaut) ou `snupkg` . Si cette propriété n’est pas spécifiée, un package de symboles hérité sera créé.

> [!Note]
> Le format hérité `.symbols.nupkg` est toujours pris en charge, mais uniquement pour des raisons de compatibilité comme les packages natifs (consultez [packages de symboles hérités](Symbol-Packages.md)). Le serveur de symboles NuGet.org accepte uniquement le nouveau format de package de symboles - `.snupkg`.

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

- Seules les extensions de fichier suivantes sont autorisées dans les packages de symboles : `.pdb` , `.nuspec` ,, `.xml` `.psmdcp` , `.rels` , `.p7s`
- Seuls les fichiers [PDB portables](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gérés sont pris en charge sur le serveur de symboles NuGet. org.
- Les fichiers PDB et leurs dll. nupkg associés doivent être générés avec le compilateur dans Visual Studio version 15,9 ou ultérieure (voir [PDB crypto Hash](https://github.com/dotnet/roslyn/issues/24429))

Les packages de symboles publiés sur NuGet.org ne seront pas validés si ces contraintes ne sont pas satisfaites. 

> [!NOTE]
> Les projets natifs, tels que les projets C++, produisent des fichiers PDB Windows au lieu de fichiers PDB portables. Ils ne sont pas pris en charge par le serveur de symboles NuGet. org. Utilisez à la place des [packages de symboles hérités](Symbol-Packages.md) .

### <a name="symbol-package-validation-and-indexing"></a>Validation et indexation du package de symboles

Les packages de symboles publiés dans [NuGet.org](https://www.nuget.org/) subissent plusieurs validations, y compris l’analyse des logiciels malveillants. Si un package ne parvient pas à effectuer une vérification de validation, sa page Détails du package affiche un message d’erreur. En outre, les propriétaires du package recevront un message électronique contenant des instructions sur la façon de résoudre les problèmes identifiés.

Quand le package de symboles a réussi toutes les validations, les symboles sont indexés par les serveurs de symboles NuGet. org et sont disponibles pour la consommation.

La validation et l’indexation du package prend généralement moins de 15 minutes. Si la publication du package prend plus de temps que prévu, visitez [Status.NuGet.org](https://status.nuget.org/) pour vérifier si NuGet.org rencontre des interruptions. Si tous les systèmes sont opérationnels et si le package n’est pas correctement publié en moins d’une heure, connectez-vous à nuget.org et contactez-nous via le lien permettant de contacter le support dans la page des détails du package.

## <a name="symbol-package-structure"></a>Structure des packages de symboles

Le package de symboles (. snupkg) présente les caractéristiques suivantes :

1) Le fichier. snupkg a le même ID et la même version que son package NuGet correspondant (. nupkg).
2) Le fichier. snupkg a la même structure de dossiers que la structure. nupkg correspondante pour tous les fichiers DLL ou EXE, à la différence qu’au lieu de dll/exe, les fichiers PDB correspondants sont inclus dans la même hiérarchie de dossiers. Les fichiers et dossiers ayant d’autres extensions que PDB ne sont pas inclus dans le fichier .snupkg.
3) Le fichier. NuSpec du package de symboles a le `SymbolsPackage` type de package :

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Si un auteur décide d’utiliser un nuspec personnalisé pour générer ses nupkg et snupkg, le snupkg doit avoir la même hiérarchie de dossiers et les mêmes fichiers que ceux décrits dans 2).
5) Les champs suivants seront exclus du NuSpec de l’snupkg : ```authors``` ,,,, ```owners``` ```requireLicenseAcceptance``` ```license type``` ```licenseUrl``` et  ```icon``` .
6) N'utilisez pas l’élément ```<license>``` . Un fichier .snupkg est couvert par la même licence que le fichier .nupkg correspondant.

## <a name="see-also"></a>Voir aussi

Envisagez d’utiliser le lien source pour activer le débogage du code source des assemblys .NET. Pour plus d’informations, reportez-vous à l’aide sur les [liens source](/dotnet/standard/library-guidance/sourcelink).

Pour plus d’informations sur les packages de symboles, reportez-vous à la spécification du [débogage du package NuGet & les améliorations des symboles](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) .
