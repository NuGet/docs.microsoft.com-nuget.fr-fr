---
title: Référence de Version de Package NuGet
description: Obtenir des détails précis sur la spécification des numéros de version et de plages pour les autres packages qui dépend d’un package NuGet, et comment les dépendances sont installées.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549771"
---
# <a name="package-versioning"></a>Contrôle de version des packages

Un package spécifique est toujours appelé à l’aide de son identificateur de package et un numéro de version exact. Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur nuget.org a plusieurs dizaines des packages spécifiques disponibles, allant de version *4.1.10311* vers la version *6.1.3* (la dernière stable mise en production) et une variété de versions préliminaires comme *6.2.0-beta1*.

Lorsque vous créez un package, vous affectez un numéro de version spécifique avec un suffixe facultatif en version préliminaire. En revanche, lors de l’utilisation des packages, vous pouvez spécifier un numéro de version exact ou une plage de versions acceptables.

Dans cette rubrique :

- [Principes de base version](#version-basics) , y compris des suffixes de la version préliminaire.
- [Caractères génériques et les plages de versions](#version-ranges-and-wildcards)
- [Numéros de version normalisée](#normalized-version-numbers)

## <a name="version-basics"></a>Principes fondamentaux de version

Un numéro de version spécifique se présente sous la forme *version_principale.version_secondaire.version_corrective [-suffixe]*, où les composants ont les significations suivantes :

- *Principales*: modifications avec rupture
- *Mineure*: nouvelles fonctionnalités, mais offre une compatibilité descendante
- *Correctif*: uniquement les correctifs de bogues offre une compatibilité descendante
- *-Suffixe* (facultatif) : un trait d’union suivie d’une chaîne qui dénote une version préliminaire (suivant la [convention Semver ou SemVer 1.0](http://semver.org/spec/v1.0.0.html)).

**Exemples :**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org rejette tout chargement du package qui ne dispose pas d’un numéro de version exact. La version doit être spécifiée dans le `.nuspec` ou le fichier projet utilisé pour créer le package.

### <a name="pre-release-versions"></a>Versions préliminaires

Techniquement parlant, créateurs de package peuvent utiliser n’importe quelle chaîne comme suffixe pour désigner une version préliminaire, que NuGet traite n’importe quelle version de ce type en tant que version préliminaire et aucune autre interprétation a fait. Autrement dit, NuGet les affiche la version complète de chaîne dans toute l’interface utilisateur est impliquée, en laissant toute interprétation du sens du suffixe au consommateur.

Ceci dit, les développeurs de packages suivent généralement les conventions de nommage reconnues :

- `-alpha`: Version alpha, généralement utilisée pour les travaux en cours et l’expérimentation.
- `-beta`: version bêta, comprenant généralement toutes les fonctionnalités de la prochaine version planifiée, mais pouvant contenir des bogues connus.
- `-rc` : version Release Candidate, généralement une version potentiellement finale (stable), sauf si des bogues importants apparaissent.

> [!Note]
> Prend en charge de NuGet 4.3.0 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de version préliminaire avec la notation à points, comme dans *1.0.1-build.23*. La notation à points n’est pas prise en charge avec les versions de NuGet antérieures à 4.3.0. Vous pouvez utiliser un format similaire à *1.0.1-build23*.

Lors de la résolution des références de package et de plusieurs versions de package diffèrent uniquement par le suffixe, NuGet choisit une version sans suffixe tout d’abord, puis applique la priorité pour les versions préliminaires dans l’ordre alphabétique inverse. Par exemple, les versions suivantes seraient choisies dans l’ordre exact indiqué :

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semver 2.0.0

Avec NuGet 4.3.0 et Visual Studio 2017 version 15.3 +, NuGet prend en charge [Semver 2.0.0](http://semver.org/spec/v2.0.0.html).

Les clients plus anciens ne prend pas en charge certaine sémantique de version de SemVer 2.0.0. NuGet prend en compte une version de package à être SemVer v2.0.0 spécifique si une des affirmations suivantes est vraie :

- L’étiquette de version préliminaire est séparé par un point, par exemple, *1.0.0-alpha.1*
- La version a des métadonnées de la build, par exemple, *1.0.0+githash*

Pour nuget.org, un package est défini comme un package de version 2.0.0 SemVer si une des affirmations suivantes est vraie :

- La version du package est v2.0.0 SemVer conforme mais pas SemVer v1.0.0 conforme, tel que défini ci-dessus.
- Une des plages de versions de dépendance du package a une version minimale ou maximale est SemVer v2.0.0 conforme mais pas SemVer v1.0.0 conforme, défini ci-dessus ; par exemple, *[1.0.0-alpha.1,)*.

Si vous téléchargez un package spécifique à la version 2.0.0 de SemVer sur nuget.org, le package est invisible aux clients plus anciens et disponible pour seulement les clients NuGet suivants :

- NuGet 4.3.0
- Visual Studio 2017 version 15.3 +
- Visual Studio 2015 avec [v3.6.0 d’extension VSIX NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (Kit de développement logiciel .NET 2.0.0+)

Les clients tiers :

- Avenant de JetBrains
- Paket version 5.0 et versions ultérieures

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Caractères génériques et les plages de versions

Lorsque vous faites référence aux dépendances de package, NuGet prend en charge à l’aide de la notation de l’intervalle pour la spécification de plages de versions, résumées comme suit :

| Notation | Règle appliquée | Description |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Version minimale, inclusive |
| (1.0,) | x > 1.0 | Version minimale, exclusive |
| [1.0] | x == 1.0 | Correspondance de la version exacte |
| (,1.0] | x ≤ 1.0 | Version maximale, inclusive |
| (,1.0) | x < 1.0 | Version maximale, exclusive |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Plage exacte, inclusif |
| (1.0,2.0) | 1.0 < x < 2.0 | Plage exacte, exclusif |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Mixte inclusive minimale et exclusive version maximale |
| (1.0)    | non valide | non valide |

Lorsque vous utilisez le format PackageReference, NuGet prend également en charge à l’aide d’une notation de caractère générique, \*, pour majeure, mineure, correctifs et des parties de suffixe de version préliminaire du nombre. Les caractères génériques ne sont pas pris en charge avec le `packages.config` format.

> [!Note]
> Versions préliminaires ne sont pas incluses lors de la résolution des plages de versions. Versions préliminaires *sont* inclus lorsque vous utilisez un caractère générique (\*). La plage de versions *[1.0,2.0]*, par exemple, n’inclut pas 2.0 bêta, mais la notation de caractère générique _2.0-*_ est. Consultez [émettre 912](https://github.com/NuGet/Home/issues/912) pour obtenir des informations sur les caractères génériques en version préliminaire.

### <a name="examples"></a>Exemples

Spécifiez toujours une version ou une plage de versions de dépendances de package dans les fichiers de projet, `packages.config` fichiers, et `.nuspec` fichiers. Sans une version ou une plage de versions, NuGet 2.8.x et précédemment choisit la dernière version de package disponibles lors de la résolution d’une dépendance, tandis que NuGet 3.x et versions ultérieures choisit la plus ancienne version de package. Spécification d’une version ou plage évite cette incertitude.

#### <a name="references-in-project-files-packagereference"></a>Références dans les fichiers de projet (PackageReference)

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

**Les références dans `packages.config`:**

Dans `packages.config`, chaque dépendance est répertorié avec un exacte `version` attribut qui est utilisé lors de la restauration des packages. Le `allowedVersions` attribut est utilisé uniquement pendant les opérations de mise à jour pour limiter les versions à laquelle le package peut être mis à jour.

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

**Les références dans `.nuspec` fichiers**

Le `version` d’attribut dans un `<dependency>` élément décrit les versions de plage qui sont acceptables pour une dépendance.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a>Numéros de version normalisée

> [!Note]
> Il s’agit d’une modification avec rupture pour NuGet 3.4 et versions ultérieures.

Lors de l’obtention des packages à partir d’un référentiel lors de l’installation, réinstaller, opérations ou de restauration, NuGet 3.4 + traite les numéros de version comme suit :

- Les zéros non significatifs sont supprimés de numéros de version :

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Un zéro dans la quatrième partie du numéro de version sera omis

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Cette normalisation n’affecte pas les numéros de version dans les packages eux-mêmes ; elle affecte uniquement comment NuGet correspond aux versions lors de la résolution des dépendances.

Toutefois, les référentiels de packages NuGet doivent traiter ces valeurs dans la même façon que NuGet pour éviter la duplication de version de package. Par conséquent, un référentiel qui contient la version *1.0* d’un package ne doit également héberger version *1.0.0* sous forme de package distincte et différente.
