---
title: Guide pratique pour créer des packages de symboles NuGet
description: Comment créer des packages NuGet qui contiennent uniquement des symboles pour prendre en charge le débogage d’autres packages NuGet dans Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3321cba9082eb35b53ba693e246db18e5d8e187b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580257"
---
# <a name="creating-symbol-packages-legacy"></a>Création de packages de symboles (hérité)

> [!Important]
> Le nouveau format recommandé pour les packages de symboles est .snupkg. Consultez [Création de packages de symboles (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg est toujours pris en charge, mais uniquement pour des raisons de compatibilité.

En plus de générer des packages pour nuget.org et d’autres sources, NuGet prend en charge la création de packages de symboles associés et leur publication dans le référentiel SymbolSource.

Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio. Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

## <a name="creating-a-symbol-package"></a>Création d’un package de symboles

Pour créer un package de symboles, respectez les conventions suivantes :

- Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.
- Nommez le package de symboles `{identifier}.symbols.nupkg` et incluez la DLL de votre assembly, vos fichiers `.pdb`, vos fichiers XMLDOC, vos fichiers sources (consultez les sections qui suivent).

Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux. Sur un Mac, vous devez également convertir les chemins Windows dans le fichier `.nuspec` en chemins de style Unix.

## <a name="symbol-package-structure"></a>Structure des packages de symboles

Un package de symboles peut cibler plusieurs versions cibles du .Net Framework de la même façon qu’un package de bibliothèque, si bien que la structure du dossier `lib` doit être exactement la même que celle du package principal, en incluant uniquement les fichiers `.pdb` avec la DLL.

Par exemple, un package de symboles ciblant le .NET 4.0 et Silverlight 4 aurait cette disposition :

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source. En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication. Un chemin de base (préfixe de chemin commun) peut être supprimé. Par exemple, considérez une bibliothèque créée à partir de ces fichiers :

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

À part le dossier `lib`, un package de symboles doit contenir cette disposition :

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

Un package de symboles peut être généré par des conventions, à partir d’une structure de dossiers comme décrit dans la section précédente, ou en spécifiant son contenu dans la section `files` du manifeste. Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publication d’un package de symboles

> [!Important]
> Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.1.0 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.

1. Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../create-packages/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Après avoir publié votre package principal sur nuget.org, envoyez le package de symboles de la manière suivante, ce qui permet d’utiliser automatiquement symbolsource.org en tant que cible puisque le nom de fichier contient `.symbols` :

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Pour publier sur un dépôt de symboles différent ou envoyer un package de symboles qui ne respecte pas les conventions de nommage, utilisez l’option `-Source` :

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Avec nuget.exe 4.5.0 ou ultérieur, les packages de symboles ne sont pas automatiquement envoyés à symbolsource.org. Vous devez envoyer les packages de symboles séparément, comme expliqué dans l’étape suivante.
   
Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.

## <a name="see-also"></a>Voir aussi

[Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
