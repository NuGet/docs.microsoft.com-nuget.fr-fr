---
title: "Guide d’introduction à la création et à la publication de package NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Didacticiel expliquant comment créer et publier un package NuGet à l’aide de l’interface de ligne de commande de nuget.exe et de Visual Studio."
keywords: "création de package NuGet, publication de package NuGet, didacticiel NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="ec8b4-104">Créer et publier un package</span><span class="sxs-lookup"><span data-stu-id="ec8b4-104">Create and publish a package</span></span>

<span data-ttu-id="ec8b4-105">La création d’un package NuGet à partir d’une bibliothèque de classes .NET et sa publication sur nuget.org sont des processus simples. Les étapes suivantes vous expliquent pas à pas comment procéder à l’aide de Visual Studio et de l’interface de ligne de commande (CLI) de NuGet :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="ec8b4-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ec8b4-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="ec8b4-107">Créer le fichier manifeste du package .nuspec</span><span class="sxs-lookup"><span data-stu-id="ec8b4-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="ec8b4-108">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="ec8b4-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="ec8b4-109">Publier le package</span><span class="sxs-lookup"><span data-stu-id="ec8b4-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="ec8b4-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ec8b4-110">Pre-requisites</span></span>

1. <span data-ttu-id="ec8b4-111">Installez une édition quelconque de Visual Studio 2017 à partir de [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="ec8b4-112">Installez l’outil CLI NuGet, `nuget.exe`, en téléchargeant la dernière version de `nuget.exe` à partir de [nuget.org/downloads](https://nuget.org/downloads) et en enregistrant le fichier `.exe` à un emplacement dans votre PATH.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="ec8b4-113">Notez que le téléchargement *est* l’outil lui-même, et pas un programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="ec8b4-114">Créez un projet de bibliothèque de classes .NET approprié pour le code que vous souhaitez empaqueter.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="ec8b4-115">Si vous n’avez pas encore de projet, vous pouvez en créer un simple comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="ec8b4-116">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > Windows**, sélectionnez le modèle « Bibliothèque de classes », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="ec8b4-117">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="ec8b4-118">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="ec8b4-119">Dans un package NuGet réel, bien sûr, vous implémenterez de nombreuses fonctionnalités utiles sur lesquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="ec8b4-120">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="ec8b4-121">Créer le fichier manifeste du package .nuspec</span><span class="sxs-lookup"><span data-stu-id="ec8b4-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="ec8b4-122">Chaque package NuGet a besoin d’un manifeste &mdash;un fichier `.nuspec`&mdash; pour décrire son contenu et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="ec8b4-123">La commande `nuget spec` crée ce fichier pour vous, et ensuite vous le personnalisez.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="ec8b4-124">Dans cet exemple, vous créez le fichier `.nuspec` à partir d’un fichier projet. Vous pouvez également créer le manifeste par d’autres moyens, comme décrit dans [Créer un package](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="ec8b4-125">Ouvrez une invite de commandes et accédez au dossier contenant votre fichier projet (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="ec8b4-126">Exécutez la commande CLI NuGet `spec` pour générer le manifeste, qui est nommé d’après votre projet, par exemple `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ec8b4-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="ec8b4-127">Ouvrez le fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-127">Open the file in a text editor.</span></span> <span data-ttu-id="ec8b4-128">Le manifeste ressemble au code ci-dessous, où les jetons au format *$`<token>`$* seront remplacés pendant le processus d’empaquetage par des valeurs tirées du fichier Properties/AssemblyInfo.cs du projet.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-128">The manifest looks something like the code below, where tokens in the form *$`<token>`$* are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="ec8b4-129">Pour plus d’informations sur les jetons, consultez [Création d’un fichier .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="ec8b4-130">Sélectionnez un ID de package qui est unique sur nuget.org. Nous vous recommandons d’utiliser les conventions d’affectation de noms décrites dans [Création d’un package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="ec8b4-131">N’oubliez pas de mettre à jour les balises d’auteur et de description, sinon vous recevrez une erreur à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="ec8b4-132">Voici un fichier `.nuspec` mis à jour en guise d’exemple :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="ec8b4-133">Pour les packages générés en vue d’une consommation publique, faites particulièrement attention à l’élément `<tags>`, car ces balises aident l’utilisateur à trouver votre package et à comprendre ce qu’il fait.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ec8b4-134">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="ec8b4-134">Run the pack command</span></span>

<span data-ttu-id="ec8b4-135">Pour générer un package NuGet (un fichier `.nupkg`) à partir d’un projet, exécutez la commande `pack` :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="ec8b4-136">Cette commande crée `AppLogger.1.0.0.0.nupkg` en utilisant le nom et le numéro de version de package tirés du fichier `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="ec8b4-137">La commande émet des avertissements si vous n’avez pas mis à jour différents champs dans le fichier `.nuspec` et remplacé leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ec8b4-138">Publier le package</span><span class="sxs-lookup"><span data-stu-id="ec8b4-138">Publish the package</span></span>

<span data-ttu-id="ec8b4-139">Une fois que vous avez un fichier `.nupkg`, vous pouvez le publier sur nuget.org à l’aide de la commande `push`.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="ec8b4-140">(Vous pouvez également utiliser le [flux de travail de publication nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).)</span><span class="sxs-lookup"><span data-stu-id="ec8b4-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="ec8b4-141">Les packages que vous publiez sur nuget.org sont visibles publiquement par d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="ec8b4-142">Pour héberger des packages en privé, consultez [Hébergement de packages](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec8b4-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>


1. <span data-ttu-id="ec8b4-143">Créez un compte gratuit sur [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), ou connectez-vous si vous en avez déjà un.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="ec8b4-144">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ec8b4-145">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="ec8b4-146">Une fois connecté, sélectionnez votre nom d’utilisateur (dans le coin supérieur droit), puis **Clés API**.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="ec8b4-147">Sélectionnez **Créer**, spécifiez un nom pour votre clé, sélectionnez **Choix des étendues > Push** sous **Clé API**, entrez * pour **Modèle Glob**, puis Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter * for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="ec8b4-148">Une fois la clé créée, sélectionnez **Copier** pour récupérer la clé d’accès dont vous aurez besoin dans l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Copie de la clé d’API dans le Presse-papiers](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="ec8b4-150">Enregistrez votre clé à un emplacement sécurisé et ne la divulguez pas.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="ec8b4-151">Si votre clé est révélée accidentellement, vous pouvez toujours la régénérer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="ec8b4-152">Vous pouvez également supprimer la clé API si vous ne souhaitez plus distribuer des packages par le biais de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="ec8b4-153">À l’invite de commandes, exécutez la commande suivante, en spécifiant votre nom de package et en remplaçant la clé par la valeur copiée à l’étape 4 :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. <span data-ttu-id="ec8b4-154">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="ec8b4-155">À partir de votre profil sur nuget.org, sélectionnez **Manage Packages** (Gérer les packages) pour voir celui que vous venez de publier.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="ec8b4-156">Vous recevrez aussi un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-156">You also receive a confirmation email.</span></span> <span data-ttu-id="ec8b4-157">Notez que l’indexation de votre package et son apparition dans les résultats de la recherche peuvent prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="ec8b4-158">Pendant ce temps, la page de votre package contient le message ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ec8b4-158">During that time your package page shows the message below:</span></span>

    ![This package has not been indexed yet. (Ce package n’a pas encore été indexé.)](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="ec8b4-161">**Analyse antivirus** : tous les packages chargés sur nuget.org sont analysés et rejetés si des virus sont détectés.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="ec8b4-162">Tous les packages répertoriés sur nuget.org sont aussi analysés régulièrement.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="ec8b4-163">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="ec8b4-163">And that's it!</span></span> <span data-ttu-id="ec8b4-164">Vous venez de publier votre premier package NuGet sur [nuget.org](https://www.nuget.org/). D’autres développeurs peuvent maintenant l’utiliser dans leurs propres projets.</span><span class="sxs-lookup"><span data-stu-id="ec8b4-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="ec8b4-165">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="ec8b4-165">Related topics</span></span>

- [<span data-ttu-id="ec8b4-166">Créer un package</span><span class="sxs-lookup"><span data-stu-id="ec8b4-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="ec8b4-167">Publier un package</span><span class="sxs-lookup"><span data-stu-id="ec8b4-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="ec8b4-168">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="ec8b4-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ec8b4-169">Gestion de version des packages</span><span class="sxs-lookup"><span data-stu-id="ec8b4-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ec8b4-170">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="ec8b4-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
