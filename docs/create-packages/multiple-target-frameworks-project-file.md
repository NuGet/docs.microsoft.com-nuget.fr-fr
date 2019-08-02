---
title: Multiciblage pour les packages NuGet dans votre fichier projet
description: Description des différentes méthodes pour cibler plusieurs versions de .NET Framework à partir d’un seul package NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: b7870bb6aac39f0865d88efc8c16751fdbecc3a8
ms.sourcegitcommit: cae759ad8518c049575a30ad3bf04fe5d06244fb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2019
ms.locfileid: "68616780"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Prendre en charge plusieurs versions de .NET Framework dans votre fichier projet

Lorsque vous créez un projet, nous recommandons de créer une bibliothèque de classes .NET Standard, car elle est compatible avec la plus large gamme de projets consommateurs. En utilisant .NET Standard, vous ajoutez une [prise en charge multiplateforme](/dotnet/standard/library-guidance/cross-platform-targeting) à une bibliothèque .NET par défaut. Toutefois, dans certains scénarios, vous devrez peut-être également inclure du code ciblant un framework particulier. Cet article vous explique comment procéder pour les projets [SDK-style](../resources/check-project-format.md).

Pour les projets SDK-style, vous pouvez configurer la prise en charge de plusieurs [frameworks de cibles (TFM](/dotnet/standard/frameworks)) dans votre `dotnet pack` fichier `msbuild /t:pack` projet, puis utiliser ou pour créer le package.

> [!NOTE]
> L’interface CLI nuget.exe ne prend pas en charge la compression de projets SDK-style. Vous devez donc utiliser uniquement `dotnet pack` ou `msbuild /t:pack`. Nous recommandons d’[inclure toutes les propriétés](../reference/msbuild-targets.md#pack-target) qui se trouvent habituellement dans le fichier `.nuspec` du fichier projet à la place. Pour cibler plusieurs versions de .NET Framework dans un projet non-SDK-style, consultez [Prise en charge de plusieurs versions de .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Créer un projet qui prend en charge plusieurs versions de .NET Framework

1. Créez une nouvelle bibliothèque de classes .NET Standard dans Visual Studio ou utilisez `dotnet new classlib`.

   Nous vous recommandons de créer une bibliothèque de classes .NET Standard pour une meilleure compatibilité.

2. Modifiez le fichier *.csproj* pour prendre en charge les frameworks cibles.

   Par exemple, remplacez `<TargetFramework>netstandard2.0</TargetFramework>` par `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.

   Veillez à modifier l’élément XML mis au pluriel (ajoutez des «s» aux balises d’ouverture et de fermeture).

3. Si vous avez du code qui ne fonctionne que dans un TFM, vous pouvez utiliser `#if NET45` ou `#if NETSTANDARD20` pour séparer du code dépendant du TFM. (Pour plus d'informations, consultez [Guide pratique du multiciblage](/dotnet/core/tutorials/libraries#how-to-multitarget).) Par exemple, vous pouvez utiliser le code suivant :

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. Ajoutez toutes les métadonnées NuGet que vous souhaitez au fichier *.csproj* en tant que propriétés MSBuild.

   Pour obtenir la liste des métadonnées de package disponibles et les noms de propriétés MSBuild, consultez [Pack Target](../reference/msbuild-targets.md#pack-target). Consultez également [Contrôle des ressources de dépendance](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Si vous souhaitez séparer les propriétés liées à la création de builds des métadonnées NuGet, vous pouvez utiliser un `PropertyGroup` différent, ou placer les propriétés NuGet dans un autre fichier et utiliser la directive `Import` de MSBuild pour l’inclure. À compter de MSBuild 15.0, `Directory.Build.Props` et `Directory.Build.Targets` sont également pris en charge.

5. À présent, utilisez `dotnet pack` et les cibles *.nupkg*. qui en résultent, .NET standard 2.0 et .NET Framework 4.5.

Voici le fichier *.csproj* généré à l’aide des étapes précédentes et de .NET Core SDK 2.2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Voir aussi

* [Guide pratique pour spécifier des frameworks cibles](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Ciblage multiplateforme](/dotnet/standard/library-guidance/cross-platform-targeting)
