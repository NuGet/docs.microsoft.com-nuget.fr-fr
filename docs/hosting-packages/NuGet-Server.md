---
title: Utilisation de NuGet.Server pour héberger des flux NuGet
description: Guide pratique pour créer et héberger un flux de packages NuGet sur un serveur exécutant IIS à l’aide de NuGet.Server de manière à rendre les packages accessibles via HTTP et OData.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 55501eedf6c5fdf054a602536ee8c03e7048d5d5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="nugetserver"></a><span data-ttu-id="04303-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="04303-103">NuGet.Server</span></span>

<span data-ttu-id="04303-104">Fourni par la .NET Foundation, NuGet.Server est un package qui crée une application ASP.NET pouvant héberger un flux de packages sur un serveur qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="04303-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="04303-105">Autrement dit, NuGet.Server rend un dossier sur le serveur accessible via HTTP(S) (en particulier, OData).</span><span class="sxs-lookup"><span data-stu-id="04303-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="04303-106">Il est facile à configurer et convient pour les scénarios simples.</span><span class="sxs-lookup"><span data-stu-id="04303-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="04303-107">Créez une application web ASP.NET vide dans Visual Studio et ajoutez-y le package NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="04303-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="04303-108">Configurez le dossier `Packages` dans l’application et ajoutez des packages.</span><span class="sxs-lookup"><span data-stu-id="04303-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="04303-109">Déployez l’application sur un serveur approprié.</span><span class="sxs-lookup"><span data-stu-id="04303-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="04303-110">Les sections suivantes vous guident pas à pas dans ce processus en C#.</span><span class="sxs-lookup"><span data-stu-id="04303-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="04303-111">Si vous avez d’autres questions sur NuGet.Server, créez un problème sur [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="04303-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="04303-112">Créer et déployer une application web ASP.NET avec NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="04303-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="04303-113">Dans Visual Studio, sélectionnez **Fichier > Nouveau > Projet**, recherchez « ASP.NET », sélectionnez le modèle **Application web ASP.NET (.NET Framework)** pour C#, puis définissez **Framework** avec la valeur « .NET Framework 4.6 » :</span><span class="sxs-lookup"><span data-stu-id="04303-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Définition du framework cible pour un nouveau projet](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="04303-115">Donnez à l’application un nom approprié *autre* que NuGet.Server, sélectionnez OK, puis dans la boîte de dialogue suivante, sélectionnez le modèle **Vide**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="04303-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="04303-116">Cliquez avec le bouton droit sur le projet et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="04303-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="04303-117">Dans l’interface utilisateur du Gestionnaire de package, sélectionnez **Parcourir**, puis recherchez et installez la dernière version du package NuGet.Server si vous ciblez le .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="04303-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="04303-118">(Vous pouvez également l’installer à partir de la console du Gestionnaire de package avec `Install-Package NuGet.Server`.) Acceptez les termes du contrat de licence si vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="04303-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Installation du package NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="04303-120">L’installation de NuGet.Server convertit l’application web vide en source de packages.</span><span class="sxs-lookup"><span data-stu-id="04303-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="04303-121">Cette opération installe d’autre packages, crée un dossier `Packages` dans l’application et modifie `web.config` pour inclure des paramètres supplémentaires (voir les commentaires dans ce fichier pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="04303-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="04303-122">Examinez attentivement `web.config` une fois que le package NuGet.Server a terminé d’apporter ses modifications à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="04303-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="04303-123">NuGet.Server ne peut pas remplacer des éléments existants, mais il peut créer des éléments en double.</span><span class="sxs-lookup"><span data-stu-id="04303-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="04303-124">Ces doublons entraîne une « erreur de serveur interne » quand vous essayez d’exécuter le projet par la suite.</span><span class="sxs-lookup"><span data-stu-id="04303-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="04303-125">Par exemple, si votre `web.config` contient `<compilation debug="true" targetFramework="4.5.2" />` avant d’installer NuGet.Server, le package ne le remplace pas mais insère un deuxième `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="04303-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="04303-126">Dans ce cas, supprimez l’élément avec l’ancienne version du framework.</span><span class="sxs-lookup"><span data-stu-id="04303-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="04303-127">Pour rendre les packages disponibles dans le flux quand vous publiez l’application sur un serveur, ajoutez chaque fichier `.nupkg` au dossier `Packages` dans Visual Studio, puis définissez chaque **Action de génération** avec la valeur **Contenu** et **Copier dans le répertoire de sortie** avec la valeur **Toujours copier** :</span><span class="sxs-lookup"><span data-stu-id="04303-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copie des packages dans le dossier Packages du projet](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="04303-129">Exécutez le site localement dans Visual Studio (en utilisant **Déboguer > Démarrer sans débogage** ou Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="04303-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="04303-130">La page d’accueil fournit les URL des flux de packages, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="04303-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="04303-131">Si vous constatez des erreurs, inspectez attentivement votre fichier `web.config` à la recherche des éléments en double mentionnés précédemment à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="04303-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Page d’accueil par défaut d’une application avec NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="04303-133">Cliquez **ici** dans la zone entourée ci-dessus pour afficher le flux OData de packages.</span><span class="sxs-lookup"><span data-stu-id="04303-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="04303-134">La première fois que vous exécutez l’application, NuGet.Server restructure le dossier `Packages` afin qu’il contienne un dossier par package.</span><span class="sxs-lookup"><span data-stu-id="04303-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="04303-135">Cela correspond à la [disposition du stockage local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduite avec NuGet 3.3 pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="04303-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="04303-136">Quand vous ajoutez des packages, continuez à suivre cette structure.</span><span class="sxs-lookup"><span data-stu-id="04303-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="04303-137">Une fois que vous avez testé votre déploiement local, déployez l’application sur un autre site interne ou externe en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="04303-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="04303-138">Une fois l’application déployée sur `http://<domain>`, l’URL que vous utilisez pour la source de packages est `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="04303-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="04303-139">Configurer le dossier Packages</span><span class="sxs-lookup"><span data-stu-id="04303-139">Configuring the Packages folder</span></span>

<span data-ttu-id="04303-140">Avec `NuGet.Server` 1.5 et ultérieur, vous pouvez configurer plus spécifiquement le dossier de packages à l’aide de la valeur `appSetting/packagesPath` dans `web.config` :</span><span class="sxs-lookup"><span data-stu-id="04303-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="04303-141">`packagesPath` peut être un chemin absolu ou virtuel.</span><span class="sxs-lookup"><span data-stu-id="04303-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="04303-142">Si vous omettez la clé `packagesPath` ou la laissez vide, le dossier Packages est la valeur par défaut `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="04303-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="04303-143">Ajouter des packages au flux de façon externe</span><span class="sxs-lookup"><span data-stu-id="04303-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="04303-144">Une fois qu’un site NuGet.Server est en cours d’exécution, vous pouvez ajouter des packages à l’aide de [nuget push](../tools/cli-ref-push.md), à condition de définir une valeur de clé API dans `web.config`.</span><span class="sxs-lookup"><span data-stu-id="04303-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="04303-145">Une fois le package NuGet.Server installé, `web.config` contient une valeur `appSetting/apiKey` vide :</span><span class="sxs-lookup"><span data-stu-id="04303-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="04303-146">Si vous omettez la clé `apiKey` ou la laissez vide, l’envoi (push) de packages au flux est désactivé.</span><span class="sxs-lookup"><span data-stu-id="04303-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="04303-147">Pour activer cette fonctionnalité, définissez la clé `apiKey` sur une valeur (dans l’idéal, un mot de passe fort) et ajoutez une clé appelée `appSettings/requireApiKey` ayant pour valeur `true` :</span><span class="sxs-lookup"><span data-stu-id="04303-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="04303-148">Si votre serveur est déjà sécurisé ou que vous n’exigez pas de clé API (par exemple, quand vous utilisez un serveur privé sur un réseau d’équipe local), vous pouvez définir `requireApiKey` sur `false`.</span><span class="sxs-lookup"><span data-stu-id="04303-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="04303-149">Tous les utilisateurs ayant accès au serveur peuvent ensuite envoyer (push) des packages.</span><span class="sxs-lookup"><span data-stu-id="04303-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="04303-150">Suppression de packages à partir du flux</span><span class="sxs-lookup"><span data-stu-id="04303-150">Removing packages from the feed</span></span>

<span data-ttu-id="04303-151">Avec NuGet.Server, la commande [nuget delete](../tools/cli-ref-delete.md) supprime un package du référentiel à condition que la clé API soit incluse avec le commentaire.</span><span class="sxs-lookup"><span data-stu-id="04303-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="04303-152">Si vous souhaitez changer le comportement pour retirer le package d’une liste (le rendant ainsi disponible pour la restauration de package), affectez à la clé `enableDelisting` dans `web.config` la valeur true.</span><span class="sxs-lookup"><span data-stu-id="04303-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="04303-153">Support NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="04303-153">NuGet.Server support</span></span>

<span data-ttu-id="04303-154">Pour obtenir de l’aide supplémentaire sur l’utilisation de NuGet.Server, créez un problème sur [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="04303-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>