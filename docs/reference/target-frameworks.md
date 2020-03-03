---
title: Référence des frameworks cibles pour NuGet
description: Les références des versions cibles de .NET Framework NuGet identifient et isolent les composants dépendants du framework d’un package.
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 995f15ae2ad823d9c814cb7e78facddee713cc8f
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230510"
---
# <a name="target-frameworks"></a>Versions cibles de .NET Framework

NuGet utilise les références des versions cibles de .NET Framework à de nombreux endroits pour identifier et isoler spécifiquement les composants dépendants du framework d’un package :

- [fichier projet](../create-packages/multiple-target-frameworks-project-file.md): pour les projets de type kit de développement logiciel (SDK), le fichier *. csproj* contient les références à la version cible du .NET Framework.
- [Manifeste .nuspec](../reference/nuspec.md) : un package peut désigner des packages distincts à inclure dans un projet en fonction de la version cible de .NET Framework du projet.
- [Nom du dossier .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) : les dossiers à l’intérieur du dossier `lib` d’un package peuvent être nommés en fonction de la version cible de .NET Framework, chacun contenant les DLL et tout autre contenu appropriés pour ce framework.
- [packages.config](../reference/packages-config.md) : l’attribut `targetframework` d’une dépendance spécifie la variante d’un package à installer.

> [!Note]
> Le code source du client NuGet qui calcule les tableaux ci-dessous se trouve aux emplacements suivants :
> - Noms des frameworks pris en charge : [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Priorité des frameworks et mappage : [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Frameworks pris en charge

Un framework est généralement référencé par un moniker du Framework cible ou TFM court. Dans .NET Standard cela est également généralisé à *TxM* pour permettre une seule référence à plusieurs infrastructures.

Les clients NuGet prennent en charge les frameworks dans le tableau ci-dessous. Les équivalents sont indiqués entre crochets []. Notez que certains outils, tels que `dotnet`, peuvent utiliser les variantes de monikers TFM canoniques dans certains fichiers. Par exemple, `dotnet pack` utilise `.NETCoreApp2.0` dans un fichier `.nuspec` plutôt que `netcoreapp2.0`. Les différents outils du client NuGet gèrent correctement ces variantes, mais vous devez toujours utiliser des monikers TFM canoniques quand vous modifiez directement les fichiers.

| Name | Abréviation | TFMs/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Windows Store) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
| Windows | win | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (non pris en charge par la plateforme Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Plateforme Windows universelle | uap | uap [uap10.0] |
| | | uap10.0 |
| | | UAP 10.0. xxxxx (où 10.0. xxxxx est la version minimale de la plateforme cible de l’application consommatrice) |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
| | | netstandard 2.1 |
Application .NET Core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
| | | netcoreapp2.2 |
| | | netcoreapp 3.0 |
| | | netcoreapp 3.1 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Frameworks dépréciés

Les frameworks suivants sont dépréciés. Les packages ciblant ces frameworks doivent migrer vers les versions de remplacement indiquées.

| Framework déprécié | Remplacement
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Priorité

Un certain nombre de frameworks sont liés et compatibles entre eux, mais sans être nécessairement équivalents :

| Framework | Peut utiliser |
| -- | --- |
| uap (Plateforme Windows universelle) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | |

## <a name="net-standard"></a>Standard NET

[.NET standard](/dotnet/standard/net-standard) simplifie les références entre les frameworks compatibles binaires, ce qui permet à un Framework cible unique de référencer une combinaison d’autres. (Pour obtenir des informations générales, consultez le [Guide de .NET](/dotnet/articles/standard/index).)

L’outil [Get Nearest Framework Nuget](https://aka.ms/s2m3th) simule ce que NuGet utilise pour la sélection d’un framework à partir de nombreuses ressources de framework disponibles dans un package, en fonction du framework du projet.

La série `dotnet` des monikers doit être utilisée dans NuGet 3.3 et versions antérieures ; la syntaxe de moniker `netstandard` doit être utilisée dans v3.4 et versions ultérieures.

## <a name="portable-class-libraries"></a>Bibliothèques de classes portables

> [!Warning]
> **Les bibliothèques de classes portables ne sont pas recommandées**. Même si elles sont prises en charge, les auteurs de packages doivent prendre en charge netstandard à la place. .NET Platform standard est une évolution de classes portables et représente la portabilité binaire entre les plateformes à l’aide d’un moniker unique qui n’est pas lié à une bibliothèque statique comme les monikers *portable-a + b + c* .

Pour définir une version cible de .NET Framework qui fait référence à plusieurs frameworks-cibles-enfants, le mot clé `portable` est utilisé pour préfixer la liste des frameworks référencés. Évitez d’inclure artificiellement des frameworks supplémentaires qui ne sont pas directement compilés, car cela peut aboutir à des effets secondaires inattendus dans ces frameworks.

D’autres frameworks définis par des tiers assurent la compatibilité avec d’autres environnements qui sont accessibles de cette manière. De plus, il existe des numéros de profil abrégés qui sont disponibles pour faire référence à ces combinaisons de frameworks connexes en tant que `Profile#`, mais l’utilisation de ces numéros n’est pas recommandée, car cela réduit la lisibilité des dossiers et de `.nuspec`.

| Numéro de profil | Frameworks | Nom complet | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

De plus, les packages NuGet ciblant Xamarin peuvent utiliser d’autres frameworks définis par Xamarin. Consultez [Création de packages NuGet pour Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Name | Description | .NET Standard |
| --- | --- | ---
| monoandroid | Prise en charge mono pour le système d’exploitation Android | netstandard1.4 |
| monotouch | Prise en charge mono pour iOS | netstandard1.4 |
| monomac | Prise en charge mono pour OSX | netstandard1.4 |
| xamarinios | Prise en charge pour Xamarin pour iOS | netstandard1.4 |
| xamarinmac | Prise en charge pour Xamarin pour Mac | netstandard1.4 |
| xamarinpsthree | Prise en charge pour Xamarin sur Playstation 3 | netstandard1.4 |
| xamarinpsfour | Prise en charge pour Xamarin sur Playstation 4 | netstandard1.4 |
| xamarinpsvita | Prise en charge pour Xamarin sur PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin pour le système d’exploitation Watch | netstandard1.4 |
| xamarintvos | Xamarin pour le système d’exploitation TV | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin pour XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin pour XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary a créé un outil qui répertorie les bibliothèques de classes portables prises en charge, que vous pouvez trouver sur son blog, [Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
