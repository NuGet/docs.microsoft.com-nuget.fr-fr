---
title: Créer et publier un package .NET Standard NuGet avec Visual Studio sur Windows
description: Ce tutoriel explique pas à pas comment créer et publier un package NuGet .NET Standard avec Visual Studio sous Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 0fc3b15c6d5ffa93eb6e26660f71cea2286ba77d
ms.sourcegitcommit: aed04cc04b0902403612de6736a900d41c265afd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68821423"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="53155-103">Démarrage rapide : Créer et publier un package NuGet avec Visual Studio (.NET Standard, Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="53155-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="53155-104">La création d’un package NuGet à partir d’une bibliothèque de classes .NET Standard dans Visual Studio sous Windows est un processus simple, de même que sa publication sur nuget.org avec un outil de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="53155-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="53155-105">Si vous utilisez Visual Studio pour Mac, consultez [ces informations](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sur la création d’un package NuGet ou utilisez les [outils CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="53155-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53155-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="53155-106">Prerequisites</span></span>

1. <span data-ttu-id="53155-107">Installez une édition de Visual Studio 2017 ou version supérieure à l’adresse [visualstudio.com](https://www.visualstudio.com/) avec une charge de travail liée à .NET Core.</span><span class="sxs-lookup"><span data-stu-id="53155-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="53155-108">Si ce n'est déjà fait, installez l’interface CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="53155-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="53155-109">Pour la CLI `dotnet`, à compter de Visual Studio 2017, la CLI `dotnet` est installée automatiquement avec les charges de travail associées à NET Core.</span><span class="sxs-lookup"><span data-stu-id="53155-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="53155-110">Dans le cas contraire, installez le [SDK .NET Core](https://www.microsoft.com/net/download/) pour obtenir la CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="53155-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="53155-111">La CLI `dotnet` dotnet est requise pour les projets .NET Standard qui utilisent le [format de style SDK](../resources/check-project-format.md) (attribut SDK).</span><span class="sxs-lookup"><span data-stu-id="53155-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="53155-112">Le modèle de bibliothèque de classes par défaut dans Visual Studio 2017 et les versions ultérieures, qui est utilisé dans cet article, utilise l’attribut SDK.</span><span class="sxs-lookup"><span data-stu-id="53155-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="53155-113">Pour cet article, la CLI `dotnet` est recommandée.</span><span class="sxs-lookup"><span data-stu-id="53155-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="53155-114">Bien que vous puissiez publier un package NuGet à l’aide de la CLI `nuget.exe`, certaines des étapes décrites dans cet article sont spécifiques aux projets de type SDK et à la CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="53155-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="53155-115">La cLI nuget.exe est utilisée pour les [projets qui ne sont pas de type SDK](../resources/check-project-format.md) (généralement .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="53155-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="53155-116">Si vous utilisez un projet qui n’est pas de type SDK, suivez les procédures décrites dans [Créer et publier un package .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pour créer et publier le package.</span><span class="sxs-lookup"><span data-stu-id="53155-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="53155-117">[Créez un compte gratuit sur nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="53155-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="53155-118">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="53155-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="53155-119">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="53155-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="53155-120">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="53155-120">Create a class library project</span></span>

<span data-ttu-id="53155-121">Vous pouvez utiliser un projet de bibliothèque de classes .NET Standard existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="53155-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="53155-122">Dans Visual Studio, choisissez **Fichier > Nouveau > Projet**, développez le nœud **Visual C# > .NET Standard**, sélectionnez le modèle « Bibliothèque de classes (.NET Standard) », nommez le projet AppLogger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="53155-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="53155-123">Cliquez avec le bouton droit sur le fichier projet résultant et sélectionnez **Générer** pour être sûr que le projet a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="53155-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="53155-124">La DLL se trouve dans le dossier Debug (ou Release si vous générez cette configuration).</span><span class="sxs-lookup"><span data-stu-id="53155-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="53155-125">Dans un package NuGet réel, vous implémenterez bien sûr de nombreuses fonctionnalités utiles, grâce auxquelles d’autres personnes pourront créer des applications.</span><span class="sxs-lookup"><span data-stu-id="53155-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="53155-126">Pour cette procédure pas à pas, toutefois, vous n’écrirez pas de code supplémentaire, car une bibliothèque de classes à partir du modèle suffit pour créer un package.</span><span class="sxs-lookup"><span data-stu-id="53155-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="53155-127">Néanmoins, si vous souhaitez obtenir du code fonctionnel pour le package, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="53155-127">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="53155-128">Sauf cas particulier, .NET Standard est la cible privilégiée pour les packages NuGet, car c’est celle qui assure la compatibilité avec le plus grand nombre de projets.</span><span class="sxs-lookup"><span data-stu-id="53155-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="53155-129">Configurer les propriétés de package</span><span class="sxs-lookup"><span data-stu-id="53155-129">Configure package properties</span></span>

1. <span data-ttu-id="53155-130">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et choisissez la commande de menu **Propriétés**, puis sélectionnez l’onglet **Package**.</span><span class="sxs-lookup"><span data-stu-id="53155-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="53155-131">L’onglet **Package** s’affiche uniquement pour les projets de type SDK dans Visual Studio, généralement les projets de bibliothèque de classes .NET Standard ou .NET Core. Si vous ciblez un projet qui n’est pas de style SDK (généralement .NET Framework), [migrez le projet](../reference/migrate-packages-config-to-package-reference.md) et utilisez la CLI `dotnet` ou consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) ou [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) à la place des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="53155-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Propriétés de package NuGet dans un projet Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="53155-133">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **Tags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="53155-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="53155-134">Donnez à votre package un identificateur unique et remplissez les propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="53155-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="53155-135">Vous trouverez une description des différentes propriétés dans la section [Informations de référence sur le fichier .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="53155-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="53155-136">Toutes ces propriétés sont ajoutées au manifeste `.nuspec` créé par Visual Studio pour le projet.</span><span class="sxs-lookup"><span data-stu-id="53155-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="53155-137">Vous devez donner au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="53155-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="53155-138">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="53155-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="53155-139">Si vous tentez de publier un package avec un nom qui existe déjà, une erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="53155-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="53155-140">Facultatif : pour afficher les propriétés directement dans le fichier projet, cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions et sélectionnez **Modifier AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="53155-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="53155-141">Cette option n’est disponible qu’à partir de Visual Studio 2017 pour les projets qui utilisent l’attribut de style SDK.</span><span class="sxs-lookup"><span data-stu-id="53155-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="53155-142">Sinon, cliquez avec le bouton droit sur le projet et choisissez **Décharger le projet**.</span><span class="sxs-lookup"><span data-stu-id="53155-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="53155-143">Cliquez ensuite avec le bouton droit sur le projet déchargé, puis choisissez **Modifier AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="53155-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="53155-144">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="53155-144">Run the pack command</span></span>

1. <span data-ttu-id="53155-145">Définissez la configuration en **Release**.</span><span class="sxs-lookup"><span data-stu-id="53155-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="53155-146">Cliquez avec le bouton droit sur le projet dans **l’Explorateur de solutions**, puis sélectionnez la commande **Empaqueter** :</span><span class="sxs-lookup"><span data-stu-id="53155-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Commande pack de NuGet dans le menu contextuel du projet Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="53155-148">Si vous ne voyez pas la commande **Pack**, cela signifie que votre projet n’est probablement pas un projet de type SDK et que vous devez utiliser la CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="53155-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="53155-149">[Migrez le projet](../reference/migrate-packages-config-to-package-reference.md) et utilisez la CLI `dotnet`, ou consultez [Créer et publier un package .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) à la place pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="53155-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="53155-150">Visual Studio génère le projet et crée le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="53155-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="53155-151">Lisez les informations qui apparaissent sur la fenêtre **Sortie** (comme dans la capture d’écran suivante), notamment le chemin d’accès du fichier de package.</span><span class="sxs-lookup"><span data-stu-id="53155-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="53155-152">Notez également que l’assembly généré est dans `bin\Release\netstandard2.0` comme il convient à la cible .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="53155-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="53155-153">(Facultatif) Générer le package à la création</span><span class="sxs-lookup"><span data-stu-id="53155-153">(Optional) Generate package on build</span></span>

<span data-ttu-id="53155-154">Vous pouvez configurer Visual Studio pour générer automatiquement le package NuGet lorsque vous générez le projet.</span><span class="sxs-lookup"><span data-stu-id="53155-154">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="53155-155">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet et choisissez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="53155-155">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="53155-156">Dans l’onglet **Package**, sélectionnez **Générer le package NuGet à la création**.</span><span class="sxs-lookup"><span data-stu-id="53155-156">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Générer automatiquement le package à la création](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="53155-158">Lorsque vous créez automatiquement le package, le délai d’attente augmente la durée de création de votre projet.</span><span class="sxs-lookup"><span data-stu-id="53155-158">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="53155-159">(Facultatif) Compresser avec MSBuild</span><span class="sxs-lookup"><span data-stu-id="53155-159">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="53155-160">En guise d’alternative à l’utilisation de la commande de menu **Pack**, NuGet 4.x+ et MSBuild 15.1+ prennent en charge une cible `pack` quand le projet contient les données de package nécessaires.</span><span class="sxs-lookup"><span data-stu-id="53155-160">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="53155-161">Ouvrez une invite de commandes, accédez au dossier de votre projet et exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="53155-161">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="53155-162">(Il est généralement recommandé de démarrer l’invite de commandes développeur pour Visual Studio à partir du menu Démarrer, car elle est configurée avec tous les chemins nécessaires pour MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="53155-162">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="53155-163">Pour plus d’informations, consultez [Créer un package avec MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="53155-163">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="53155-164">Publier le package</span><span class="sxs-lookup"><span data-stu-id="53155-164">Publish the package</span></span>

<span data-ttu-id="53155-165">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de l’interface CLI `nuget.exe` ou `dotnet.exe`, avec une clé API acquise sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="53155-165">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="53155-166">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="53155-166">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="53155-167">Publier avec dotnet nuget push (CLI dotnet)</span><span class="sxs-lookup"><span data-stu-id="53155-167">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="53155-168">Cette étape est l’alternative recommandée à l’utilisation de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="53155-168">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="53155-169">Avant de pouvoir publier le package, vous devez d’abord ouvrir une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="53155-169">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="53155-170">Publier avec nuget push (CLI nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="53155-170">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="53155-171">Cette étape aboutit au même résultat que `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="53155-171">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="53155-172">Ouvrez une ligne de commande et accédez au dossier contenant le fichier `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="53155-172">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="53155-173">Exécutez la commande suivante, en spécifiant le nom de votre package (ID de package unique) et en remplaçant la valeur de la clé par celle de votre clé API :</span><span class="sxs-lookup"><span data-stu-id="53155-173">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="53155-174">nuget.exe affiche les résultats du processus de publication :</span><span class="sxs-lookup"><span data-stu-id="53155-174">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="53155-175">Voir [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="53155-175">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="53155-176">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="53155-176">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="53155-177">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="53155-177">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="53155-178">Ajout d’un fichier Lisez-moi et d’autres fichiers</span><span class="sxs-lookup"><span data-stu-id="53155-178">Adding a readme and other files</span></span>

<span data-ttu-id="53155-179">Pour spécifier directement les fichiers à inclure dans le package, modifiez le fichier projet et utilisez la propriété `content` :</span><span class="sxs-lookup"><span data-stu-id="53155-179">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="53155-180">Cela inclut un fichier nommé `readme.txt` dans la racine du package.</span><span class="sxs-lookup"><span data-stu-id="53155-180">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="53155-181">Visual Studio affiche le contenu de ce fichier sous forme de texte brut immédiatement après avoir installé le package directement.</span><span class="sxs-lookup"><span data-stu-id="53155-181">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="53155-182">(Les fichiers Lisez-moi ne s’affichent pas pour les packages installés en tant que dépendances).</span><span class="sxs-lookup"><span data-stu-id="53155-182">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="53155-183">Par exemple, voici comment s’affiche le fichier Lisez-moi du package HtmlAgilityPack :</span><span class="sxs-lookup"><span data-stu-id="53155-183">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Affichage d’un fichier Lisez-moi pour un package NuGet lors de l’installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="53155-185">Le simple ajout du fichier readme.txt à la racine du projet ne permet pas de l’ajouter dans le package résultant.</span><span class="sxs-lookup"><span data-stu-id="53155-185">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="53155-186">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="53155-186">Related topics</span></span>

- [<span data-ttu-id="53155-187">Créer un package</span><span class="sxs-lookup"><span data-stu-id="53155-187">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="53155-188">Publier un package</span><span class="sxs-lookup"><span data-stu-id="53155-188">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="53155-189">Packages de préversion</span><span class="sxs-lookup"><span data-stu-id="53155-189">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="53155-190">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="53155-190">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="53155-191">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="53155-191">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="53155-192">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="53155-192">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="53155-193">Documentation de la bibliothèque .NET Standard</span><span class="sxs-lookup"><span data-stu-id="53155-193">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="53155-194">Portage vers .NET Core à partir du .NET Framework</span><span class="sxs-lookup"><span data-stu-id="53155-194">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
