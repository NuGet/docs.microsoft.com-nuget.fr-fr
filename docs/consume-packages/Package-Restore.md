---
title: Restauration des packages NuGet
description: Vue d’ensemble décrivant comment NuGet restaure les packages dont dépend un projet (notamment les procédures de désactivation de la restauration et de restriction des versions).
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467798"
---
# <a name="package-restore"></a>Restauration des packages

Pour promouvoir un environnement de développement plus propre et réduire la taille du référentiel, la fonctionnalité de **restauration de package** de NuGet installe toutes les dépendances d’un projet qui sont listées dans le fichier projet ou `packages.config`. Le commandes `dotnet build` et `dotnet run` de .NET Core 2.0+ effectuent une restauration automatique des packages. Visual Studio peut restaurer les packages automatiquement à la génération d’un projet. Vous pouvez aussi restaurer des packages manuellement, à tout moment, en utilisant Visual Studio, `nuget restore`, `dotnet restore` et xbuild sur Mono.

La restauration des packages garantit la disponibilité de toutes les dépendances d’un projet sans avoir à les stocker dans le contrôle de code source. Pour configurer votre référentiel de contrôle de code source afin d’exclure les binaires des packages, consultez [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Vue d’ensemble de la restauration des packages

La restauration des packages installe tout d’abord les dépendances directes nécessaires d’un projet, puis toutes les dépendances du graphe des dépendances de ces packages.

Si un package n’est pas déjà installé, NuGet essaie d’abord de le récupérer à partir du [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Si le package ne se trouve pas dans le cache, NuGet tente de le télécharger à partir de toutes les sources activées dans la liste sous **Outils** > **Options** > **Gestionnaire de package NuGet** > **Sources de package** dans Visual Studio. Lors de la restauration, NuGet ignore l’ordre des sources de packages et utilise le package provenant de la première source à répondre aux requêtes. Pour plus d’informations sur le comportement de NuGet, consultez [Configurations courantes de NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet n’indique pas l’échec de la restauration d’un package tant que toutes les sources n’ont pas été vérifiées. À ce stade, NuGet ne signale de défaillance que pour la dernière source de la liste. L’erreur implique que le package ne se trouvait dans *aucune* autre source, même si les erreurs ne sont pas affichées pour chacune de ces sources.

Vous pouvez déclencher la restauration des packages à l’aide des méthodes suivantes :

- **Interface CLI dotnet** : utilisez la commande [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) pour restaurer les packages listés dans le fichier projet avec [PackageReference](../consume-packages/package-references-in-project-files.md). Dans .NET Core 2.0 et ultérieur, la restauration s’effectue automatiquement avec les commandes `dotnet build` et `dotnet run`.  

- **Gestionnaire de package** : dans Visual Studio sur Windows, la restauration des packages est automatique quand vous créez un projet à partir d’un modèle ou que vous générez un projet, selon les options décrites dans [Activer et désactiver la restauration des packages](#enable-and-disable-package-restore). Dans NuGet 4.0+, la restauration se produit également automatiquement quand vous modifiez un projet basé sur le SDK .NET Core.

    Pour restaurer des packages manuellement, cliquez avec le bouton droit sur la solution dans l’**Explorateur de solutions**, puis sélectionnez **Restaurer des packages NuGet**. Si un ou plusieurs packages ne sont toujours pas installés correctement, l’**Explorateur de solutions** affiche une icône d’erreur. Cliquez avec le bouton droit et sélectionnez **Gérer les packages NuGet**, puis utilisez le **Gestionnaire de package** pour désinstaller et réinstaller les packages souhaités. Pour plus d’informations, consultez [Réinstaller et mettre à jour des packages](../consume-packages/reinstalling-and-updating-packages.md)

    Si vous voyez l’erreur « Ce projet référence un ou plusieurs packages NuGet qui sont introuvables sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », [activez la restauration automatique](#enable-and-disable-package-restore). Consultez également [Résolution des problèmes de restauration de package](Package-restore-troubleshooting.md).

- **Interface CLI nuget.exe** : utilisez la commande [nuget restore](../tools/cli-ref-restore.md) pour restaurer les packages listés dans un fichier projet ou solution, ou dans `packages.config`. 

- **MSBuild** : utilisez la commande [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) pour restaurer les packages listés dans le fichier projet avec PackageReference. Cette commande est disponible uniquement dans NuGet 4.x+ et MSBuild 15.1+, inclus avec Visual Studio 2017 et les versions ultérieures. `nuget restore` et `dotnet restore` utilisent cette commande pour les projets applicables.

- **Azure Pipelines** : quand vous créez une définition de build dans Azure Pipelines, incluez la tâche [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) de NuGet ou la tâche [restore](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) de .NET Core dans la définition avant de lancer des tâches de build. Certains modèles de build incluent la tâche restore par défaut.

- **Azure DevOps Server** : Azure DevOps Server et TFS 2013 et ultérieur restaurent automatiquement les packages au moment de la build, si vous utilisez un modèle Team Build de TFS 2013 ou ultérieur. Pour les versions antérieures de TFS, vous pouvez inclure une étape de build qui exécute une option de restauration en ligne de commande, ou éventuellement migrer le modèle de build vers une version ultérieure. Pour plus d’informations, consultez [Configurer la restauration de packages avec Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore"></a>Activer et désactiver la restauration des packages

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

Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../reference/package-versioning.md).

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

## <a name="troubleshooting"></a>Résolution des problèmes

Consultez [Résolution des erreurs de restauration](package-restore-troubleshooting.md).
