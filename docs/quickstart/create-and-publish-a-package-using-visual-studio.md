---
title: Créer et publier un package .NET Standard avec Visual Studio sous Windows
description: Ce didacticiel explique pas à pas comment créer et publier un package NuGet .NET Standard avec Visual Studio 2017 sous Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: d30e89473b5f00895136b75a90d8d95b7645a100
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812977"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="acb4f-103">Démarrage rapide : Créer et publier un package NuGet avec Visual Studio (.NET Standard, Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="acb4f-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="acb4f-104">La création d’un package NuGet à partir d’une bibliothèque de classes .NET Standard dans Visual Studio sous Windows est un processus simple, de même que sa publication sur nuget.org avec un outil de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="acb4f-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="acb4f-105">Ce démarrage rapide s’applique à Visual Studio 2017 pour Windows uniquement.</span><span class="sxs-lookup"><span data-stu-id="acb4f-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="acb4f-106">Visual Studio pour Mac n’intègre pas les fonctionnalités décrites ici.</span><span class="sxs-lookup"><span data-stu-id="acb4f-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="acb4f-107">Utilisez dans ce cas les [outils de l’interface CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="acb4f-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acb4f-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="acb4f-108">Prerequisites</span></span>

1. <span data-ttu-id="acb4f-109">Installez une édition de Visual Studio 2017 à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET.</span><span class="sxs-lookup"><span data-stu-id="acb4f-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="acb4f-110">Visual Studio 2017 intègre automatiquement les fonctionnalités NuGet lorsqu’une charge de travail .NET est installée.</span><span class="sxs-lookup"><span data-stu-id="acb4f-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="acb4f-111">Installez l’un des outils CLI.</span><span class="sxs-lookup"><span data-stu-id="acb4f-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="acb4f-112">Pour l’interface CLI `dotnet`, installez le [SDK .NET Core](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="acb4f-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="acb4f-113">L’interface CLI dotnet est requise pour les projets .NET Standard qui utilisent le format de style SDK (attribut SDK).</span><span class="sxs-lookup"><span data-stu-id="acb4f-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="acb4f-114">Pour la CLI `nuget.exe`, téléchargez-la à partir de [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), en enregistrant le fichier `.exe` dans un dossier approprié et en ajoutant ce dossier à votre variable d’environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="acb4f-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="acb4f-115">L’interface CLI nuget.exe est utilisée pour les bibliothèques .NET Standard au format non SDK.</span><span class="sxs-lookup"><span data-stu-id="acb4f-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="acb4f-116">[Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="acb4f-116">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="acb4f-117">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="acb4f-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="acb4f-118">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="acb4f-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="acb4f-119">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="acb4f-119">Create a class library project</span></span>

<span data-ttu-id="acb4f-120">Vous pouvez utiliser un projet de bibliothèque de classes .NET Standard existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="acb4f-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="acb4f-121">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez le modèle « Bibliothèque de classes (.NET Standard) », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="acb4f-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="acb4f-122">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="acb4f-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="acb4f-123">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="acb4f-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="acb4f-124">Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="acb4f-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="acb4f-125">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="acb4f-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="acb4f-126">Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="acb4f-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="acb4f-127">Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.</span><span class="sxs-lookup"><span data-stu-id="acb4f-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="acb4f-128">Configurer les propriétés de package</span><span class="sxs-lookup"><span data-stu-id="acb4f-128">Configure package properties</span></span>

1. <span data-ttu-id="acb4f-129">Sélectionnez la commande de menu **Projet > Propriétés**, puis l’onglet **Package**. (L’onglet **Package** s’affiche uniquement pour les projets de bibliothèque de classes .NET Standard ; si vous ciblez le .NET Framework, consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="acb4f-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="acb4f-130">Si cet onglet n’est pas visible pour un projet .NET Standard, vous devrez peut-être mettre à jour Visual Studio 2017 avec la dernière version.)</span><span class="sxs-lookup"><span data-stu-id="acb4f-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Propriétés de package NuGet dans un projet Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="acb4f-132">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="acb4f-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="acb4f-133">Donnez à votre package un identificateur unique et remplissez les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="acb4f-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="acb4f-134">Vous trouverez une description des différentes propriétés dans la section [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="acb4f-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="acb4f-135">Toutes ces propriétés sont ajoutées au manifeste `.nuspec` créé par Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="acb4f-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="acb4f-136">Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="acb4f-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="acb4f-137">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="acb4f-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="acb4f-138">Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="acb4f-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="acb4f-139">Facultatif : pour afficher les propriétés directement dans le fichier projet, cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et sélectionnez **Modifier AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="acb4f-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="acb4f-140">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="acb4f-140">Run the pack command</span></span>

1. <span data-ttu-id="acb4f-141">Définissez la configuration en **Release**.</span><span class="sxs-lookup"><span data-stu-id="acb4f-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="acb4f-142">Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez la commande **Empaqueter** :</span><span class="sxs-lookup"><span data-stu-id="acb4f-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Commande pack de NuGet dans le menu contextuel du projet Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="acb4f-144">Visual Studio génère le projet et crée le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="acb4f-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="acb4f-145">Lisez les informations qui apparaissent sur la fenêtre **Sortie** (comme dans la capture d’écran suivante), notamment le chemin d’accès du fichier de package.</span><span class="sxs-lookup"><span data-stu-id="acb4f-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="acb4f-146">Notez également que l’assembly généré est dans `bin\Release\netstandard2.0` comme il convient à la cible .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="acb4f-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="acb4f-147">Autre option : pack avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="acb4f-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="acb4f-148">En guise d’alternative à l’utilisation de la commande de menu **Pack**, NuGet 4.x+ et MSBuild 15.1+ prennent en charge une cible `pack` quand le projet contient les données de package nécessaires.</span><span class="sxs-lookup"><span data-stu-id="acb4f-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="acb4f-149">Ouvrez une invite de commandes, accédez au dossier de votre projet et exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="acb4f-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="acb4f-150">(Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu Démarrer, car elle est configurée avec tous les chemins nécessaires pour MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="acb4f-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="acb4f-151">Vous trouverez alors le package dans le dossier `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="acb4f-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="acb4f-152">Pour plus d’options avec `msbuild -t:pack`, consultez [Commandes pack et restore NuGet comme cibles MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="acb4f-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="acb4f-153">Publier le package</span><span class="sxs-lookup"><span data-stu-id="acb4f-153">Publish the package</span></span>

<span data-ttu-id="acb4f-154">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de l’interface CLI `nuget.exe` ou `dotnet.exe`, avec une clé API acquise sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="acb4f-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="acb4f-155">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="acb4f-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="acb4f-156">Publier avec dotnet nuget push (CLI dotnet)</span><span class="sxs-lookup"><span data-stu-id="acb4f-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="acb4f-157">Cette étape aboutit au même résultat que `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="acb4f-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="acb4f-158">Publier avec nuget push (CLI nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="acb4f-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="acb4f-159">Cette étape aboutit au même résultat que `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="acb4f-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="acb4f-160">Accédez au dossier contenant le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="acb4f-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="acb4f-161">Exécutez la commande suivante, en spécifiant le nom de votre package et en remplaçant la valeur de la clé par celle de votre clé API :</span><span class="sxs-lookup"><span data-stu-id="acb4f-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="acb4f-162">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="acb4f-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="acb4f-163">Voir [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="acb4f-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="acb4f-164">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="acb4f-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="acb4f-165">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="acb4f-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="acb4f-166">Ajout d’un fichier Lisez-moi et d’autres fichiers</span><span class="sxs-lookup"><span data-stu-id="acb4f-166">Adding a readme and other files</span></span>

<span data-ttu-id="acb4f-167">Pour spécifier directement les fichiers à inclure dans le package, modifiez le fichier projet et utilisez la propriété `content` :</span><span class="sxs-lookup"><span data-stu-id="acb4f-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="acb4f-168">Cela inclut un fichier nommé `readme.txt` dans la racine du package.</span><span class="sxs-lookup"><span data-stu-id="acb4f-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="acb4f-169">Visual Studio affiche le contenu de ce fichier sous forme de texte brut immédiatement après avoir installé le package directement.</span><span class="sxs-lookup"><span data-stu-id="acb4f-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="acb4f-170">(Les fichiers Lisez-moi ne s’affichent pas pour les packages installés en tant que dépendances).</span><span class="sxs-lookup"><span data-stu-id="acb4f-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="acb4f-171">Par exemple, voici comment s’affiche le fichier Lisez-moi du package HtmlAgilityPack :</span><span class="sxs-lookup"><span data-stu-id="acb4f-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Affichage d’un fichier Lisez-moi pour un package NuGet lors de l’installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="acb4f-173">Le simple ajout du fichier readme.txt à la racine du projet ne permet pas de l’ajouter dans le package résultant.</span><span class="sxs-lookup"><span data-stu-id="acb4f-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="acb4f-174">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="acb4f-174">Related topics</span></span>

- [<span data-ttu-id="acb4f-175">Créer un package</span><span class="sxs-lookup"><span data-stu-id="acb4f-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="acb4f-176">Publier un package</span><span class="sxs-lookup"><span data-stu-id="acb4f-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="acb4f-177">Packages de préversion</span><span class="sxs-lookup"><span data-stu-id="acb4f-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="acb4f-178">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="acb4f-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="acb4f-179">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="acb4f-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="acb4f-180">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="acb4f-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="acb4f-181">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="acb4f-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="acb4f-182">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="acb4f-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
