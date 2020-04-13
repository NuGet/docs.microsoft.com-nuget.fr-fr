---
title: Utilisation de NuGet.Server pour héberger des flux NuGet
description: Guide pratique pour créer et héberger un flux de packages NuGet sur un serveur exécutant IIS à l’aide de NuGet.Server de manière à rendre les packages accessibles via HTTP et OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059530"
---
# <a name="nugetserver"></a><span data-ttu-id="40c23-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="40c23-103">NuGet.Server</span></span>

<span data-ttu-id="40c23-104">Fourni par la .NET Foundation, NuGet.Server est un package qui crée une application ASP.NET pouvant héberger un flux de packages sur un serveur qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="40c23-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="40c23-105">Autrement dit, NuGet.Server rend un dossier sur le serveur accessible via HTTP(S) (en particulier, OData).</span><span class="sxs-lookup"><span data-stu-id="40c23-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="40c23-106">Il est facile à configurer et convient pour les scénarios simples.</span><span class="sxs-lookup"><span data-stu-id="40c23-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="40c23-107">Créez une application web ASP.NET vide dans Visual Studio et ajoutez-y le package NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="40c23-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="40c23-108">Configurez le dossier `Packages` dans l’application et ajoutez des packages.</span><span class="sxs-lookup"><span data-stu-id="40c23-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="40c23-109">Déployez l’application sur un serveur approprié.</span><span class="sxs-lookup"><span data-stu-id="40c23-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="40c23-110">Les sections suivantes vous guident pas à pas dans ce processus en C#.</span><span class="sxs-lookup"><span data-stu-id="40c23-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="40c23-111">Si vous avez d’autres questions sur NuGet.Server, créez un problème sur [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="40c23-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="40c23-112">Créer et déployer une application web ASP.NET avec NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="40c23-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="40c23-113">Dans Visual Studio, sélectionnez **File > New > Project**, recherchez « ASP.NET Web Application (.NET Framework) », sélectionnez le modèle de correspondance pour le C.</span><span class="sxs-lookup"><span data-stu-id="40c23-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![Sélectionnez le modèle de projet Web .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="40c23-115">Définir **le cadre** à ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="40c23-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Définition du framework cible pour un nouveau projet](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="40c23-117">Donnez à l’application un nom approprié *autre* que NuGet.Server, sélectionnez OK, puis dans la boîte de dialogue suivante, sélectionnez le modèle **Vide**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="40c23-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Sélectionnez le projet web vide](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="40c23-119">Cliquez avec le bouton droit sur le projet et sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="40c23-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="40c23-120">Dans l’interface utilisateur du Gestionnaire de package, sélectionnez **Parcourir**, puis recherchez et installez la dernière version du package NuGet.Server si vous ciblez le .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="40c23-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="40c23-121">(Vous pouvez également l’installer à `Install-Package NuGet.Server`partir de la console Package Manager avec .) Acceptez les conditions de licence si vous êtes invité.</span><span class="sxs-lookup"><span data-stu-id="40c23-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Installation du package NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="40c23-123">L’installation de NuGet.Server convertit l’application web vide en source de packages.</span><span class="sxs-lookup"><span data-stu-id="40c23-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="40c23-124">Cette opération installe d’autre packages, crée un dossier `Packages` dans l’application et modifie `web.config` pour inclure des paramètres supplémentaires (voir les commentaires dans ce fichier pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="40c23-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="40c23-125">Examinez attentivement `web.config` une fois que le package NuGet.Server a terminé d’apporter ses modifications à ce fichier.</span><span class="sxs-lookup"><span data-stu-id="40c23-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="40c23-126">NuGet.Server ne peut pas remplacer des éléments existants, mais il peut créer des éléments en double.</span><span class="sxs-lookup"><span data-stu-id="40c23-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="40c23-127">Ces doublons entraîne une « erreur de serveur interne » quand vous essayez d’exécuter le projet par la suite.</span><span class="sxs-lookup"><span data-stu-id="40c23-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="40c23-128">Par exemple, si votre `web.config` contient `<compilation debug="true" targetFramework="4.5.2" />` avant d’installer NuGet.Server, le package ne le remplace pas mais insère un deuxième `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="40c23-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="40c23-129">Dans ce cas, supprimez l’élément avec l’ancienne version du framework.</span><span class="sxs-lookup"><span data-stu-id="40c23-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="40c23-130">Exécutez le site localement dans Visual Studio (en utilisant **Déboguer > Démarrer sans débogage** ou Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="40c23-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="40c23-131">La page d’accueil fournit les URL des flux de packages, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="40c23-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="40c23-132">Si vous voyez des erreurs, inspectez soigneusement vos `web.config` éléments en double comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="40c23-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Page d’accueil par défaut d’une application avec NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="40c23-134">La première fois que vous exécutez l’application, NuGet.Server restructure le dossier `Packages` afin qu’il contienne un dossier par package.</span><span class="sxs-lookup"><span data-stu-id="40c23-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="40c23-135">Cela correspond à la [disposition du stockage local](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduite avec NuGet 3.3 pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="40c23-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="40c23-136">Quand vous ajoutez des packages, continuez à suivre cette structure.</span><span class="sxs-lookup"><span data-stu-id="40c23-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="40c23-137">Une fois que vous avez testé votre déploiement local, déployez l’application sur un autre site interne ou externe en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="40c23-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="40c23-138">Une fois l’application déployée sur `http://<domain>`, l’URL que vous utilisez pour la source de packages est `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="40c23-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="40c23-139">Ajouter des packages au flux de façon externe</span><span class="sxs-lookup"><span data-stu-id="40c23-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="40c23-140">Une fois qu’un site NuGet.Server est en cours d’exécution, vous pouvez ajouter des packages à l’aide de [nuget push](../reference/cli-reference/cli-ref-push.md), à condition de définir une valeur de clé API dans `web.config`.</span><span class="sxs-lookup"><span data-stu-id="40c23-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="40c23-141">Une fois le package NuGet.Server installé, `web.config` contient une valeur `appSetting/apiKey` vide :</span><span class="sxs-lookup"><span data-stu-id="40c23-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="40c23-142">Si vous omettez la clé `apiKey` ou la laissez vide, l’envoi (push) de packages au flux est désactivé.</span><span class="sxs-lookup"><span data-stu-id="40c23-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="40c23-143">Pour activer cette fonctionnalité, définissez la clé `apiKey` sur une valeur (dans l’idéal, un mot de passe fort) et ajoutez une clé appelée `appSettings/requireApiKey` ayant pour valeur `true` :</span><span class="sxs-lookup"><span data-stu-id="40c23-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="40c23-144">Si votre serveur est déjà sécurisé ou que vous n’exigez pas de clé API (par exemple, quand vous utilisez un serveur privé sur un réseau d’équipe local), vous pouvez définir `requireApiKey` sur `false`.</span><span class="sxs-lookup"><span data-stu-id="40c23-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="40c23-145">Tous les utilisateurs ayant accès au serveur peuvent ensuite envoyer (push) des packages.</span><span class="sxs-lookup"><span data-stu-id="40c23-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="40c23-146">En commençant par NuGet.Server 3.0.0, l’URL pour pousser les paquets a été changer pour `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="40c23-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="40c23-147">Avant la version 3.0.0, l’URL push était `http://<domain>/api/v2/package`.</span><span class="sxs-lookup"><span data-stu-id="40c23-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="40c23-148">Avec NuGet 3.2.1 et plus `/api/v2/package` récent, cette `/nuget` URL héritée est activée en plus par défaut via `enableLegacyPushRoute: true` option dans votre config startup (par`NuGetODataConfig.cs` défaut).</span><span class="sxs-lookup"><span data-stu-id="40c23-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="40c23-149">Notez que cette fonctionnalité ne fonctionne pas lorsque plusieurs flux sont hébergés dans le même projet.</span><span class="sxs-lookup"><span data-stu-id="40c23-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="40c23-150">Suppression de packages à partir du flux</span><span class="sxs-lookup"><span data-stu-id="40c23-150">Removing packages from the feed</span></span>

<span data-ttu-id="40c23-151">Avec NuGet.Server, la commande [nuget delete](../reference/cli-reference/cli-ref-delete.md) supprime un package du référentiel à condition que la clé API soit incluse avec le commentaire.</span><span class="sxs-lookup"><span data-stu-id="40c23-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="40c23-152">Si vous souhaitez changer le comportement pour retirer le package d’une liste (le rendant ainsi disponible pour la restauration de package), affectez à la clé `enableDelisting` dans `web.config` la valeur true.</span><span class="sxs-lookup"><span data-stu-id="40c23-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="40c23-153">Configurer le dossier Packages</span><span class="sxs-lookup"><span data-stu-id="40c23-153">Configuring the Packages folder</span></span>

<span data-ttu-id="40c23-154">Avec `NuGet.Server` 1.5 et plus tard, vous pouvez `appSettings/packagesPath` personnaliser `web.config`le dossier de paquet en utilisant la valeur dans :</span><span class="sxs-lookup"><span data-stu-id="40c23-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="40c23-155">`packagesPath` peut être un chemin absolu ou virtuel.</span><span class="sxs-lookup"><span data-stu-id="40c23-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="40c23-156">Si vous omettez la clé `packagesPath` ou la laissez vide, le dossier Packages est la valeur par défaut `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="40c23-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="40c23-157">Rendre les paquets disponibles lorsque vous publiez l’application web</span><span class="sxs-lookup"><span data-stu-id="40c23-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="40c23-158">Pour rendre les packages disponibles dans le flux quand vous publiez l’application sur un serveur, ajoutez chaque fichier `.nupkg` au dossier `Packages` dans Visual Studio, puis définissez chaque **Action de génération** avec la valeur **Contenu** et **Copier dans le répertoire de sortie** avec la valeur **Toujours copier** :</span><span class="sxs-lookup"><span data-stu-id="40c23-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Copie des packages dans le dossier Packages du projet](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="40c23-160">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="40c23-160">Release Notes</span></span>

<span data-ttu-id="40c23-161">Les notes de sortie de NuGet.Server sont disponibles sur la [page de sortie GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="40c23-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="40c23-162">Cela comprend des détails sur les correctifs de bogues et les nouvelles fonctionnalités qui sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="40c23-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="40c23-163">Support NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="40c23-163">NuGet.Server support</span></span>

<span data-ttu-id="40c23-164">Pour plus d’aide à l’aide [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)de NuGet.Server, créez un problème sur .</span><span class="sxs-lookup"><span data-stu-id="40c23-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
