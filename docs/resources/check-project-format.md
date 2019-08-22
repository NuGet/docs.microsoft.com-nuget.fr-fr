---
title: Identifier le format du projet
description: Décrit comment identifier le format de votre projet
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488479"
---
# <a name="identify-the-project-format"></a>Identifier le format du projet

NuGet fonctionne avec tous les projets .NET. Toutefois, le format de projet (de type SDK ou non SDK) détermine certains des outils et méthodes que vous devez utiliser pour consommer et créer des packages NuGet. Les projets de style SDK utilisent [l’attribut SDK](/dotnet/core/tools/csproj#additions). Il est important d’identifier votre type de projet, car les méthodes et les outils que vous utilisez pour utiliser et créer des packages NuGet dépendent du format du projet. Pour les projets qui ne sont pas de type SDK, les méthodes et les outils dépendent également du fait que le projet a été migré vers le format `PackageReference` ou pas.

La méthode utilisée pour créer le projet détermine si votre projet est de style SDK ou pas. Le tableau suivant indique le format de projet par défaut et l’outil CLI associé à votre projet lorsque vous le créez à l’aide de Visual Studio 2017 et les versions ultérieures.

| Projet&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Format de projet par défaut | Outil CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Notes |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Style SDK | [Interface CLI .NET](../install-nuget-client-tools.md#dotnetexe-cli) | Les projets créés avant Visual Studio 2017 ne sont pas de type SDK. Utilisez la CLI `nuget.exe`. |
| .NET Core | Style SDK | [Interface CLI .NET](../install-nuget-client-tools.md#dotnetexe-cli) | Les projets créés avant Visual Studio 2017 ne sont pas de type SDK. Utilisez la CLI `nuget.exe`. |
| .NET Framework | Pas de style SDK | [Interface CLI de nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Les projets .NET Framework créés à l’aide d’autres méthodes peuvent être des projets de type SDK. Pour ceux-ci, utilisez la [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli) à la place. |
| Projet .NET [migré](../consume-packages/migrate-packages-config-to-package-reference.md) | Pas de style SDK| Pour créer des packages, utilisez [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) pour créer des packages. | Pour créer des packages, `msbuild -t:pack` est recommandé. Sinon, utilisez la [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Les projets migrés ne sont pas des projets de type SDK. |

## <a name="check-the-project-format"></a>Vérifier le format du projet

Si vous ne savez pas si le projet est au format de type SDK, recherchez l’attribut SDK dans l’élément `<Project>` du fichier projet (pour C#, il s’agit du fichier *.csproj). Si cet élément est présent, le projet est de type SDK.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Vérifier le format du projet dans Visual Studio

Si vous travaillez dans Visual Studio, vous pouvez rapidement vérifier le format du projet à l’aide de l’une des méthodes suivantes:

- Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions, puis sélectionnez **Modifier myprojectname.csproj**.

   Cette option n’est disponible qu’à partir de Visual Studio 2017 pour les projets qui utilisent l’attribut de style SDK. Sinon, utilisez l’autre méthode.

   ![Modifier le fichier projet](media/edit-project-file.png)

   Un projet de type SDK affiche [l’attribut SDK](/dotnet/core/tools/csproj#additions) dans le fichier projet.
   
- Dans le menu **Projet**, choisissez **Décharger le projet** (ou cliquez sur le projet avec le bouton droit et choisissez **Décharger le projet**).

   Ce projet n’inclut pas l’attribut SDK dans le fichier projet. Il ne s’agit pas d’un projet de type SDK.

   ![Décharger le projet](media/unload-project.png)

   Cliquez ensuite avec le bouton droit sur le projet déchargé et choisissez **Modifier myprojectname.csproj**.

## <a name="see-also"></a>Voir aussi

- [Créer des packages .NET Standard avec la CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Créer des packages .NET Standard avec Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Créer et publier un package .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md)
