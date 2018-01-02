---
title: "Informations de référence sur le fichier project.json pour NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d64fa6d8-a3f7-4c72-95d3-1a964375ccb8
description: "Dans certains types de projets, project.json gère la liste des packages NuGet utilisés dans le projet."
keywords: "project.json NuGet, références de package NuGet, dépendances NuGet, project.lock.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e8763c22bda0c384b8bb1a00078a314e4bedc262
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-reference"></a>Documentation de référence sur project.json

*NuGet 3.x+*

Le fichier `project.json` gère une liste de packages utilisés dans un projet, appelée format de référence de package. Il remplace `packages.config` mais est à son tour remplacé par [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) avec NuGet 4.0 +.

Le fichier [`project.lock.json`](#projectlockjson) (décrit ci-dessous) est également utilisé dans les projets employant `project.json`.

`project.json` présente la structure de base suivante, où chacun des quatre objets de niveau supérieur peut avoir un nombre quelconque d’objets enfants :

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }  
}
```
 
## <a name="dependencies"></a>Dépendances

Répertorie les dépendances de package NuGet de votre projet sous la forme suivante :

```json
"PackageID" : "version_constraint"
```
  
Exemple :

```json
"dependencies": {   
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"   
}
```

La section `dependencies` est l’emplacement où la boîte de dialogue Gestionnaire de package NuGet ajoute des dépendances de package à votre projet.

L’ID du package correspond à l’ID du package sur nuget.org, identique à l’ID utilisé dans la console du Gestionnaire de package : `Install-Package Microsoft.NETCore`.

Lors de la restauration de packages, la contrainte de version `"5.0.0"` implique `>= 5.0.0`. Autrement dit, si 5.0.0 n’est pas disponible sur le serveur mais que 5.0.1 l’est, NuGet installe 5.0.1 et vous informe de la mise à niveau. NuGet récupère sinon la version la plus ancienne possible sur le serveur correspondant à la contrainte.

Consultez [Résolution des dépendances](../consume-packages/dependency-resolution.md) pour plus d’informations sur les règles de résolution.

### <a name="managing-dependency-assets"></a>Gestion des ressources de dépendance

Les ressources des dépendances qui sont transférées dans le projet de niveau supérieur sont contrôlées en spécifiant un ensemble de balises séparées par des virgules dans les propriétés `include` et `exclude` de la référence de dépendance. Les balises sont répertoriées dans le tableau ci-dessous :

| Balise include/exclude | Dossiers affectés de la cible |
| --- | --- |
| contentFiles | Contenu  |
| runtime | Runtime, Resources et FrameworkAssemblies  |
| compile | lib |
| build | build (propriétés et cibles MSBuild) |
| natifs | natifs |
| aucun | Aucun dossier |
| toutes les | Tous les dossiers |

Les balises spécifiées avec `exclude` sont prioritaires sur celles spécifiées avec `include`. Par exemple, `include="runtime, compile" exclude="compile"` est identique à `include="runtime"`.

Par exemple, pour inclure les dossiers `build` et `native` d’une dépendance, utilisez le code suivant :

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Pour exclure les dossiers `content` et `build` d’une dépendance, utilisez le code suivant :

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Frameworks

Répertorie les frameworks sur lesquels le projet est exécuté, comme `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Une seule entrée est autorisée dans la section `frameworks`. (Les fichiers `project.json` pour les projets ASP.NET qui sont générés avec une chaîne d’outils DNX dépréciée, ce qui permet plusieurs cibles, représentent une exception.)

## <a name="runtimes"></a>Runtimes

Répertorie les systèmes d’exploitation et les architectures sur lesquels votre application est exécutée, comme `win10-arm`, `win8-x64`, `win8-x86`.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Un package contenant une bibliothèque de classes portable qui peut s’exécuter sur n’importe quel runtime n’a pas besoin d’en spécifier un. Cela doit également être vrai pour toutes les dépendances, sinon vous devez spécifier les runtimes.


## <a name="supports"></a>Prises en charge

Définit un ensemble de vérifications pour les dépendances de package. Vous pouvez définir l’emplacement d’exécution prévu pour la bibliothèque de classes portable ou l’application. Les définitions ne sont pas restrictives, comme votre code peut être en mesure de s’exécuter à un autre emplacement. Toutefois, la spécification de ces vérifications permet à NuGet de contrôler que toutes les dépendances sont satisfaites sur les monikers du Framework cible répertoriés. `net46.app`, `uwp.10.0.app`, entre autres, en sont des exemples de valeurs.

Cette section doit être renseignée automatiquement quand vous sélectionnez une entrée dans la boîte de dialogue des cibles de bibliothèque de classes portable.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importations

Les importations sont conçues pour permettre aux packages qui utilisent le moniker du Framework cible `dotnet` de fonctionner avec les packages qui ne déclarent pas de moniker du Framework cible dotnet. Si votre projet utilise le moniker du Framework cible `dotnet`, tous les packages dont vous dépendez doivent également avoir un moniker du Framework cible `dotnet`, sauf si vous ajoutez le code suivant à votre fichier `project.json` afin de permettre à des plateformes autres que `dotnet` d’être compatibles avec `dotnet` :

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Si vous utilisez le moniker du Framework cible `dotnet`, le système de projet de bibliothèque de classes portable ajoute l’instruction `imports` appropriée selon les cibles prises en charge.

## <a name="differences-from-portable-apps-and-web-projects"></a>Différences par rapport à des applications portables et des projets web

Le fichier `project.json` utilisé par NuGet est un sous-ensemble des éléments se trouvant dans les projets ASP.NET Core. Dans ASP.NET Core, `project.json` est utilisé pour les métadonnées de projet, les informations de compilation et les dépendances. Quand ils sont utilisés dans d’autres systèmes de projet, ces trois éléments sont répartis en fichiers distincts et `project.json` contient moins d’informations. Les différences notables sont notamment les suivantes :

- Il ne peut exister qu’un framework dans la section `frameworks`.

- Le fichier ne peut pas contenir de dépendances, d’options de compilation ni d’autres éléments que vous voyez dans les fichiers `project.json` DNX. Étant donné qu’il ne peut exister qu’un seul framework, il est inutile d’entrer des dépendances spécifiques au framework.

- La compilation étant gérée par MSBuild, les options de compilation et les définitions du préprocesseur, entre autres, font toutes partie du fichier projet MSBuild et non de `project.json`.

Dans NuGet 3+, les développeurs ne sont pas censés modifier manuellement le fichier `project.json`, car l’interface utilisateur du Gestionnaire de package dans Visual Studio manipule le contenu. Ceci dit, vous pouvez certainement modifier le fichier, mais vous devez générer le projet pour démarrer une restauration de package ou appeler la restauration d’une autre façon. Consultez [Restauration de packages](../Consume-Packages/Package-Restore.md).


## <a name="projectlockjson"></a>project.lock.json

Le fichier `project.lock.json` est généré au cours de la restauration des packages NuGet dans les projets qui utilisent `project.json`. Il contient un instantané de toutes les informations qui sont générées quand NuGet parcourt le graphique des packages et inclut la version, le contenu et les dépendances de tous les packages dans votre projet. Le système de génération l’utilise pour choisir les packages à partir d’un emplacement global qui sont pertinents lors de la génération du projet au lieu de dépendre d’un dossier de packages local dans le projet lui-même. Les performances de génération sont ainsi plus rapides, car il est nécessaire d’accéder en lecture seule à `project.lock.json` et non à de nombreux fichiers `.nuspec` séparés.

`project.lock.json` étant généré automatiquement lors de la restauration de package, il peut être omis du contrôle de code source en l’ajoutant aux fichiers `.gitignore` et `.tfignore` (consultez [Packages et contrôle de code source](../Consume-Packages/Packages-and-Source-Control.md)). Toutefois, si vous l’incluez dans le contrôle de code source, l’historique des modifications affiche les modifications dans les dépendances résolues au fil du temps.
