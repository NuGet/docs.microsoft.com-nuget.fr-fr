---
title: Créer et publier un package .NET Standard NuGet - Visual Studio sur Windows
description: Ce tutoriel explique pas à pas comment créer et publier un package NuGet .NET Standard avec Visual Studio sous Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231290"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="46acc-103">Démarrage rapide : Créer et publier un package NuGet avec Visual Studio (.NET Standard, Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="46acc-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="46acc-104">La création d’un package NuGet à partir d’une bibliothèque de classes .NET Standard dans Visual Studio sous Windows est un processus simple, de même que sa publication sur nuget.org avec un outil de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="46acc-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="46acc-105">Si vous utilisez Visual Studio pour Mac, consultez [ces informations](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sur la création d’un package NuGet ou utilisez les [outils CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46acc-106">Conditions préalables requises</span><span class="sxs-lookup"><span data-stu-id="46acc-106">Prerequisites</span></span>

1. <span data-ttu-id="46acc-107">Installez une édition de Visual Studio 2019 à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec n’importe quelle charge de travail liée à .NET Core.</span><span class="sxs-lookup"><span data-stu-id="46acc-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="46acc-108">Si ce n'est déjà fait, installez l’interface CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="46acc-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="46acc-109">Pour la CLI `dotnet`, à compter de Visual Studio 2017, la CLI `dotnet` est installée automatiquement avec les charges de travail associées à NET Core.</span><span class="sxs-lookup"><span data-stu-id="46acc-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="46acc-110">Dans le cas contraire, installez le [SDK .NET Core](https://www.microsoft.com/net/download/) pour obtenir la CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="46acc-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="46acc-111">La CLI `dotnet` dotnet est requise pour les projets .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md) (attribut SDK).</span><span class="sxs-lookup"><span data-stu-id="46acc-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="46acc-112">Le modèle de bibliothèque de classes .NET Standard par défaut dans Visual Studio 2017 et les versions ultérieures, qui est utilisé dans cet article, utilise l’attribut SDK.</span><span class="sxs-lookup"><span data-stu-id="46acc-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="46acc-113">Si vous utilisez un projet qui n’est pas de type SDK, suivez les procédures décrites dans [Créer et publier un package .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pour créer et publier le package à la place.</span><span class="sxs-lookup"><span data-stu-id="46acc-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="46acc-114">Pour cet article, la CLI `dotnet` est recommandée.</span><span class="sxs-lookup"><span data-stu-id="46acc-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="46acc-115">Bien que vous puissiez publier un package NuGet à l’aide de la CLI `nuget.exe`, certaines des étapes décrites dans cet article sont spécifiques aux projets de type SDK et à la CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="46acc-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="46acc-116">La cLI nuget.exe est utilisée pour les [projets qui ne sont pas de type SDK](../resources/check-project-format.md) (généralement .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="46acc-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="46acc-117">[Créez un compte gratuit sur nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="46acc-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="46acc-118">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="46acc-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="46acc-119">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="46acc-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="46acc-120">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="46acc-120">Create a class library project</span></span>

<span data-ttu-id="46acc-121">Vous pouvez utiliser un projet de bibliothèque de classes .NET Standard existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="46acc-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="46acc-122">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez le modèle « Bibliothèque de classes (.NET Standard) », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="46acc-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="46acc-123">Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.</span><span class="sxs-lookup"><span data-stu-id="46acc-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="46acc-124">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="46acc-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="46acc-125">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="46acc-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="46acc-126">Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="46acc-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="46acc-127">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="46acc-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="46acc-128">Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="46acc-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="46acc-129">Configurer les propriétés de package</span><span class="sxs-lookup"><span data-stu-id="46acc-129">Configure package properties</span></span>

1. <span data-ttu-id="46acc-130">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et choisissez la commande de menu **Propriétés**, puis sélectionnez l’onglet **Package**.</span><span class="sxs-lookup"><span data-stu-id="46acc-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="46acc-131">L’onglet **Package** s’affiche uniquement pour les projets de type SDK dans Visual Studio, généralement les projets de bibliothèque de classes .NET Standard ou .NET Core. Si vous ciblez un projet qui n’est pas de style SDK (généralement .NET Framework), [migrez le projet](../consume-packages/migrate-packages-config-to-package-reference.md) ou consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) à la place des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="46acc-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Propriétés de package NuGet dans un projet Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="46acc-133">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="46acc-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="46acc-134">Donnez à votre package un identificateur unique et remplissez les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="46acc-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="46acc-135">Pour un mappage des propriétés MSBuild (projet de type SDK) aux propriétés d'un fichier *.nuspec*, voir [Cibles de pack](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="46acc-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="46acc-136">Pour les descriptions des propriétés, voir la référence du fichier [.nuspec ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="46acc-137">Toutes ces propriétés sont ajoutées au manifeste `.nuspec` créé par Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="46acc-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="46acc-138">Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="46acc-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="46acc-139">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="46acc-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="46acc-140">Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="46acc-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="46acc-141">(Facultatif) Pour afficher les propriétés directement dans le fichier projet, cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et sélectionnez **Modifier AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="46acc-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="46acc-142">Cette option n’est disponible qu’à partir de Visual Studio 2017 pour les projets qui utilisent l’attribut de style SDK.</span><span class="sxs-lookup"><span data-stu-id="46acc-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="46acc-143">Sinon, cliquez avec le bouton droit sur le projet et choisissez **Décharger le projet**.</span><span class="sxs-lookup"><span data-stu-id="46acc-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="46acc-144">Cliquez ensuite avec le bouton droit sur le projet déchargé, puis choisissez **Modifier AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="46acc-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="46acc-145">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="46acc-145">Run the pack command</span></span>

1. <span data-ttu-id="46acc-146">Définissez la configuration en **Release**.</span><span class="sxs-lookup"><span data-stu-id="46acc-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="46acc-147">Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez la commande **Empaqueter** :</span><span class="sxs-lookup"><span data-stu-id="46acc-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Commande pack de NuGet dans le menu contextuel du projet Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="46acc-149">Si vous ne voyez pas la commande **Pack**, cela signifie que votre projet n’est probablement pas un projet de type SDK et que vous devez utiliser la CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="46acc-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="46acc-150">[Migrez le projet](../consume-packages/migrate-packages-config-to-package-reference.md) et utilisez la CLI `dotnet`, ou consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) à la place pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="46acc-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="46acc-151">Visual Studio génère le projet et crée le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="46acc-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="46acc-152">Lisez les informations qui apparaissent sur la fenêtre **Sortie** (comme dans la capture d’écran suivante), notamment le chemin d’accès du fichier de package.</span><span class="sxs-lookup"><span data-stu-id="46acc-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="46acc-153">Notez également que l’assembly généré est dans `bin\Release\netstandard2.0` comme il convient à la cible .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="46acc-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="46acc-154">(Facultatif) Générer le package à la création</span><span class="sxs-lookup"><span data-stu-id="46acc-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="46acc-155">Vous pouvez configurer Visual Studio pour générer automatiquement le package NuGet lorsque vous générez le projet.</span><span class="sxs-lookup"><span data-stu-id="46acc-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="46acc-156">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet et choisissez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="46acc-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="46acc-157">Dans l’onglet **Package**, sélectionnez **Générer le package NuGet à la création**.</span><span class="sxs-lookup"><span data-stu-id="46acc-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Générer automatiquement le package à la création](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="46acc-159">Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="46acc-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="46acc-160">(Facultatif) Compresser avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="46acc-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="46acc-161">En guise d’alternative à l’utilisation de la commande de menu **Pack**, NuGet 4.x+ et MSBuild 15.1+ prennent en charge une cible `pack` quand le projet contient les données de package nécessaires.</span><span class="sxs-lookup"><span data-stu-id="46acc-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="46acc-162">Ouvrez une invite de commandes, accédez au dossier de votre projet et exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="46acc-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="46acc-163">(Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu Démarrer, car elle est configurée avec tous les chemins nécessaires pour MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="46acc-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="46acc-164">Pour plus d’informations, consultez [Créer un package avec MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="46acc-165">Publier le package</span><span class="sxs-lookup"><span data-stu-id="46acc-165">Publish the package</span></span>

<span data-ttu-id="46acc-166">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de l’interface CLI `nuget.exe` ou `dotnet.exe`, avec une clé API acquise sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="46acc-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="46acc-167">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="46acc-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="46acc-168">Publier avec l’interface CLI dotnet ou nuget.exe</span><span class="sxs-lookup"><span data-stu-id="46acc-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="46acc-169">Sélectionnez l'onglet de votre outil CLI, soit **.NET Core CLI** (CLI dotnet) ou **NuGet** (CLI nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="46acc-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="46acc-170">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="46acc-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="46acc-171">Cette étape est l’alternative recommandée à l’utilisation de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="46acc-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="46acc-172">Avant de pouvoir publier le package, vous devez d’abord ouvrir une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="46acc-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="46acc-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="46acc-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="46acc-174">Cette étape aboutit au même résultat que `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="46acc-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="46acc-175">Ouvrez une ligne de commande et accédez au dossier contenant le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="46acc-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="46acc-176">Exécutez la commande suivante, en spécifiant le nom de votre package (ID de package unique) et en remplaçant la valeur de la clé par celle de votre clé API :</span><span class="sxs-lookup"><span data-stu-id="46acc-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="46acc-177">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="46acc-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="46acc-178">Voir [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="46acc-179">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="46acc-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="46acc-180">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="46acc-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="46acc-181">Ajout d’un fichier Lisez-moi et d’autres fichiers</span><span class="sxs-lookup"><span data-stu-id="46acc-181">Adding a readme and other files</span></span>

<span data-ttu-id="46acc-182">Pour spécifier directement les fichiers à inclure dans le package, modifiez le fichier projet et utilisez la propriété `content` :</span><span class="sxs-lookup"><span data-stu-id="46acc-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="46acc-183">Cela inclut un fichier nommé `readme.txt` dans la racine du package.</span><span class="sxs-lookup"><span data-stu-id="46acc-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="46acc-184">Visual Studio affiche le contenu de ce fichier sous forme de texte brut immédiatement après avoir installé le package directement.</span><span class="sxs-lookup"><span data-stu-id="46acc-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="46acc-185">(Les fichiers Lisez-moi ne s’affichent pas pour les packages installés en tant que dépendances).</span><span class="sxs-lookup"><span data-stu-id="46acc-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="46acc-186">Par exemple, voici comment s’affiche le fichier Lisez-moi du package HtmlAgilityPack :</span><span class="sxs-lookup"><span data-stu-id="46acc-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Affichage d’un fichier Lisez-moi pour un package NuGet lors de l’installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="46acc-188">Le simple ajout du fichier readme.txt à la racine du projet ne permet pas de l’ajouter dans le package résultant.</span><span class="sxs-lookup"><span data-stu-id="46acc-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="46acc-189">Vidéo connexe</span><span class="sxs-lookup"><span data-stu-id="46acc-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="46acc-190">Recherchez d’autres vidéos NuGet sur [Channel 9](https://channel9.msdn.com/Series/NuGet-101) et [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="46acc-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="46acc-191">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="46acc-191">Related topics</span></span>

- [<span data-ttu-id="46acc-192">Créer un package</span><span class="sxs-lookup"><span data-stu-id="46acc-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="46acc-193">Publier un package</span><span class="sxs-lookup"><span data-stu-id="46acc-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="46acc-194">Packages de préversion</span><span class="sxs-lookup"><span data-stu-id="46acc-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="46acc-195">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="46acc-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="46acc-196">Gestion de version des packages</span><span class="sxs-lookup"><span data-stu-id="46acc-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="46acc-197">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="46acc-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="46acc-198">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="46acc-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="46acc-199">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="46acc-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
