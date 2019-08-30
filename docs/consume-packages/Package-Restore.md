---
title: Restauration des packages NuGet
description: Vue d’ensemble décrivant comment NuGet restaure les packages dont dépend un projet (notamment les procédures de désactivation de la restauration et de restriction des versions).
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 93a94a5468b48179d27b89825cebf2447657c8f2
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999982"
---
# <a name="restore-packages-using-package-restore"></a>Restaurer des packages avec la restauration de packages

Pour promouvoir un environnement de développement plus propre et réduire la taille du référentiel, la fonctionnalité de **restauration de package** de NuGet installe toutes les dépendances d’un projet qui sont listées dans le fichier projet ou `packages.config`. Le commandes `dotnet build` et `dotnet run` de .NET Core 2.0+ effectuent une restauration automatique des packages. Visual Studio peut restaurer les packages automatiquement à la génération d’un projet. Vous pouvez aussi restaurer des packages manuellement, à tout moment, en utilisant Visual Studio, `nuget restore`, `dotnet restore` et xbuild sur Mono.

La restauration des packages garantit la disponibilité de toutes les dépendances d’un projet sans avoir à les stocker dans le contrôle de code source. Pour configurer votre référentiel de contrôle de code source afin d’exclure les binaires des packages, consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Vue d’ensemble de la restauration des packages

La restauration des packages installe tout d’abord les dépendances directes nécessaires d’un projet, puis toutes les dépendances du graphe des dépendances de ces packages.

Si un package n’est pas déjà installé, NuGet essaie d’abord de le récupérer à partir du [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Si le package ne se trouve pas dans le cache, NuGet tente de le télécharger à partir de toutes les sources activées dans la liste sous **Outils** > **Options** > **Gestionnaire de package NuGet** > **Sources de package** dans Visual Studio. Lors de la restauration, NuGet ignore l’ordre des sources de packages et utilise le package provenant de la première source à répondre aux requêtes. Pour plus d’informations sur le comportement de NuGet, consultez [Configurations courantes de NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet n’indique pas l’échec de la restauration d’un package tant que toutes les sources n’ont pas été vérifiées. À ce stade, NuGet ne signale de défaillance que pour la dernière source de la liste. L’erreur implique que le package ne se trouvait dans *aucune* autre source, même si les erreurs ne sont pas affichées pour chacune de ces sources.

## <a name="restore-packages"></a>Restaurer des packages

La restauration du package tente d’installer toutes les dépendances de package dans l’état correct correspondant aux références de votre fichier projet ( *. csproj* ) ou de votre fichier *packages. config*. (Dans Visual Studio, les références s’affichent dans l’Explorateur de solutions sous **Dependencies \ NuGet** ou sous le nœud **Références**.)

1. Si les références du package dans votre fichier projet sont correctes, utilisez votre outil préféré pour restaurer les packages.

   - [Visual Studio](#restore-using-visual-studio) ([restauration automatique](#restore-packages-automatically-using-visual-studio) ou [restauration manuelle](#restore-packages-manually-using-visual-studio))
   - [Interface CLI .NET](#restore-using-the-dotnet-cli)
   - [Interface CLI de nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Si les références de package dans votre fichier projet ( *.csproj*) ou votre fichier *packages.config* sont incorrectes (elles ne correspondent pas à l’état souhaité après la restauration du package), vous devez installer ou mettre à jour les packages à la place.

   Pour les projets utilisant PackageReference, après une restauration réussie le package doit se trouver dans le dossier *global-packages* et le fichier `obj/project.assets.json` est recréé. Pour les projets qui utilisent `packages.config`, le package doit apparaître dans le dossier `packages` du projet. Le projet doit à présent être généré. 

2. Après l’exécution de la restauration du package, si vous faites toujours face à des packages manquants ou à des erreurs liées aux packages (comme des icônes d’erreur dans l’Explorateur de solutions de Visual Studio), vous devrez peut-être suivre les instructions fournies dans [Résolution des erreurs de restauration des packages](package-restore-troubleshooting.md) ou bien [réinstaller et mettre à jour les packages](../consume-packages/reinstalling-and-updating-packages.md).

   Dans Visual Studio, la console du gestionnaire de package fournit plusieurs options flexibles pour la réinstallation des packages. Consultez [Utilisation de la mise à jour de package](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Restaurer à l’aide de Visual Studio

Dans Visual Studio sur Windows :

- Restaurer automatiquement les packages, ou

- Restaurer manuellement les packages

### <a name="restore-packages-automatically-using-visual-studio"></a>Restaurer automatiquement les packages avec Visual Studio

La restauration des packages est automatique quand vous créez un projet à partir d’un modèle ou que vous générez un projet, selon les options décrites dans [Activer et désactiver la restauration des packages](#enable-and-disable-package-restore-in-visual-studio). Dans NuGet 4.0+, la restauration se produit également automatiquement quand vous modifiez un projet de type SDK (généralement, un projet .NET Core ou .NET Standard).

1. Activez la restauration automatique des packages en choisissant **Outils** > **Options** > **Gestionnaire de package NuGet**, puis en sélectionnant **Rechercher automatiquement les packages manquants lors de la création dans Visual Studio** sous **Restauration du package**.

   Pour les projets qui ne sont pas de type SDK, vous devez d’abord sélectionner **Autoriser NuGet à télécharger les packages manquants** pour activer l’option de restauration automatique.

1. Générez le projet.

   Si un ou plusieurs packages ne sont toujours pas installés correctement, l’**Explorateur de solutions** affiche une icône d’erreur. Cliquez avec le bouton droit et sélectionnez **Gérer les packages NuGet**, puis utilisez le **Gestionnaire de package** pour désinstaller et réinstaller les packages souhaités. Pour plus d’informations, consultez [Réinstaller et mettre à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)

   Si vous voyez l’erreur « Ce projet référence un ou plusieurs packages NuGet qui sont introuvables sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », [activez la restauration automatique](#enable-and-disable-package-restore-in-visual-studio). Pour les projets plus anciens, consultez également [Migrer vers la restauration automatique des packages](#migrate-to-automatic-package-restore-visual-studio). Consultez également [Résolution des problèmes de restauration de package](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Restaurer manuellement des packages à l’aide de Visual Studio

1. Activez la restauration des packages en choisissant**Outils** > **Options** > **Gestionnaire de package NuGet**. Sous les options **Restauration de package**, sélectionnez **Autoriser NuGet à télécharger les packages manquants**.

1. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur la solution et sélectionnez **Restaurer des packages NuGet**.

   Si un ou plusieurs packages ne sont toujours pas installés correctement, l’**Explorateur de solutions** affiche une icône d’erreur. Cliquez avec le bouton droit et sélectionnez **Gérer les packages NuGet**, puis utilisez le **Gestionnaire de package** pour désinstaller et réinstaller les packages souhaités. Pour plus d’informations, consultez [Réinstaller et mettre à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)

   Si vous voyez l’erreur « Ce projet référence un ou plusieurs packages NuGet qui sont introuvables sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », [activez la restauration automatique](#enable-and-disable-package-restore-in-visual-studio). Pour les projets plus anciens, consultez également [Migrer vers la restauration automatique des packages](#migrate-to-automatic-package-restore-visual-studio). Consultez également [Résolution des problèmes de restauration de package](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Activer et désactiver la restauration des packages dans Visual Studio

Dans Visual Studio, vous contrôlez la restauration des packages essentiellement dans **Outils** > **Options** > **Gestionnaire de package NuGet** :

![Contrôle de la restauration des packages avec les options du Gestionnaire de package NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Autoriser NuGet à télécharger les packages manquants** : contrôle toutes les formes de restauration de packages en changeant la valeur du paramètre `packageRestore/enabled`, défini dans la [section packageRestore](../reference/nuget-config-file.md#packagerestore-section) du fichier `NuGet.Config`, à la valeur `%AppData%\NuGet\` sur Windows ou `~/.nuget/NuGet/` sur Mac/Linux. Ce paramètre active également la commande **Restaurer les packages NuGet** figurant dans le menu contextuel de la solution dans Visual Studio.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Pour remplacer le paramètre `packageRestore/enabled` globalement, définissez la variable d’environnement **EnableNuGetPackageRestore** à la valeur True ou False avant de lancer Visual Studio ou de démarrer une build.

- **Rechercher automatiquement les packages manquants pendant la génération dans Visual Studio** : contrôle la restauration automatique en changeant la valeur du paramètre `packageRestore/automatic` dans la section [packageRestore](../reference/nuget-config-file.md#packagerestore-section) du fichier `NuGet.Config`. Quand cette option est définie à True, l’exécution d’une build à partir de Visual Studio restaure automatiquement tous les packages manquants. Ce paramètre ne s’applique pas aux builds exécutées à partir de la ligne de commande MSBuild.

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

Pour activer ou désactiver la restauration des packages pour tous les utilisateurs d’un ordinateur, un développeur ou une entreprise peut ajouter les paramètres de configuration dans un fichier `nuget.config` global. Le fichier `nuget.config` global se trouve dans `%ProgramData%\NuGet\Config` (parfois dans un dossier Visual Studio `\{IDE}\{Version}\{SKU}\` spécifique) sur Windows, ou dans `~/.local/share` sur Mac/Linux. Chaque utilisateur peut ensuite activer la restauration au niveau d’un projet, si nécessaire. Pour plus d’informations sur la façon dont NuGet hiérarchise les fichiers de configuration, consultez [Configurations courantes de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Si vous modifiez les paramètres `packageRestore` directement dans `nuget.config`, redémarrez Visual Studio pour que la boîte de dialogue **Options** affiche les valeurs actuelles.

## <a name="restore-using-the-dotnet-cli"></a>Restauration à l’aide de l’interface CLI dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Pour ajouter une référence de package manquant au fichier projet, utilisez le [package dotnet add](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), qui exécute également la commande `restore`.

## <a name="restore-using-the-nugetexe-cli"></a>Restaurer à l’aide de l’interface CLI nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> La commande `restore` ne modifie ni un fichier projet ni *packages. config*. Pour ajouter une dépendance, soit vous ajoutez un package via l’interface utilisateur ou la console du Gestionnaire de package dans Visual Studio, soit vous modifiez *packages.config* et exécutez ensuite `install` ou `restore`.

## <a name="restore-using-msbuild"></a>Restaurer avec MSBuild

Pour restaurer les packages listés dans le fichier projet avec PackageReference. utilisez la commande [msbuild -t:restore](../reference/msbuild-targets.md#restore-target). Cette commande est disponible uniquement dans NuGet 4.x+ et MSBuild 15.1+, inclus avec Visual Studio 2017 et les versions ultérieures. `nuget restore` et `dotnet restore` utilisent cette commande pour les projets applicables.

1. Ouvrez une invite de commandes développeur (dans la zone **Rechercher**, saisissez **Invite de commandes développeur**).

   Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu **Démarrer**, car elle est configurée avec tous les chemins nécessaires pour MSBuild.

2. Basculez vers le dossier contenant le fichier projet et saisissez la commande suivante.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Tapez la commande suivante pour régénérer le projet.

   ```cmd
   msbuild
   ```

   Assurez-vous que la sortie MSBuild indique que la génération s’est terminée avec succès.

## <a name="restore-using-azure-pipelines"></a>Restauration avec Azure Pipelines

quand vous créez une définition de build dans Azure Pipelines, incluez la tâche [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) de NuGet ou la tâche [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) de .NET Core dans la définition avant de lancer des tâches de build. Certains modèles de build incluent la tâche restore par défaut.

## <a name="restore-using-azure-devops-server"></a>Restauration avec Azure DevOps Server

Azure DevOps Server et TFS 2013 et ultérieur restaurent automatiquement les packages au moment de la build, si vous utilisez un modèle Team Build de TFS 2013 ou ultérieur. Pour les versions antérieures de TFS, vous pouvez inclure une étape de build qui exécute une option de restauration en ligne de commande, ou éventuellement migrer le modèle de build vers une version ultérieure. Pour plus d’informations, consultez [Configurer la restauration de packages avec Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Restreindre les versions de package avec la restauration

Quand NuGet restaure des packages avec l’une des méthodes disponibles, il respecte toutes les restrictions que vous avez spécifiées dans `packages.config` ou dans le fichier projet :

- Dans `packages.config`, vous pouvez spécifier une plage de versions dans la propriété `allowedVersion` de la dépendance. Pour plus d’informations, consultez [Restriction des versions de mise à niveau](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Par exemple :

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Dans un fichier projet, vous pouvez utiliser PackageReference pour spécifier directement la plage d’une dépendance. Par exemple :

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Forcer la restauration à partir de sources de packages

Par défaut, les opérations de restauration NuGet utilisent des packages provenant des dossiers *global-packages* et *http-cache*, décrits dans [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).

Pour éviter d’utiliser le dossier *global-packages*, effectuez l’une des opérations suivantes :

- Effacez le dossier avec `nuget locals global-packages -clear` ou `dotnet nuget locals global-packages --clear`.
- Changez temporairement l’emplacement du dossier *global-packages* avant l’opération de restauration, en choisissant l’une des méthodes ci-dessous :
  - Définissez la variable d’environnement NUGET_PACKAGES sur un autre dossier.
  - Créez un fichier `NuGet.Config` qui définit `globalPackagesFolder` (si vous utilisez PackageReference) ou `repositoryPath` (si vous utilisez `packages.config`) sur un autre dossier. Pour plus d’informations, consultez les [paramètres de configuration](../reference/nuget-config-file.md#config-section).
  - MSBuild uniquement : spécifiez un autre dossier avec la propriété `RestorePackagesPath`.

Pour éviter d’utiliser le cache pour les sources HTTP, effectuez l’une des opérations suivantes :

- Utilisez l’option `-NoCache` avec `nuget restore`, ou l’option `--no-cache` avec `dotnet restore`. Ces options ne s’appliquent pas aux opérations de restauration effectuées par le biais de la console ou du Gestionnaire de package dans Visual Studio.
- Effacez le cache avec `nuget locals http-cache -clear` ou `dotnet nuget locals http-cache --clear`.
- Définissez temporairement la variable d’environnement NUGET_HTTP_CACHE_PATH sur un autre dossier.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrer vers la restauration automatique des packages (Visual Studio)

Pour NuGet 2.6 et versions antérieures, la restauration de packages intégrée à MSBuild était précédemment prise en charge, mais ce n’est plus le cas. (Elle était généralement activée en cliquant avec le bouton droit sur une solution dans Visual Studio et en sélectionnant **Activer la restauration des packages NuGet**). Si votre projet utilise la restauration de packages intégrée MSBuild dépréciée, effectuez une migration vers la restauration automatique des packages.

Les projets qui utilisent la restauration de packages intégrée à MSBuild contiennent généralement un dossier *.nuget* avec trois fichiers : *NuGet.config*, *nuget.exe* et *NuGet.targets*. La présence d’un fichier *NuGet.targets* détermine si NuGet va continuer à utiliser l’approche intégrée à MSBuild, donc ce fichier doit être supprimé au cours de la migration.

Pour migrer vers la restauration automatique des packages :

1. Fermez Visual Studio.
2. Supprimez *.nuget/nuget.exe* et *.nuget/NuGet.targets*.
3. Pour chaque fichier projet, supprimez l’élément `<RestorePackages>` et supprimez toute référence à *NuGet.targets*.

Pour tester la restauration automatique des packages :

1. Supprimez le dossier *packages* de la solution.
2. Ouvrez la solution dans Visual Studio et démarrez une build.

   La restauration automatique des packages doit télécharger et installer chaque package de dépendances, sans les ajouter au contrôle de code source.

## <a name="troubleshooting"></a>Résolution des problèmes

Consultez [Résolution des erreurs de restauration](package-restore-troubleshooting.md).
