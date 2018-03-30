---
title: Format PackageReference NuGet (références de package dans des fichiers projet) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
keywords: Dépendances de package NuGet, références de package, fichiers projet, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Références de package (PackageReference) dans les fichiers projet

Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé. L’utilisation de PackageReference n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.Config` (notamment les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](configuring-nuget-behavior.md).

Avec PackageReference, vous pouvez aussi utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework, configuration, plateforme ou autre type de regroupement. Elle permet également de mieux contrôler les dépendances et les flux de contenu. Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).

Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP. Les projets .NET Framework Full prennent en charge PackageReference, mais utilisent par défaut `packages.config`. Pour utiliser PackageReference, migrez les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.

## <a name="adding-a-packagereference"></a>Ajout d’un PackageReference

Ajoutez une dépendance dans votre fichier projet en utilisant la syntaxe suivante :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Contrôle des versions des dépendances

Pour spécifier la version d’un package, la convention est la même que pour `packages.config` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="floating-versions"></a>Versions flottantes

Les [versions flottantes](../consume-packages/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Contrôle des ressources de dépendance

Vous pouvez utiliser une dépendance uniquement comme un atelier de développement et ne pas l’exposer aux projets qui utilisent votre package. Dans ce scénario, vous pouvez utiliser les métadonnées `PrivateAssets` pour contrôler ce comportement.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Les balises de métadonnées suivantes permettent de contrôler les ressources de dépendance :

| Balise | Description | Valeur par défaut |
| --- | --- | --- |
| IncludeAssets | Ces ressources sont consommées. | toutes les |
| ExcludeAssets | Ces ressources ne sont pas consommées. | aucun |
| PrivateAssets | Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent. | contentfiles;analyzers;build |

Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :

| Value | Description |
| --- | ---
| compile | Contenu du dossier `lib` |
| runtime | Contenu du dossier `runtimes` |
| contentFiles | Contenu du dossier `contentfiles` |
| build | Propriétés et cibles du dossier `build` |
| analyzers | Analyseurs .NET |
| natifs | Contenu du dossier `native` |
| aucun | Aucune des valeurs ci-dessus n’est utilisée. |
| toutes les | Toutes les valeurs ci-dessus sont utilisées (sauf `none`) |

Dans l’exemple suivant, tout (à l’exception des fichiers de contenu du package) est consommé par le projet et tout (à l’exception des fichiers de contenu et des analyseurs) est acheminé vers le projet parent.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Étant donné que `build` n’est pas inclus dans `PrivateAssets`, les cibles et les propriétés *sont acheminées* vers le projet parent. Imaginons, par exemple, que la référence ci-dessus soit utilisée dans un projet qui crée un package NuGet appelé AppLogger. AppLogger peut consommer les cibles et les propriétés de `Contoso.Utility.UsefulStuff`, tout comme les projets peuvent consommer AppLogger.

## <a name="adding-a-packagereference-condition"></a>Ajout d’une condition PackageReference

Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles. Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.

Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`. Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile. Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.json est inclus en tant que dépendance uniquement pour une cible `net452` :

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
