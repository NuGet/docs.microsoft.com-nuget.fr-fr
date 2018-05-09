---
title: Guide d’introduction à la création et à la publication de package NuGet .NET Framework avec Visual Studio
description: Ce didacticiel explique pas à pas comment créer et publier un package NuGet .NET Framework avec Visual Studio 2017.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: quickstart
ms.openlocfilehash: 01760034a121b1ff6f227e006415779898c4cf6d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="f8141-103">Démarrage rapide : Créer et publier un package avec Visual Studio (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="f8141-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="f8141-104">La création d’un package NuGet à partir d’une bibliothèque de classes .NET Framework implique la création de la DLL dans Visual Studio, puis l’utilisation de l’outil en ligne de commande nuget.exe pour créer et publier le package.</span><span class="sxs-lookup"><span data-stu-id="f8141-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8141-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f8141-105">Prerequisites</span></span>

1. <span data-ttu-id="f8141-106">Installez une édition de Visual Studio 2017 à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET.</span><span class="sxs-lookup"><span data-stu-id="f8141-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="f8141-107">Visual Studio 2017 intègre automatiquement les fonctionnalités NuGet lorsqu’une charge de travail .NET est installée.</span><span class="sxs-lookup"><span data-stu-id="f8141-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="f8141-108">Installez l’interface CLI `nuget.exe` en la téléchargeant sur [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) : enregistrez ce fichier `.exe` dans un dossier approprié et ajoutez ce dossier à votre variable d’environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="f8141-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="f8141-109">[Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="f8141-109">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="f8141-110">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="f8141-110">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f8141-111">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="f8141-111">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="f8141-112">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="f8141-112">Create a class library project</span></span>

<span data-ttu-id="f8141-113">Vous pouvez utiliser un projet de bibliothèque de classes .NET Framework existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="f8141-113">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="f8141-114">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, sélectionnez le nœud **Visual C#**, sélectionnez le modèle « Bibliothèque de classes (.NET Framework) », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8141-114">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="f8141-115">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="f8141-115">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f8141-116">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="f8141-116">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="f8141-117">Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="f8141-117">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="f8141-118">Vous pouvez également définir la version cible de .NET Framework comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="f8141-118">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="f8141-119">Par exemple, consultez les guides pour [UWP](../guides/create-uwp-packages.md) et [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="f8141-119">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="f8141-120">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="f8141-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="f8141-121">Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f8141-121">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="f8141-122">Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.</span><span class="sxs-lookup"><span data-stu-id="f8141-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="f8141-123">Consultez [Créer et publier un package avec Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f8141-123">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="f8141-124">Configurer les propriétés du projet pour le package</span><span class="sxs-lookup"><span data-stu-id="f8141-124">Configure project properties for the package</span></span>

<span data-ttu-id="f8141-125">Un package NuGet contient un manifeste (fichier `.nuspec`), qui contient des métadonnées pertinentes telles que l’identificateur du package, le numéro de version, la description, etc.</span><span class="sxs-lookup"><span data-stu-id="f8141-125">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="f8141-126">Certaines de ces métadonnées peuvent être obtenues directement à partir des propriétés du projet, ce qui évite d’avoir à les mettre à jour séparément dans le projet et le manifeste.</span><span class="sxs-lookup"><span data-stu-id="f8141-126">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="f8141-127">Cette section décrit où définir les propriétés applicables.</span><span class="sxs-lookup"><span data-stu-id="f8141-127">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="f8141-128">Sélectionnez la commande de menu **Projet > Propriétés**, puis sélectionnez l’onglet **Application**.</span><span class="sxs-lookup"><span data-stu-id="f8141-128">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="f8141-129">Dans le champ **Nom de l’assembly**, donnez à votre package d’un identificateur unique.</span><span class="sxs-lookup"><span data-stu-id="f8141-129">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="f8141-130">Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f8141-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="f8141-131">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="f8141-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="f8141-132">Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="f8141-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="f8141-133">Sélectionnez le bouton **Informations sur l’assembly** pour afficher une boîte de dialogue dans laquelle vous pouvez entrer les autres propriétés à passer au manifeste (consultez [Informations de référence sur le fichier .nuspec - jetons de remplacement](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="f8141-133">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="f8141-134">Les champs les plus couramment utilisés sont **Titre**, **Description**, **Société**, **Copyright** et **Version de l’assembly**.</span><span class="sxs-lookup"><span data-stu-id="f8141-134">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="f8141-135">Veillez à utiliser des propriétés descriptives, car elles se retrouveront avec votre package sur un hôte comme nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f8141-135">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informations sur l’assembly dans un projet .NET Framework dans Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="f8141-137">Facultatif : Pour afficher et modifier les propriétés directement, ouvrez le fichier `Properties/AssemblyInfo.cs` dans le projet.</span><span class="sxs-lookup"><span data-stu-id="f8141-137">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="f8141-138">Une fois les propriétés définies, faites passer la configuration du projet en **Version finale** et regénérez le projet pour générer la DLL mise à jour.</span><span class="sxs-lookup"><span data-stu-id="f8141-138">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="f8141-139">Générer le manifeste initial</span><span class="sxs-lookup"><span data-stu-id="f8141-139">Generate the initial manifest</span></span>

<span data-ttu-id="f8141-140">Une fois la DLL en main et les propriétés du projet définies, utilisez la commande `nuget spec` pour générer un fichier `.nuspec` initial à partir du projet.</span><span class="sxs-lookup"><span data-stu-id="f8141-140">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="f8141-141">Cette étape inclut les jetons de remplacement appropriés pour obtenir des informations à partir du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="f8141-141">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="f8141-142">Vous exécutez `nuget spec` une seule fois pour générer le manifeste initial.</span><span class="sxs-lookup"><span data-stu-id="f8141-142">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="f8141-143">Au moment de la mise à jour le package, vous changez les valeurs dans votre projet ou modifiez directement le manifeste.</span><span class="sxs-lookup"><span data-stu-id="f8141-143">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="f8141-144">Ouvrez une invite de commandes et accédez au dossier projet contenant le fichier (`AppLogger.csproj`).</span><span class="sxs-lookup"><span data-stu-id="f8141-144">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="f8141-145">Exécutez la commande suivante : `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="f8141-145">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="f8141-146">Quand vous spécifiez un projet, NuGet crée un manifeste qui correspond au nom du projet (dans ce cas, `AppLogger.nuspec`).</span><span class="sxs-lookup"><span data-stu-id="f8141-146">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="f8141-147">Il inclut également les jetons de remplacement dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="f8141-147">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="f8141-148">Ouvrez `AppLogger.nuspec` dans un éditeur de texte pour examiner son contenu, qui doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="f8141-148">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="f8141-149">Modifier le manifeste</span><span class="sxs-lookup"><span data-stu-id="f8141-149">Edit the manifest</span></span>

1. <span data-ttu-id="f8141-150">NuGet génère une erreur si vous essayez de créer un package avec les valeurs par défaut dans votre fichier `.nuspec`. Vous devez donc modifier les champs suivants avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="f8141-150">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="f8141-151">Consultez [Informations de référence sur le fichier .nuspec - éléments uniques](../reference/nuspec.md#single-elements) pour obtenir une description de la façon dont ils sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="f8141-151">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="f8141-152">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="f8141-152">licenseUrl</span></span>
    - <span data-ttu-id="f8141-153">projectUrl</span><span class="sxs-lookup"><span data-stu-id="f8141-153">projectUrl</span></span>
    - <span data-ttu-id="f8141-154">iconUrl</span><span class="sxs-lookup"><span data-stu-id="f8141-154">iconUrl</span></span>
    - <span data-ttu-id="f8141-155">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="f8141-155">releaseNotes</span></span>
    - <span data-ttu-id="f8141-156">étiquettes</span><span class="sxs-lookup"><span data-stu-id="f8141-156">tags</span></span>

1. <span data-ttu-id="f8141-157">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages sur des sources comme nuget.org et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="f8141-157">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="f8141-158">Vous pouvez également ajouter des éléments au manifeste à ce stade, comme décrit dans [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f8141-158">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="f8141-159">Enregistrez le fichier avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="f8141-159">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f8141-160">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="f8141-160">Run the pack command</span></span>

1. <span data-ttu-id="f8141-161">À partir d’une invite de commandes dans le dossier contenant votre fichier `.nuspec`, exécutez la commande `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="f8141-161">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="f8141-162">NuGet génère un fichier `.nupkg` au format *identifier-version.nupkg* que vous trouverez dans le dossier actif.</span><span class="sxs-lookup"><span data-stu-id="f8141-162">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f8141-163">Publier le package</span><span class="sxs-lookup"><span data-stu-id="f8141-163">Publish the package</span></span>

<span data-ttu-id="f8141-164">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de la commande `nuget.exe` avec une clé API acquise sur nuget.org. Pour nuget.org, vous devez utiliser `nuget.exe` 4.1.0 ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="f8141-164">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="f8141-165">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="f8141-165">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="f8141-166">Publier avec nuget push</span><span class="sxs-lookup"><span data-stu-id="f8141-166">Publish with nuget push</span></span>

1. <span data-ttu-id="f8141-167">Accédez au dossier contenant le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f8141-167">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="f8141-168">Exécutez la commande suivante, en spécifiant le nom de votre package et en remplaçant la valeur de la clé par celle de votre clé API :</span><span class="sxs-lookup"><span data-stu-id="f8141-168">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f8141-169">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="f8141-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="f8141-170">Voir [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="f8141-170">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="f8141-171">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="f8141-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="f8141-172">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="f8141-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="f8141-173">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="f8141-173">Related topics</span></span>

- [<span data-ttu-id="f8141-174">Créer un package</span><span class="sxs-lookup"><span data-stu-id="f8141-174">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="f8141-175">Publier un package</span><span class="sxs-lookup"><span data-stu-id="f8141-175">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="f8141-176">Packages de préversion</span><span class="sxs-lookup"><span data-stu-id="f8141-176">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="f8141-177">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="f8141-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f8141-178">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="f8141-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f8141-179">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="f8141-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
