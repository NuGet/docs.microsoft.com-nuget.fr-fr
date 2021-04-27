---
title: Définir un type de package NuGet
description: Décrit les types de packages pour indiquer l’utilisation prévue d’un package.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067274"
---
# <a name="set-a-nuget-package-type"></a>Définir un type de package NuGet

Les packages peuvent être marqués avec un plus grand nombre de *types* de packages pour indiquer l’utilisation prévue.

## <a name="known-package-types"></a>Types de packages connus

- Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).

- `DotnetTool` les packages de type sont des outils .NET qui peuvent être installés par l' [interface CLI dotnet](/dotnet/articles/core/tools/index).

- `Template` les packages de type fournissent des [modèles personnalisés](/dotnet/core/tools/custom-templates) qui peuvent être utilisés pour créer des fichiers ou des projets comme une application, un service, un outil ou une bibliothèque de classes.

Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.

> [!NOTE]
> La prise en charge des types de packages a été ajoutée dans NuGet 3,5.
> Si vous n’avez pas besoin d’un type de package personnalisé, il est préférable de *ne pas* définir explicitement le type de package.
> La valeur par défaut de NuGet `Dependency` est le type quand aucun type n’est spécifié.

## <a name="custom-package-types"></a>Types de packages personnalisés

Vous pouvez marquer votre package avec un ou plusieurs types de packages personnalisés si son utilisation ne correspond pas aux [types de packages connus](#known-package-types).

Par exemple, imaginez que les clients de l' `Contoso` application peuvent installer des extensions. L’application peut exiger que les auteurs d’extension utilisent le type de package personnalisé `ContosoExtension` pour identifier leurs packages comme des extensions appropriées qui suivent les conventions requises.

> [!WARNING]
> Un package avec un type de package personnalisé ne peut pas être installé par Visual Studio ou nuget.exe. Pour plus d’informations, consultez [NuGet/page de démarrage # 10468](https://github.com/NuGet/Home/issues/10468) .

# <a name="using-dotnet-cli"></a>[Utilisation de l’interface CLI dotnet](#tab/dotnet)

Les types de packages peuvent être définis dans le fichier projet ( `.csproj` ) :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Les packages avec plusieurs utilisations prévues peuvent être marqués avec plusieurs types de packages à l’aide du `;` délimiteur :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

La gestion des versions des types de package peut se faire à l’aide d’un `,` délimiteur entre le type de package et sa [`Version`](/dotnet/api/system.version) chaîne :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Utilisation de nuget.exe](#tab/nugetexe)

Les types de package sont définis dans le `.nuspec` fichier au sein d’un `packageTypes\packageType` nœud sous l' `<metadata>` élément :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

Les packages avec plusieurs utilisations prévues peuvent être marqués avec plusieurs types de packages :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

Les types de package peuvent être avec version à l’aide d’une [`Version`](/dotnet/api/system.version) chaîne :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

Le format d’une chaîne de type de package est exactement comme un ID de package. Autrement dit, un type de package est une chaîne ne respectant pas la casse qui correspond à l’expression régulière `^\w+([_.-]\w+)*$` contenant au moins un caractère et au plus 100 caractères.

Si elle est fournie, la version du type de package est une [`Version`](/dotnet/api/system.version) chaîne. La version du type de package est facultative et prend par défaut la valeur `0.0` .
