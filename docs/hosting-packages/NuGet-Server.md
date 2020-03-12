---
title: Utilisation de NuGet.Server pour héberger des flux NuGet
description: Guide pratique pour créer et héberger un flux de packages NuGet sur un serveur exécutant IIS à l’aide de NuGet.Server de manière à rendre les packages accessibles via HTTP et OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79059530"
---
# <a name="nugetserver"></a>NuGet.Server

Fourni par la .NET Foundation, NuGet.Server est un package qui crée une application ASP.NET pouvant héberger un flux de packages sur un serveur qui exécute IIS. Autrement dit, NuGet.Server rend un dossier sur le serveur accessible via HTTP(S) (en particulier, OData). Il est facile à configurer et convient pour les scénarios simples.

1. Créez une application web ASP.NET vide dans Visual Studio et ajoutez-y le package NuGet.Server.
1. Configurez le dossier `Packages` dans l’application et ajoutez des packages.
1. Déployez l’application sur un serveur approprié.

Les sections suivantes vous guident pas à pas dans ce processus en C#.

Si vous avez d’autres questions sur NuGet.Server, créez un problème sur [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Créer et déployer une application web ASP.NET avec NuGet.Server

1. Dans Visual Studio, sélectionnez **fichier > nouveau > projet**, recherchez « Application Web ASP.NET (.NET Framework) », puis sélectionnez le modèle correspondant pour C#.

    ![Sélectionner le modèle de projet Web .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Définissez **Framework** sur « .NET Framework 4,6 ».

    ![Définition du framework cible pour un nouveau projet](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Donnez à l’application un nom approprié *autre* que NuGet.Server, sélectionnez OK, puis dans la boîte de dialogue suivante, sélectionnez le modèle **Vide**, puis sélectionnez **OK**.

    ![Sélectionner le projet Web vide](media/Hosting_02-NuGet.Server-Empty.png)

1. Cliquez avec le bouton droit sur le projet et sélectionnez **Gérer les packages NuGet**.

1. Dans l’interface utilisateur du Gestionnaire de package, sélectionnez **Parcourir**, puis recherchez et installez la dernière version du package NuGet.Server si vous ciblez le .NET Framework 4.6. (Vous pouvez également l’installer à partir de la console du gestionnaire de package avec `Install-Package NuGet.Server`.) Acceptez les termes du contrat de licence si vous y êtes invité.

    ![Installation du package NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. L’installation de NuGet.Server convertit l’application web vide en source de packages. Cette opération installe d’autre packages, crée un dossier `Packages` dans l’application et modifie `web.config` pour inclure des paramètres supplémentaires (voir les commentaires dans ce fichier pour plus d’informations).

    > [!Important]
    > Examinez attentivement `web.config` une fois que le package NuGet.Server a terminé d’apporter ses modifications à ce fichier. NuGet.Server ne peut pas remplacer des éléments existants, mais il peut créer des éléments en double. Ces doublons entraîne une « erreur de serveur interne » quand vous essayez d’exécuter le projet par la suite. Par exemple, si votre `web.config` contient `<compilation debug="true" targetFramework="4.5.2" />` avant d’installer NuGet.Server, le package ne le remplace pas mais insère un deuxième `<compilation debug="true" targetFramework="4.6" />`. Dans ce cas, supprimez l’élément avec l’ancienne version du framework.

1. Exécutez le site localement dans Visual Studio (en utilisant **Déboguer > Démarrer sans débogage** ou Ctrl+F5). La page d’accueil fournit les URL des flux de packages, comme indiqué ci-dessous. Si vous constatez des erreurs, examinez attentivement votre `web.config` pour rechercher des éléments en double, comme indiqué précédemment.

    ![Page d’accueil par défaut d’une application avec NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  La première fois que vous exécutez l’application, NuGet.Server restructure le dossier `Packages` afin qu’il contienne un dossier par package. Cela correspond à la [disposition du stockage local](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduite avec NuGet 3.3 pour améliorer les performances. Quand vous ajoutez des packages, continuez à suivre cette structure.

1. Une fois que vous avez testé votre déploiement local, déployez l’application sur un autre site interne ou externe en fonction des besoins.

1. Une fois l’application déployée sur `http://<domain>`, l’URL que vous utilisez pour la source de packages est `http://<domain>/nuget`.

## <a name="adding-packages-to-the-feed-externally"></a>Ajouter des packages au flux de façon externe

Une fois qu’un site NuGet.Server est en cours d’exécution, vous pouvez ajouter des packages à l’aide de [nuget push](../reference/cli-reference/cli-ref-push.md), à condition de définir une valeur de clé API dans `web.config`.

Une fois le package NuGet.Server installé, `web.config` contient une valeur `appSetting/apiKey` vide :

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Si vous omettez la clé `apiKey` ou la laissez vide, l’envoi (push) de packages au flux est désactivé.

Pour activer cette fonctionnalité, définissez la clé `apiKey` sur une valeur (dans l’idéal, un mot de passe fort) et ajoutez une clé appelée `appSettings/requireApiKey` ayant pour valeur `true` :

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Si votre serveur est déjà sécurisé ou que vous n’exigez pas de clé API (par exemple, quand vous utilisez un serveur privé sur un réseau d’équipe local), vous pouvez définir `requireApiKey` sur `false`. Tous les utilisateurs ayant accès au serveur peuvent ensuite envoyer (push) des packages.

À compter de NuGet. Server 3.0.0, l’URL pour l’envoi de packages a été changée en `http://<domain>/nuget`. Avant la version 3.0.0, l’URL de transmission était `http://<domain>/api/v2/package`.

Avec NuGet 3.2.1 et versions ultérieures, cette URL héritée `/api/v2/package` est activée en plus de `/nuget` par défaut via `enableLegacyPushRoute: true` option dans votre configuration de démarrage (`NuGetODataConfig.cs` par défaut). Notez que cette fonctionnalité ne fonctionne pas lorsque plusieurs flux sont hébergés dans le même projet.

## <a name="removing-packages-from-the-feed"></a>Suppression de packages à partir du flux

Avec NuGet.Server, la commande [nuget delete](../reference/cli-reference/cli-ref-delete.md) supprime un package du référentiel à condition que la clé API soit incluse avec le commentaire.

Si vous souhaitez changer le comportement pour retirer le package d’une liste (le rendant ainsi disponible pour la restauration de package), affectez à la clé `enableDelisting` dans `web.config` la valeur true.

## <a name="configuring-the-packages-folder"></a>Configurer le dossier Packages

Avec `NuGet.Server` 1,5 et versions ultérieures, vous pouvez personnaliser le dossier de package à l’aide de la valeur de `appSettings/packagesPath` dans `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` peut être un chemin absolu ou virtuel.

Si vous omettez la clé `packagesPath` ou la laissez vide, le dossier Packages est la valeur par défaut `~/Packages`.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Mise à disposition des packages lors de la publication de l’application Web

Pour rendre les packages disponibles dans le flux quand vous publiez l’application sur un serveur, ajoutez chaque fichier `.nupkg` au dossier `Packages` dans Visual Studio, puis définissez chaque **Action de génération** avec la valeur **Contenu** et **Copier dans le répertoire de sortie** avec la valeur **Toujours copier** :

![Copie des packages dans le dossier Packages du projet](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Notes de publication

Les notes de publication de NuGet. Server sont disponibles sur la [page de publication de GitHub](https://github.com/NuGet/NuGet.Server/releases).
Cela comprend des détails sur les correctifs de bogues et les nouvelles fonctionnalités ajoutées.

## <a name="nugetserver-support"></a>Support NuGet.Server

Pour obtenir de l’aide supplémentaire sur l’utilisation de NuGet.Server, créez un problème sur [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).
