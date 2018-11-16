---
title: Restauration des packages NuGet
description: Vue d’ensemble décrivant comment NuGet restaure les packages dont dépend un projet (notamment les procédures de désactivation de la restauration et de restriction des versions).
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: da69181aebe3bebcea6acd6e15fde6b77dd33452
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580296"
---
# <a name="package-restore"></a>Restauration des packages

Pour promouvoir un environnement de développement plus propre et réduire la taille du référentiel, la fonctionnalité de **restauration de package** de NuGet installe toutes les dépendances d’un projet telles qu’elles sont listées dans le fichier projet ou `packages.config`. Visual Studio peut restaurer les packages automatiquement à la génération d’un projet. Les commandes `dotnet build` et `dotnet run` (.NET Core 2.0+) effectuent également une restauration automatique. Vous pouvez aussi restaurer les packages à tout moment avec Visual Studio, `nuget restore`, `dotnet restore` et xbuild sur Mono.

La restauration de package permet de garantir la disponibilité de toutes les dépendances d’un projet sans stocker les packages dans le contrôle de code source. Consultez la page [Packages et contrôle de code source](../consume-packages/packages-and-source-control.md) pour savoir comment configurer votre référentiel de façon à exclure les binaires des packages.

## <a name="package-restore-overview"></a>Présentation de la restauration de package

La restauration de package installe tout d’abord les dépendances directes nécessaires d’un projet, puis toutes les dépendances du graphique de dépendance de ces packages.

Si un package n’est pas déjà installé, NuGet essaie d’abord de le récupérer à partir du [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Si le package ne se trouve pas dans le cache, NuGet tente de le télécharger à partir de toute les sources activées (consultez la page [Configurer le comportement de NuGet](Configuring-NuGet-Behavior.md) ; les sources apparaissent également dans la liste **Outils > Options > Gestionnaire de package NuGet > Sources de packages** dans Visual Studio). Lors de la restauration, NuGet ignore l’ordre des sources de packages et utilise le package provenant de la première source à répondre aux requêtes.

> [!Note]
> NuGet n’indique pas l’échec de la restauration d’un package tant que toutes les sources n’ont pas été vérifiées. À ce stade, NuGet ne signale de défaillance que pour la dernière source de la liste. L’erreur implique que le package ne se trouvait dans *aucune* autre source, même si les erreurs ne sont pas affichées pour chacune de ces sources.

La restauration du package est déclenchée comme suit :

- **Interface CLI dotnet** : utilisez la commande [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), qui restaure les packages répertoriés dans le fichier projet (consultez [PackageReference](../consume-packages/package-references-in-project-files.md)). Avec .NET Core 2.0 et versions ultérieures, la restauration est effectuée automatiquement avec `dotnet build` et `dotnet run`.

- **Interface utilisateur du Gestionnaire de package (Visual Studio sous Windows)** : les packages sont automatiquement restaurés lors de la création d’un projet à partir d’un modèle et lors de la création d’un projet (selon l’option décrite dans [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore)). Dans NuGet 4.0+, la restauration se produit également automatiquement lorsque des modifications sont apportées à un projet basé sur le kit SDK .NET Core.

    Pour effectuer une restauration manuelle, cliquez avec le bouton droit sur la solution dans l’Explorateur de solutions puis sélectionnez **Restaurer des packages NuGet**. Si un ou plusieurs packages individuels ne sont toujours pas installés correctement (comme en témoigne une icône d’erreur dans l’Explorateur de solutions), utilisez l’interface utilisateur du Gestionnaire de package pour désinstaller puis réinstaller les packages affectés. Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md).

    Si vous voyez l’erreur « Ce projet fait référence à des packages NuGet qui sont manquants sur cet ordinateur » ou l’erreur « Un ou plusieurs packages NuGet doivent être restaurés mais n’ont pas pu l’être, car le consentement n’a pas été octroyé », activez la restauration automatique en suivant les instructions de la section [Activation et désactivation de la restauration des packages](#enabling-and-disabling-package-restore). Consultez également la page [Résolution des problèmes de restauration de package](Package-restore-troubleshooting.md).

- **Interface CLI NuGet** : utilisez la commande [nuget restore](../tools/cli-ref-restore.md), qui restaure les packages listés dans le fichier projet ou dans `packages.config`. Vous pouvez également spécifier un fichier solution.

- **MSBuild** : utilisez la commande [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), qui restaure les packages listés dans le fichier projet (PackageReference uniquement). Disponible uniquement dans NuGet 4.x+ et MSBuild 15.1+, inclus avec Visual Studio 2017. `nuget restore` et `dotnet restore` utilisent cette commande pour les projets applicables.

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

Dans certains cas, un développeur ou une société peuvent vouloir activer ou désactiver la restauration de package pour tous les utilisateurs d’un ordinateur. Pour cela, ajoutez les paramètres ci-dessus au fichier de configuration NuGet global situé dans `%ProgramData%\NuGet\Config` (Windows, potentiellement sous un dossier `\{IDE}\{Version}\{SKU}\` propre à Visual Studio) ou `~/.local/share` (Mac/Linux). Chaque utilisateur peut ensuite activer la restauration au niveau d’un projet, si nécessaire. Pour plus d’informations sur la façon dont NuGet hiérarchise les fichiers de configuration, consultez [Configuration du comportement de NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Si vous modifiez les paramètres `packageRestore` directement dans `nuget.config`, redémarrez Visual Studio pour que la boîte de dialogue des options affiche les valeurs actuelles.

## <a name="constraining-package-versions-with-restore"></a>Restriction des versions de package avec la restauration

Lors de la restauration des packages avec l’une des méthodes disponibles, NuGet respecte toutes les restrictions spécifiées dans `packages.config` ou le fichier projet :

- `packages.config` : permet de spécifier une plage de versions dans la propriété `allowedVersion` de la dépendance. Consultez [Réinstallation et mise à jour des packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Exemple :

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Fichier projet (PackageReference) : permet de spécifier une plage de versions directement avec le numéro de version de la dépendance. Exemple :

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Dans tous les cas, utilisez la notation décrite dans [Gestion des versions du package](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Forcer la restauration à partir de sources de packages

Par défaut, les opérations de restauration NuGet utilisent des packages provenant des dossiers *global-packages* et *http-cache*, décrits sur la page [Gérer les dossiers de packages globaux et de cache](managing-the-global-packages-and-cache-folders.md).

Pour éviter d’utiliser le dossier *global-packages*, effectuez l’une des opérations suivantes :

- Effacez le dossier avec `nuget locals global-packages -clear` ou `dotnet nuget locals global-packages --clear`.
- Modifiez temporairement l’emplacement du dossier *global-packages* avant l’opération de restauration en suivant l’une des méthodes ci-dessous :
  - Définissez la variable d’environnement NUGET_PACKAGES sur un autre dossier.
  - Créez un fichier `NuGet.Config` qui définit `globalPackagesFolder` (si vous utilisez PackageReference) ou `repositoryPath` (si vous utilisez `packages.config`) sur un autre dossier (consultez les [paramètres de configuration](../reference/nuget-config-file.md#config-section)).
  - MSBuild uniquement : spécifiez un autre dossier avec la propriété `RestorePackagesPath`.

Pour éviter d’utiliser le cache pour les sources HTTP, effectuez l’une des opérations suivantes :

- Utilisez l’option `-NoCache` avec `nuget restore` ou l’option `--no-cache` avec `dotnet restore`. Elles n’affectent pas les opérations de restauration effectuées par le biais de la console ou de l’interface utilisateur du Gestionnaire de package de Visual Studio.
- Effacez le cache avec `nuget locals http-cache -clear` ou `dotnet nuget locals http-cache --clear`.
- Définissez temporairement la variable d’environnement NUGET_HTTP_CACHE_PATH sur un autre dossier.

## <a name="troubleshooting"></a>Résolution des problèmes

Consultez [Résolution des erreurs de restauration](package-restore-troubleshooting.md).
