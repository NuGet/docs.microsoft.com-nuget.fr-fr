---
title: "Utilisation de NuGet.Server pour héberger des flux NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: "Guide pratique pour créer et héberger un flux de packages NuGet sur un serveur exécutant IIS à l’aide de NuGet.Server de manière à rendre les packages accessibles via HTTP et OData."
keywords: flux NuGet, galerie NuGet, flux de packages distant, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a><span data-ttu-id="aabfb-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="aabfb-104">NuGet.Server</span></span>

<span data-ttu-id="aabfb-105">Fourni par la .NET Foundation, NuGet.Server est un package qui crée une application ASP.NET pouvant héberger un flux de packages sur un serveur qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="aabfb-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="aabfb-106">Autrement dit, NuGet.Server rend un dossier sur le serveur accessible via HTTP(S) (en particulier, OData).</span><span class="sxs-lookup"><span data-stu-id="aabfb-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="aabfb-107">Il est facile à configurer et convient pour les scénarios simples.</span><span class="sxs-lookup"><span data-stu-id="aabfb-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="aabfb-108">Créez une application web ASP.NET vide dans Visual Studio et ajoutez-y le package NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="aabfb-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="aabfb-109">Configurez le dossier `Packages` dans l’application et ajoutez des packages.</span><span class="sxs-lookup"><span data-stu-id="aabfb-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="aabfb-110">Déployez l’application sur un serveur approprié.</span><span class="sxs-lookup"><span data-stu-id="aabfb-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="aabfb-111">Les sections suivantes vous guident pas à pas dans ce processus en C#.</span><span class="sxs-lookup"><span data-stu-id="aabfb-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="aabfb-112">Créer et déployer une application web ASP.NET avec NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="aabfb-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="aabfb-113">Dans Visual Studio, sélectionnez **Fichier > Nouveau > Projet**, définissez la version cible pour .NET Framework 4.6 (voir ci-dessous), recherchez « ASP.NET », puis sélectionnez le modèle **Application web ASP.NET (.NET Framework)** pour C#.</span><span class="sxs-lookup"><span data-stu-id="aabfb-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Définition de la cible .NET Framework sur 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="aabfb-115">Donnez à l’application un nom approprié *autre* que NuGet.Server, sélectionnez OK, puis dans la boîte de dialogue suivante, sélectionnez le modèle **Vide** et sélectionnez OK.</span><span class="sxs-lookup"><span data-stu-id="aabfb-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="aabfb-116">Cliquez avec le bouton droit sur le projet, sélectionnez **Gérer les packages NuGet**, puis dans l’interface utilisateur du Gestionnaire de package, recherchez et installez la dernière version du package NuGet.Server si vous ciblez .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="aabfb-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="aabfb-117">(Vous pouvez également l’installer à partir de la console du Gestionnaire de package avec `Install-Package NuGet.Server`.)</span><span class="sxs-lookup"><span data-stu-id="aabfb-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Installation du package NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="aabfb-119">Si votre application web cible .NET Framework 4.5.2, vous devez installer NuGet Server **2.10.3** à la place.</span><span class="sxs-lookup"><span data-stu-id="aabfb-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="aabfb-120">L’installation de NuGet.Server convertit l’application web vide en source de packages.</span><span class="sxs-lookup"><span data-stu-id="aabfb-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="aabfb-121">Cette opération crée un dossier `Packages` dans l’application et remplace `web.config` pour inclure des paramètres supplémentaires (voir les commentaires dans ce fichier pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="aabfb-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="aabfb-122">Pour rendre les packages disponibles dans le flux quand vous publiez l’application sur un serveur, ajoutez leurs fichiers `.nupkg` au dossier `Packages` dans Visual Studio, puis définissez leur **Action de génération** sur **Contenu** et **Copier dans le répertoire de sortie** sur **Toujours copier** :</span><span class="sxs-lookup"><span data-stu-id="aabfb-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copie des packages dans le dossier Packages du projet](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="aabfb-124">Exécutez le site localement dans Visual Studio (sans effectuer de débogage, en appuyant sur Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="aabfb-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="aabfb-125">La page d’accueil fournit les URL des flux de packages :</span><span class="sxs-lookup"><span data-stu-id="aabfb-125">The home page provides the package feed URLs:</span></span>

    ![Page d’accueil par défaut d’une application avec NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="aabfb-127">Cliquez **ici** dans la zone entourée ci-dessus pour afficher le flux OData de packages.</span><span class="sxs-lookup"><span data-stu-id="aabfb-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="aabfb-128">La première fois que vous exécutez l’application, NuGet.Server restructure le dossier `Packages` afin qu’il contienne un dossier par package.</span><span class="sxs-lookup"><span data-stu-id="aabfb-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="aabfb-129">Cela correspond à la [disposition du stockage local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduite avec NuGet 3.3 pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="aabfb-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="aabfb-130">Quand vous ajoutez des packages, continuez à suivre cette structure.</span><span class="sxs-lookup"><span data-stu-id="aabfb-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="aabfb-131">Une fois que vous avez testé votre déploiement local, déployez l’application sur un autre site interne ou externe en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="aabfb-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="aabfb-132">Une fois l’application déployée sur `http://<domain>`, l’URL que vous utilisez pour la source de packages est `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="aabfb-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="aabfb-133">Configurer le dossier Packages</span><span class="sxs-lookup"><span data-stu-id="aabfb-133">Configuring the Packages folder</span></span>

<span data-ttu-id="aabfb-134">Avec `NuGet.Server` 1.5 et ultérieur, vous pouvez configurer plus spécifiquement le dossier de packages à l’aide de la valeur `appSetting/packagesPath` dans `web.config` :</span><span class="sxs-lookup"><span data-stu-id="aabfb-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="aabfb-135">`packagesPath` peut être un chemin absolu ou virtuel.</span><span class="sxs-lookup"><span data-stu-id="aabfb-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="aabfb-136">Si vous omettez la clé `packagesPath` ou la laissez vide, le dossier Packages est la valeur par défaut `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="aabfb-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="aabfb-137">Ajouter des packages au flux de façon externe</span><span class="sxs-lookup"><span data-stu-id="aabfb-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="aabfb-138">Une fois qu’un site NuGet.Server est en cours d’exécution, vous pouvez ajouter ou supprimer des packages à l’aide de nuget.exe, à condition de définir une valeur de clé API dans `web.config`.</span><span class="sxs-lookup"><span data-stu-id="aabfb-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="aabfb-139">Une fois le package NuGet.Server installé, `web.config` contient une valeur `appSetting/apiKey` vide :</span><span class="sxs-lookup"><span data-stu-id="aabfb-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="aabfb-140">Si vous omettez la clé `apiKey` ou la laissez vide, l’envoi (push) de packages au flux est désactivé.</span><span class="sxs-lookup"><span data-stu-id="aabfb-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="aabfb-141">Pour activer cette fonctionnalité, définissez la clé `apiKey` sur une valeur (dans l’idéal, un mot de passe fort) et ajoutez une clé appelée `appSettings/requireApiKey` ayant pour valeur `true` :</span><span class="sxs-lookup"><span data-stu-id="aabfb-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="aabfb-142">Si votre serveur est déjà sécurisé ou que vous n’exigez pas de clé API (par exemple, quand vous utilisez un serveur privé sur un réseau d’équipe local), vous pouvez définir `requireApiKey` sur `false`.</span><span class="sxs-lookup"><span data-stu-id="aabfb-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="aabfb-143">Tous les utilisateurs ayant accès au serveur peuvent ensuite envoyer (push) ou supprimer des packages.</span><span class="sxs-lookup"><span data-stu-id="aabfb-143">All users with access to the server can then push or delete packages.</span></span>