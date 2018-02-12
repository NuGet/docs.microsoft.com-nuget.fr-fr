---
title: "Guide d’introduction à la création et à la publication de package NuGet avec Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Ce didacticiel explique pas à pas comment créer et publier un package NuGet avec Visual Studio 2017."
keywords: "Création de package NuGet, publication de package NuGet, didacticiel NuGet, création de package NuGet avec Visual Studio, pack msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a><span data-ttu-id="e4a3b-104">Créer et publier un package avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4a3b-104">Create and publish a package using Visual Studio</span></span>

<span data-ttu-id="e4a3b-105">La création d’un package NuGet à partir d’une bibliothèque de classes .NET dans Visual Studio est un processus simple, de même que sa publication sur nuget.org avec un outil de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="e4a3b-105">It's a simple process to create a NuGet package from a .NET Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="e4a3b-106">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e4a3b-106">Pre-requisites</span></span>

1. <span data-ttu-id="e4a3b-107">Installez une édition de Visual Studio 2017 à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="e4a3b-108">Visual Studio 2017 intègre automatiquement les fonctionnalités NuGet lorsqu’une charge de travail .NET est installée.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="e4a3b-109">Installez l’interface CLI `nuget.exe` en la téléchargeant sur [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) : enregistrez ce fichier `.exe` dans un dossier approprié et ajoutez ce dossier à votre variable d’environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="e4a3b-110">Si le [Kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/download/) est installé, vous pouvez également utiliser l’interface CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="e4a3b-111">[Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="e4a3b-112">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="e4a3b-113">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="e4a3b-114">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="e4a3b-114">Create a class library project</span></span>

<span data-ttu-id="e4a3b-115">Vous pouvez utiliser un projet de bibliothèque de classes .NET existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-115">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="e4a3b-116">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez le modèle « Bibliothèque de classes (.NET Standard) », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="e4a3b-117">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="e4a3b-118">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="e4a3b-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="e4a3b-119">Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="e4a3b-120">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="e4a3b-121">Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-121">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
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
> <span data-ttu-id="e4a3b-122">Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="e4a3b-123">Configurer les propriétés de package</span><span class="sxs-lookup"><span data-stu-id="e4a3b-123">Configure package properties</span></span>

1. <span data-ttu-id="e4a3b-124">Sélectionnez la commande de menu **Projet > Propriétés**, puis sélectionnez l’onglet **Package** :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-124">Select the **Project > Properties** menu command, then select the **Package** tab:</span></span>

    ![Propriétés de package NuGet dans un projet Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="e4a3b-126">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="e4a3b-127">Donnez à votre package un identificateur unique et remplissez les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="e4a3b-128">Vous trouverez une description des différentes propriétés dans la section [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e4a3b-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="e4a3b-129">Toutes ces propriétés sont ajoutées au manifeste `.nuspec` créé par Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="e4a3b-130">Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="e4a3b-131">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="e4a3b-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="e4a3b-132">Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="e4a3b-133">Facultatif : pour afficher les propriétés directement dans le fichier projet, cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et sélectionnez **Modifier AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="e4a3b-134">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="e4a3b-134">Run the pack command</span></span>

1. <span data-ttu-id="e4a3b-135">Définissez la configuration en **Release**.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="e4a3b-136">Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez la commande **Empaqueter** :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Commande pack de NuGet dans le menu contextuel du projet Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="e4a3b-138">Visual Studio génère le projet et crée le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="e4a3b-139">Lisez les informations qui apparaissent sur la fenêtre **Sortie** (comme dans la capture d’écran suivante), notamment le chemin d’accès du fichier de package.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="e4a3b-140">Notez également que l’assembly généré est dans `bin\Release\netstandard2.0` comme il convient à la cible .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="e4a3b-141">Autre option : pack avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="e4a3b-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="e4a3b-142">En guise d’alternative à l’utilisation de la commande de menu **Pack**, NuGet 4.x+ et MSBuild 15.1+ prennent en charge une cible `pack` lorsque le projet contient les données de package nécessaires :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data:</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="e4a3b-143">Vous trouverez alors le package dans le dossier `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-143">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="e4a3b-144">Pour plus d’options avec `msbuild /t:pack`, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="e4a3b-144">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="e4a3b-145">Publier le package</span><span class="sxs-lookup"><span data-stu-id="e4a3b-145">Publish the package</span></span>

<span data-ttu-id="e4a3b-146">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de l’interface CLI `nuget.exe` ou `dotnet.exe`, avec une clé API acquise sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-146">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="e4a3b-147">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="e4a3b-147">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="e4a3b-148">Publier avec nuget push</span><span class="sxs-lookup"><span data-stu-id="e4a3b-148">Publish with nuget push</span></span>

<span data-ttu-id="e4a3b-149">Cette étape aboutit au même résultat que `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-149">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="e4a3b-150">Accédez au dossier contenant le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-150">Change to the folder containing the `.nupkg` file..</span></span>

1. <span data-ttu-id="e4a3b-151">Exécutez la commande suivante, en spécifiant le nom de votre package et en remplaçant la valeur de la clé par celle de votre clé API :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-151">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="e4a3b-152">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="e4a3b-152">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="e4a3b-153">Voir [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="e4a3b-153">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="e4a3b-154">Publier avec dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="e4a3b-154">Publish with dotnet nuget push</span></span>

<span data-ttu-id="e4a3b-155">Cette étape aboutit au même résultat que `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="e4a3b-155">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="e4a3b-156">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="e4a3b-156">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="e4a3b-157">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="e4a3b-157">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="e4a3b-158">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="e4a3b-158">Related topics</span></span>

- [<span data-ttu-id="e4a3b-159">Créer un package</span><span class="sxs-lookup"><span data-stu-id="e4a3b-159">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="e4a3b-160">Publier un package</span><span class="sxs-lookup"><span data-stu-id="e4a3b-160">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="e4a3b-161">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="e4a3b-161">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e4a3b-162">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="e4a3b-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="e4a3b-163">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="e4a3b-163">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="e4a3b-164">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="e4a3b-164">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e4a3b-165">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e4a3b-165">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)