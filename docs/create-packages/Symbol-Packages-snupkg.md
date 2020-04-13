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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380416"
---
# <a name="creating-symbol-packages-snupkg"></a>Création de packages de symboles (.snupkg)

Une bonne expérience de débogage repose sur la présence de symboles de déboguer car ils fournissent des informations critiques comme l’association entre le code compilé et le code source, les noms des variables locales, les traces de pile, et plus encore. Vous pouvez utiliser des paquets de symboles (.snupkg) pour distribuer ces symboles et améliorer l’expérience de débogage de vos paquets NuGet.

## <a name="prerequisites"></a>Prérequis

[nuget.exe v4.9.0 ou au-dessus](https://www.nuget.org/downloads) ou [dotnet CLI v2.2.0 ou au-dessus](https://www.microsoft.com/net/download/dotnet-core/2.2), qui implémentent les [protocoles NuGet](../api/nuget-protocols.md)requis .

## <a name="creating-a-symbol-package"></a>Création d’un package de symboles

Si vous utilisez dotnet CLI ou MSBuild, `IncludeSymbols` vous `SymbolPackageFormat` devez définir le fichier .snupkg et les propriétés pour créer un fichier .snupkg en plus du fichier .nupkg.

* Ajoutez les propriétés suivantes à votre fichier .csproj :

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Ou spécifiez ces propriétés sur la ligne de commande :

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

La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) propriété peut avoir l’une des deux valeurs: `symbols.nupkg` (la valeur par défaut) ou `snupkg`. Si cette propriété n’est pas spécifiée, un paquet de symbole hérité sera créé.

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

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org contraintes de paquet de symboles

NuGet.org a les contraintes suivantes pour les paquets de symboles :

- Seules les extensions de fichiers suivantes `.pdb` `.nuspec`sont `.xml` `.psmdcp`autorisées dans les paquets de symboles: , , , , `.rels``.p7s`
- Seuls les [BDP portables](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gérés sont pris en charge sur le serveur symbole de NuGet.org.
- Les DB et leurs DLL associés .nupkg doivent être construits avec le compilateur dans visual Studio version 15.9 ou au-dessus (voir [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))

Les paquets de symboles publiés à NuGet.org échoueront à la validation si ces contraintes ne sont pas remplies. 

### <a name="symbol-package-validation-and-indexing"></a>Validation et indexation du package de symboles

Les paquets de [symboles](https://www.nuget.org/) publiés pour NuGet.org subissent plusieurs validations, y compris la numérisation des logiciels malveillants. Si un paquet échoue à une vérification de validation, sa page de détails de paquet affichera un message d’erreur. De plus, les propriétaires du forfait recevront un courriel avec des instructions sur la façon de résoudre les problèmes identifiés.

Lorsque le paquet symbole a passé toutes les validations, les symboles seront indexés par les serveurs symboles de NuGet.org et seront disponibles à la consommation.

La validation et l’indexation du package prend généralement moins de 15 minutes. Si la publication de colis prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si NuGet.org subit des interruptions. Si tous les systèmes sont opérationnels et si le package n’est pas correctement publié en moins d’une heure, connectez-vous à nuget.org et contactez-nous via le lien permettant de contacter le support dans la page des détails du package.

## <a name="symbol-package-structure"></a>Structure des packages de symboles

Le paquet de symboles (.snupkg) a les caractéristiques suivantes :

1) Le .snupkg a le même id et la même version que son paquet NuGet correspondant (.nupkg).
2) Le .snupkg a la même structure de dossier que ses .nupkg correspondants pour tous les fichiers DLL ou EXE avec la distinction qu’au lieu de DLLs / EXE, leurs PDB correspondants seront inclus dans la même hiérarchie de dossier. Les fichiers et dossiers ayant d’autres extensions que PDB ne sont pas inclus dans le fichier .snupkg.
3) Le fichier .nuspec du paquet `SymbolsPackage` de symbole a le type de paquet :

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Si un auteur décide d’utiliser un nuspec personnalisé pour générer ses nupkg et snupkg, le snupkg doit avoir la même hiérarchie de dossiers et les mêmes fichiers que ceux décrits dans 2).
5) Les champs suivants seront exclus du nuspec du ```authors```snupkg ```licenseUrl```: ```icon```, ```owners```, ```requireLicenseAcceptance```, ```license type```, , et .
6) N'utilisez pas l’élément ```<license>``` . Un fichier .snupkg est couvert par la même licence que le fichier .nupkg correspondant.

## <a name="see-also"></a>Voir aussi

Envisagez d’utiliser Source Link pour activer le débogage de code source des assemblages .NET. Pour plus d’informations, veuillez consulter les [directives source Link](/dotnet/standard/library-guidance/sourcelink).

Pour plus d’informations sur les paquets de symboles, veuillez consulter le [modèle NuGet Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) spécification de conception.
