---
title: Restauration des packages NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Vue d’ensemble décrivant comment NuGet restaure les packages dont dépend un projet (notamment les procédures de désactivation de la restauration et de restriction des versions)."
keywords: "Restauration des packages NuGet, installation des packages NuGet, installation de package, restauration des packages, versions des dépendances, désactivation de la restauration automatique, restriction des versions de package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>Restauration des packages

Pour promouvoir un environnement de développement plus propre et pour réduire la taille du référentiel, la fonctionnalité de **restauration des packages** de NuGet installe tous les packages référencés avant la génération d’un projet. Cette fonctionnalité largement utilisée &mdash;disponible dans Visual Studio, .NET Core 2.0+ et avec xbuild sur Mono&mdash; garantit la disponibilité de toutes les dépendances dans un projet, sans que les packages ne doivent être stockés dans le contrôle de code source (consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md) pour configurer votre référentiel de manière à exclure les fichiers binaires des packages). Vous pouvez également à tout moment restaurer manuellement les packages.

Pour plus d’informations concernant la restauration des packages sur les serveurs de builds, consultez [Restauration des packages avec TFBuild](../consume-packages/team-foundation-build.md).

## <a name="package-restore-overview"></a>Présentation de la restauration de package

La restauration des packages installe tout d’abord les dépendances directes d’un projet selon les besoins, puis toutes les dépendances de ces packages dans l’ensemble du graphique de dépendance.

Si un package n’est pas déjà installé, NuGet essaie d’abord de le récupérer à partir du [cache](../consume-packages/managing-the-nuget-cache.md). Si le package ne se trouve pas dans le cache, NuGet tente alors de télécharger (et de mettre en cache) le package à partir de toute les sources activées (consultez [Configuration du comportement de NuGet](Configuring-NuGet-Behavior.md)). Les sources apparaissent également dans la liste **Outils > Options > Gestionnaire de package NuGet > Sources de package** dans Visual Studio. NuGet ignore l’ordre des sources de package et utilise le package provenant de la première source à répondre aux requêtes.

> [!Note]
> NuGet n’indique pas l’échec de la restauration d’un package tant que toutes les sources n’ont pas été vérifiées. À ce stade, NuGet ne signale l’échec que pour la dernière source dans la liste. L’erreur implique que le package ne se trouvait dans *aucune* autre source, même si les erreurs ne sont pas affichées pour chacune de ces sources.

La restauration du package est déclenchée comme suit :

- **Interface CLI dotnet** : utilisez la commande [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), qui restaure les packages répertoriés dans le fichier projet (consultez [PackageReference](../consume-packages/package-references-in-project-files.md)). Avec .NET Core 2.0 et versions ultérieures, la restauration est effectuée automatiquement avec `dotnet build` et `dotnet run`.

- **Interface utilisateur du Gestionnaire de package (Visual Studio sous Windows)** : les packages sont automatiquement restaurés lors de la création d’un projet à partir d’un modèle et lors de la création d’un projet (selon l’option décrite dans [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore)). Dans NuGet 4.0+, la restauration se produit également automatiquement lorsque des modifications sont apportées à un projet basé sur le kit SDK .NET Core.

    Pour effectuer une restauration manuelle, cliquez avec le bouton droit sur la solution dans l’Explorateur de solutions puis sélectionnez **Restaurer des packages NuGet**. Si un ou plusieurs packages individuels ne sont toujours pas installés correctement (comme en témoigne une icône d’erreur dans l’Explorateur de solutions), utilisez l’interface utilisateur du Gestionnaire de package pour désinstaller puis réinstaller les packages affectés. Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md).

    Si vous voyez l’erreur « Ce projet fait référence à des packages NuGet qui sont manquants sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », activez la restauration automatique en suivant les instructions de la section [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore).

- **Interface CLI NuGet** : utilisez la commande [nuget restore](../tools/cli-ref-restore.md), qui restaure les packages répertoriés dans le fichier projet (consultez [PackageReference](../consume-packages/package-references-in-project-files.md)) ou dans un fichier [packages.config](../reference/packages-config.md). Vous pouvez également spécifier un fichier solution.

- **MSBuild** : utilisez la commande [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), qui restaure les packages répertoriés dans le fichier projet (consultez [PackageReference](../consume-packages/package-references-in-project-files.md)). Disponible uniquement dans NuGet 4.x+ et MSBuild 15.1+, inclus avec Visual Studio 2017. `nuget restore` et `dotnet restore` utilisent cette commande pour les projets applicables.

- **Visual Studio Team Services** : lorsque vous créez une définition de build dans Team Services, incluez la tâche [Restauration NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) ou [Restauration .NET Core](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) avant de procéder à toute tâche de génération. Cette tâche est incluse par défaut dans plusieurs modèles de build.

- **Team Foundation Server** : TFS 2013 et versions ultérieures restaure automatiquement les packages lors de la génération, sous réserve que vous utilisiez un modèle Team Build pour TFS 2013 ou version ultérieure. Pour les versions antérieures de TFS, vous pouvez inclure une étape de génération destinée à appeler une des options de restauration en ligne de commande ci-dessus. Vous pouvez éventuellement migrer le modèle de build vers TFS 2013. Pour plus d’informations, consultez [Procédure pas à pas pour la restauration des packages avec Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Activation et désactivation de la restauration des packages

La restauration du package est généralement activée via **Outils > Options > Gestionnaire de package NuGet** dans Visual Studio :

![Contrôle du comportement de la restauration de package via les options du gestionnaire de package NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Autoriser NuGet à télécharger les packages manquants** : contrôle toutes les formes de restauration de package en changeant la valeur du paramètre `packageRestore/enabled` dans le fichier `NuGet.Config`, comme indiqué ci-dessous (`%AppData%\NuGet\NuGet.Config` sur Windows, `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux). Dans Visual Studio, ce paramètre permet à la commande **Restaurer les packages NuGet** figurant dans le menu contextuel de la solution de fonctionner.

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

- **Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** : contrôle la restauration automatique en changeant la valeur du paramètre `packageRestore/automatic` dans le fichier `NuGet.Config`, comme indiqué ci-dessous (`%AppData%\NuGet\NuGet.Config` sur Windows, `~/.nuget/NuGet/NuGet.Config` sur Mac/Linux). Quand cette option est définie, l’exécution d’une build à partir de Visual Studio restaure automatiquement tous les packages manquants. L’option n’affecte pas les builds exécutées à partir de la ligne de commande avec MSBuild.

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

Pour référence, consultez [Fichier config NuGet - Section packageRestore](../reference/nuget-config-file.md#packagerestore-section).

Dans certains cas, un développeur ou une société peuvent vouloir activer ou désactiver la restauration de package pour tous les utilisateurs d’un ordinateur. Pour cela, ajoutez les paramètres ci-dessus au fichier de configuration NuGet global situé dans `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Chaque utilisateur peut ensuite activer la restauration au niveau d’un projet, si nécessaire. Pour plus d’informations sur la façon dont NuGet hiérarchise les fichiers de configuration, consultez [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

## <a name="constraining-package-versions-with-restore"></a>Restriction des versions de package avec la restauration

Lors de la restauration des packages avec l’une des méthodes disponibles, NuGet respecte toutes les restrictions spécifiées dans `packages.config` ou le fichier projet :

- `packages.config` : permet de spécifier une plage de versions dans la propriété `allowedVersion` de la dépendance. Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Exemple :

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference : permet de spécifier une plage de versions directement avec le numéro de version de la dépendance. Exemple :

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../reference/package-versioning.md).

## <a name="troubleshooting"></a>Résolution des problèmes

Consultez [Résolution des erreurs de restauration](package-restore-troubleshooting.md).