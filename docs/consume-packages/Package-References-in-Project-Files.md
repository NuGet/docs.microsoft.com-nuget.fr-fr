---
title: Format PackageReference NuGet (références de package dans des fichiers projet)
description: Cet article donne des informations détaillées sur le format PackageReference NuGet dans les fichiers projet, pris en charge par NuGet 4.0 (et versions ultérieures), Visual Studio 2017 et .NET Core 2.0.
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: dcaed83ca54e3234702e963ffc2ebbde4cd75b28
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235761"
---
# <a name="package-references-packagereference-in-project-files"></a>Références de package (PackageReference) dans les fichiers projet

Les références de package utilisent le nœud `PackageReference` pour gérer les dépendances NuGet directement dans les fichiers projet, et non un fichier `packages.config` séparé. L’utilisation de PackageReference n’a pas d’impact sur les autres aspects de NuGet. Par exemple, les paramètres des fichiers `NuGet.config` (notamment les sources de packages) continuent d’être appliqués, comme cela est expliqué dans [Configurations courantes de NuGet](configuring-nuget-behavior.md).

Avec PackageReference, vous pouvez également utiliser des conditions MSBuild pour choisir des références de package par version cible de .NET Framework ou d’autres regroupements. Elle permet également de mieux contrôler les dépendances et les flux de contenu. Pour plus d’informations, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).

## <a name="project-type-support"></a>Prise en charge de type de projet

Par défaut, PackageReference est utilisé pour les projets .NET Core, les projets .NET Standard et les projets UWP ciblant Windows 10 Build 15063 (Creators Update) et version ultérieure, excepté les projets C++ UWP. Les projets .NET Framework prennent en charge PackageReference, mais utilisent par défaut `packages.config`. Pour utiliser PackageReference, [migrez](../consume-packages/migrate-packages-config-to-package-reference.md) les dépendances de `packages.config` dans votre fichier projet, puis supprimez packages.config.

Les applications ASP.NET ciblant le .NET Framework incluent uniquement une [prise en charge limitée](https://github.com/NuGet/Home/issues/5877) pour PackageReference. Les types de projets C++ et JavaScript ne sont pas pris en charge.

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

Dans l’exemple ci-dessus, 3.6.0 correspond à n’importe quelle version supérieure ou égale à 3.6.0, avec une préférence pour la version la plus ancienne, comme décrit dans [Gestion des versions de package](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Utilisation de PackageReference pour un projet sans PackageReferences

Avancé : Si vous n’avez aucun package installé dans un projet (aucune PackageReferences dans le fichier projet et aucun fichier packages.config), mais que vous souhaitez restaurer le projet en tant que style PackageReference, vous pouvez définir une propriété de projet RestoreProjectStyle avec la valeur PackageReference dans votre fichier projet.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Cela peut être utile si vous référencez des projets qui sont de style PackageReference (projets csproj ou de style SDK existants). Cela permet aux packages auxquels ces projets font référence d’être référencés « transitivement » par votre projet.

## <a name="packagereference-and-sources"></a>PackageReference et sources

Dans les projets PackageReference, les versions de dépendances transitives sont résolues au moment de la restauration. Par conséquent, dans les projets PackageReference, toutes les sources doivent être disponibles pour toutes les restaurations. 

## <a name="floating-versions"></a>Versions flottantes

Les [versions flottantes](../concepts/dependency-resolution.md#floating-versions) peuvent être utilisées avec `PackageReference` :

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

| Tag | Description | Valeur par défaut |
| --- | --- | --- |
| IncludeAssets | Ces ressources sont consommées. | all |
| ExcludeAssets | Ces ressources ne sont pas consommées. | aucun |
| PrivateAssets | Ces ressources sont consommées, mais ne sont pas acheminées vers le projet parent. | contentfiles;analyzers;build |

Les valeurs autorisées pour ces balises sont les suivantes (les valeurs multiples doivent être séparées par un point-virgule, à l’exception de `all` et de `none` qui doivent s’afficher seules) :

| Valeur | Description |
| --- | ---
| compile | Contenu du dossier `lib` et contrôles permettant de déterminer si votre projet peut être compilé avec les assemblys dans le dossier |
| runtime | Contenu des dossiers `lib` et `runtimes` contrôles permettant de déterminer si ces assemblys seront copiés vers le répertoire de sortie de build |
| contentFiles | Contenu du dossier `contentfiles` |
| build | `.props` et `.targets` dans le dossier `build` |
| buildMultitargeting | *(4.0)* `.props` et `.targets` dans le dossier `buildMultitargeting`, pour le ciblage multi-infrastructures |
| buildTransitive | *(5.0 +)* `.props` et `.targets` dans le dossier `buildTransitive`, pour les ressources qui circulent de manière transitive vers n’importe quel projet consommateur. Consultez la page [Fonctionnalité](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). |
| analyzers | Analyseurs .NET |
| native | Contenu du dossier `native` |
| aucun | Aucune des valeurs ci-dessus n’est utilisée. |
| all | Toutes les valeurs ci-dessus sont utilisées (sauf `none`) |

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

> [!NOTE]
> Si la propriété `developmentDependency` est définie sur `true` dans un fichier `.nuspec`, elle marque un package comme dépendance de développement uniquement, ce qui l’empêche d’être inclus en tant que dépendance dans d’autres packages. Avec PackageReference *(NuGet 4.8+)*, cet indicateur signifie également que la propriété exclura les ressources de la compilation. Pour plus d'informations, voir [Prise en charge de DevelopmentDependency pour PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Ajout d’une condition PackageReference

Vous pouvez utiliser une condition pour contrôler si un package doit être inclus, ainsi que l’endroit où les conditions peuvent utiliser une variable MSBuild ou une variable définie dans le fichier de propriétés ou de cibles. Toutefois, à l’heure actuelle, seule la variable `TargetFramework` est prise en charge.

Par exemple, supposons que vous souhaitiez cibler `netstandard1.4` et `net452`, mais que l’une de vos dépendances ne s’applique qu’à `net452`. Dans ce cas, il n’est pas souhaitable qu’un projet `netstandard1.4` utilise votre package pour ajouter cette dépendance inutile. Pour éviter cela, spécifiez une condition sur `PackageReference` de la façon suivante :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Dans un package créé à l’aide de ce projet, le fichier Newtonsoft.Json est inclus en tant que dépendance uniquement pour une cible `net452` :

![Résultat de l’application d’une condition à PackageReference avec VS2017](media/PackageReference-Condition.png)

Les conditions peuvent également être appliquées au niveau d’un `ItemGroup`, à tous les éléments enfants `PackageReference` :

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Cette fonctionnalité est disponible avec NuGet **5,0** ou version ultérieure et avec Visual Studio 2019 **16,0** ou version ultérieure.

Il est parfois souhaitable de référencer des fichiers dans un package à partir d’une cible MSBuild.
Dans `packages.config` les projets basés sur, les packages sont installés dans un dossier relatif au fichier projet. Toutefois, dans PackageReference, les packages sont [consommés](../concepts/package-installation-process.md) à partir du dossier *Global-packages* , qui peut varier d’un ordinateur à l’ordinateur.

Pour combler ce fossé, NuGet a introduit une propriété qui pointe vers l’emplacement à partir duquel le package sera consommé.

Exemple :

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

En outre, NuGet génère automatiquement les propriétés des packages contenant un dossier Tools.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

Les propriétés MSBuild et les identités de package n’ont pas les mêmes restrictions afin que l’identité du package doive être remplacée par un nom convivial MSBuild, préfixé par le mot `Pkg` .
Pour vérifier le nom exact de la propriété générée, examinez le fichier [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) généré.

## <a name="packagereference-aliases"></a>Alias PackageReference

Dans certains cas rares, différents packages contiendront des classes dans le même espace de noms. À compter de NuGet 5,7 & Visual Studio 2019 Update 7, équivalent à ProjectReference, PackageReference prend en charge [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .
Par défaut, aucun alias n’est fourni. Lorsqu’un alias est spécifié, *tous les* assemblys provenant du package annoté doivent être référencés avec un alias.

Vous pouvez examiner l’utilisation de l’exemple sur [NuGet\Samples](https://github.com/NuGet/Samples/tree/master/PackageReferenceAliasesExample)

Dans le fichier projet, spécifiez les alias comme suit :

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

et dans le code, utilisez-le comme suit :

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>Avertissements et erreurs NuGet

*Cette fonctionnalité est disponible avec NuGet **4,3** ou version ultérieure et avec Visual Studio 2017 **15,3** ou version ultérieure.*

Pour de nombreux scénarios de packs et de restaurations, tous les avertissements et erreurs NuGet sont codés, et commencent par `NU****` . Toutes les erreurs et avertissements NuGet sont répertoriés dans la documentation de [référence](../reference/errors-and-warnings.md) .

NuGet observe les propriétés d’avertissement suivantes :

- `TreatWarningsAsErrors`, considérer tous les avertissements comme des erreurs
- `WarningsAsErrors`, traiter des avertissements spécifiques comme des erreurs
- `NoWarn`, masquez des avertissements spécifiques, à l’ensemble du projet ou à l’ensemble du package.

Exemples :

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Suppression des avertissements NuGet

Bien qu’il soit recommandé de résoudre tous les avertissements NuGet au cours de vos opérations de Pack et de restauration, il est justifié, dans certaines situations, de les supprimer.
Pour supprimer un projet d’avertissement en largeur, envisagez d’effectuer les opérations suivantes :

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Parfois, les avertissements s’appliquent uniquement à un package donné du graphique. Nous pouvons choisir de supprimer cet avertissement de manière plus sélective en ajoutant un `NoWarn` sur l’élément PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Suppression des avertissements du package NuGet dans Visual Studio

Dans Visual Studio, vous pouvez également [supprimer des avertissements](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) par le biais de l’IDE.

## <a name="locking-dependencies"></a>Verrouillage des dépendances

*Cette fonctionnalité est disponible avec NuGet **4.9** ou ultérieur, et avec Visual Studio 2017 **15.9** ou ultérieur.*

L’entrée de la restauration NuGet est un ensemble de références de package provenant du fichier de projet (dépendances de niveau supérieur ou directes). La sortie est une fermeture complète de toutes les dépendances de package, notamment les dépendances transitives. NuGet s’efforce toujours de produire la même fermeture complète des dépendances de package si la liste PackageReference d’entrée ne change pas. Toutefois, tous les scénarios ne s’y prêtent pas. Par exemple :

* Quand vous utilisez des versions flottantes comme `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. L’intention ici est de flotter vers la dernière version à chaque restauration de package. Mais dans certains scénarios, les utilisateurs peuvent exiger le verrouillage du graphe à une version récente donnée et son flottement vers une version ultérieure, si celle-ci est disponible, à la suite d’un mouvement explicite.
* Une version plus récente du package correspondant aux exigences de version de PackageReference est publiée. Par exemple, 

  * Premier jour : Vous spécifiez `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, mais les versions disponibles sur les dépôts NuGet sont 4.1.0, 4.2.0 et 4.3.0. Dans ce cas, NuGet résout la version en 4.1.0 (la plus proche de la version minimale).

  * Deuxième jour : La version 4.0.0 est publiée. NuGet trouve désormais la correspondance exacte et commence à résoudre la version en 4.0.0.

* Une version de package donnée est supprimée du dépôt. Bien que nuget.org n’autorise pas la suppression de packages, d’autres dépôts de packages n’ont pas cette contrainte. NuGet trouve donc la meilleure correspondance quand la version supprimée rend impossible la résolution.

### <a name="enabling-lock-file"></a>Activation du fichier de verrouillage

Pour rendre persistante la fermeture complète des dépendances de package, vous pouvez choisir d’utiliser la fonctionnalité de fichier de verrouillage en définissant la propriété MSBuild `RestorePackagesWithLockFile` pour votre projet :

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Si cette propriété est définie, la restauration NuGet génère un fichier de verrouillage (`packages.lock.json`) au niveau du répertoire racine du projet qui liste toutes les dépendances du package. 

> [!Note]
> Quand un projet a un fichier `packages.lock.json` dans son répertoire racine, le fichier de verrouillage est toujours utilisé avec la restauration, même si la propriété `RestorePackagesWithLockFile` n’est pas définie. Une autre façon de choisir cette fonctionnalité consiste à créer un fichier `packages.lock.json` vide factice dans le répertoire racine du projet.

### <a name="restore-behavior-with-lock-file"></a>Comportement de `restore` avec fichier de verrouillage
Si un fichier de verrouillage est présent pour le projet, NuGet utilise ce fichier de verrouillage pour exécuter `restore`. NuGet effectue une vérification rapide pour voir si les dépendances de package ont changé, comme indiqué dans le fichier projet (ou les fichiers des projets dépendants). Si aucun changement n’est détecté, il restaure simplement les packages mentionnés dans le fichier de verrouillage. Les dépendances de package ne sont pas réévaluées.

Si NuGet détecte un changement dans les dépendances définies indiquées dans le ou les fichiers projet, il réévalue le graphe du package et met à jour le fichier de verrouillage pour refléter la nouvelle fermeture de package du projet.

Dans CI/CD et d’autres scénarios où vous ne voulez pas changer les dépendances de package à la volée, vous pouvez définir `lockedmode` avec la valeur `true` :

Pour dotnet.exe, exécutez :

```
> dotnet.exe restore --locked-mode
```

Pour msbuild.exe, exécutez :

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Vous pouvez également définir cette propriété MSBuild conditionnelle dans votre fichier projet :

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Si le mode verrouillé est `true`, soit la restauration restaure les packages exacts figurant dans la liste du fichier de verrouillage, soit elle échoue si vous avez mis à jour les dépendances de package définies pour le projet une fois le fichier de verrouillage créé.

### <a name="make-lock-file-part-of-your-source-repository"></a>Intégrer le fichier de verrouillage dans votre dépôt source
Si vous générez un exécutable d’application et que le projet en question se trouve à la début de la chaîne de dépendance, archivez le fichier de verrouillage dans le dépôt de code source pour que NuGet puisse l’utiliser durant la restauration.

Toutefois, si votre projet est un projet de bibliothèque que vous ne prévoyez pas de distribuer ou un projet de code commun dont dépendent d’autres projets, **n’archivez pas** le fichier de verrouillage dans le cadre de votre code source. Le fait de conserver le fichier de verrouillage ne pose aucun risque. Toutefois, vous ne pouvez pas utiliser les dépendances de package verrouillées pour le projet de code commun, qui figurent dans la liste du fichier de verrouillage, durant la restauration/génération d’un projet qui dépend de ce projet de code commun.

par exemple

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Si `ProjectA` a une dépendance à un `PackageX` version `2.0.0` et qu’il référence également `ProjectB` qui dépend de `PackageX` version `1.0.0`, le fichier de verrouillage pour `ProjectB` liste une dépendance à `PackageX` version `1.0.0`. Toutefois, lorsque `ProjectA` est généré, son fichier de verrouillage contient une dépendance sur `PackageX` **`2.0.0`** la version **et non** `1.0.0` dans le fichier de verrouillage pour `ProjectB` . Le fichier de verrouillage d’un projet de code commun a donc peu de contrôle sur les packages résolus pour les projets qui en dépendent.

### <a name="lock-file-extensibility"></a>Extensibilité du fichier de verrouillage

Vous pouvez contrôler divers comportements de restauration avec un fichier de verrouillage, comme décrit ci-dessous :

| Option NuGet.exe | option dotnet | Option MSBuild équivalente | Description |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Opte pour l’utilisation d’un fichier de verrouillage. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Active le mode verrouillé pour la restauration. Cela est utile dans les scénarios d’intégration continue et de livraison continue dans lesquels vous souhaitez créer des builds reproductibles.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Cette option est utile avec des packages dont la version flottante est définie dans le projet. Par défaut, NuGet Restore ne met pas à jour automatiquement la version du package lors de chaque restauration, sauf si vous exécutez Restore avec cette option. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Définit un emplacement de fichier de verrouillage personnalisé pour un projet. Par défaut, NuGet prend en charge `packages.lock.json` au niveau du répertoire racine. Si vous avez plusieurs projets dans le même répertoire, NuGet prend en charge le fichier de verrouillage `packages.<project_name>.lock.json` spécifique au projet. |

## <a name="assettargetfallback"></a>AssetTargetFallback

La `AssetTargetFallback` propriété vous permet de spécifier des versions de Framework compatibles supplémentaires pour les projets que votre projet référence et les packages NuGet que votre projet utilise.

Si vous spécifiez une dépendance de package à l’aide de `PackageReference` , mais que ce package ne contient pas les ressources qui sont compatibles avec le Framework cible de votre projet, la `AssetTargetFallback` propriété entre en lecture. La compatibilité du package référencé est revérifiée à l’aide de chaque version cible de .NET Framework spécifiée dans `AssetTargetFallback` .
Quand un `project` ou un `package` est référencé par le biais de `AssetTargetFallback` , l’avertissement [NU1701](../reference/errors-and-warnings/NU1701.md) est déclenché.

Reportez-vous au tableau ci-dessous pour obtenir des exemples d' `AssetTargetFallback` impact sur la compatibilité.

| Infrastructure de projet | AssetTargetFallback | Infrastructures de package | Résultats |
|-------------------|---------------------|--------------------|--------|
| .NET Framework 4.7.2 | | .NET Standard 2.0 | .NET Standard 2.0 |
| Application .NET Core 3,1 | | .NET Standard 2,0, .NET Framework 4.7.2 | .NET Standard 2.0 |
| Application .NET Core 3,1 | | .NET Framework 4.7.2 | Incompatible, échec avec [`NU1202`](../reference/errors-and-warnings/NU1202.md) |
| Application .NET Core 3,1 | net472;net471 | .NET Framework 4.7.2 | .NET Framework 4.7.2 avec [`NU1701`](../reference/errors-and-warnings/NU1701.md) |

Plusieurs infrastructures peuvent être spécifiées à l’aide de `;` comme délimiteur. Pour ajouter une infrastructure de secours, vous pouvez effectuer les opérations suivantes :

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

Vous pouvez abandonner `$(AssetTargetFallback)` si vous souhaitez remplacer les valeurs existantes au lieu de les ajouter `AssetTargetFallback` .

> [!NOTE]
> Si vous utilisez un [projet basé sur le kit de développement logiciel (SDK) .net](/dotnet/core/sdk), les `$(AssetTargetFallback)` valeurs appropriées sont configurées et vous n’avez pas besoin de les définir manuellement.
>
> `$(PackageTargetFallback)` était une fonctionnalité antérieure qui tentait de résoudre ce problème, mais elle est radicalement rompue et ne *doit* pas être utilisée. Pour migrer de `$(PackageTargetFallback)` vers `$(AssetTargetFallback)` , il vous suffit de modifier le nom de la propriété.
