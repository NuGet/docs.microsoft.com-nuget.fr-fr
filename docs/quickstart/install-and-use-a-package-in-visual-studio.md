---
title: Installer et utiliser un package NuGet dans Visual Studio
description: Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775525"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="212f4-103">Démarrage rapide : installer et utiliser un package dans Visual Studio (Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="212f4-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="212f4-104">Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="212f4-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="212f4-105">Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="212f4-106">Les packages sont installés dans un projet Visual Studio à l’aide du gestionnaire de package NuGet, de la [console du gestionnaire de package](../consume-packages/install-use-packages-powershell.md)ou de l' [interface CLI dotnet](install-and-use-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell.md), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="212f4-107">Cet article explique le processus avec le package [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) bien connu et un projet Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="212f4-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="212f4-108">Le même processus s’applique à n’importe quel autre projet .NET ou .NET Core.</span><span class="sxs-lookup"><span data-stu-id="212f4-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="212f4-109">Une fois l’installation terminée, reportez-vous au package dans le code `using <namespace>` où \<namespace\> est spécifique au package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="212f4-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="212f4-110">Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.</span><span class="sxs-lookup"><span data-stu-id="212f4-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="212f4-111">**Commencez avec NuGet.org**: la navigation *NuGet.org* est la manière dont les développeurs .net recherchent généralement les composants qu’ils peuvent réutiliser dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="212f4-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="212f4-112">Vous pouvez effectuer une recherche directement dans *NuGet.org* , ou Rechercher et installer des packages dans Visual Studio, comme indiqué dans cet article.</span><span class="sxs-lookup"><span data-stu-id="212f4-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="212f4-113">Pour obtenir des informations générales, consultez [Rechercher et évaluer des packages NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="212f4-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="212f4-114">Prerequisites</span></span>

- <span data-ttu-id="212f4-115">Visual Studio 2019 avec la charge de travail Développement .NET Desktop.</span><span class="sxs-lookup"><span data-stu-id="212f4-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="212f4-116">Vous pouvez installer l’édition Community 2019 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="212f4-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="212f4-117">Si vous utilisez Visual Studio pour Mac, consultez [installer et utiliser un package dans Visual Studio pour Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="212f4-118">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="212f4-118">Create a project</span></span>

<span data-ttu-id="212f4-119">Les packages NuGet peuvent être installés dans n’importe quel projet .NET, à condition qu’ils prennent en charge la même version cible de .NET Framework que le projet.</span><span class="sxs-lookup"><span data-stu-id="212f4-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="212f4-120">Pour cette procédure pas à pas, utilisez une application WPF simple.</span><span class="sxs-lookup"><span data-stu-id="212f4-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="212f4-121">Créez un projet dans Visual Studio à l’aide de **fichier**  >  **nouveau projet**, en tapant **.net** dans la zone de recherche, puis en sélectionnant l' **application WPF (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="212f4-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="212f4-122">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="212f4-122">Click **Next**.</span></span> <span data-ttu-id="212f4-123">Acceptez les valeurs par défaut pour **Framework** quand vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="212f4-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="212f4-124">Visual Studio crée le projet qui s’ouvre dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="212f4-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="212f4-125">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="212f4-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="212f4-126">Pour installer le package, vous pouvez utiliser l’interface utilisateur du gestionnaire de package NuGet ou la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="212f4-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="212f4-127">Quand vous installez un package, NuGet enregistre la dépendance dans votre fichier projet ou dans un fichier `packages.config` (en fonction du format du projet).</span><span class="sxs-lookup"><span data-stu-id="212f4-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="212f4-128">Pour plus d’informations, consultez [Vue d’ensemble et flux de consommation des packages](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="212f4-129">Gestionnaire de package NuGet</span><span class="sxs-lookup"><span data-stu-id="212f4-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="212f4-130">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** et choisissez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="212f4-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="212f4-132">Choisissez « nuget.org » comme **Source du package**, sélectionnez l’onglet **Parcourir**, recherchez **Newtonsoft.Json**, sélectionnez-le dans la liste, puis sélectionnez **Installer** :</span><span class="sxs-lookup"><span data-stu-id="212f4-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Recherche du package Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="212f4-134">Si vous souhaitez plus d’informations sur le gestionnaire de package NuGet, consultez [Installer et gérer des packages avec Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="212f4-135">Acceptez toutes les invites de licence.</span><span class="sxs-lookup"><span data-stu-id="212f4-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="212f4-136">(Visual Studio 2017 uniquement) Si vous êtes invité à sélectionner un format de gestion de package, sélectionnez **PackageReference dans le fichier projet** :</span><span class="sxs-lookup"><span data-stu-id="212f4-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Sélectionner un format de gestion des packages](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="212f4-138">Si vous êtes invité à vérifier les modifications, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="212f4-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="212f4-139">Console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="212f4-139">Package Manager Console</span></span>

1. <span data-ttu-id="212f4-140">Sélectionnez la   >  commande de menu de la console Gestionnaire de **package NuGet** outils gestionnaire de package NuGet  >   .</span><span class="sxs-lookup"><span data-stu-id="212f4-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="212f4-141">Une fois la console ouverte, vérifiez que la liste déroulante **Projet par défaut** affiche le projet dans lequel vous souhaitez installer le package.</span><span class="sxs-lookup"><span data-stu-id="212f4-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="212f4-142">Si la solution ne contient qu’un seul projet, il est déjà sélectionné.</span><span class="sxs-lookup"><span data-stu-id="212f4-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Sélectionner un projet pour le package](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="212f4-144">Entrez la commande `Install-Package Newtonsoft.Json` (consultez [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="212f4-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="212f4-145">La fenêtre de la console affiche la sortie de la commande.</span><span class="sxs-lookup"><span data-stu-id="212f4-145">The console window shows output for the command.</span></span> <span data-ttu-id="212f4-146">Les erreurs indiquent généralement que le package n’est pas compatible avec le framework cible du projet.</span><span class="sxs-lookup"><span data-stu-id="212f4-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="212f4-147">Si vous souhaitez plus d’informations sur la console du gestionnaire de package, consultez [Installer et gérer des packages avec la console du gestionnaire de package](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="212f4-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="212f4-148">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="212f4-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="212f4-149">Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.</span><span class="sxs-lookup"><span data-stu-id="212f4-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="212f4-150">Ouvrez `MainWindow.xaml` et remplacez l’élément `Grid` existant par l’élément suivant :</span><span class="sxs-lookup"><span data-stu-id="212f4-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="212f4-151">Ouvrez le fichier `MainWindow.xaml.cs` (situé sous le nœud `MainWindow.xaml` dans l’Explorateur de solutions), puis insérez le code suivant dans la classe `MainWindow` :</span><span class="sxs-lookup"><span data-stu-id="212f4-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="212f4-152">Bien que vous ayez ajouté le package Newtonsoft.Json au projet, des tildes rouges s’affichent sous `JsonConvert`, car vous avez besoin d’une instruction `using` en haut du fichier de code :</span><span class="sxs-lookup"><span data-stu-id="212f4-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="212f4-153">Générez et exécutez l’application en appuyant sur F5 ou en sélectionnant **Déboguer**  >  **Démarrer le débogage**:</span><span class="sxs-lookup"><span data-stu-id="212f4-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Sortie initiale de l’application WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="212f4-155">Cliquez sur le bouton pour remplacer le contenu du TextBlock par du texte JSON :</span><span class="sxs-lookup"><span data-stu-id="212f4-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Sortie de l’application WPF après un clic sur le bouton](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="212f4-157">Vidéo connexe</span><span class="sxs-lookup"><span data-stu-id="212f4-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="212f4-158">Recherchez d’autres vidéos NuGet sur [Channel 9](https://channel9.msdn.com/Series/NuGet-101) et [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="212f4-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="212f4-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="212f4-159">Next steps</span></span>

<span data-ttu-id="212f4-160">Félicitations pour l’installation et l’utilisation de votre premier package NuGet !</span><span class="sxs-lookup"><span data-stu-id="212f4-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="212f4-161">Installer et gérer des packages à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="212f4-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="212f4-162">Installer et gérer des packages à l’aide de la Console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="212f4-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="212f4-163">Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="212f4-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="212f4-164">Vue d’ensemble et flux de travail de consommation de package</span><span class="sxs-lookup"><span data-stu-id="212f4-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="212f4-165">Recherche et sélection de packages</span><span class="sxs-lookup"><span data-stu-id="212f4-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="212f4-166">Références de package dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="212f4-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
