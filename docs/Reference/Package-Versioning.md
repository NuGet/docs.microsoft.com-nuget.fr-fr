---
title: "Référence de Version de Package NuGet | Documents Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "Détails exacts sur la spécification des numéros de version et de plages pour d’autres packages qui dépend d’un package NuGet, et comment les dépendances sont installées."
keywords: "le contrôle de version, les dépendances de package NuGet, versions de dépendance de NuGet, les numéros de version de NuGet, version du package NuGet, plages de versions, les spécifications de version, les numéros de version normalisée"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25b74ab629cab0fff7114bf1621606de5fc18dd2
ms.sourcegitcommit: 89bb9d429c19ff69084c35acad09daea3e16d56b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="package-versioning"></a>Contrôle de version de package

Un package spécifique est toujours appelée à l’aide de son identificateur de package et un numéro de version exact. Par exemple, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sur nuget.org a plusieurs dizaines des packages spécifiques disponibles, allant de version *4.1.10311* vers la version *6.1.3* (la dernière stable version) et les diverses versions préliminaires telles que *6.2.0-beta1*.

Lorsque vous créez un package, vous assignez un numéro de version spécifique avec un suffixe facultatif en version préliminaire. En revanche, lors de l’utilisation de packages, vous pouvez spécifier un numéro de version exacte ou d’une plage de versions acceptables.

Dans cette rubrique :

- [Principes de base version](#version-basics) , y compris les suffixes de la version préliminaire.
- [Les caractères génériques et les plages de versions](#version-ranges-and-wildcards)
- [Numéros de version normalisée](#normalized-version-numbers)

## <a name="version-basics"></a>Principes fondamentaux de version

Un numéro de version est au format *majeure.mineure.correctif [-suffixe]*, où les composants ont les significations suivantes :

- *Principaux*: modifications avec rupture
- *Secondaire*: nouvelles fonctionnalités, mais offre une compatibilité descendante
- *Correctif*: offre une compatibilité descendante correctifs de bogues
- *-Suffixe* (facultatif) : un trait d’union suivi d’une chaîne qui dénote une version préliminaire (suivant la [convention de contrôle de version sémantique ou SemVer 1.0](http://semver.org/spec/v1.0.0.html)).

**Exemples :**
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> NuGet.org rejette tout le téléchargement du package qui ne dispose pas d’un numéro de version exact. La version doit être spécifiée dans le `.nuspec` ou le fichier de projet utilisé pour créer le package.

### <a name="pre-release-versions"></a>Versions préliminaires

Techniquement parlant, créateurs de package peuvent utiliser n’importe quelle chaîne comme suffixe pour désigner une version préliminaire, NuGet traite n’importe quelle version de ce type en tant que version préliminaire et rend les autres sans interprétation. Autrement dit, affiche NuGet la version complète de chaîne dans l’interface utilisateur est impliquée, laissant toute interprétation de, autrement dit le suffixe au consommateur.

Ceci dit, les développeurs de packages suivent les conventions d’affectation de noms reconnues :

- `-alpha`: Version alpha, généralement utilisée pour les travaux en cours et d’expérimentation.
- `-beta`: Bêta, généralement une fonctionnalité complète pour le prochain planifié, mais il peut contenir des bogues.
- `-rc`: Version release candidate, généralement une version finale potentiellement (stable), sauf si l’apparition de bogues importants.

> [!Note]
> Prend en charge de NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), qui prend en charge les numéros de version préliminaire avec la notation à points, comme dans *1.0.1-build.23*. Notation par points n’est pas pris en charge avec les versions de NuGet antérieures 4.3.0. Vous pouvez utiliser un formulaire comme *1.0.1-build23*.

Lors de la résolution des références de package et de plusieurs versions de package diffèrent uniquement par le suffixe, NuGet choisit une version sans suffixe tout d’abord, puis applique la priorité pour la version préliminaire dans l’ordre alphabétique inverse. Par exemple, les versions suivantes sont choisies en respectant l’ordre indiqué :

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

## <a name="semantic-versioning-200"></a>Contrôle de version sémantique 2.0.0

Avec NuGet 4.3.0+ et Visual Studio 2017 version 15.3 +, NuGet prend en charge [contrôle de version sémantique 2.0.0](http://semver.org/spec/v2.0.0.html).

Certaines sémantiques de SemVer v2.0.0 ne sont pas pris en charge de clients plus anciens. NuGet considère qu’une version de package à être v2.0.0 SemVer spécifiques si une des affirmations suivantes est vraie :

- L’étiquette de la version préliminaire est séparée par un point, par exemple, *1.0.0-alpha.1*
- La version a des métadonnées de la génération, par exemple, *1.0.0+githash*

Pour nuget.org, un package est défini en tant que package v2.0.0 SemVer si une des affirmations suivantes est vraie :

- La version du package est v2.0.0 SemVer conforme, mais pas les v1.0.0 SemVer conforme, tel qu’indiqué ci-dessus.
- Une des plages de versions de dépendance du package dont la version minimale ou maximale est v2.0.0 SemVer conforme, mais pas les v1.0.0 SemVer conforme, définis ci-dessus ; par exemple, *[1.0.0-alpha.1,)*.

Si vous téléchargez un package de v2.0.0 spécifiques SemVer nuget.org, le package est invisible pour les clients plus anciens et disponible aux clients NuGet uniquement suivants :

- NuGet 4.3.0+
- Visual Studio 2017 version 15.3 + 
- dotnet.exe (Kit de développement .NET 2.0.0+)

Les clients tiers :

- JetBrains avenant
- Paket version 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Les caractères génériques et les plages de versions

Lorsque vous faites référence aux dépendances de package, NuGet prend en charge à l’aide de la notation de l’intervalle pour la spécification de plages de versions, résumées comme suit :

| Notation | Règle appliquée | Description |
|----------|--------------|-------------|
| 1.0 | 1.0 ≤ x | Version minimale, inclusive |
| (1.0,) | 1.0 < x | Version minimale, exclusive |
| [1.0] | x == 1.0 | Correspondance exacte |
| (,1.0] | x ≤ 1.0 | Version maximale, inclusive |
| (,1.0) | x < 1.0 | Version maximale, exclusive |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Plage exacte, inclusif |
| (1.0,2.0) | 1.0 < x < 2.0 | Plage exacte, exclusif |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Inclusive minimum et exclusive maximale version mixte |
| (1.0)    | non valide | non valide |

Lorsque vous utilisez la PackageReference ou `project.json` package NuGet, référence des formats également prend en charge à l’aide d’une notation de caractère générique, \*, pour majeure, mineure, Patch et parties de suffixe de la version préliminaire du nombre. Les caractères génériques ne sont pas pris en charge avec les `packages.config` format.

> [!Note]
> Versions antérieures ne sont pas incluses lors de la résolution des plages de versions. Versions préliminaires *sont* inclus lorsque vous utilisez un caractère générique (\*). La plage de versions *[1.0,2.0]*, par exemple, n’inclut pas 2.0 bêta, mais les génériques _2.0-*_ est. Consultez [émettre 912](https://github.com/NuGet/Home/issues/912) pour obtenir des informations sur les caractères génériques de la version préliminaire.

### <a name="examples"></a>Exemples

Spécifiez toujours une version ou une plage de versions pour les dépendances de package dans les fichiers de projet, `packages.config` fichiers, et `.nuspec` fichiers. Sans une version ou d’une plage de versions, NuGet 2.8.x et précédemment choisit la dernière version de package disponibles lors de la résolution d’une dépendance, tandis que NuGet 3.x et choisit ensuite d’utiliser la version du package le plus bas. Spécification d’une version ou plage permet d’éviter cette incertitude.

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Références de `packages.config`:**

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

**Références de `.nuspec` fichiers**

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

Lors de l’obtention de packages à partir d’un référentiel pendant l’installation, réinstallez ou restaurer les opérations, NuGet 3.4 + traite les numéros de version comme suit :

- Les zéros non significatifs sont supprimés de numéros de version :

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- Un zéro dans la quatrième partie du numéro de version sera omis

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

Cette normalisation n’affecte pas les numéros de version dans les packages eux-mêmes ; elle affecte uniquement comment NuGet correspond aux versions lors de la résolution des dépendances.

Toutefois, les dépôts de package NuGet doivent traiter ces valeurs dans la même façon que NuGet pour éviter la duplication de version de package. Par conséquent, un référentiel qui contient la version *1.0* d’un package ne doivent pas également héberger version *1.0.0* en tant que package distinct et différent.
