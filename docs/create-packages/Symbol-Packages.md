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
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Création de paquets de symboles hérités (.symbols.nupkg)

> [!Important]
> Le nouveau format recommandé pour les packages de symboles est .snupkg. Consultez [Création de packages de symboles (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg est toujours pris en charge, mais uniquement pour des raisons de compatibilité.

En plus de construire des paquets pour nuget.org ou d’autres sources, NuGet prend également en charge la création de paquets de symboles associés qui peuvent être publiés sur des serveurs de symboles. Le format de paquet de symbole hérité, .symbols.nupkg, peut être poussé au référentiel SymbolSource.

Les consommateurs de packages peuvent alors ajouter `https://nuget.smbsrc.net` à leurs sources de symbole dans Visual Studio, ce qui permet d’exécuter pas à pas le code du package dans le débogueur Visual Studio. Pour plus d’informations sur ce processus, consultez [Spécifier les fichiers de symboles (.pdb) et les fichiers sources dans le débogueur Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

## <a name="creating-a-legacy-symbol-package"></a>Création d’un ensemble de symboles hérités

Pour créer un ensemble de symboles hérités, suivez ces conventions :

- Nommez le package principal (avec votre code) `{identifier}.nupkg` et incluez tous vos fichiers à l’exception des fichiers `.pdb`.
- Nommez le `{identifier}.symbols.nupkg` paquet de symboles `.pdb` hérités et incluez votre DLL d’assemblage, fichiers, fichiers XMLDOC, fichiers sources (voir les sections qui suivent).

Vous pouvez créer les deux packages avec l’option `-Symbols`, soit à partir d’un fichier `.nuspec`, soit un fichier de projet :

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Notez que `pack` nécessite Mono 4.4.2 sur Mac OS X et ne fonctionne pas sur les systèmes Linux. Sur un Mac, vous devez également convertir les chemins d’accès Windows dans le fichier `.nuspec` en chemins d’accès de style Unix.

## <a name="legacy-symbol-package-structure"></a>Structure de paquet de symbole d’héritage

Un ensemble de symboles hérités peut cibler plusieurs cadres cibles de la `lib` même manière qu’un paquet de bibliothèque, de sorte que la structure du dossier doit être exactement la même que le paquet principal, seulement y compris `.pdb` les fichiers aux côtés de la DLL.

Par exemple, un ensemble de symboles hérités qui cible .NET 4.0 et Silverlight 4 aurait cette disposition :

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Les fichiers sources sont alors placés dans un dossier spécial distinct nommé `src`, qui doit suivre la structure relative de votre dépôt de code source. En effet, les fichiers PDB contiennent des chemins absolus aux fichiers sources utilisés pour compiler la DLL correspondante et doivent être détectés pendant le processus de publication. Un chemin de base (préfixe de voie commune) peut être démonté. Par exemple, considérez une bibliothèque construite à partir de ces fichiers :

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

En dehors `lib` du dossier, un paquet de symbole hérité devrait contenir cette mise en page:

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

Un ensemble de symboles hérités peut être construit par des conventions, à partir d’une structure de dossier comme décrit dans la section précédente, ou en spécifiant son contenu dans la `files` section du manifeste. Par exemple, pour générer le package indiqué dans la section précédente, utilisez les éléments suivants dans le fichier `.nuspec` :

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Publication d’un paquet de symboles hérités

> [!Important]
> Pour envoyer (push) des packages à nuget.org, vous devez utiliser [nuget.exe v4.9.1 ou plus](https://www.nuget.org/downloads), qui implémente les [protocoles NuGet](../api/nuget-protocols.md) requis.

1. Pour des raisons pratiques, commencez par enregistrer votre clé API auprès de NuGet (consultez [Publier un package](../nuget-org/publish-a-package.md), ce qui s’applique à nuget.org et symbolsource.org, étant donné que symbolsource.org vérifie auprès de nuget.org que vous êtes le propriétaire du package).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Après la publication de votre colis principal pour nuget.org, poussez le paquet de symboles hérités comme suit, qui utilisera automatiquement symbolsource.org comme cible `.symbols` en raison du nom de fichier dans le nom de fichier:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Pour publier sur un autre référentiel de symboles, ou pour pousser un `-Source` paquet de symbole hérité qui ne suit pas la convention de nommage, utilisez l’option :

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Vous pouvez également envoyer les packages principaux et de symboles aux deux dépôts en même temps en utilisant ce qui suit :

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Avec nuget.exe 4.5.0 ou plus, les paquets de symboles ne sont pas automatiquement poussés à symbolsource.org. Vous auriez besoin de pousser les paquets de symboles séparément comme expliqué dans les étapes précédentes.
   
Dans ce cas, NuGet publie `MyPackage.symbols.nupkg`, le cas échéant, sur https://nuget.smbsrc.net/ (URL push pour symbolsource.org), après avoir publié le package principal sur nuget.org.

## <a name="see-also"></a>Voir aussi

* [Création de paquets de symboles (.snupkg)](Symbol-Packages-snupkg.md) - Le nouveau format recommandé pour les paquets de symboles
* [Passer au nouveau moteur SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
