---
title: Créer un package NuGet à l’aide de l’interface CLI dotnet
description: Guide détaillé sur le processus de conception et de création d’un package NuGet, comprenant des points de décision clés comme les fichiers et la gestion de versions.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462456"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Créer un package NuGet à l’aide de l’interface CLI dotnet

Quel que soit la fonction de votre package ou le code qu’il contient, vous utilisez l’un des outils CLI, `nuget.exe` ou `dotnet.exe`, pour empaqueter cette fonctionnalité dans un composant qui peut être partagé et utilisé avec d’autres développeurs. Cet article décrit comment créer un package à l’aide de l’interface CLI dotnet. Pour installer l’interface CLI `dotnet`, consultez [Installer les outils clients NuGet](../install-nuget-client-tools.md). À compter de Visual Studio 2017, l’interface CLI dotnet est incluse dans les charges de travail .NET Core.

Pour les projets .NET Core et .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md), et tout autre projet de style SDK, NuGet utilise les informations dans le fichier projet directement pour créer un package. Pour des tutoriels pas à pas, consultez [Créer des packages .NET Standard avec l’interface CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Créer des packages .NET Standard avec Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` est fonctionnellement équivalent à `dotnet pack`. Pour créer avec MSBuild, les concepts sont les mêmes que ceux décrits dans cet article, mais les commandes de ligne de commande sont légèrement différentes. De même, avec un projet non-SDK-style autre que SDK et avec `<PackageReference>`, vous pouvez utiliser `msbuild /t:pack`. Dans ces scénarios, vous devez ajouter le package NuGet. Build.Tasks.Pack à leurs dépendances. Consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md).

> [!IMPORTANT]
> Cette rubrique s’applique aux projets [SDK-style](../resources/check-project-format.md), qui sont généralement des projets .net Core et .NET Standard.

## <a name="set-properties"></a>Définir des propriétés

Les propriétés suivantes sont requises pour créer un package.

- `PackageId`, l’identificateur du package, qui doit être unique dans toute la galerie qui héberge le package. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.
- `Version`, un numéro de version spécifique au format *version_principale.version_secondaire.version_corrective [-suffixe]* où *-suffixe* identifie les [versions préliminaires](prerelease-packages.md). Si elle n’est pas spécifiée, la valeur par défaut est 1.0.0.
- Titre du package tel qu’il doit apparaître sur l’hôte (par exemple nuget.org)
- `Authors`, informations sur l’auteur et le propriétaire. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.
- `Company`, le nom de votre entreprise. Si elle n’est pas spécifiée, la valeur par défaut est `AssemblyName`.

Dans Visual Studio, vous pouvez définir ces valeurs dans les propriétés du projet (cliquez avec le bouton droit sur le projet dans Explorateur de solutions, choisissez **Propriétés**, puis sélectionnez l’onglet **Package**). Vous pouvez aussi définir directement ces propriétés dans les fichiers projet (`.csproj`).

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> Donnez au package un identificateur unique sur nuget.org ou dans la source de package que vous utilisez.

Vous pouvez également définir les propriétés optionnelles, telles que `Title`, `PackageDescription` et `PackageTags`, comme cela est décrit dans [les cibles de packages MSBuild](../reference/msbuild-targets.md#pack-target), [Contrôle des ressources de dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) et [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.

Pour plus d’informations sur la déclaration des dépendances et la spécification des numéros de version, consultez [Gestion des versions de package](../reference/package-versioning.md). Il est également possible de faire remonter les ressources des dépendances directement dans le package à l’aide des attributs `<IncludeAssets>` et `<ExcludeAssets>`. Pour plus d’informations, consultez [Contrôle des ressources des dépendances](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Choisir un identificateur de package unique et définir le numéro de version

L’identificateur de package et le numéro de version sont les deux valeurs les plus importantes dans le projet, car ils identifient de façon unique le code exact contenu dans le package.

**Bonnes pratiques en matière d’identificateur de package :**

- **Unicité** : L’identificateur doit être unique sur nuget.org ou dans la galerie qui héberge le package, quelle qu’elle soit. Avant de déterminer un identificateur, faites une recherche dans la galerie applicable pour vérifier si le nom est déjà en cours d’utilisation. Pour éviter les conflits, utilisez le nom de votre société comme première partie de l’identificateur, par exemple `Contoso.`.
- **Noms comme les espaces de noms** : Suivez un modèle similaire aux espaces de noms dans .NET, en utilisant la notation à points au lieu de traits d’union. Par exemple, utilisez `Contoso.Utility.UsefulStuff` plutôt que `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`. Les consommateurs trouvent également pratique de faire correspondre l’identificateur du package aux espaces de noms utilisés dans le code.
- **Exemples de package** : Si vous produisez un package d’exemple de code qui montre comment utiliser un autre package, attachez `.Sample` comme suffixe à l’identificateur, comme dans `Contoso.Utility.UsefulStuff.Sample`. (L’exemple de package dépend naturellement de l’autre package.) Lorsque vous créez un exemple de package, utilisez la valeur `contentFiles` dans `<IncludeAssets>`. Dans le dossier `content`, réorganisez l’exemple de code dans un dossier appelé `\Samples\<identifier>` comme dans `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Bonnes pratiques en matière de version de package :**

- En général, définissez la version du package pour qu’elle corresponde au projet (ou à l’assembly), bien que cela ne soit pas strictement obligatoire. C’est simple lorsque vous limitez un package à un assembly unique. Globalement, n’oubliez pas que NuGet lui-même traire les versions de package lors de la résolution des dépendances, pas les versions d’assembly.
- Lorsque vous utilisez un schéma de version non standard, veillez à prendre en compte les règles de gestion de versions NuGet, comme expliqué dans [Gestion des versions de package](../reference/package-versioning.md). NuGet est la plupart du temps [conforme à SemVer 2](../reference/package-versioning.md#semantic-versioning-200).

> Pour plus d’informations sur la résolution des dépendances, consultez [Résolution des dépendances avec PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Pour obtenir des informations plus anciennes qui peuvent également aider à mieux comprendre le contrôle de version, consultez cette série de billets de blog.
>
> - [Partie 1 : Affronter les difficultés liées aux DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Partie 2 : L’algorithme principal](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Partie 3 : Unification par le biais de redirections de liaison](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a>Exécuter la commande pack

Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `dotnet pack`, qui génère également le projet automatiquement :

```cli
# Uses the project file in the current folder by default
dotnet pack
```

La sortie affiche le chemin d’accès du fichier `.nupkg` :

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Générer automatiquement le package à la création

Pour exécuter automatiquement `dotnet pack` pendant l’exécution de `dotnet build`, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Quand vous exécutez `dotnet pack` sur une solution, cela compresse tous les projets de la solution qui peuvent être compressés (la propriété [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) a la valeur `true`).

> [!NOTE]
> Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.

### <a name="test-package-installation"></a>Tester l’installation de package

Avant de publier un package, il est d’usage de tester son processus d’installation dans un projet de test. Les tests permettent de s’assurer que les fichiers nécessaires se placent tous au bon endroit dans le projet.

Vous pouvez tester des installations manuellement dans Visual Studio ou à partir de la ligne de commande en suivant les [étapes d’installation normales du package](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Les packages sont immuables. Si vous remédiez à un problème, modifiez le contenu du package et compressez-le à nouveau. Si vous répétez un test, vous utiliserez l’ancienne version du package tant que vous n’aurez pas [effacé votre dossier de packages globaux](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). C’est particulièrement utile lorsque vous testez des packages qui n’utilisent pas une étiquette de version préliminaire unique sur chaque build.

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez créé un package, qui est un fichier `.nupkg`, vous pouvez le publier dans la galerie de votre choix comme décrit dans [Publication d’un package](../nuget-org/publish-a-package.md).

Vous pouvez également étendre les fonctionnalités de votre package ou prendre en charge d’autres scénarios comme décrit dans les rubriques suivantes :

- [Gestion des versions de package](../reference/package-versioning.md)
- [Prendre en charge plusieurs frameworks cibles](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformations de fichiers sources et de configuration](../create-packages/source-and-config-file-transformations.md)
- [Localisation](../create-packages/creating-localized-packages.md)
- [Préversions](../create-packages/prerelease-packages.md)
- [Définir un type de package](../create-packages/set-package-type.md)
- [Créer des packages avec des assemblys COM Interop](../create-packages/author-packages-with-COM-interop-assemblies.md)

Enfin, il existe d’autres types de package à connaître :

- [Packages natifs](../create-packages/native-packages.md)
- [Packages de symboles](../create-packages/symbol-packages.md)
