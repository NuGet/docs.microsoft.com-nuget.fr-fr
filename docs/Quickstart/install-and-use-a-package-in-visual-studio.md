---
title: "Guide d’introduction à l’utilisation des packages NuGet dans Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet Visual Studio."
keywords: "installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet, utilisation de packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0030877803ac7403f26e27ac3c5a0303d69c489
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="5a2af-104">Installer et utiliser un package dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a2af-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="5a2af-105">Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="5a2af-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="5a2af-106">Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="5a2af-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="5a2af-107">Les packages sont installés dans un projet Visual Studio à l’aide de l’interface utilisateur du Gestionnaire de package ou de la Console du Gestionnaire de package, comme décrit dans cet article pour le package courant [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) et un projet de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="5a2af-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="5a2af-108">Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="5a2af-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="5a2af-109">Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.</span><span class="sxs-lookup"><span data-stu-id="5a2af-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="5a2af-110">**Commencez par nuget.org** : les développeurs .NET parcourent nutget.org à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="5a2af-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="5a2af-111">Vous pouvez effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.</span><span class="sxs-lookup"><span data-stu-id="5a2af-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="5a2af-112">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="5a2af-112">Pre-requisites</span></span>

- <span data-ttu-id="5a2af-113">Visual Studio 2017 avec la charge de travail Développement pour la plateforme Windows universelle ou</span><span class="sxs-lookup"><span data-stu-id="5a2af-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="5a2af-114">Visual Studio 2015 Update 3 avec les Outils pour les applications Windows universelles.</span><span class="sxs-lookup"><span data-stu-id="5a2af-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="5a2af-115">Vous pouvez installer l’édition Community 2017 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5a2af-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="5a2af-116">Créer un projet</span><span class="sxs-lookup"><span data-stu-id="5a2af-116">Create a project</span></span>

<span data-ttu-id="5a2af-117">Les packages NuGet peuvent être installés dans tout type de projet .NET.</span><span class="sxs-lookup"><span data-stu-id="5a2af-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="5a2af-118">Pour cette procédure pas à pas, vous utilisez une application Windows universelle (UWP) simple.</span><span class="sxs-lookup"><span data-stu-id="5a2af-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="5a2af-119">Créez un projet dans Visual Studio en sélectionnant le menu **Fichier > Nouveau projet...** puis **Windows universel > Application vide (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="5a2af-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="5a2af-120">À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.</span><span class="sxs-lookup"><span data-stu-id="5a2af-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="5a2af-121">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="5a2af-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="5a2af-122">Pour installer le package, vous pouvez utiliser l’interface utilisateur du Gestionnaire de package ou sur la console du Gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="5a2af-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="5a2af-123">Interface utilisateur du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="5a2af-123">Package Manager UI</span></span>

1. <span data-ttu-id="5a2af-124">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** et choisissez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5a2af-124">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="5a2af-126">Choisissez « nuget.org » comme **Source du package**, sélectionnez l’onglet **Parcourir**, recherchez **Newtonsoft.Json**, sélectionnez-le dans la liste, puis sélectionnez **Installer** :</span><span class="sxs-lookup"><span data-stu-id="5a2af-126">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Recherche du package Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="5a2af-128">Acceptez toutes les invites de licence.</span><span class="sxs-lookup"><span data-stu-id="5a2af-128">Accept any license prompts.</span></span>

1. <span data-ttu-id="5a2af-129">(Visual Studio 2017) Si vous êtes invité à sélectionner un format de gestion de package, sélectionnez **PackageReference dans le fichier projet** :</span><span class="sxs-lookup"><span data-stu-id="5a2af-129">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Sélection d’un format de référence de package](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="5a2af-131">Si vous êtes invité à vérifier les modifications, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a2af-131">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="5a2af-132">Console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="5a2af-132">Package Manager Console</span></span>

1. <span data-ttu-id="5a2af-133">Sélectionnez la commande de menu **Outils -> Gestionnaire de package NuGet -> Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="5a2af-133">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="5a2af-134">Une fois la console ouverte, vérifiez que la liste déroulante **Projet par défaut** affiche le projet dans lequel vous souhaitez installer le package.</span><span class="sxs-lookup"><span data-stu-id="5a2af-134">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="5a2af-135">Si la solution ne contient qu’un seul projet, il est déjà sélectionné.</span><span class="sxs-lookup"><span data-stu-id="5a2af-135">If you have a single project in the solution, it is already selected.</span></span>

    ![Recherche du package Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="5a2af-137">Entrez la commande `Install-Package Newtonsoft.json` (consultez [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="5a2af-137">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="5a2af-138">La fenêtre de la console affiche la sortie de la commande.</span><span class="sxs-lookup"><span data-stu-id="5a2af-138">The console window shows output for the command.</span></span> <span data-ttu-id="5a2af-139">Les erreurs indiquent généralement que le package n’est pas compatible avec le framework cible du projet.</span><span class="sxs-lookup"><span data-stu-id="5a2af-139">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="5a2af-140">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="5a2af-140">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="5a2af-141">Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.</span><span class="sxs-lookup"><span data-stu-id="5a2af-141">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="5a2af-142">Ouvrez `MainPage.xaml` et remplacez l’élément `Grid` existant par l’élément suivant :</span><span class="sxs-lookup"><span data-stu-id="5a2af-142">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="5a2af-143">Ouvrez le fichier `MainPage.xaml.cs` (situé sous le nœud `MainPage.xaml` dans l’Explorateur de solutions), puis insérez le code suivant dans le constructeur `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="5a2af-143">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="5a2af-144">Bien que vous ayez ajouté le package Newtonsoft.Json au projet, des tildes rouges s’affichent sous `JsonConvert`, car vous avez besoin d’une instruction `using` en haut du fichier de code :</span><span class="sxs-lookup"><span data-stu-id="5a2af-144">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="5a2af-145">Générez et exécutez l’application en appuyant sur F5 ou en sélectionnant **Déboguer > Démarrer le débogage** :</span><span class="sxs-lookup"><span data-stu-id="5a2af-145">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Sortie initiale de l’application UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="5a2af-147">Cliquez sur le bouton pour remplacer le contenu du TextBlock par du texte JSON :</span><span class="sxs-lookup"><span data-stu-id="5a2af-147">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Sortie de l’application UWP après un clic sur le bouton](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="5a2af-149">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="5a2af-149">Related articles</span></span>

- [<span data-ttu-id="5a2af-150">Vue d’ensemble et flux de travail de consommation de package</span><span class="sxs-lookup"><span data-stu-id="5a2af-150">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="5a2af-151">Recherche et sélection des packages</span><span class="sxs-lookup"><span data-stu-id="5a2af-151">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="5a2af-152">Méthodes d’installation d’un package</span><span class="sxs-lookup"><span data-stu-id="5a2af-152">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="5a2af-153">Configuration du comportement de NuGet</span><span class="sxs-lookup"><span data-stu-id="5a2af-153">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
