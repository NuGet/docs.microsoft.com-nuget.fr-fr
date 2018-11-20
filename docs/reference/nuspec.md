---
title: Référence du fichier .nuspec pour NuGet
description: Le fichier .nuspec contient des métadonnées de package utilisées lors de la création d’un package et pour fournir des informations aux consommateurs de packages.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e8d4ed1f3fe4394d084a5847200901b23a1b7b39
ms.sourcegitcommit: c825eb7e222d4a551431643f5b5617ae868ebe0a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51944078"
---
# <a name="nuspec-reference"></a>Informations de référence sur le fichier .nuspec

Un fichier `.nuspec` est un manifeste XML qui contient des métadonnées de package. Ce manifeste est utilisé à la fois pour générer le package et pour fournir des informations aux consommateurs. Le manifeste est toujours inclus dans un package.

Dans cette rubrique :

- [Forme générale et schéma](#general-form-and-schema)
- [Jetons de remplacement](#replacement-tokens) (lors d’une utilisation avec un projet Visual Studio)
- [Dépendances](#dependencies)
- [Références d’assembly explicite](#explicit-assembly-references)
- [Références d’assembly Framework](#framework-assembly-references)
- [Inclusion des fichiers d’assembly](#including-assembly-files)
- [Inclusion des fichiers de contenu](#including-content-files)
- [Exemples de fichiers nuspec](#example-nuspec-files)

## <a name="general-form-and-schema"></a>Forme générale et schéma

Le fichier de schéma `nuspec.xsd` actuel se trouve dans le [dépôt GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

Dans ce schéma, un fichier `.nuspec` a la forme générale suivante :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Pour obtenir une représentation visuelle claire du schéma, ouvrez le fichier de schéma dans Visual Studio en mode Design et cliquez sur le lien **Explorateur de schémas XML**. Vous pouvez également ouvrir le fichier en tant que code, cliquer avec le bouton droit dans l’éditeur, puis sélectionner **Show XML Schema Explorer** (Afficher l’Explorateur de schémas XML). Dans les deux cas, vous obtenez un affichage semblable à celui ci-dessous (quand il est en grande partie développé) :

![Explorateur de schémas Visual Studio avec nuspec.xsd ouvert](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Éléments de métadonnées requis

Bien que les éléments suivants correspondent à la configuration minimale requise pour un package, vous devez envisager d’ajouter les [éléments de métadonnées facultatifs](#optional-metadata-elements) afin d’améliorer l’expérience globale des développeurs avec votre package. 

Ces éléments doivent apparaître dans un élément `<metadata>`.

#### <a name="id"></a>ID 
Identificateur de package ne respectant pas la casse, qui doit être unique dans nuget.org ou dans toute autre galerie susceptible d’héberger le package. Les ID ne peuvent pas contenir d’espaces ni de caractères qui ne sont pas valides pour une URL et suivent généralement les règles d’espace de noms .NET. Pour obtenir des conseils, consultez [Choix d’un identificateur de package unique](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).
#### <a name="version"></a>version
Version du package, selon le modèle *version_principale.version_secondaire.version_corrective*. Les numéros de version peuvent inclure un suffixe de préversion comme décrit dans [Gestion de versions des packages](../reference/package-versioning.md#pre-release-versions). 
#### <a name="description"></a>Description
Description longue du package pour l’affichage de l’interface utilisateur. 
#### <a name="authors"></a>authors
Liste séparée par des virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la galerie NuGet sur nuget.org et servent à croiser les références des packages de mêmes auteurs. 

### <a name="optional-metadata-elements"></a>Éléments de métadonnées facultatifs

#### <a name="title"></a>titre
Titre convivial du package, généralement utilisé dans les affichages de l’interface utilisateur comme sur nuget.org et dans le gestionnaire de package de Visual Studio. Si non spécifié, l’ID de package est utilisé. 
#### <a name="owners"></a>owners
Liste des créateurs de packages séparés par des virgules, qui utilisent des noms de profil sur nuget.org. Il s’agit souvent de la même liste que dans `authors` et elle est ignorée lors du chargement du package sur nuget.org. Consultez [Gestion des propriétaires de packages sur nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). 
#### <a name="projecturl"></a>projectUrl
URL de la page d’accueil du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org. 
#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl est déconseillé. Utilisez à la place des licences.

URL de la licence du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org.
#### <a name="license"></a>licence
SPDX licence expression ou chemin d’accès à un fichier de licence dans le package, souvent affiché dans l’interface utilisateur, ainsi que sur nuget.org. Si vous activez votre licence du package sous une licence courants tels que BSD-2-Clause ou MIT, utilisez l’identificateur de licence SPDX associé.<br>Par exemple :`<license type="expression">MIT</license>`

Voici la liste complète des [identificateurs de licence SPDX](https://spdx.org/licenses/). NuGet.org accepte uniquement OSI ou expression de type de licence lors de l’utilisation des licences FSF approuvée.

Si votre package est concédé sous licence selon plusieurs licences courantes, vous pouvez spécifier une licence composite à l’aide de la [SPDX version 2.0 de la syntaxe expression](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).<br>Par exemple :`<license type="expression">BSD-2-Clause OR MIT</license>`

Si vous utilisez une licence qui n’a pas été attribuée à un identificateur SPDX, ou il s’agit d’une licence personnalisée, vous pouvez empaqueter un fichier avec le texte de la licence. Exemple :
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```
La syntaxe exacte des expressions de licence de NuGet est décrite ci-dessous dans [ABNF](https://tools.ietf.org/html/rfc5234).
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl
URL d’une image 64x64 avec un arrière-plan transparent à utiliser comme icône pour le package dans l’affichage de l’interface utilisateur. Vérifiez que cet élément contient *l’URL directe de l’image* et non l’URL d’une page web contenant l’image. Par exemple, pour utiliser une image à partir de GitHub, utilisez le fichier brut comme URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>. 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package.
#### <a name="developmentdependency"></a>developmentDependency
*(2.8+)* Valeur booléenne qui spécifie si le package doit être marqué comme dépendance de développement uniquement, ce qui l’empêche d’être inclus en tant que dépendance dans d’autres packages. Avec PackageReference (NuGet 4.8 +), cet indicateur signifie également qu’il exclut les ressources de compilation à partir de la compilation. Consultez [prise en charge de DevelopmentDependency pour PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)
#### <a name="summary"></a>résumé
Brève description du package pour l’affichage de l’interface utilisateur. Si cet élément est omis, une version tronquée de `description` est utilisée.
#### <a name="releasenotes"></a>releaseNotes
*(1.5+)* Description des changements apportés à cette version du package, souvent utilisée dans l’interface utilisateur, par exemple sous l’onglet **Mises à jour** du Gestionnaire de package Visual Studio à la place de la description du package.
#### <a name="copyright"></a>copyright
*(1.5+)* Détails de copyright pour le package.
#### <a name="language"></a>language
ID de paramètres régionaux du package. Consultez [Création de packages localisés](../create-packages/creating-localized-packages.md).
#### <a name="tags"></a>étiquettes
Liste de balises et de mots clés délimités par des espaces, qui décrivent le package et permettent de découvrir les packages grâce à des fonctions de recherche et de filtrage. 
#### <a name="serviceable"></a>pièce remplaçable par 
*(3.3+)* Uniquement réservé à un usage NuGet interne.
#### <a name="repository"></a>dépôt
Métadonnées du référentiel, composé de quatre attributs facultatifs : *type* et *url* *(4.0 +)*, et *branche* et  *validation* *(4.6 +)*. Ces attributs permettent de mapper le fichier .nupkg vers le référentiel qui, générés avec la possibilité d’obtenir aussi détaillée que la branche individuel ou de la validation qui a créé le package. Ce doit être une url accessible au public qui peut être appelé directement par un logiciel de contrôle de version. Il ne doit pas être une page html comme cela est destiné à l’ordinateur. Pour un lien vers la page de projet, utilisez le `projectUrl` champ, à la place.

#### <a name="minclientversion"></a>MinClientVersion
Spécifie la version minimale du client NuGet qui peut installer ce package, appliquée par nuget.exe et le gestionnaire de package Visual Studio. Cet attribut est utilisé chaque fois que le package dépend de fonctionnalités spécifiques du fichier `.nuspec` qui ont été ajoutées dans une version particulière du client NuGet. Par exemple, un package utilisant l’attribut `developmentDependency` doit spécifier « 2.8 » pour `minClientVersion`. De même, un package utilisant l’élément `contentFiles` (consultez la section suivante) doit affecter à `minClientVersion` la valeur « 3.3 ». Notez également que, comme les clients NuGet antérieurs à 2.5 ne reconnaissent pas cet indicateur, ils refusent *toujours* d’installer le package, quel que soit le contenu de `minClientVersion`.

#### <a name="collection-elements"></a>Éléments de collection

#### <a name="packagetypes"></a>PackageTypes
*(3.5+)* Collection de zéro ou plusieurs éléments `<packageType>` spécifiant le type du package s’il est différent du package de dépendances classique. Chaque élément packageType a des attributs *name* et *version*. Consultez [Définition d’un type de package](../create-packages/creating-a-package.md#setting-a-package-type).
#### <a name="dependencies"></a>dépendances
Collection de zéro ou plusieurs éléments `<dependency>` spécifiant les dépendances du package. Chaque dépendance a des attributs *id*, *version*, *include* (3.x+) et *exclude* (3.x+). Consultez [Dépendances](#dependencies-element) ci-dessous.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 +)* Collection de zéro ou plusieurs éléments `<frameworkAssembly>` identifiant les références d’assembly .NET Framework nécessaires à ce package, ce qui garantit que les références sont ajoutées à des projets utilisant le package. Chaque élément frameworkAssembly a des attributs *assemblyName* et *targetFramework*. Consultez [Références d’assembly Framework](#specifying-framework-assembly-references-gac) ci-dessous. |
#### <a name="references"></a>Références
*(1.5+)* Collection de zéro ou plusieurs éléments `<reference>` nommant des assemblys dans le dossier `lib` du package qui sont ajoutés en tant que références de projet. Chaque référence a un attribut *file*. `<references>` peut également contenir un élément `<group>` avec un attribut *targetFramework* qui contient à son tour des éléments `<reference>`. Si cet élément est omis, toutes les références dans `lib` sont incluses. Consultez [Références d’assembly explicite](#specifying-explicit-assembly-references) ci-dessous.
#### <a name="contentfiles"></a>contentFiles
*(3.3+)* Collection d’éléments `<files>` qui identifient les fichiers de contenu à inclure dans le projet de consommation. Ces fichiers sont spécifiés avec un ensemble d’attributs qui décrivent comment ils doivent être utilisés dans le système de projet. Consultez [Inclusion des fichiers d’assembly](#specifying-files-to-include-in-the-package) ci-dessous.
#### <a name="files"></a>fichiers  
Le `<package>` nœud peut contenir un `<files>` nœud en tant que frère à `<metadata>`et un `<contentFiles>` enfant sous `<metadata>`, pour spécifier les fichiers d’assembly et le contenu à inclure dans le package. Consultez [Inclusion des fichiers d’assembly](#including-assembly-files) et [Inclusion des fichiers de contenu](#including-content-files) plus loin dans cette rubrique pour plus d’informations.

## <a name="replacement-tokens"></a>Jetons de remplacement

Lors de la création d’un package, la [commande `nuget pack`](../tools/cli-ref-pack.md) remplace les jetons séparés par des $ dans le nœud `<metadata>` du fichier `.nuspec` par des valeurs provenant d’un fichier projet ou du commutateur `-properties` de la commande `pack`.

Sur la ligne de commande, vous spécifiez des valeurs de jeton avec `nuget pack -properties <name>=<value>;<name>=<value>`. Par exemple, vous pouvez utiliser un jeton tel que `$owners$` et `$desc$` dans le fichier `.nuspec` et fournir les valeurs au moment de la compression comme suit :

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Pour utiliser les valeurs à partir d’un projet, spécifiez les jetons décrits dans le tableau ci-dessous (AssemblyInfo fait référence au fichier dans `Properties` comme `AssemblyInfo.cs` ou `AssemblyInfo.vb`).

Pour utiliser ces jetons, exécutez `nuget pack` avec le fichier projet et non simplement le fichier `.nuspec`. Par exemple, quand vous utilisez la commande suivante, les jetons `$id$` et `$version$` dans un fichier `.nuspec` sont remplacés par les valeurs `AssemblyName` et `AssemblyVersion` du projet :

```ps
nuget pack MyProject.csproj
```

En général, quand vous avez un projet, vous créez le fichier `.nuspec` initialement à l’aide de `nuget spec MyProject.csproj` qui inclut automatiquement certains de ces jetons standard. Toutefois, si un projet ne possède pas de valeurs pour les éléments `.nuspec` requis, `nuget pack` échoue. De plus, si vous modifiez des valeurs de projet, veillez à regénérer avant de créer le package ; pour effectuer cette opération en toute facilité, utilisez le commutateur `build` de la commande pack.

À l’exception de `$configuration$`, les valeurs dans le projet sont préférées à celles affectées au même jeton sur la ligne de commande.

| Token | Source de valeur | Value
| --- | --- | ---
| **$id$** | Fichier projet | AssemblyName (titre) à partir du fichier de projet |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion si présente, sinon AssemblyVersion |
| **$authors$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | DLL d’assembly | Configuration utilisée pour générer l’assembly, Debug étant la valeur par défaut. Notez que, pour créer un package à l’aide d’une configuration Release, vous utilisez toujours `-properties Configuration=Release` sur la ligne de commande. |

Les jetons peuvent également être utilisés pour résoudre les chemins quand vous incluez des [fichiers d’assembly](#including-assembly-files) et [fichiers de contenu](#including-content-files). Les jetons ont les mêmes noms que les propriétés MSBuild, ce qui permet de sélectionner les fichiers à inclure en fonction de la configuration de build actuelle. Par exemple, si vous utilisez les jetons suivants dans le fichier `.nuspec` :

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

Et que vous générez un assembly dont `AssemblyName` est `LoggingLibrary` avec la configuration `Release` dans MSBuild, les lignes résultantes dans le fichier `.nuspec` du package sont les suivantes :

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Élément de dépendances

L’élément `<dependencies>` dans `<metadata>` contient un nombre quelconque d’éléments `<dependency>` qui identifient d’autres packages dont dépend le package de niveau supérieur. Les attributs pour chaque élément `<dependency>` sont les suivants :

| Attribut | Description |
| --- | --- |
| `id` | (Obligatoire) ID de package de la dépendance, tel que « EntityFramework » et « NUnit », qui est le nom du package nuget.org affiché sur une page de package. |
| `version` | (Obligatoire) Plage de versions acceptables en tant que dépendance. Consultez [Gestion de versions des packages](../reference/package-versioning.md#version-ranges-and-wildcards) pour connaître la syntaxe exacte. |
| include | Liste de balises include/exclude séparées par des virgules (voir ci-dessous) indiquant la dépendance à inclure dans le package final. La valeur par défaut est `all`. |
| exclude | Liste de balises include/exclude séparées par des virgules (voir ci-dessous) indiquant la dépendance à exclure dans le package final. La valeur par défaut est `build,analyzers` qui peut être remplacé. Mais `content/ ContentFiles` sont également implicitement exclus dans le package final qui ne peut pas être remplacé. Les balises spécifiées avec `exclude` sont prioritaires sur celles spécifiées avec `include`. Par exemple, `include="runtime, compile" exclude="compile"` est identique à `include="runtime"`. |

| Balise include/exclude | Dossiers affectés de la cible |
| --- | --- |
| contentFiles | Contenu |
| runtime | Runtime, Resources et FrameworkAssemblies |
| compile | lib |
| build | build (propriétés et cibles MSBuild) |
| native | native |
| none | Aucun dossier |
| all | Tous les dossiers |

Par exemple, les lignes suivantes indiquent les dépendances sur `PackageA` version 1.1.0 ou ultérieure, et `PackageB` version 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Les lignes suivantes indiquent les dépendances sur les mêmes packages, mais spécifient d’inclure les dossiers `contentFiles` et `build` de `PackageA` et tous les éléments sauf les dossiers `native` et `compile` de `PackageB`.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Remarque : Quand vous créez un fichier `.nuspec` à partir d’un projet avec `nuget spec`, les dépendances qui existent dans le projet sont automatiquement incluses dans le fichier `.nuspec` obtenu.

### <a name="dependency-groups"></a>Groupes de dépendances

*Version 2.0+*

Comme alternative à une liste plate unique, les dépendances peuvent être spécifiées selon le profil de framework du projet cible avec les éléments `<group>` dans `<dependencies>`.

Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<dependency>`. Ces dépendances sont installées ensemble quand la version cible de .NET Framework est compatible avec le profil de framework du projet.

L’élément `<group>` sans un attribut `targetFramework` est utilisé comme valeur par défaut ou liste de secours de dépendances. Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.

> [!Important]
> Le format de groupe ne peut pas être mélangé avec une liste plate.

L’exemple suivant illustre différentes variantes de l’élément `<group>` :

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Références d’assembly explicite

L’élément `<references>` spécifie explicitement les assemblys que le projet cible doit référencer lors de l’utilisation du package. Quand cet élément est présent, NuGet n’ajoute des références qu’aux assemblys répertoriés ; il n’ajoute de références pour aucun autre assembly dans le dossier `lib` du package.

Par exemple, l’élément `<references>` suivant demande à NuGet d’ajouter des références à `xunit.dll` et `xunit.extensions.dll` uniquement même s’il existe d’autres assemblys dans le package :

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Des références explicites sont généralement utilisées pour les assemblys uniquement au moment du design. Quand vous utilisez des [contrats de code](/dotnet/framework/debug-trace-profile/code-contracts), par exemple, les assemblys de contrat doivent être en regard des assemblys de runtime qu’ils augmentent afin que Visual Studio puisse les trouver, mais les assemblys de contrat n’ont pas à être référencés par le projet ni copiés dans le dossier `bin` du projet.

De même, des références explicites peuvent servir pour les frameworks de tests unitaires, tels que XUnit,dont les assemblys d’outils doivent être situés en regard des assemblys de runtime, mais qui n’ont pas besoin d’être inclus comme références de projet.

### <a name="reference-groups"></a>Groupes de référence

Comme alternative à une liste plate unique, les références peuvent être spécifiées selon le profil de framework du projet cible avec les éléments `<group>` dans `<references>`.

Chaque groupe possède un attribut nommé `targetFramework` et contient zéro ou plusieurs éléments `<reference>`. Ces références sont ajoutées à un projet quand la version cible de .NET Framework est compatible avec le profil de framework du projet.

L’élément `<group>` sans un attribut `targetFramework` est utilisé comme valeur par défaut ou liste de secours de références. Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts.

> [!Important]
> Le format de groupe ne peut pas être mélangé avec une liste plate.

L’exemple suivant illustre différentes variantes de l’élément `<group>` :

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Références d’assembly Framework

Les assemblys Framework sont ceux qui font partie du .NET Framework et doivent déjà figurer dans le GAC (Global Assembly Cache) pour un ordinateur donné. En identifiant ces assemblys dans l’élément `<frameworkAssemblies>`, un package peut garantir que les références requises sont ajoutées à un projet si le projet ne dispose pas déjà de telles références. Ces assemblys, bien entendu, ne sont pas directement inclus dans un package.

L’élément `<frameworkAssemblies>` contient zéro ou plusieurs éléments `<frameworkAssembly>`, chacun d’eux spécifiant les attributs suivants :

| Attribut | Description |
| --- | --- |
| **assemblyName** | (Obligatoire) Nom d’assembly qualifié complet. |
| **targetFramework** | (Facultatif) Spécifie la version cible de .NET Framework à laquelle s’applique cette référence. Si cet attribut est omis, indique que la référence s’applique à tous les frameworks. Consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md) pour connaître les identificateurs de framework exacts. |

L’exemple suivant montre une référence à `System.Net` pour toutes les versions cibles de .NET Framework et une référence à `System.ServiceModel` pour .NET Framework 4.0 uniquement :

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Inclusion des fichiers d’assembly

Si vous suivez les conventions décrites dans [Création d’un package](../create-packages/creating-a-package.md), il est inutile de spécifier explicitement une liste de fichiers dans le fichier `.nuspec`. La commande `nuget pack` sélectionne automatiquement les fichiers nécessaires.

> [!Important]
> Quand un package est installé dans un projet, NuGet ajoute automatiquement des références d’assembly aux DLL du package, *à l’exclusion* de celles nommées `.resources.dll`, car elles sont supposées être des assemblys satellites localisés. C’est pourquoi vous devez éviter d’utiliser `.resources.dll` pour les fichiers qui contiennent du code de package essentiel.

Pour ignorer ce comportement automatique et contrôler explicitement les fichiers qui sont inclus dans un package, placez un élément `<files>` en tant qu’enfant de `<package>` (et frère de `<metadata>`), identifiant chaque fichier avec un élément `<file>` distinct. Exemple :

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Avec NuGet 2.x et versions antérieures, et des projets utilisant `packages.config`, l’élément `<files>` est également utilisé pour inclure les fichiers de contenu non modifiables quand un package est installé. Avec NuGet 3.3+ et les projets PackageReference, l’élément `<contentFiles>` est utilisé à la place. Consultez [Inclusion des fichiers de contenu](#including-content-files) ci-dessous pour plus d’informations.

### <a name="file-element-attributes"></a>Attributs des éléments File

Chaque élément `<file>` spécifie les attributs suivants :

| Attribut | Description |
| --- | --- |
| **src** | Emplacement du ou des fichiers à inclure, soumis à des exclusions définies par l’attribut `exclude`. Le chemin est relatif au fichier `.nuspec` sauf si un chemin absolu est spécifié. Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive. |
| **target** | Chemin relatif vers le dossier dans le package où les fichiers sources sont placés, qui doit commencer par `lib`, `content`, `build` ou `tools`. Consultez [Création d’un fichier .nuspec à partir d’un répertoire de travail basé sur une convention](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Liste de fichiers ou de modèles de fichiers séparés par un point-virgule à exclure de l’emplacement `src`. Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive. |

### <a name="examples"></a>Exemples

**Assembly unique**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Assembly unique spécifique à une version cible de .NET Framework**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Ensemble de DLL avec un caractère générique**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**DLL de différents frameworks**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Exclusion de fichiers**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Inclusion des fichiers de contenu

Les fichiers de contenu sont des fichiers non modifiables qu’un package doit inclure dans un projet. Comme ils ne sont pas modifiables, ils ne sont pas destinés à être changés par le projet de consommation. Des exemples de fichiers de contenu sont notamment :

- Images incorporées en tant que ressources
- Fichiers sources qui sont déjà compilés
- Scripts qui doivent être inclus avec la sortie de génération du projet
- Fichiers de configuration pour le package qui doivent être inclus dans le projet, mais ne nécessitent aucune modification spécifique au projet

Les fichiers de contenu sont inclus dans un package à l’aide de l’élément `<files>`, en spécifiant le dossier `content` dans l’attribut `target`. Toutefois, ces fichiers sont ignorés quand le package est installé dans un projet utilisant PackageReference, qui utilise à la place l’élément `<contentFiles>`.

Pour une compatibilité maximale avec les projets de consommation, un package spécifie dans l’idéal les fichiers de contenu dans les deux éléments.

### <a name="using-the-files-element-for-content-files"></a>Utilisation de l’élément files pour les fichiers de contenu

Pour les fichiers de contenu, utilisez simplement le même format que pour les fichiers d’assembly, mais spécifiez `content` comme dossier de base dans l’attribut `target` comme indiqué dans les exemples suivants.

**Fichiers de contenu de base**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Fichiers de contenu avec structure de répertoires**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Fichier de contenu spécifique à une version cible de .NET Framework**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Fichier de contenu copié vers un dossier avec un point dans le nom**

Dans ce cas, NuGet détecte que l’extension dans `target` ne correspond pas à l’extension dans `src` et traite par conséquent cette partie du nom dans `target` en tant que dossier :

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Fichiers de contenu sans extensions**

Pour inclure les fichiers sans extension, utilisez les caractères génériques `*` ou `**` :

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Fichiers de contenu avec chemin complet et cible complète**

Dans ce cas, étant donné que les extensions de fichier de la source et de la cible correspondent, NuGet part du principe que la cible est un nom de fichier et non un dossier :

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Modification du nom d’un fichier de contenu dans le package**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Exclusion de fichiers**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Utilisation de l’élément contentFiles pour les fichiers de contenu

*NuGet 4.0 + avec PackageReference*

Par défaut, un package place le contenu dans un dossier `contentFiles` (voir ci-dessous) et `nuget pack` a mis tous les fichiers dans ce dossier à l’aide des attributs par défaut. Dans ce cas, il n’est pas du tout nécessaire d’inclure un nœud `contentFiles` dans le fichier `.nuspec`.

Pour contrôler les fichiers qui sont inclus, l’élément `<contentFiles>` spécifie une collection d’éléments `<files>` qui identifient exactement les fichiers à ajouter.

Ces fichiers sont spécifiés avec un ensemble d’attributs qui décrivent comment ils doivent être utilisés dans le système de projet :

| Attribut | Description |
| --- | --- |
| **include** | (Obligatoire) Emplacement du ou des fichiers à inclure, soumis à des exclusions définies par l’attribut `exclude`. Le chemin est relatif au fichier `.nuspec` sauf si un chemin absolu est spécifié. Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive. |
| **exclude** | Liste de fichiers ou de modèles de fichiers séparés par un point-virgule à exclure de l’emplacement `src`. Le caractère générique `*` est autorisé et le caractère générique double `**` implique une recherche de dossier récursive. |
| **buildAction** | Action de génération à affecter à l’élément de contenu pour MSBuild, comme `Content`, `None`, `Embedded Resource`, `Compile`, etc. La valeur par défaut est `Compile`. |
| **copyToOutput** | Valeur booléenne indiquant s’il faut copier des éléments de contenu à la build (ou publiez) dossier de sortie. La valeur par défaut est false. |
| **flatten** | Valeur booléenne indiquant s’il faut copier des éléments de contenu dans un dossier unique dans la sortie de génération (true) ou conserver la structure de dossiers dans le package (false). Cet indicateur fonctionne uniquement lorsque l’indicateur copyToOutput est défini sur true. La valeur par défaut est false. |

Lors de l’installation d’un package, NuGet applique les éléments enfants de `<contentFiles>` de haut en bas. Si plusieurs entrées correspondent au même fichier, toutes les entrées sont appliquées. L’entrée supérieure remplace les entrées inférieures s’il existe un conflit pour le même attribut.

#### <a name="package-folder-structure"></a>Structure de dossiers de package

Le projet de package doit structurer le contenu à l’aide du modèle suivant :

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` peut être `cs`, `vb`, `fs`, `any`, ou l’équivalent en minuscules d’un élément `$(ProjectLanguage)` donné.
- `TxM` est n’importe quel moniker du Framework cible légal pris en charge par NuGet (consultez [Versions cibles de .NET Framework](../reference/target-frameworks.md)).
- Toute structure de dossiers peut être ajoutée à la fin de cette syntaxe.

Exemple :

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Les dossiers vides peuvent utiliser `.` pour choisir de ne pas fournir de contenu pour certaines combinaisons de langage et TxM, par exemple :

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Exemple de section contentFiles

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>Exemples de fichiers nuspec

**Fichier `.nuspec` simple qui ne spécifie pas de dépendances ni de fichiers**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**Fichier `.nuspec` avec des dépendances**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**Fichier `.nuspec` avec des fichiers**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**Fichier `.nuspec` avec des assemblys Framework**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

Dans cet exemple, les éléments suivants sont installés pour les cibles de projets spécifiques :

- .NET4 -> `System.Web`, `System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
