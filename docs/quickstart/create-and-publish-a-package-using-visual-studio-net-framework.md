---
title: Créer et publier un package .NET Framework NuGet avec Visual Studio sur Windows
description: Ce tutoriel explique pas à pas comment créer et publier un package NuGet .NET Framework avec Visual Studio dans Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380643"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="bfe2c-103">Démarrage rapide : Créer et publier un package avec Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="bfe2c-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="bfe2c-104">La création d’un package NuGet à partir d’une bibliothèque de classes .NET Framework implique de créer la DLL dans Visual Studio sous Windows, puis d’utiliser l’outil en ligne de commande nuget.exe pour créer et publier le package.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="bfe2c-105">Ce Quickstart s’applique à Visual Studio 2017 et aux versions supérieures pour Windows uniquement.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-105">This Quickstart applies to Visual Studio 2017 and higher versions for Windows only.</span></span> <span data-ttu-id="bfe2c-106">Visual Studio pour Mac n’intègre pas les fonctionnalités décrites ici.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="bfe2c-107">Utilisez dans ce cas les [outils de l’interface CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfe2c-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="bfe2c-108">Prerequisites</span></span>

1. <span data-ttu-id="bfe2c-109">Installez une édition de Visual Studio 2017 ou version supérieure à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-109">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="bfe2c-110">Visual Studio 2017 intègre automatiquement les fonctionnalités NuGet lorsqu’une charge de travail .NET est installée.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="bfe2c-111">Installez l’interface CLI `nuget.exe` en la téléchargeant sur [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) : enregistrez ce fichier `.exe` dans un dossier approprié et ajoutez ce dossier à votre variable d’environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="bfe2c-112">[Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="bfe2c-113">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="bfe2c-114">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="bfe2c-115">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="bfe2c-115">Create a class library project</span></span>

<span data-ttu-id="bfe2c-116">Vous pouvez utiliser un projet de bibliothèque de classes .NET Framework existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="bfe2c-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="bfe2c-117">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, sélectionnez le nœud **Visual C#**, sélectionnez le modèle « Bibliothèque de classes (.NET Framework) », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="bfe2c-118">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="bfe2c-119">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="bfe2c-120">Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="bfe2c-121">Vous pouvez également définir la version cible de .NET Framework comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="bfe2c-122">Par exemple, consultez les guides pour [UWP](../guides/create-uwp-packages.md) et [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="bfe2c-123">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="bfe2c-124">Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="bfe2c-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="bfe2c-125">Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="bfe2c-126">Consultez [Créer et publier un package avec Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="bfe2c-127">Configurer les propriétés du projet pour le package</span><span class="sxs-lookup"><span data-stu-id="bfe2c-127">Configure project properties for the package</span></span>

<span data-ttu-id="bfe2c-128">Un package NuGet contient un manifeste (fichier `.nuspec`), qui contient des métadonnées pertinentes telles que l’identificateur du package, le numéro de version, la description, etc.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="bfe2c-129">Certaines de ces métadonnées peuvent être obtenues directement à partir des propriétés du projet, ce qui évite d’avoir à les mettre à jour séparément dans le projet et le manifeste.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="bfe2c-130">Cette section décrit où définir les propriétés applicables.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="bfe2c-131">Sélectionnez la commande de menu **Projet > Propriétés**, puis sélectionnez l’onglet **Application**.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="bfe2c-132">Dans le champ **Nom de l’assembly**, donnez à votre package d’un identificateur unique.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="bfe2c-133">Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="bfe2c-134">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="bfe2c-135">Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="bfe2c-136">Sélectionnez le bouton **Informations sur l’assembly** pour afficher une boîte de dialogue dans laquelle vous pouvez entrer les autres propriétés à passer au manifeste (consultez [Informations de référence sur le fichier .nuspec - jetons de remplacement](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="bfe2c-137">Les champs les plus couramment utilisés sont **Titre**, **Description**, **Société**, **Copyright** et **Version de l’assembly**.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="bfe2c-138">Veillez à utiliser des propriétés descriptives, car elles se retrouveront avec votre package sur un hôte comme nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informations sur l’assembly dans un projet .NET Framework dans Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="bfe2c-140">Facultatif : Pour afficher et modifier les propriétés directement, ouvrez le fichier `Properties/AssemblyInfo.cs` dans le projet.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="bfe2c-141">Une fois les propriétés définies, faites passer la configuration du projet en **Version finale** et regénérez le projet pour générer la DLL mise à jour.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="bfe2c-142">Générer le manifeste initial</span><span class="sxs-lookup"><span data-stu-id="bfe2c-142">Generate the initial manifest</span></span>

<span data-ttu-id="bfe2c-143">Une fois la DLL en main et les propriétés du projet définies, utilisez la commande `nuget spec` pour générer un fichier `.nuspec` initial à partir du projet.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="bfe2c-144">Cette étape inclut les jetons de remplacement appropriés pour obtenir des informations à partir du fichier projet.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="bfe2c-145">Vous exécutez `nuget spec` une seule fois pour générer le manifeste initial.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="bfe2c-146">Au moment de la mise à jour le package, vous changez les valeurs dans votre projet ou modifiez directement le manifeste.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="bfe2c-147">Ouvrez une invite de commandes et accédez au dossier projet contenant le fichier (`AppLogger.csproj`).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="bfe2c-148">Exécutez la commande suivante : `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="bfe2c-149">Quand vous spécifiez un projet, NuGet crée un manifeste qui correspond au nom du projet (dans ce cas, `AppLogger.nuspec`).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="bfe2c-150">Il inclut également les jetons de remplacement dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="bfe2c-151">Ouvrez `AppLogger.nuspec` dans un éditeur de texte pour examiner son contenu, qui doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="bfe2c-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="bfe2c-152">Modifier le manifeste</span><span class="sxs-lookup"><span data-stu-id="bfe2c-152">Edit the manifest</span></span>

1. <span data-ttu-id="bfe2c-153">NuGet génère une erreur si vous essayez de créer un package avec les valeurs par défaut dans votre fichier `.nuspec`. Vous devez donc modifier les champs suivants avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="bfe2c-154">Consultez [Informations de référence sur le fichier .nuspec - éléments de métadonnées facultatifs](../reference/nuspec.md#optional-metadata-elements) pour obtenir une description de la façon dont ils sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="bfe2c-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="bfe2c-155">licenseUrl</span></span>
    - <span data-ttu-id="bfe2c-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="bfe2c-156">projectUrl</span></span>
    - <span data-ttu-id="bfe2c-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="bfe2c-157">iconUrl</span></span>
    - <span data-ttu-id="bfe2c-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="bfe2c-158">releaseNotes</span></span>
    - <span data-ttu-id="bfe2c-159">tags</span><span class="sxs-lookup"><span data-stu-id="bfe2c-159">tags</span></span>

1. <span data-ttu-id="bfe2c-160">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages sur des sources comme nuget.org et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="bfe2c-161">Vous pouvez également ajouter des éléments au manifeste à ce stade, comme décrit dans [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="bfe2c-162">Enregistrez le fichier avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="bfe2c-163">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="bfe2c-163">Run the pack command</span></span>

1. <span data-ttu-id="bfe2c-164">À partir d’une invite de commandes dans le dossier contenant votre fichier `.nuspec`, exécutez la commande `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="bfe2c-165">NuGet génère un fichier `.nupkg` au format *identifier-version.nupkg* que vous trouverez dans le dossier actif.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="bfe2c-166">Publier le package</span><span class="sxs-lookup"><span data-stu-id="bfe2c-166">Publish the package</span></span>

<span data-ttu-id="bfe2c-167">Une fois `.nupkg` que vous avez un fichier, `nuget.exe` vous le publiez à nuget.org à l’aide d’une clé API acquise à partir de nuget.org. Pour nuget.org vous devez `nuget.exe` utiliser 4.1.0 ou plus.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="bfe2c-168">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="bfe2c-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="bfe2c-169">Publier avec nuget push</span><span class="sxs-lookup"><span data-stu-id="bfe2c-169">Publish with nuget push</span></span>

1. <span data-ttu-id="bfe2c-170">Ouvrez une ligne de commande et accédez au dossier contenant le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="bfe2c-171">Exécutez la commande suivante, en spécifiant le nom de votre package et en remplaçant la valeur de la clé par celle de votre clé API :</span><span class="sxs-lookup"><span data-stu-id="bfe2c-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="bfe2c-172">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="bfe2c-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="bfe2c-173">Voir [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="bfe2c-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="bfe2c-174">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="bfe2c-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="bfe2c-175">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="bfe2c-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="bfe2c-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bfe2c-176">Next steps</span></span>

<span data-ttu-id="bfe2c-177">Félicitations pour la création de votre premier package NuGet !</span><span class="sxs-lookup"><span data-stu-id="bfe2c-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfe2c-178">Créer un package</span><span class="sxs-lookup"><span data-stu-id="bfe2c-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="bfe2c-179">Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bfe2c-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="bfe2c-180">Publier un forfait</span><span class="sxs-lookup"><span data-stu-id="bfe2c-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="bfe2c-181">Forfaits de pré-version</span><span class="sxs-lookup"><span data-stu-id="bfe2c-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="bfe2c-182">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="bfe2c-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="bfe2c-183">Contrôle de version des packages</span><span class="sxs-lookup"><span data-stu-id="bfe2c-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="bfe2c-184">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="bfe2c-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
