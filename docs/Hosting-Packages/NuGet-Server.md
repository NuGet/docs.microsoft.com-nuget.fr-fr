---
title: "Utilisation de NuGet.Server pour héberger des flux NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Guide pratique pour créer et héberger un flux de packages NuGet sur un serveur exécutant IIS à l’aide de NuGet.Server de manière à rendre les packages accessibles via HTTP et OData."
keywords: flux NuGet, galerie NuGet, flux de packages distant, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a>NuGet.Server

Fourni par la .NET Foundation, NuGet.Server est un package qui crée une application ASP.NET pouvant héberger un flux de packages sur un serveur qui exécute IIS. Autrement dit, NuGet.Server rend un dossier sur le serveur accessible via HTTP(S) (en particulier, OData). Il est facile à configurer et convient pour les scénarios simples.

1. Créez une application web ASP.NET vide dans Visual Studio et ajoutez-y le package NuGet.Server.
1. Configurez le dossier `Packages` dans l’application et ajoutez des packages.
1. Déployez l’application sur un serveur approprié.

Les sections suivantes vous guident pas à pas dans ce processus en C#.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Créer et déployer une application web ASP.NET avec NuGet.Server

1. Dans Visual Studio, sélectionnez **Fichier > Nouveau > Projet**, définissez la version cible pour .NET Framework 4.6 (voir ci-dessous), recherchez « ASP.NET », puis sélectionnez le modèle **Application web ASP.NET (.NET Framework)** pour C#.

    ![Définition de la cible .NET Framework sur 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Donnez à l’application un nom approprié *autre* que NuGet.Server, sélectionnez OK, puis dans la boîte de dialogue suivante, sélectionnez le modèle **Vide** et sélectionnez OK.

1. Cliquez avec le bouton droit sur le projet, sélectionnez **Gérer les packages NuGet**, puis dans l’interface utilisateur du Gestionnaire de package, recherchez et installez la dernière version du package NuGet.Server si vous ciblez .NET Framework 4.6. (Vous pouvez également l’installer à partir de la console du Gestionnaire de package avec `Install-Package NuGet.Server`.)

    ![Installation du package NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Si votre application web cible .NET Framework 4.5.2, vous devez installer NuGet Server **2.10.3** à la place.

1. L’installation de NuGet.Server convertit l’application web vide en source de packages. Cette opération crée un dossier `Packages` dans l’application et remplace `web.config` pour inclure des paramètres supplémentaires (voir les commentaires dans ce fichier pour plus d’informations).

1. Pour rendre les packages disponibles dans le flux quand vous publiez l’application sur un serveur, ajoutez leurs fichiers `.nupkg` au dossier `Packages` dans Visual Studio, puis définissez leur **Action de génération** sur **Contenu** et **Copier dans le répertoire de sortie** sur **Toujours copier** :

    ![Copie des packages dans le dossier Packages du projet](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Exécutez le site localement dans Visual Studio (sans effectuer de débogage, en appuyant sur Ctrl+F5). La page d’accueil fournit les URL des flux de packages :

    ![Page d’accueil par défaut d’une application avec NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Cliquez **ici** dans la zone entourée ci-dessus pour afficher le flux OData de packages.

1. La première fois que vous exécutez l’application, NuGet.Server restructure le dossier `Packages` afin qu’il contienne un dossier par package. Cela correspond à la [disposition du stockage local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduite avec NuGet 3.3 pour améliorer les performances. Quand vous ajoutez des packages, continuez à suivre cette structure.

1. Une fois que vous avez testé votre déploiement local, déployez l’application sur un autre site interne ou externe en fonction des besoins.
1. Une fois l’application déployée sur `http://<domain>`, l’URL que vous utilisez pour la source de packages est `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Configurer le dossier Packages

Avec `NuGet.Server` 1.5 et ultérieur, vous pouvez configurer plus spécifiquement le dossier de packages à l’aide de la valeur `appSetting/packagesPath` dans `web.config` :

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` peut être un chemin absolu ou virtuel.

Si vous omettez la clé `packagesPath` ou la laissez vide, le dossier Packages est la valeur par défaut `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Ajouter des packages au flux de façon externe

Une fois qu’un site NuGet.Server est en cours d’exécution, vous pouvez ajouter ou supprimer des packages à l’aide de nuget.exe, à condition de définir une valeur de clé API dans `web.config`.

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

Si votre serveur est déjà sécurisé ou que vous n’exigez pas de clé API (par exemple, quand vous utilisez un serveur privé sur un réseau d’équipe local), vous pouvez définir `requireApiKey` sur `false`. Tous les utilisateurs ayant accès au serveur peuvent ensuite envoyer (push) ou supprimer des packages.