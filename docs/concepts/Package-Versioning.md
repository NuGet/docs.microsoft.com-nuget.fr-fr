---
title: Référence de version de package NuGet
description: Détails exacts sur la spécification des numéros de version et des plages pour les autres packages dont dépend un package NuGet, et comment les dépendances sont installées.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5ba7860fae1037c0c0eb4c55d2df12d98b1d77cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775119"
---
# <a name="package-versioning"></a>Contrôle de version des packages

Un package spécifique est toujours référencé à l'aide de son identificateur de package et d'un numéro de version exact. Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur nuget.org propose plusieurs dizaines de packages spécifiques disponibles, allant de la version *4.1.10311* à la version *6.1.3*. (la dernière version stable) et une variété de préversions comme *6.2.0-beta1*.

Lors de la création d'un package, vous attribuez un numéro de version spécifique avec un suffixe de texte de préversion optionnel. En revanche, lorsque vous consommez des packages, vous pouvez spécifier un numéro de version exact ou une plage de versions acceptables.

Dans cette rubrique :

- [Principes de base d’une version](#version-basics), y compris les suffixes de préversion.
- [Plages de versions](#version-ranges)
- [Numéros de version normalisés](#normalized-version-numbers)

## <a name="version-basics"></a>Principes de base d’une version

Un numéro de version spécifique se présente sous la forme *Major.Minor.Patch[-Suffix]*, où les composants ont la signification suivante :

- *Majeure*: modifications avec rupture
- *Mineure*: nouvelles fonctionnalités, mais à compatibilité descendante
- *Patch*: correctifs de bogues à compatibilité descendante uniquement
- *-Suffix* (optionnel) : un trait d'union suivi d'une chaîne de caractères indiquant une version préversion (suivant la convention [Semantic Versioning ou SemVer 1.0](https://semver.org/spec/v1.0.0.html)).

**Exemples :**

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> nuget.org rejette tout upload de package sans numéro de version exact. La version doit être spécifiée dans le fichier `.nuspec` ou fichier projet utilisé pour créer le package.

### <a name="pre-release-versions"></a>Préversions

Techniquement parlant, les créateurs de packages peuvent utiliser n'importe quelle chaîne de caractères comme suffixe pour désigner une préversion car NuGet traite une telle version comme une préversion et ne fait aucune autre interprétation. En d'autres termes, NuGet affiche la chaîne de caractères de la version complète, quelle que soit l'interface utilisateur concernée, laissant au consommateur le soin d'interpréter la signification du suffixe.

Cela dit, les développeurs de packages adoptent généralement des conventions d’affectation de noms reconnues :

- `-alpha`: Version alpha, généralement utilisée pour les travaux en cours et l’expérimentation.
- `-beta`: version beta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.
- `-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.

> [!Note]
> NuGet 4.3.0+ prend en charge [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de préversion utilisant la notation à points (par exemple, *1.0.1-build.23*). La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0. Vous pouvez utiliser un format comme *1.0.1-build23*.

Lorsque vous résolvez des références de packages et que plusieurs versions de packages ne diffèrent que par le suffixe, NuGet choisit d'abord une version sans suffixe, puis applique la priorité aux préversions dans l'ordre alphabétique inverse. Par exemple, les versions suivantes seraient choisies dans l'ordre exact indiqué :

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

Avec NuGet 4.3.0+ et Visual Studio 2017 version 15.3+, NuGet prend en charge [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

Certaines sémantiques de SemVer 2.0.0 ne sont pas prises en charge dans les clients plus anciens. NuGet considère une version de package comme spécifique à SemVer 2.0.0 si l'un des énoncés suivants est vrai :

- L'étiquette de préversion est séparée par des points, par exemple, *1.0.0-alpha.1*
- La version contient des métadonnées de build, par exemple, *1.0.0+githash*

Pour nuget.org, un package est défini comme un package SemVer 2.0.0 si l'un des énoncés suivants est vrai :

- La propre version du package est conforme à SemVer 2.0.0 mais pas à SemVer 1.0.0, comme défini ci-dessus.
- Toutes les plages de versions des dépendances du package ont une version minimale ou maximale conforme à SemVer 2.0.0 mais non conforme à SemVer 1.0.0, définie ci-dessus ; par exemple, *[1.0.0-alpha.1, )*.

Si vous uploadez un package spécifique à SemVer 2.0.0 sur nuget.org, le package est invisible pour les anciens clients et disponible uniquement pour les clients NuGet suivants :

- NuGet 4.3.0+
- Visual Studio 2017 15.3+
- Visual Studio 2015 with [NuGet VSIX 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Clients tiers :

- JetBrains Rider
- Paket version 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Plages de versions

Lorsque NuGet fait référence à des dépendances de packages, il prend en charge l'utilisation de la notation d'intervalle pour spécifier les plages de versions, résumées comme suit :

| Notation | Règle appliquée | Description |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Version minimale, inclusive |
| (1.0,) | x > 1.0 | Version minimale, exclusive |
| [1.0] | x == 1.0 | Correspondance exacte des versions |
| (,1.0] | x ≤ 1.0 | Version maximale, inclusive |
| (,1.0) | x < 1.0 | Version maximale, exclusive |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Plage exacte, inclusive |
| (1.0,2.0) | 1.0 < x < 2.0 | Plage exacte, exclusive |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Version maximum exclusive et minimum inclusive mixte |
| (1.0)    | non valide | non valide |

Lors de l’utilisation du format PackageReference, NuGet prend également en charge l’utilisation d’une notation flottante, \* , pour les parties de suffixe majeure, mineure, de correctif et de préversion du nombre. Les versions flottantes ne sont pas prises en charge avec le `packages.config` format. Quand une version flottante est spécifiée, la règle doit être résolue en la version existante la plus élevée qui correspond à la description de la version. Vous trouverez ci-dessous des exemples de versions flottantes et de résolution.

> [!Note]
> Les plages de versions dans PackageReference incluent des préversions. De par leur conception, les versions flottantes ne résolvent pas les préversions à moins que vous ne l’ayez décidé. Pour connaître l'état de la demande de fonctionnalité associée, voir le [problème 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Exemples

Spécifiez toujours une version ou une plage de versions pour les dépendances de packages dans les fichiers projet, les fichiers `packages.config` et les fichiers `.nuspec`. Sans version ou plage de versions, NuGet 2.8.x (et versions antérieures) choisit la dernière version de package disponible lors de la résolution d'une dépendance, tandis que NuGet 3.x (et versions ultérieures) sélectionne la version de package la plus basse. La spécification d'une version ou d'une plage de versions permet de lever ce doute.

#### <a name="references-in-project-files-packagereference"></a>Références dans les fichiers projet (PackageReference)

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a>Résolutions de version flottante 

| Version | Versions présentes sur le serveur | Résolution | Motif | Notes |
|----------|--------------|-------------|-------------|-------------|
| * | 1.1.0 <br> 1.1.1 <br> 1.2.0 <br> 1.3.0-alpha  | 1.2.0 | Version stable la plus élevée. |
| 1.1.* | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.2.0-alpha | 1.1.1 | Version stable la plus élevée qui respecte le modèle spécifié.|
| * - * | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.3.0-beta  | 1.3.0-beta | La version la plus élevée, y compris les versions non stables. | Disponible dans Visual Studio version 16,6, NuGet version 5,6, kit SDK .NET Core version 3.1.300 |
| 1.1. *-* | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.1.2-beta <br> 1.3.0-beta  | 1.1.2-beta | Version la plus élevée respectant le modèle et incluant les versions non stables. | Disponible dans Visual Studio version 16,6, NuGet version 5,6, kit SDK .NET Core version 3.1.300 |

**Références dans `packages.config` :**

dans `packages.config`, chaque dépendance est répertoriée avec un attribut `version` exact utilisé lors de la restauration des packages. L'attribut `allowedVersions` n'est utilisé que pendant les opérations de mise à jour afin de limiter les versions avec lesquelles le package peut être mis à jour.

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

**Références dans les fichiers `.nuspec`**

L'attribut `version` d'un élément `<dependency>` décrit les versions de plage acceptables pour une dépendance.

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
> Il s’agit d’un changement important pour NuGet 3.4 et versions ultérieures.

Lorsque vous obtenez des packages à partir d'un référentiel pendant l'installation, la réinstallation ou la restauration, NuGet 3.4+ traite les numéros de version comme suit :

- Les zéros non significatifs sont supprimés des numéros de version :

  1.00 est traité comme 1.0 1.01.1 est traité comme 1.1.1 1.00.0.1 est traité comme 1.0.0.1

- Un zéro dans la quatrième partie du numéro de version sera omis

  1.0.0.0 est traité comme 1.0.0 1.0.01.0 est traité comme 1.0.1

- Suppression des métadonnées de build SemVer 2.0.0

  1.0.7 + r3456 est traité comme 1.0.7

Les opérations `pack` et `restore` normalisent les versions lorsque cela est possible. Pour les packages déjà construits, cette normalisation n'affecte pas les numéros de version dans les packages eux-mêmes ; elle affecte uniquement la façon dont NuGet mappe les versions lors de la résolution des dépendances.

Cependant, les dépôts de packages NuGet doivent traiter ces valeurs de la même manière que NuGet pour éviter la duplication des versions de packages. Ainsi, un référentiel qui contient la version *1.0* d'un package ne doit pas également héberger la version *1.0.0* comme un package séparé et différent.
