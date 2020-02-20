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
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Création de packages de symboles hérités (. Symbols. nupkg)

> [!Important]
> Le nouveau format recommandé pour les packages de symboles est .snupkg. Consultez [Création de packages de symboles (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg est toujours pris en charge, mais uniquement pour des raisons de compatibilité.

En plus de créer des packages pour nuget.org ou d’autres sources, NuGet prend également en charge la création de packages de symboles associés qui peuvent être publiés sur des serveurs de symboles. Le format de package de symboles hérité,. Symbols. nupkg, peut faire l’objet d’un push vers le référentiel SymbolSource.

Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio. Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

## <a name="creating-a-legacy-symbol-package"></a>Création d’un package de symboles hérité

Pour créer un package de symboles hérité, respectez les conventions suivantes :

- Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.
- Nommez le package de symboles hérité `{identifier}.symbols.nupkg` et incluez votre DLL d’assembly, les fichiers de `.pdb`, les fichiers XMLDOC, les fichiers sources (voir les sections qui suivent).

Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Notez que `pack` requiert Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux. Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.

## <a name="legacy-symbol-package-structure"></a>Structure de package de symboles héritée

Un package de symboles hérité peut cibler plusieurs frameworks cibles de la même manière qu’un package de bibliothèque, de sorte que la structure du dossier `lib` doit être exactement la même que celle du package principal, y compris les fichiers `.pdb` avec la DLL.

Par exemple, un package de symboles hérité qui cible .NET 4,0 et Silverlight 4 aura cette disposition :

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source. En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication. Un chemin d’accès de base (préfixe de chemin d’accès commun) peut être supprimé. Prenons l’exemple d’une bibliothèque générée à partir de ces fichiers :

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

En dehors du dossier `lib`, un package de symboles hérité doit contenir cette disposition :

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

## <a name="referring-to-files-in-the-nuspec"></a>Référence à des fichiers dans le fichier nuspec

Un package de symboles hérité peut être généré par des conventions, à partir d’une structure de dossiers comme décrit dans la section précédente, ou en spécifiant son contenu dans la section `files` du manifeste. Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Publication d’un package de symboles hérité

> [!Important]
> Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.9.1 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.

1. Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Après la publication de votre package principal sur nuget.org, envoyez le package de symboles hérités comme suit, qui utilisera automatiquement symbolsource.org en tant que cible en raison de l' `.symbols` dans le nom de fichier :

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Pour publier dans un autre référentiel de symboles ou pour pousser un package de symboles hérité qui ne respecte pas la Convention d’affectation de noms, utilisez l’option `-Source` :

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Avec NuGet. exe 4.5.0 ou version ultérieure, les packages de symboles ne sont pas automatiquement envoyés à symbolsource.org. Vous devez envoyer les packages de symboles séparément, comme expliqué dans les étapes précédentes.
   
Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.

## <a name="see-also"></a>Voir aussi

* [Création de packages de symboles (. snupkg)](Symbol-Packages-snupkg.md) -nouveau format recommandé pour les packages de symboles
* [Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
