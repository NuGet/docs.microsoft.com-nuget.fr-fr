---
title: Guide pratique pour créer un package NuGet
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 1221631b22eed7d2d8e58bd08ff120d91231d49b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580392"
---
# <a name="creating-nuget-packages"></a>Création de packages NuGet

Quel que soit la fonction de votre package ou le code qu’il contient, vous utilisez `nuget.exe` pour empaqueter cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs. Pour installer `nuget.exe`, consultez [Installer l’interface de ligne de commande NuGet](../install-nuget-client-tools.md#nugetexe-cli). Notez que Visual Studio n’inclut pas automatiquement `nuget.exe`.

Techniquement parlant, un package NuGet n’est qu’un fichier ZIP renommé avec l’extension `.nupkg` et dont le contenu correspond à certaines conventions. Cette rubrique décrit le processus détaillé de création d’un package qui répond à ces conventions. Pour consulter une procédure pas à pas ciblée, reportez-vous à [Démarrage rapide : créer et publier un package](../quickstart/create-and-publish-a-package.md).

L’empaquetage commence par le code compilé (assemblys), les symboles et/ou d’autres fichiers à remettre sous forme de package (consultez [Vue d’ensemble et flux de travail](overview-and-workflow.md)). Ce processus est indépendant de la compilation ou de la génération des fichiers destinés au package, même si vous pouvez tirer des informations contenues dans un fichier projet pour maintenir synchronisés les assemblys et packages compilés.

> [!Note]
> Cette rubrique s’applique aux types de projet autres que les projets .NET Core utilisant Visual Studio 2017 et NuGet 4.0+. Dans ces projets .NET Core, NuGet utilise des informations contenues dans le fichier projet directement. Pour plus d’informations, consultez [Créer des packages .NET standard avec Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) et [Commandes NuGet pack et restore en tant que cibles MSBuild](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Déterminer quels assemblys empaqueter

La plupart des packages à usage général contiennent un ou plusieurs assemblys que d’autres développeurs peuvent utiliser dans leurs propres projets.

- En règle générale, il est préférable d’avoir un seul assembly par package NuGet, à condition que chaque assembly soit indépendamment utile. Par exemple, si vous avez un `Utilities.dll` qui dépend de `Parser.dll`, et que `Parser.dll` est utile tout seul, créez un seul package pour chacun. Ainsi, les développeurs peuvent utiliser `Parser.dll` indépendamment de `Utilities.dll`.

- Si votre bibliothèque se compose de plusieurs assemblys qui ne sont pas indépendamment utiles, alors il est possible de les combiner en un seul package. À l’aide de l’exemple précédent, si `Parser.dll` contient du code utilisé uniquement par `Utilities.dll`, alors il est possible de conserver `Parser.dll` dans le même package.

- De même, si `Utilities.dll` dépend de `Utilities.resources.dll`, et que ce dernier n’est pas utile tout seul, alors placez les deux dans le même package.

En réalité, les ressources correspondent à un cas spécial. Lorsqu’un package est installé dans un projet, NuGet ajoute automatiquement des références d’assembly aux DLL du package, *à l’exclusion* de celles nommées `.resources.dll`, car elles sont supposées être des assemblys satellites localisés (consultez [Création de packages localisés](creating-localized-packages.md)). C’est pourquoi vous devez éviter d’utiliser `.resources.dll` pour les fichiers qui contiennent du code de package essentiel.

Si votre bibliothèque contient des assemblys COM Interop, suivez les instructions supplémentaires données dans [Création de packages avec des assemblys COM Interop](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rôle et structure du fichier .nuspec

Une fois que vous savez quels fichiers vous voulez empaqueter, l’étape suivante consiste à créer un manifeste de package dans un fichier XML `.nuspec`.

Le manifeste :

1. Décrit le contenu du package et est lui-même inclus dans le package.
1. Dirige la création du package et indique à NuGet comment installer le package dans un projet. Par exemple, le manifeste identifie les autres dépendances de package pour que NuGet puisse également les installer lorsque le package principal est installé.
1. Contient des propriétés à la fois obligatoires et facultatives comme décrit ci-dessous. Pour plus de précision, notamment sur les autres propriétés non mentionnées ici, consultez les [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).

Propriétés obligatoires :

- Identificateur du package, qui doit être unique dans toute la galerie qui héberge le package.
- Numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [préversions](prerelease-packages.md).
- Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)
- Informations sur l’auteur et le propriétaire.
- Longue description du package.

Propriétés facultatives communes :

- Notes de publication
- Informations de copyright
- Brève description de l’[interface utilisateur du gestionnaire de package dans Visual Studio](../tools/package-manager-ui.md)
- ID de paramètres régionaux
- URL de la page d’accueil et de la licence
- URL de l’icône
- Listes des dépendances et références
- Balises facilitant les recherches dans la galerie

Voici un fichier `.nuspec` classique (mais fictif), avec des commentaires décrivant les propriétés :

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Gestion des versions de package](../reference/package-versioning.md). Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `include` et `exclude` sur l’élément `dependency`. Consultez [Informations de référence sur le fichier .nuspec - Dépendances](../reference/nuspec.md#dependencies).

Étant donné que le manifeste est inclus dans le package à partir duquel il est créé, vous pouvez en trouver de nombreux autres exemples en examinant les packages existants. Le dossier *global-packages*, sur votre ordinateur, représente une bonne source ; son emplacement est retourné par la commande suivante :

```cli
nuget locals -list global-packages
```

Accédez à un dossier *package\version* quelconque, copiez le fichier `.nupkg` dans un fichier `.zip`, puis ouvrez ce fichier `.zip` et examinez le fichier `.nuspec` qu’il contient.

> [!Note]
> Lorsque vous créez un fichier `.nuspec` à partir d’un projet Visual Studio, le manifeste contient les jetons qui sont remplacés par des informations du projet lors de la génération du package. Consultez [Création du fichier .nuspec à partir d’un projet Visual Studio](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Création du fichier .nuspec

La création d’un manifeste complet commence généralement par un fichier `.nuspec` de base généré par l’intermédiaire de l’une des méthodes suivantes :

- [Un répertoire de travail basé sur une convention](#from-a-convention-based-working-directory)
- [Une DLL d’assembly](#from-an-assembly-dll)
- [Un projet Visual Studio](#from-a-visual-studio-project)    
- [Un nouveau fichier avec des valeurs par défaut](#new-file-with-default-values)

Vous modifiez ensuite le fichier manuellement afin qu’il décrive le contenu exact que vous voulez dans le package final.

> [!Important]
> Les fichiers `.nuspec` générés contiennent des espaces réservés qui doivent être modifiés avant de créer le package avec la commande `nuget pack`. Cette commande échoue si le fichier `.nuspec` contient des espaces réservés.

### <a name="from-a-convention-based-working-directory"></a>À partir d’un répertoire de travail basé sur une convention

Dans la mesure où un package NuGet n’est qu’un fichier ZIP renommé avec l’extension `.nupkg`, il est souvent plus simple de créer la structure de dossiers souhaitée sur le système de fichiers local, puis de créer directement le fichier `.nuspec` à partir de cette structure. La commande `nuget pack` ajoute alors automatiquement tous les fichiers dans cette structure de dossiers (à l’exclusion des dossiers qui commencent par `.`, ce qui vous permet de conserver les fichiers privés dans la même structure).

L’avantage de cette approche est que vous n’avez pas besoin de spécifier, dans le manifeste, les fichiers à inclure dans le package (comme expliqué plus loin dans cette rubrique). Vous pouvez simplement demander à votre processus de génération de produire la structure de dossiers exacte qui est placée dans le package et vous pouvez facilement inclure d’autres fichiers qui ne font peut-être pas partie d’un projet :

- Contenu et code source à injecter dans le projet cible.
- Scripts PowerShell (les packages utilisés dans NuGet 2.x peuvent aussi inclure des scripts d’installation, ce qui n’est pas pris en charge dans NuGet 3.x et les versions ultérieures).
- Transformations des fichiers de configuration et de code source existants dans un projet.

Les conventions de dossier sont les suivantes :

| Dossier | Description | Action à l’installation du package |
| --- | --- | --- |
| (racine) | Emplacement du fichier Lisez-moi.txt | Visual Studio affiche un fichier Lisez-moi.txt à la racine du package lorsque le package est installé. |
| lib/{tfm} | Fichiers d’assembly (`.dll`), de documentation (`.xml`) et de symbole (`.pdb`) du TFM (moniker de la version cible de .NET Framework) donné | Les assemblys sont ajoutés comme références pour la compilation et l’exécution. `.xml` et `.pdb` sont copiés dans les dossiers du projet. Consultez [Prise en charge de plusieurs frameworks cibles](supporting-multiple-target-frameworks.md) pour créer des sous-dossiers propres à la cible du framework. |
| ref/{tfm} | Fichiers d’assembly (`.dll`) et de symbole (`.pdb`) du TFM (moniker de framework cible) donné | Les assemblys étant uniquement ajoutés comme références pour la compilation, rien n’est copié dans le dossier bin du projet. |
| runtimes | Fichiers d’assemblies propres à l’architecture (`.dll`), de symboles (`.pdb`) et de ressources natives (`.pri`) | Les assemblys sont uniquement ajoutés comme références pour l’exécution. Les autres fichiers sont copiés dans les dossiers du projet. Il doit toujours y avoir un assembly spécifique à `AnyCPU` (TFM) correspondant sous le dossier `/ref/{tfm}` pour fournir l’assembly correspondant au moment de la compilation. Consultez [Prise en charge de plusieurs frameworks cibles](supporting-multiple-target-frameworks.md). |
| contenu | Fichiers arbitraires | Le contenu est copié à la racine du projet. Considérez que le dossier **content** est la racine de l’application cible qui consomme le package en définitive. Pour que le package ajoute une image dans le dossier */images* de l’application, placez-le dans le dossier *content/images* du package. |
| build | Fichiers `.targets` et `.props` MSBuild | Automatiquement insérés dans le fichier projet ou `project.lock.json` (NuGet 3.x+). |
| outils | Scripts PowerShell et programmes accessibles à partir de la console du gestionnaire de package | Le dossier `tools` est ajouté à la variable d’environnement `PATH` de la console du gestionnaire de package uniquement (et *non* à `PATH` comme défini pour MSBuild lors de la génération du projet). |

Dans la mesure où la structure de dossiers peut contenir n’importe quel nombre d’assemblys pour n’importe quel nombre de frameworks cibles, cette méthode est nécessaire pour créer des packages qui prennent en charge plusieurs frameworks.

Dans tous les cas, une fois que la structure de dossiers voulue est en place, exécutez la commande suivante dans ce dossier pour créer le fichier `.nuspec` :

```cli
nuget spec
```

Là encore, le fichier `.nuspec` généré ne contient aucune référence explicite aux fichiers inclus dans la structure de dossiers. NuGet inclut automatiquement tous les fichiers lorsque le package est créé. Vous devez quand même modifier les valeurs d’espace réservé dans d’autres parties du manifeste.

### <a name="from-an-assembly-dll"></a>À partir d’une DLL d’assembly

Dans le cas simple d’une création de package à partir d’un assembly, vous pouvez générer un fichier `.nuspec` à partir des métadonnées incluses dans l’assembly à l’aide de la commande suivante :

```cli
nuget spec <assembly-name>.dll
```

L’utilisation de cette forme remplace quelques espaces réservés dans le manifeste par des valeurs spécifiques de l’assembly. Par exemple, la propriété `<id>` est définie sur le nom de l’assembly et `<version>` est définie sur la version de l’assembly. Les autres propriétés dans le manifeste, en revanche, n’ont pas de valeurs correspondantes dans l’assembly et contiennent donc toujours des espaces réservés.

### <a name="from-a-visual-studio-project"></a>À partir d’un projet Visual Studio

La création d’un fichier `.nuspec` à partir d’un fichier `.csproj` ou `.vbproj` s’avère pratique, car les autres packages installés dans ces projets sont automatiquement référencés en tant que dépendances. Utilisez simplement la commande suivante dans le même dossier que le fichier projet :

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Le fichier `<project-name>.nuspec` obtenu contient les *jetons* qui sont remplacés au moment de l’empaquetage par des valeurs du projet, notamment des références à tous les autres packages qui ont déjà été installés.

Un jeton est délimité par des symboles `$` des deux côtés de la propriété de projet. Par exemple, la valeur `<id>` dans un manifeste généré de cette manière se présente généralement comme suit :

```xml
<id>$id$</id>
```

Ce jeton est remplacé par la valeur `AssemblyName` du fichier projet au moment de l’empaquetage. Pour connaître le mappage exact des valeurs de projet sur les jetons `.nuspec`, consultez les [Informations de référence sur les jetons de remplacement](../reference/nuspec.md#replacement-tokens).

Les jetons vous évite d’avoir à mettre à jour des valeurs cruciales comme le numéro de version dans le fichier `.nuspec` quand vous mettez à jour le projet. (Vous pouvez toujours remplacer les jetons par des valeurs littérales, si vous le souhaitez). 

Notez qu’il existe plusieurs autres options d’empaquetage disponibles quand vous utilisez un projet Visual Studio, comme décrit plus loin dans [Exécution de nuget pack pour générer le fichier .nupkg](#running-nuget-pack-to-generate-the-nupkg-file).

#### <a name="solution-level-packages"></a>Packages au niveau de la solution

*NuGet 2.x uniquement. Non disponible dans NuGet 3.0+.*

NuGet 2.x prenait en charge la notion de package au niveau de la solution qui permettait d’installer des outils ou des commandes supplémentaires pour la console du gestionnaire de package (contenu du dossier `tools`), sans ajouter de références, de contenu, ni générer des personnalisations pour les projets de la solution. De tels packages ne contiennent aucun fichier dans leurs dossiers `lib`, `content` ou `build` directs et aucune de leurs dépendances n’ont des fichiers dans leurs dossiers `lib`, `content` ou `build` respectifs.

NuGet assure le suivi des packages installés au niveau de la solution dans un fichier `packages.config` du dossier `.nuget`, au lieu du fichier `packages.config` du projet.

### <a name="new-file-with-default-values"></a>Nouveau fichier avec des valeurs par défaut

La commande suivante crée un manifeste par défaut avec des espaces réservés, ce qui vous permet d’être sûr de commencer avec la structure de fichiers appropriée :

```cli
nuget spec [<package-name>]
```

Si vous omettez le \<nom_du_package\>, le fichier obtenu est `Package.nuspec`. Si vous fournissez un nom comme `Contoso.Utility.UsefulStuff`, le fichier est `Contoso.Utility.UsefulStuff.nuspec`.

Le fichier `.nuspec` obtenu contient des espaces réservés pour des valeurs telles que `projectUrl`. Veillez à modifier le fichier avant de l’utiliser pour créer le fichier `.nupkg` final.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Choix d’un identificateur de package unique et définition du numéro de version

L’identificateur de package (élément `<id>`) et le numéro de version (élément `<version>`) sont les deux valeurs les plus importantes dans le manifeste, car ils identifient de façon unique le code exact contenu dans le package.

**Bonnes pratiques en matière d’identificateur de package :**

- **Unicité** : l’identificateur doit être unique sur nuget.org ou dans la galerie qui héberge le package, quelle qu’elle soit. Avant de déterminer un identificateur, faites une recherche dans la galerie applicable pour vérifier si le nom est déjà en cours d’utilisation. Pour éviter les conflits, utilisez le nom de votre société comme première partie de l’identificateur, par exemple `Contoso.`.
- **Noms comme les espaces de noms** : suivez un modèle similaire aux espaces de noms dans .NET, en utilisant la notation à points au lieu de traits d’union. Par exemple, utilisez `Contoso.Utility.UsefulStuff` plutôt que `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`. Les consommateurs trouvent également pratique de faire correspondre l’identificateur du package aux espaces de noms utilisés dans le code.
- **Exemples de package** : si vous produisez un package d’exemple de code qui montre comment utiliser un autre package, attachez `.Sample` comme suffixe à l’identificateur, comme dans `Contoso.Utility.UsefulStuff.Sample`. (L’exemple de package dépend naturellement de l’autre package.) Lorsque vous créez un exemple de package, utilisez la méthode du répertoire de travail basé sur une convention décrite précédemment. Dans le dossier `content`, réorganisez l’exemple de code dans un dossier appelé `\Samples\<identifier>` comme dans `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Bonnes pratiques en matière de version de package :**

- En général, définissez la version du package pour qu’elle corresponde à la bibliothèque, bien que cela ne soit pas strictement obligatoire. C’est très simple lorsque vous limitez un package à un seul assembly, comme décrit précédemment dans [Déterminer quels assemblys empaqueter](#deciding-which-assemblies-to-package). Globalement, n’oubliez pas que NuGet lui-même traire les versions de package lors de la résolution des dépendances, pas les versions d’assembly.
- Lorsque vous utilisez un schéma de version non standard, veillez à prendre en compte les règles de gestion de versions NuGet, comme expliqué dans [Gestion des versions de package](../reference/package-versioning.md).

> Les séries suivantes de courts billets de blog s’avèrent également utiles pour comprendre la gestion de versions :
>
> - [Partie 1 : Affronter les difficultés liées aux DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Partie 2 : L’algorithme principal](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Partie 3 : Unification par le biais de redirections de liaison](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Définition d’un type de package

Avec NuGet 3.5+, les packages peuvent être marqués avec un *type de package* spécifique pour indiquer leur usage prévu. Les packages non marqués avec un type, notamment tous les packages créés avec des versions antérieures de NuGet, sont du type `Dependency` par défaut.

- Les packages de type `Dependency` ajoutent des ressources de build ou d’exécution aux bibliothèques et applications et peuvent être installés dans n’importe quel type de projet (en supposant qu’ils soient compatibles).

- Les packages de type `DotnetCliTool` sont des extensions de l’[interface de ligne de commande .NET](/dotnet/articles/core/tools/index) et ils sont appelés à partir de la ligne de commande. De tels packages peuvent être installés uniquement dans des projets .NET Core et n’ont aucun effet sur les opérations de restauration. Plus d’informations sur ces extensions par projet sont disponibles dans la documentation [Extensibilité de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Les packages de type personnalisé utilisent un identificateur de type arbitraire qui respecte les mêmes règles de format que les ID de package. Tous les types autres que `Dependency` et `DotnetCliTool`, en revanche, ne sont pas reconnus par le gestionnaire de package NuGet dans Visual Studio.

Les types de package sont définis dans le fichier `.nuspec`. Il est préférable pour la compatibilité descendante de ne *pas* définir explicitement le type `Dependency` et de plutôt compter sur le fait que NuGet supposera qu’il s’agit de ce type quand aucun type n’est spécifié.

- `.nuspec` : indique le type de package dans un nœud `packageTypes\packageType` sous l’élément `<metadata>` :

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>Ajout d’un fichier Lisez-moi et d’autres fichiers

Pour spécifier directement les fichiers à inclure dans le package, utilisez le nœud `<files>` dans le fichier `.nuspec`, ce qui *suit* la balise `<metadata>` :

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Lorsque vous utilisez la méthode du répertoire de travail basé sur une convention, vous pouvez placer le fichier Lisez-moi.txt à la racine du package et le reste du contenu dans le dossier `content`. Aucun élément `<file>` n’est nécessaire dans le manifeste.

Lorsque vous incluez un fichier nommé `readme.txt` à la racine du package, Visual Studio affiche le contenu de ce fichier sous forme de texte brut immédiatement après avoir installé le package directement. (Les fichiers Lisez-moi ne s’affichent pas pour les packages installés en tant que dépendances). Par exemple, voici comment s’affiche le fichier Lisez-moi du package HtmlAgilityPack :

![Affichage d’un fichier Lisez-moi pour un package NuGet lors de l’installation](media/Create_01-ShowReadme.png)

> [!Note]
> Si vous incluez un nœud `<files>` vide dans le fichier `.nuspec`, NuGet n’inclut aucun autre contenu dans le package autre que celui du dossier `lib`.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>Inclusion de cibles et de propriétés MSBuild dans un package

Vous pouvez être amené à ajouter des cibles ou propriétés de build personnalisées dans les projets qui utilisent votre package, comme dans le cas de l’exécution d’un processus ou outil personnalisé pendant la génération. Pour cela, vous placez les fichiers sous la forme de `<package_id>.targets` ou `<package_id>.props` (par exemple, `Contoso.Utility.UsefulStuff.targets`) dans le dossier `\build` du projet.

Les fichiers inclus dans le dossier `\build` racine sont considérés comme appropriés à toutes les versions cibles de .Net Framework. Pour fournir des fichiers spécifiques au framework, commencez par les placer dans les sous-dossiers appropriés, notamment :

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Ensuite, dans le fichier `.nuspec`, veillez à faire référence à ces fichiers dans le nœud `<files>` :

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

L’inclusion des propriétés et des cibles MSBuild dans un package a été [introduite avec NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). Il est donc recommandé d’ajouter l’attribut `minClientVersion="2.5"` à l’élément `metadata` pour indiquer la version minimale du client NuGet nécessaire pour utiliser le package.

Quand NuGet installe un package avec des fichiers `\build`, il ajoute des éléments `<Import>` MSBuild au fichier projet pointant vers les fichiers `.targets` et `.props`. (`.props` est ajouté en haut du fichier projet. `.targets` est ajouté en bas.) Un élément `<Import>` MSBuild conditionnel distinct est ajouté pour chaque version cible de .NET Framework.

Les fichiers `.props` et `.targets` MSBuild du ciblage multi-infrastructure peuvent être placés dans le dossier `\buildCrossTargeting`. Lors de l’installation de package, NuGet ajoute les éléments `<Import>` correspondants au fichier projet à la condition que la version cible de .NET Framework ne soit pas définie (la propriété MSBuild `$(TargetFramework)` doit être vide).

Avec NuGet 3.x, les cibles ne sont pas ajoutées au projet, mais accessibles via `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Création de packages avec des assemblys COM Interop

Les packages qui contiennent des assemblys COM Interop doivent inclure un [fichier de cibles](#including-msbuild-props-and-targets-in-a-package) approprié afin que les bonnes métadonnées `EmbedInteropTypes` soient ajoutées aux projets en utilisant le format PackageReference. Par défaut, les métadonnées `EmbedInteropTypes` sont toujours fausses pour tous les assemblys lorsque PackageReference est utilisé, si bien que le fichier de cibles ajoute ces métadonnées explicitement. Pour éviter les conflits, le nom de la cible doit être unique ; dans l’idéal, utilisez une combinaison du nom de votre package et de l’assembly incorporé, en remplaçant `{InteropAssemblyName}` dans l’exemple ci-dessous par cette valeur. (Consultez également [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) pour obtenir un exemple.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Notez que, si le format de gestion `packages.config` est utilisé, l’ajout de références aux assemblys à partir des packages amène NuGet et Visual Studio à rechercher des assemblys COM Interop et à affecter à `EmbedInteropTypes` la valeur true dans le fichier projet. Dans ce cas, les cibles sont remplacées.

De plus, [les ressources de build ne circulent pas de manière transitive](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) par défaut. Les packages créés comme décrit ici fonctionnent différemment quand ils sont extraits en tant que dépendance transitive d’un projet vers une référence de projet. Le consommateur du package peut les autoriser à circuler en modifiant la valeur par défaut PrivateAssets de sorte à ce qu’elle n’inclue pas de build.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Exécution de nuget pack pour générer le fichier .nupkg

Lorsque vous utilisez un assembly ou le répertoire de travail basé sur une convention, créez un package en exécutant `nuget pack` avec votre fichier `.nuspec`, en remplaçant `<project-name>` par votre nom de fichier spécifique :

```cli
nuget pack <project-name>.nuspec
```

Lorsque vous utilisez un projet Visual Studio, exécutez `nuget pack` avec votre fichier projet, ce qui charge automatiquement le fichier `.nuspec` du projet et remplace tous les jetons qu’il contient en utilisant les valeurs contenues dans le fichier projet :

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Il est nécessaire d’utiliser le fichier projet directement pour le remplacement des jetons, car le projet est la source des valeurs de jeton. Le remplacement des jetons ne se produit pas si vous utilisez `nuget pack` avec un fichier `.nuspec`.

Dans tous les cas, `nuget pack` exclut les dossiers qui commencent par un point, comme `.git` ou `.hg`.

NuGet indique s’il existe des erreurs dans le fichier `.nuspec` à corriger, comme l’oubli de modifier des valeurs d’espace réservé dans le manifeste.

Une fois que `nuget pack` réussit, vous avez un fichier `.nupkg` que vous pouvez publier dans une galerie appropriée, comme décrit dans [Publication d’un package](../create-packages/publish-a-package.md).

> [!Tip]
> Une manière utile d’examiner un package après l’avoir créé consiste à l’ouvrir dans l’outil [Explorateur de package](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer). Vous obtenez ainsi une vue graphique du contenu du package et de son manifeste. Vous pouvez également renommer le fichier `.nupkg` obtenu en fichier `.zip` et explorer son contenu directement.

### <a name="additional-options"></a>Options supplémentaires

Vous pouvez utiliser divers commutateurs de ligne de commande avec `nuget pack` pour exclure des fichiers, remplacer le numéro de version dans le manifeste et modifier le dossier de sortie, entre autres fonctionnalités. Pour en obtenir la liste complète, reportez-vous aux [informations de référence sur la commande pack](../tools/cli-ref-pack.md).

Les options suivantes figurent parmi les quelques options communes aux projets Visual Studio :

- **Projets référencés** : si le projet fait référence à d’autres projets, vous pouvez ajouter les projets référencés dans le cadre du package, ou en tant que dépendances, à l’aide de l’option `-IncludeReferencedProjects` :

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Ce processus d’inclusion est récursif, donc si `MyProject.csproj` fait référence aux projets B et C, et que ces projets font référence aux projets D, E et F, alors les fichiers de B, C, D, E et F sont inclus dans le package.

    Si un projet référencé inclut un fichier `.nuspec` bien à lui, alors NuGet ajoute ce projet référencé plutôt en tant que dépendance.  Vous devez empaqueter et publier ce projet séparément.

- **Configuration de build** : par défaut, NuGet utilise la configuration de build par défaut définie dans le fichier projet, généralement *Debug*. Pour compresser des fichiers d’une configuration de build différente, comme *Release*, utilisez l’option `-properties` avec la configuration :

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symboles** : pour inclure les symboles qui permettent aux utilisateurs de parcourir votre code de package dans le débogueur, utilisez l’option `-Symbols` :

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Test de l’installation du package

Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test. Les tests permettent de s’assurer que les fichiers nécessaires se placent tous au bon endroit dans le projet.

Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/ways-to-install-a-package.md).

Pour les tests automatisés, le processus de base est le suivant :

1. Copiez le fichier `.nupkg` dans un dossier local.
1. Ajoutez le dossier à vos sources de package à l’aide de la commande `nuget sources add -name <name> -source <path>` (consultez [Sources nuget](../tools/cli-ref-sources.md)). Notez que vous ne devez définir cette source locale qu’une seule fois sur un ordinateur donné.
1. Installez le package à partir de cette source en utilisant `nuget install <packageID> -source <name>` où `<name>` correspond au nom de votre source tel qu’il est donné à `nuget sources`. La spécification de la source permet de s’assurer que le package est installé à partir de cette source uniquement.
1. Examinez votre système de fichiers pour vérifier que les fichiers sont correctement installés.

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../create-packages/publish-a-package.md).

Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :

- [Gestion des versions de package](../reference/package-versioning.md)
- [Prise en charge de plusieurs frameworks cibles](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md)
- [Localisation](../create-packages/creating-localized-packages.md)
- [Préversions](../create-packages/prerelease-packages.md)

Enfin, il existe d’autres types de package à connaître :

- [Packages natifs](../create-packages/native-packages.md)
- [Packages de symboles](../create-packages/symbol-packages.md)
