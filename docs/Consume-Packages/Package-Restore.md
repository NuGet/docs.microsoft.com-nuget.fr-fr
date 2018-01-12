---
title: Restauration des packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Explique comment NuGet restaure les packages dont dépend un projet, y compris comment désactiver la restauration et restreindre les versions."
keywords: "Restauration des packages NuGet, installation des packages NuGet, installation de package, restauration des packages, versions des dépendances, désactivation de la restauration automatique, restriction des versions de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>Restauration des packages

Pour promouvoir un environnement de développement plus propre et pour réduire la taille du référentiel, la fonctionnalité de **restauration des packages** de NuGet installe tous les packages référencés avant la génération d’un projet. Cette fonctionnalité largement utilisée garantit la disponibilité de toutes les dépendances dans un projet, sans que les packages ne doivent être stockés dans le contrôle de code source (consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md) pour configurer votre référentiel de manière à exclure les fichiers binaires des packages).

Dans cette rubrique :
- [Guide rapide pour restaurer des packages](#quick-guide-to-package-restore)
- [Présentation de la restauration de package](#package-restore-overview)
- [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore)
- [Restriction des versions de package avec la restauration](#constraining-package-versions-with-restore)
- [Restauration en ligne de commande](#command-line-restore), pour toutes les versions de NuGet
- [Restauration automatique dans Visual Studio](#automatic-restore-in-visual-studio), pour NuGet 2.7 et versions ultérieures
- [Restauration intégrée à MSBuild dans Visual Studio](#msbuild-integrated-restore), pour NuGet 2.6 et versions antérieures
- [Restauration des packages avec Team Foundation Build](#package-restore-with-team-foundation-build)

Le comportement de restauration varie selon la version. Pour vérifier votre version de NuGet, exécutez `nuget.exe` sur la ligne de commande, puis regardez la première ligne de sortie.

Pour plus d’informations concernant la restauration des packages sur les serveurs de builds, consultez [Restauration des packages avec TFBuild](../consume-packages/team-foundation-build.md).

> [!Note]
> Les projets configurés pour la restauration de package fonctionnent également avec xbuild sur Mono.

## <a name="quick-guide-to-package-restore"></a>Guide rapide pour restaurer des packages

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Si vous voyez l’erreur « Ce projet fait référence à des packages NuGet qui sont manquants sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », activez la restauration automatique en suivant les instructions de la section [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Présentation de la restauration de package

Tout d’abord, les références de package sont conservées dans l’un des formats de gestion de package suivants, selon le type du projet et la version de NuGet. Notez que NuGet 4 et MSBuild 15.1 sont installés avec Visual Studio 2017.

| Méthode | Version de NuGet | Description | 
| --- | --- | --- |
| `packages.config` | 2.x+ | Répertorie l’ensemble complet de dépendances. Les packages ajoutés à `packages.config` doivent également être ajoutés au fichier projet, tout comme les cibles et les propriétés. Il s’agit de la méthode de référence pour toutes les versions de NuGet. Cependant, comparée aux autres options, cette méthode ralentit les performances (consultez [Schéma packages.config](../schema/packages-config.md)). | 
| `project.json` | 3.x+ | Utilisé uniquement par défaut avec les projets UWP. Toutefois, les projets peuvent être convertis à partir de `packages.config`. `project.json` répertorie uniquement les dépendances de niveau supérieur. Les références, les cibles et les propriétés sont ajoutées dynamiquement au projet lors de la génération, ce qui permet de meilleures performances par rapport à `packages.config` (consultez [Schéma project.json](../schema/project-json.md)).|
| PackageReference | 4.x+ | Répertorie les dépendances directement dans le fichier projet, dans le nœud `<PackageReference>`, en même temps que `<Reference>` et `<ProjectReference>`. Son fonctionnement est similaire à celui de `project.json`. Consultez [Références de package dans les fichiers projet](../Consume-Packages/Package-References-in-Project-Files.md). |

Ensuite, vous pouvez démarrer une restauration à l’aide de la liste de références de plusieurs façons :

À partir de la ligne de commande ou dans la [console du gestionnaire de package](../tools/Package-Manager-Console.md) :

| Commande | Scénarios applicables |
| --- | --- | 
| `nuget restore` | Toutes les versions de NuGet et tous les types référence. Consultez [Restauration en ligne de commande](#command-line-restore) ci-dessous. | 
| `dotnet restore` | Comme avec `nuget restore` pour les projets .NET Core. Consultez [dotnet restore](/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | NuGet 4.x+ et MSBuild 15.1+ avec les [références de package dans les fichiers projet](../Consume-Packages/Package-References-in-Project-Files.md) uniquement. `nuget restore` et `dotnet restore` utilisent cette commande pour les projets applicables. Consultez [Commandes pack et restore NuGet comme cibles MSBuild - restore target](../schema/msbuild-targets.md#restore-target).|

Visual Studio restaure également des packages à différents moments :

| Type | Moment de la restauration |
| --- | --- |
| Restauration de modèle | Lors de la création d’un projet, puisque certains modèles dépendent de packages externes. |
| Restauration de build | La première étape d’une génération. |
| Restauration de solution | Lorsque l’utilisateur clique avec le bouton droit sur une solution et sélectionne **Restaurer des packages NuGet**. |
| Restauration après modification du projet | *(NuGet 4.x uniquement)* Quand un projet basé sur le SDK .NET Core est utilisé, y compris lorsque l’état du projet change. |

## <a name="enabling-and-disabling-package-restore"></a>Activation et désactivation de la restauration des packages

La restauration du package est généralement activée via **Outils > Options > Gestionnaire de package NuGet** dans Visual Studio :

![Contrôle du comportement de la restauration de package via les options du gestionnaire de package NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Autoriser NuGet à télécharger les packages manquants** : contrôle toutes les formes de restauration de package, en modifiant la valeur du paramètre `packageRestore/enabled` dans le fichier `%AppData%\NuGet\NuGet.Config`, comme indiqué ci-dessous.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  Le paramètre `packageRestore/enabled` peut être remplacé globalement en définissant une variable d’environnement appelée **EnableNuGetPackageRestore** sur la valeur TRUE ou FALSE, avant le lancement de Visual Studio ou le démarrage d’une génération.
    

- **Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** : contrôle la restauration automatique pour NuGet 2.7 et versions ultérieures, en modifiant la valeur du paramètre `packageRestore/automatic` dans le fichier `%AppData%\NuGet\NuGet.Config`, comme indiqué ci-dessous.
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Pour référence, consultez [Fichier config NuGet - Section packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

Dans certains cas, un développeur ou une société peuvent vouloir activer ou désactiver la restauration de package sur un ordinateur par défaut pour tous les utilisateurs. Pour cela, ajoutez les paramètres ci-dessus au fichier de configuration NuGet global situé dans `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Chaque utilisateur peut ensuite activer la restauration au niveau d’un projet, si nécessaire. Pour plus d’informations sur la façon dont NuGet hiérarchise les fichiers de configuration, consultez [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

## <a name="constraining-package-versions-with-restore"></a>Restriction des versions de package avec la restauration

Lorsque NuGet restaure des packages avec l’une des méthodes disponibles, il respecte toutes les restrictions spécifiées dans `packages.config`, `project.json` ou le fichier projet :

- `packages.config` : permet de spécifier une plage de versions dans la propriété `allowedVersion` de la dépendance. Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Exemple :

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json` : permet de spécifier une plage de versions directement avec le numéro de version de la dépendance. Exemple :

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Références de package dans les fichiers projet : spécifiez une plage de versions directement avec le numéro de version de la dépendance. Exemple :
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Restauration en ligne de commande

Pour NuGet 2.7 et versions ultérieures, utilisez la commande [Restore](../tools/cli-ref-restore.md) pour restaurer tous les packages d’une solution (qu’elle utilise `packages.config`, `project.json` ou les références de package dans les fichiers projet). Pour un dossier de projet donné comme `c:\proj\app`, chacune des variations courantes ci-dessous restaure les packages :

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Pour NuGet 4.0+ et MSBuild 15.1+, vous pouvez également utiliser `MSBuild /t:restore`, comme décrit dans [Commandes pack et restore NuGet comme cibles MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Restauration au moment de la génération dans Visual Studio

Par défaut, Visual Studio restaure automatiquement les packages manquants au début d’une génération. Ce comportement peut être modifié en désactivant l’option **Outils > Options > Gestionnaire de package NuGet > Général > Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio**.

Lorsqu’elle est activée, la restauration automatique fonctionne de la manière suivante :

1. Lorsqu’une génération démarre, Visual Studio indique à NuGet de restaurer les packages.
1. NuGet recherche de manière récursive tous les fichiers `packages.config` dans la solution, recherche `project.json`, ou effectue une recherche dans le fichier projet.
1. Pour chaque package répertorié dans les fichiers de référence, NuGet vérifie s’il existe déjà dans la solution (le dossier `packages`, `project.lock.json` ou `project.assets.json`, selon que le projet utilise `packages.config`, `project.json` ou les références de package des fichiers projet).
1. Si le package est introuvable, NuGet tente tout d’abord de le récupérer à partir de son cache (consultez [Gestion du cache NuGet](../consume-packages/managing-the-nuget-cache.md). Si le package ne se trouve pas dans le cache, NuGet tente de télécharger le package à partir des sources activées qui figurent sous **Outils > Options > Gestionnaire de package NuGet > Sources de package**, en suivant l’ordre dans lequel apparaissent les sources. Dans ce cas, NuGet n’indique pas que le package est introuvable tant que toutes les sources n’ont pas été vérifiées. Une fois toutes les sources vérifiées, le package est signalé comme étant introuvable dans la dernière source de la liste. Cependant, cette erreur signifie également que le package ne se trouvait dans aucune autre source, même si aucune erreur ne s’est affichée pour les autres sources.
1. Si le téléchargement réussit, NuGet met en cache le package et l’installe dans la solution (là encore, dans le dossier `packages`, dans `project.lock.json` ou dans ou `project.assets.json`). Sinon, NuGet échoue, ainsi que la génération.

Durant ce processus, une boîte de dialogue de progression s’affiche, avec une option permettant d’annuler la restauration du package.

## <a name="package-restore-with-team-foundation-build"></a>Restauration des packages avec Team Foundation Build

La restauration de package est couramment utilisée lors de la génération de projets sur des serveurs de builds, ainsi qu’avec Team Foundation Server (TFS) et Visual Studio Team Services (et d’autres systèmes de génération, qui ne sont pas abordés ici).

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Lorsque vous créez une définition de build dans Team Services, vous devez inclure la tâche Restaurer les packages NuGet dans la définition avant de procéder à toute tâche de génération. Cette tâche est incluse par défaut dans plusieurs modèles de build.

![Tâche de restauration de package NuGet dans une définition de build Visual Studio Team Services](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Avec TFS 2013 et versions ultérieures, les packages sont automatiquement restaurés par défaut lors de la génération, sous réserve que vous utilisiez un modèle Team Build pour Team Foundation Server 2013 ou version ultérieure.

Si vous utilisez une version antérieure des modèles de build (par exemple, dans un projet qui a été migré à partir de versions antérieures de TFS), vous devrez également migrer les modèles de build vers TFS 2013. Autrement dit, vous allez recréer les parties personnalisées des modèles de build à l’aide du modèle adapté à votre contrôle de code source (TFVC ou Git).

Pour les versions antérieures de TFS, vous pouvez simplement inclure une étape de génération destinée à appeler une [restauration en ligne de commande](#command-line-restore), comme décrit précédemment.

Pour plus d’informations, consultez [Procédure pas à pas pour la restauration des packages NuGet avec Team Foundation Build](../consume-packages/team-foundation-build.md).    
