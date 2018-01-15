---
title: "Références de package (PackageReference) NuGet dans les fichiers projet Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Informations détaillées sur les références de package (PackageReference) NuGet dans les fichiers projet pris en charge par NuGet 4.0+ et Visual Studio 2017"
keywords: "Dépendances de package NuGet, références de package, fichiers projet, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Références de package (PackageReference) dans les fichiers projet

En utilisant le nœud `PackageReference`, les références de package permettent de gérer les dépendances NuGet directement dans les fichiers projet, ce qui évite d’avoir à utiliser un fichier `packages.config` ou `project.json` séparé. Cette méthode n’affecte pas les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.Config` (y compris les sources de package) continuent d’être appliqués, comme expliqué dans [Configuration du comportement de NuGet](Configuring-NuGet-Behavior.md).

> [!Important]
> Actuellement, les références de package sont prises en charge uniquement dans Visual Studio 2017 pour les projets .NET Core, .NET Standard et UWP qui ciblent Windows 10 build 15063 (Creators Update).

L’approche `PackageReference` vous permet d’utiliser des conditions MSBuild pour choisir des références de package par version cible du .NET Framework, par configuration, par plateforme ou autre type de regroupement. Elle permet également de mieux contrôler les dépendances et les flux de contenu. Au niveau du comportement et de la [résolution des dépendances](Dependency-Resolution.md), cela revient à utiliser `project.json`.

Pour plus d’informations sur l’intégration de MSBuild aux références de package des fichiers projet, consultez [Commandes pack et restore NuGet en tant que cibles MSBuild](../schema/msbuild-targets.md).

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

Pour spécifier la version d’un package, la convention est la même que celle utilisée pour `packages.config` ou `project.json` :

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
| runtime | Contenu du dossier `runtime` |
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
