---
title: Meilleures pratiques de création de packages
description: Guide général des meilleures pratiques pour la création de packages NuGet de haute qualité.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859068"
---
# <a name="package-authoring-best-practices"></a>Meilleures pratiques de création de packages

Ce guide est destiné à fournir aux auteurs de package NuGet une référence légère pour créer et publier des packages de haute qualité. Il se concentre principalement sur les meilleures pratiques spécifiques aux packages, telles que les métadonnées et la compression. Pour obtenir des suggestions plus approfondies sur la création de bibliothèques de haute qualité, consultez le Guide de la [bibliothèque open source](https://docs.microsoft.com/dotnet/standard/library-guidance/).net.

## <a name="types-of-recommendations"></a>Types de suggestions

Chaque article présente quatre types de suggestions : **À faire**, **Envisager**, **Éviter** et **À ne pas faire**. Le type de recommandation indique le degré de détail de la procédure à suivre.

Vous devez presque toujours suivre une suggestion **À faire**. Par exemple :

✔️ incluez une brève description de votre package qui décrit ce qu’il fait.

En revanche, **envisagez** d’utiliser des recommandations en général, mais il existe des exceptions légitimes à la règle :

✔️ À ENVISAGER : Choisir un nom de package NuGet avec un préfixe qui répond à la réservation du préfixe des [critères](https://docs.microsoft.com/nuget/reference/id-prefix-reservation) NuGet.

Les suggestions **Éviter** indiquent quelque chose qui n’est généralement pas une bonne idée, mais enfreindre les règles peut parfois avoir du sens :

❌ Évitez les références de package NuGet qui demandent une version exacte.

Et enfin, les suggestions **À ne pas faire** désignent quelque chose que vous ne devez presque jamais faire :

❌ N’utilisez pas la `LicenseUrl` propriété de métadonnées.

## <a name="create-a-nuget-package"></a>Créer un package NuGet

La dernière méthode recommandée pour créer un package NuGet provient d’un [projet de type SDK](https://docs.microsoft.com/nuget/resources/check-project-format). Les propriétés du projet de type SDK, y compris le [Framework cible](https://docs.microsoft.com/dotnet/standard/frameworks) et les [métadonnées du package](#package-metadata), sont définies dans le [fichier projet](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Créez un package à partir de votre projet de style SDK en définissant les propriétés et l’empaquetage nécessaires dans [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) ou l’interface de ligne de [commande dotnet](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).

✔️ créer un projet de type SDK et créer (Pack) votre package à l’aide de Visual Studio ou de l’interface de ligne de commande dotnet.

Pour obtenir des instructions plus détaillées sur la création de packages, notamment les outils clients nécessaires, l’exemple de fichier de projet et les commandes, consultez [créer un package NuGet à l’aide de l’interface CLI dotnet](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).

Pour vous aider à choisir les frameworks .NET à cibler, consultez nos [dernières instructions sur le ciblage multiplateforme](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Métadonnées de package

Les métadonnées sont un composant fondamental d’un package NuGet. La qualité de vos métadonnées peut considérablement influencer la détectabilité, la facilité d’utilisation et la fiabilité de votre package.

Dans Visual Studio, la méthode recommandée pour spécifier les métadonnées de package consiste à accéder aux propriétés du projet > [nom du projet] > package.

Les éléments de métadonnées de package peuvent également être [spécifiés directement dans le fichier projet](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).

Vous trouverez ci-dessous un mappage de table et décrivant les éléments de métadonnées de package disponibles :

| Nom de la propriété Visual Studio                   | [Fichier projet/nom de la propriété MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nom de la propriété NuSpec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | Description                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | Nom ou identificateur du package.                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | Version du package NuGet.                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | Liste séparée par des virgules des auteurs de packages, souvent en utilisant le « nom convivial » de l’individu ou d’une organisation.                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | Description du package.                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | Détails de copyright pour le package.                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | Expression de licence SPDX.       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | Chemin d’accès à un fichier de licence personnalisé.                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | URL de la page d’accueil du projet.                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | Chemin du fichier image de l’icône de package.                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | URL du référentiel à partir duquel le package a été généré.                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | Type de référentiel sur lequel pointe l’URL de dépôt (c.-à-d., « git »).                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | Liste délimitée par des espaces des balises et mots clés qui décrivent le package. Les balises sont utilisées lors de la recherche des packages. |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | Description des modifications apportées à cette version du package.                                                 |

### <a name="package-id"></a>ID du package

Si vous publiez un package entièrement nouveau :

✔️ choisir un ID de package unique et clairement différencié des packages existants sur NuGet.org.
> Vous pouvez vérifier si un ID de package est unique et dérivables en recherchant l’ID sur NuGet.org ou en vérifiant si le lien suivant existe : https://www.nuget.org/packages/<package nom \> .

✔️ ENVISAGER de choisir un nom de package NuGet avec un préfixe qui répond aux [critères de réservation de préfixe](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)de NuGet.
> La réservation de l’ID de préfixe pour votre package vous permet d’obtenir la coche vérifiée : ![ image](media/Verified-check-mark.png)
> 
> Consultez les [documents de réservation de préfixe d’ID de package](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) pour en savoir plus.

### <a name="package-version"></a>Version du package

✔️ envisagez d’utiliser [SemVer](https://semver.org/) pour la version de votre package NuGet.
> Fondamentalement, cela implique l’utilisation du format majeur. minor. patch [-version préliminaire].

✔️ publiez un package en tant que package de préversion, s’il est non stable ou en [version](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) préliminaire.

Pour obtenir des instructions plus avancées, consultez le Guide de contrôle de version de la [bibliothèque .net](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) .

### <a name="authors"></a>Auteurs

✔️ Utilisez le champ auteur pour votre ou le « nom convivial » de votre organisation.
> Par exemple, si le nom d’utilisateur de mon NuGet.org est « jdoe », l’utilisation de « Jane Doe » pour le champ d’auteur peut aider les utilisateurs à se reconnaître comme auteur. Si le nom d’utilisateur NuGet.org de mon organisation est « ContosoToolkit », l’utilisation de « Contoso Corporation » peut être plus reconnaissable et inspirer une confiance plus grande aux consommateurs.
### <a name="description"></a>Description

✔️ incluez une brève description (jusqu’à 4000 caractères) pour décrire votre package.
> Les descriptions de packages sont l’un des champs les plus importants dans la recherche NuGet. il s’agit probablement de la première chose que les consommateurs potentiels recherchent pour déterminer si un package est adapté à ces derniers.

### <a name="copyright"></a>copyright

✔️ envisagez de Copyrighter votre package avec « Copyright (c) <nom/entreprise \> <année \> ».
>Une mention de droits d’auteur indique essentiellement que votre travail ne peut pas être copié sans votre autorisation. L’inclusion d’une mention de droits d’auteur dans votre package est simple et n’a aucun effet.

Exemple : Copyright (c) contoso 2020

### <a name="licensing"></a>Licence

✔️ [inclure une expression de licence ou un fichier de licence dans votre package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Un projet sans licence utilise par défaut le [Copyright exclusif](https://choosealicense.com/no-permission/), ce qui signifie que vous n’avez accordé aucune autorisation pour utiliser votre projet.

❌ N’utilisez pas la propriété de `LicenseUrl` métadonnées déconseillées.
> Cela présente une ambiguïté légale au fur et à mesure que les modifications de licence au niveau de l’URL modifient rétroactivement la licence affichée pour les versions précédentes du package.

#### <a name="if-your-package-is-open-source"></a>Si votre package est [Open source](https://opensource.org/osd)

✔️ [Choisissez une licence Open source](https://choosealicense.com/) pour rendre votre package open source.
> *« Les licences Open source sont des licences conformes à la définition Open source. en bref, elles autorisent l’utilisation, la modification et le partage de logiciels librement. »* -Open Source Initiative. Pour en savoir plus sur les logiciels open source et l’initiative Open source, consultez https://opensource.org/ .

✔️ envisagez [d’inclure une expression de licence dans votre package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Les expressions de licence sont exposées le plus clairement et le rendent plus évidente aux consommateurs s’ils peuvent utiliser votre package ou si la licence a été modifiée. 
> [!Note]
> NuGet.org accepte uniquement des expressions de licence pour les licences approuvées par l’initiative Open source ou la Fondation logicielle gratuite.

#### <a name="if-your-package-is-not-open-source"></a>Si votre package n’est pas Open source

✔️ [incluez un fichier de licence dans votre package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Tout fichier de licence (. txt ou. MD) peut être ajouté à votre package, y compris les licences non standard. 

### <a name="project-url"></a>URL du projet

✔️ envisagez d’inclure un lien vers un projet, un référentiel ou un site Web d’entreprise associé.
> Votre site de projet doit avoir tout ce que les utilisateurs doivent savoir sur votre package et sera probablement là où les utilisateurs rechercheront de la documentation.

### <a name="icon"></a>Icône

✔️ envisagez d' [inclure une icône avec votre package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) pour vous aider à le distinguer visuellement. Il s’agit d’un ajout relativement petit qui peut améliorer la perception de la qualité des packages.
> Les icônes peuvent être spécifiques à des packages individuels ou être un logo de personnalisation.

✔️ Utilisez une image 128 x 128 et dotée d’un arrière-plan transparent (PNG) pour un meilleur affichage des résultats.
> NuGet met automatiquement à l’échelle votre image sur le client sur lequel elle est affichée.

❌ N’utilisez pas la propriété de `IconUrl` métadonnées déconseillées.

### <a name="repository-type-and-url"></a>Type de référentiel et URL

✔️ envisagez de configurer le [lien source](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) pour ajouter automatiquement les métadonnées du contrôle de code source à votre package NuGet et rendre votre bibliothèque plus facile à déboguer.
> Le lien source ajoute automatiquement `Repository URL` et `Repository Type` aux métadonnées du package. Elle ajoute également la validation spécifique associée à la version de votre package.

### <a name="tags"></a>Étiquettes

✔️ inclure plusieurs balises avec des termes clés liés à votre package pour améliorer la détectabilité.
> Les balises sont prises en compte dans l’algorithme de recherche de NuGet. org et sont particulièrement utiles pour les termes qui ne sont pas dans l’ID de package, mais qui sont pertinents.

Par exemple, si j’ai publié un package pour enregistrer des chaînes dans la console, je vais inclure : « journalisation, Journal, console, chaîne, sortie »

### <a name="release-notes"></a>Notes de publication

✔️ envisagez d’inclure des notes de publication avec chaque mise à jour décrivant les modifications apportées.
> Bien qu’il n’existe aucun format spécifique requis pour les notes de publication, nous vous recommandons d’inclure :
>
> 1. Changements cassants
> 2. Nouvelles fonctionnalités
> 3. Résolution des bogues
> 
> Si vous avez déjà suivi des notes de publication ou un journal des modifications dans votre référentiel, vous pouvez également inclure un lien vers le fichier approprié.

## <a name="related-topics"></a>Rubriques connexes

- [Créer et publier un package (interface CLI dotnet)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [Créer et publier un package (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
