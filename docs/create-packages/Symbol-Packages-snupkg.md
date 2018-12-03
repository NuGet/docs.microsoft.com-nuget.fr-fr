---
title: Guide pratique pour publier des packages de symboles NuGet à l’aide du nouveau format de package de symboles « .snupkg »| Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
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
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453453"
---
# <a name="creating-symbol-packages-snupkg"></a>Création de packages de symboles (.snupkg)

## <a name="prerequisites"></a>Prérequis

[nuget.exe v4.9.0 ou version ultérieure](https://www.nuget.org/downloads), ou [dotnet.exe v2.2.0 ou version ultérieure](https://www.microsoft.com/net/download/dotnet-core/2.2), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) nécessaires.

## <a name="creating-a-symbol-package"></a>Création d’un package de symboles

Vous pouvez créer un package de symboles snupkg à partir d’un fichier .nuspec ou d’un fichier .csproj. NuGet.exe et dotnet.exe sont tous deux pris en charge. Quand vous utilisez les options ```-Symbols -SymbolPackageFormat snupkg``` avec la commande pack de nuget.exe, un fichier .snupkg est créé en plus du fichier .nupkg.

Exemples de commandes permettant de créer des fichiers .snupkg
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

Les `.snupkgs` ne sont pas produits par défaut. Vous devez passer la propriété `SymbolPackageFormat` avec `-Symbols` si vous utilisez nuget.exe, `--include-symbols` si vous utilisez dotnet.exe, ou `-p:IncludeSymbols` si vous utilisez msbuild.

La propriété SymbolPackageFormat peut avoir l’une des deux valeurs suivantes : `symbols.nupkg` (valeur par défaut) ou `snupkg`. Si SymbolPackageFormat n’est pas spécifié, la valeur par défaut est `symbols.nupkg`, et un package de symboles hérité est créé.

> [!Note]
> Le format hérité `.symbols.nupkg` est toujours pris en charge, mais uniquement pour des raisons de compatibilité (consultez [Packages de symboles hérités](Symbol-Packages.md)). Le serveur de symboles NuGet.org accepte uniquement le nouveau format de package de symboles - `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publication d’un package de symboles

1. Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../create-packages/publish-a-package.md)).

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

## <a name="nugetorg-symbol-server"></a>Serveur de symboles NuGet.org

NuGet.org prend en charge son propre dépôt de serveur de symboles et accepte uniquement le nouveau format de package de symboles - `.snupkg`. Les consommateurs de package peuvent utiliser les symboles publiés sur le serveur de symboles nuget.org en ajoutant `https://symbols.nuget.org/download/symbols` à leurs sources de symboles dans Visual Studio, ce qui permet d’effectuer un pas à pas détaillé du code de package dans le débogueur Visual Studio. Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017).

### <a name="nugetorg-symbol-package-constraints"></a>Contraintes liées au package de symboles Nuget.org

Les packages de symboles pris en charge sur nuget.org ont les contraintes suivantes

- Seules les extensions de fichier suivantes peuvent être ajoutées à un package de symboles. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Seuls les fichiers [pdb portables](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) managés sont pris en charge sur le serveur de symboles nuget.
- Les fichiers pdb et les fichiers dll associés de nupkg doivent être générés avec le compilateur de Visual Studio version 15.9 ou version ultérieure (consultez [code de hachage de chiffrement de fichier pdb](https://github.com/dotnet/roslyn/issues/24429))

La publication du package de symboles sur nuget.org ne peut pas s’effectuer correctement si d’autres types de fichier sont inclus dans le fichier .snupkg.

### <a name="symbol-package-validation-and-indexing"></a>Validation et indexation du package de symboles

Les packages de symboles publiés sur [NuGet.org](https://www.nuget.org/) sont soumis à plusieurs validations, par exemple des contrôles antivirus.

Une fois que tous les contrôles de validation du package ont réussi, il est parfois nécessaire d’attendre un certain temps avant que les symboles ne soient indexés et disponibles pour être consommés à partir des serveurs de symboles NuGet.org. En cas d’échec d’un contrôle de validation du package, la page des détails de package du fichier .nupkg se met à jour pour afficher l’erreur associée. De plus, vous recevez un e-mail de notification.

La validation et l’indexation du package prend généralement moins de 15 minutes. Si la publication du package prend plus de temps que prévu, visitez [status.nuget.org](https://status.nuget.org/) pour vérifier si nuget.org rencontre des interruptions. Si tous les systèmes sont opérationnels et si le package n’est pas correctement publié en moins d’une heure, connectez-vous à nuget.org et contactez-nous via le lien permettant de contacter le support dans la page des détails du package.

## <a name="symbol-package-structure"></a>Structure des packages de symboles

Le fichier .nupkg est exactement le même qu’aujourd’hui. Toutefois, le fichier .snupkg présente les caractéristiques suivantes :

1) Le fichier .snupkg a le même ID et la même version que le fichier .nupkg correspondant.
2) Le fichier .snupkg comporte la même structure de dossiers que le fichier .nupkg pour tous les fichiers DLL ou EXE, à la différence qu’au lieu de fichiers DLL/EXE, les fichiers PDB correspondants sont inclus dans la même hiérarchie de dossiers. Les fichiers et dossiers ayant d’autres extensions que PDB ne sont pas inclus dans le fichier .snupkg.
3) Le fichier .nuspec dans le fichier .snupkg spécifie également un nouveau PackageType, comme indiqué ci-dessous. Il doit s’agir du seul PackageType spécifié. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Si un auteur décide d’utiliser un nuspec personnalisé pour générer ses nupkg et snupkg, le snupkg doit avoir la même hiérarchie de dossiers et les mêmes fichiers que ceux décrits dans 2).
5) Les champs ```authors``` et ```owners``` sont exclus du nuspec de snupkg.

## <a name="see-also"></a>Voir aussi

[Améliorations apportées au débogage et aux symboles de packages NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
