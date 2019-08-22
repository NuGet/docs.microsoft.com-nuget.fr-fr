---
title: Contenu d’archive project.json NuGet
description: Éléments divers du contenu de project.json supprimés à d’autres endroits de la documentation NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 87116669c1e685ffd0dbe4142c2f7e357c413497
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488243"
---
# <a name="projectjson-archive"></a>Archive project.json

Le format de gestion `project.json`, introduit avec NuGet 3.x, est utilisé pour certains types de projets. Il est déconseillé depuis l’introduction du format PackageReference, suivant lequel les dépendances sont listées directement dans le fichier projet.

Voir aussi :

- [Schéma project.json](project-json.md)
- [Impact de project.json sur les auteurs de packages](project-json-impact.md)
- [project.json et UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Format de gestion project.json

*À l’origine dans [Restauration de packages](../what-is-nuget.md).*

Dans la liste des formats de gestion :

- [`project.json`](project-json.md) : *(déconseillé)* fichier JSON qui gère la liste des dépendances du projet avec un graphique de packages global dans un fichier associé, `project.lock.json`. Ce format est déconseillé ; préférer PackageReference.

## <a name="nuget-restore-on-mono"></a>Restauration NuGet sur Mono

*À l’origine dans [Installer les outils clients NuGet](../install-nuget-client-tools.md).*

Fonctionne avec `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Restriction des versions de package avec la restauration

*À l’origine dans [Restauration de packages](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*

- `project.json`: permet de spécifier une plage de versions directement avec le numéro de version de la dépendance. Par exemple :

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Commandes CLI NuGet

- `nuget install` ne fonctionne pas avec `project.json`.
- `nuget restore` : avec des projets qui utilisent `project.json`, génère un fichier `project.lock.json` et un fichier `<project>.nuget.props`, si nécessaire. (Les deux fichiers ne doivent pas obligatoirement figurer dans le contrôle de code source.) L’argument `<projectPath>` peut pointer vers un fichier `project.json` ; il a le même comportement que s’il pointait vers un fichier `packages.config` ou un fichier projet. Dans l’ordre de priorité des dossiers de packages, `%userprofile%\.nuget\packages` est parcouru en premier lorsque `project.json` est utilisé.
- `nuget update`: sur Mono, cette commande ne fonctionne pas avec les projets qui utilisent `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Résolution des dépendances avec PackageReference

*À l’origine dans [Résolution des dépendances](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*

Le comportement de PackageReference s’applique également à `project.json`. La restauration NuGet écrit le graphique de dépendance dans un fichier nommé `project.lock.json` à côté de `project.json`.

## <a name="managing-dependency-assets"></a>Gestion des ressources de dépendance

*À l’origine dans [Résolution des dépendances](../concepts/dependency-resolution.md#managing-dependency-assets).*

Le format `project.json` permet de choisir les ressources des dépendances qui seront acheminées dans le projet de niveau supérieur. Pour plus d’informations, consultez la section [project.json](project-json.md).

## <a name="excluding-references"></a>Exclusion de références

*À l’origine dans [Résolution des dépendances](../concepts/dependency-resolution.md#excluding-references).*

- `project.json` : ajoutez `"exclude" : "all"` dans la dépendance au Package C :

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Résolution des erreurs de package incompatible

*À l’origine dans [Résolution des dépendances](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*

Voici un autre moyen de résoudre les erreurs :

- **Non recommandé** : lorsque vous collaborez avec l’auteur du package, vous pouvez, comme solution temporaire, faire en sorte que les projets ciblant `netcore`, `netstandard` et `netcoreapp` référencent d’autres frameworks comme étant compatibles. Vous permettez ainsi l’utilisation des packages qui ciblent ces autres frameworks. Consultez [Importations project.json](project-json.md#imports) et [Restauration de cibles MSBuild avec PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Cela peut provoquer des comportements inattendus. Par conséquent, il est préférable de résoudre les incompatibilités de package en travaillant à une mise à jour du package avec son auteur.

## <a name="target-frameworks"></a>Versions cibles de .NET Framework

*À l’origine dans [Versions cibles de .NET Framework](../reference/target-frameworks.md).*

- [project.json](project-json.md) : le nœud `frameworks` spécifie les versions de framework avec lesquelles le projet peut être compilé.

## <a name="creating-a-package"></a>Créer un package

*À l’origine dans [Créer un package](../create-packages/creating-a-package.md).*

### <a name="setting-a-package-type"></a>Définition d’un type de package

Avec .NET Core 1.x, lors de l’installation d’un package DotnetCliTool, Visual Studio le place dans le nœud `project.json` `tools` plutôt que dans le nœud `dependencies`.

Les types de package sont définis dans `project.json`.

- `project.json`: indique le type de package dans un json de propriété `packOptions.packageType` :

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Ajout de cibles et de propriétés pour MSBuild

*À l’origine dans [Créer des packages NuGet .NET Standard avec Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Quand vous utilisez `project.json`, les cibles ne sont pas ajoutées au projet, mais sont accessibles via `project.lock.json`.

### <a name="package-versioning"></a>Contrôle de version des packages

*À l’origine dans [Contrôle de version des packages](../concepts/package-versioning.md).*

Lorsque le format `project.json` est utilisé, NuGet prend également en charge la notation avec le caractère générique \* pour le suffixe du chiffre correspondant aux versions majeure, mineure, corrective et préversion.

### <a name="nugetconfig-reference"></a>Informations de référence sur NuGet.Config

*À l’origine dans [Informations de référence sur NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` s’applique uniquement à `project.json`. (Remarque supplémentaire : s’applique également à PackageReference.)

### <a name="nuspec-file-reference"></a>Informations de référence sur nuspec

*À l’origine dans [Informations de référence sur nuspec](../reference/nuspec.md).*

L’élément `<contentFiles>` est utilisé à la place de `<files>` avec `project.json`.

### <a name="package-manager-options-control"></a>Contrôle des options du Gestionnaire de package

*À l’origine dans [Informations de référence sur l’interface utilisateur du Gestionnaire de package](../consume-packages/install-use-packages-visual-studio.md).*

Les projets qui utilisent le format de gestion `project.json` présentent uniquement l’option **Afficher la fenêtre d’aperçu**.

### <a name="visual-studio-templates"></a>Modèles Visual Studio

*À l’origine dans [Packages NuGet dans les modèles Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Meilleures pratiques : les modèles ne comportent pas de fichier `project.json` ; n’incluez aucune référence ni aucun contenu qui serait ajouté lors de l’installation des packages NuGet.