---
title: Référence de version du package NuGet
description: Des détails précis sur la spécification des numéros de version et des plages pour d’autres packages dont dépend un package NuGet et sur la façon dont les dépendances sont installées.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019994"
---
# <a name="package-versioning"></a>Contrôle de version des packages

Un package spécifique est toujours référencé à l’aide de son identificateur de package et d’un numéro de version exact. Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur NuGet.org dispose de plusieurs douzaines de packages spécifiques disponibles, allant de la version *4.1.10311* à la version *6.1.3* (la dernière version stable) et à une variété de versions préliminaires comme *6.2.0-beta1* .

Lorsque vous créez un package, vous affectez un numéro de version spécifique avec un suffixe de texte en préversion facultatif. En revanche, lors de l’utilisation de packages, vous pouvez spécifier un numéro de version exact ou une plage de versions acceptables.

Dans cette rubrique :

- [Notions de base](#version-basics) sur les versions, y compris les suffixes de préversion.
- [Plages de versions et caractères génériques](#version-ranges-and-wildcards)
- [Numéros de version normalisés](#normalized-version-numbers)

## <a name="version-basics"></a>Notions de base sur les versions

Un numéro de version spécifique se présente sous la forme *major. minor. patch [-suffixe]* , où les composants ont les significations suivantes:

- *Principal*: Modifications avec rupture
- *Mineure*: Nouvelles fonctionnalités, offrant néanmoins une compatibilité descendante
- *Correctif*: Correctifs de bogues à compatibilité descendante uniquement
- *-Suffixe* (facultatif): trait d’Union suivi d’une chaîne désignant une préversion (selon le contrôle de [version sémantique ou la Convention SemVer 1,0](http://semver.org/spec/v1.0.0.html)).

**Exemples :**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org rejette tout téléchargement de package qui ne dispose pas d’un numéro de version exact. La version doit être spécifiée dans le `.nuspec` fichier projet ou utilisé pour créer le package.

### <a name="pre-release-versions"></a>Versions préliminaires

Techniquement parlant, les créateurs de packages peuvent utiliser n’importe quelle chaîne comme suffixe pour désigner une préversion, car NuGet traite une telle version comme une version préliminaire et n’effectue aucune autre interprétation. Autrement dit, NuGet affiche la chaîne de version complète dans n’importe quelle interface utilisateur, en laissant toute interprétation de la signification du suffixe au consommateur.

Cela dit, les développeurs de packages suivent généralement les conventions de nommage reconnues:

- `-alpha`: Version alpha, généralement utilisée pour les travaux en cours et l’expérimentation.
- `-beta`: Version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.
- `-rc`: Version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.

> [!Note]
> NuGet 4.3.0 + prend en charge [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de préversion avec la notation par points, comme dans la version *1.0.1-Build. 23*. La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0. Vous pouvez utiliser un formulaire comme *1.0.1-build23*.

Lors de la résolution des références de package et que plusieurs versions de package diffèrent uniquement par le suffixe, NuGet choisit une version sans suffixe en premier, puis applique la précédence aux versions préliminaires dans l’ordre alphabétique inversé. Par exemple, les versions suivantes sont choisies dans l’ordre exact indiqué:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Contrôle de version de sémantique 2.0.0

Avec NuGet 4.3.0 + et Visual Studio 2017 version 15.3 +, NuGet prend en charge le contrôle de [version sémantique 2.0.0](http://semver.org/spec/v2.0.0.html).

Certaines sémantiques de SemVer v 2.0.0 ne sont pas prises en charge dans les clients plus anciens. NuGet considère qu’une version de package est spécifique à SemVer v 2.0.0 si l’une des affirmations suivantes est vraie:

- L’étiquette de préversion est séparée par des points, par exemple, *1.0.0-alpha. 1*
- La version comporte des métadonnées de build, par exemple, *1.0.0 + githash*

Pour nuget.org, un package est défini en tant que package SemVer v 2.0.0 si l’une des affirmations suivantes est vraie:

- La version du package est conforme à SemVer v 2.0.0, mais pas à SemVer v 1.0.0 conforme, comme défini ci-dessus.
- Les plages de versions de dépendance du package ont une version minimale ou maximale qui est conforme à SemVer v 2.0.0, mais pas à SemVer v 1.0.0 conforme, définie ci-dessus. par exemple, *[1.0.0-alpha. 1,)* .

Si vous chargez un package spécifique à SemVer v 2.0.0 sur nuget.org, le package est invisible pour les clients plus anciens et n’est disponible que pour les clients NuGet suivants:

- NuGet 4.3.0 +
- Visual Studio 2017 version 15.3 +
- Visual Studio 2015 avec [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore. exe (kit de développement logiciel (SDK) .NET 2.0.0 +)

Clients tiers:

- Avenant JetBrains
- Paket version 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Plages de versions et caractères génériques

Lorsque vous faites référence à des dépendances de package, NuGet prend en charge l’utilisation de la notation d’intervalle pour spécifier les plages de versions, résumée comme suit:

| Notation | Règle appliquée | Description |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Version minimale, incluse |
| (1.0,) | x > 1,0 | Version minimale, exclusive |
| [1.0] | x = = 1,0 | Correspondance de version exacte |
| (,1.0] | x ≤ 1,0 | Version maximale, inclusive |
| (,1.0) | x < 1,0 | Version maximale, exclusive |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Plage exacte, inclusive |
| (1.0,2.0) | 1,0 < x < 2,0 | Plage exacte, exclusive |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Version maximale et minimale inclusive mixte |
| (1.0)    | non valide | non valide |

Lors de l’utilisation du format PackageReference, NuGet prend également en charge l' \*utilisation d’une notation générique,, pour les parties de suffixe majeure, mineure, de correctif et de préversion du nombre. Les caractères génériques ne sont pas pris `packages.config` en charge avec le format.

> [!Note]
> Les plages de versions dans PackageReference incluent des versions préliminaires. Par défaut, les versions flottantes ne résolvent pas les versions préliminaires sauf si elles sont activées. Pour connaître l’état de la demande de fonctionnalité associée, consultez le [problème 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Exemples

Spécifiez toujours une version ou une plage de versions pour les dépendances `packages.config` de package dans `.nuspec` les fichiers projet, les fichiers et les fichiers. Sans une version ou une plage de versions, NuGet 2.8. x et les versions antérieures sélectionnent la dernière version disponible du package lors de la résolution d’une dépendance, tandis que NuGet 3. x et versions ultérieures sélectionnent la version de package la plus basse. La spécification d’une version ou d’une plage de versions évite cette incertitude.

#### <a name="references-in-project-files-packagereference"></a>Références dans les fichiers projet (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Références dans `packages.config`:**

Dans `packages.config`, chaque dépendance est indiquée avec un attribut `version` exact qui est utilisé lors de la restauration des packages. L' `allowedVersions` attribut est utilisé uniquement pendant les opérations de mise à jour pour limiter les versions vers lesquelles le package peut être mis à jour.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Références dans `.nuspec` les fichiers**

L' `version` attribut d’un `<dependency>` élément décrit les versions de plage acceptables pour une dépendance.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Numéros de version normalisés

> [!Note]
> Il s’agit d’une modification avec rupture pour NuGet 3,4 et versions ultérieures.

Lors de l’obtention de packages à partir d’un référentiel pendant les opérations d’installation, de réinstallation ou de restauration, NuGet 3.4 + traite les numéros de version comme suit:

- Les zéros non significatifs sont supprimés des numéros de version:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Un zéro dans la quatrième partie du numéro de version sera omis

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`et `restore` les opérations normalisent les versions chaque fois que cela est possible. Pour les packages déjà générés, cette normalisation n’affecte pas les numéros de version dans les packages eux-mêmes. elle affecte uniquement la manière dont NuGet correspond aux versions lors de la résolution des dépendances.

Toutefois, les dépôts de packages NuGet doivent traiter ces valeurs de la même façon que NuGet pour empêcher la duplication de version de package. Par conséquent, un référentiel qui contient la version *1,0* d’un package ne doit pas héberger également la version *1.0.0* comme un package distinct et différent.
