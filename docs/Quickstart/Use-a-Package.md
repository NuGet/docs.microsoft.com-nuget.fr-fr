---
title: "Guide d’introduction à l’utilisation des packages NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet."
keywords: "installer NuGet, consommation de package NuGet, installation de packages NuGet, références de package NuGet, utilisation de packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="a5732-104">Installer et utiliser un package</span><span class="sxs-lookup"><span data-stu-id="a5732-104">Install and use a package</span></span>

<span data-ttu-id="a5732-105">Les packages NuGet sont des unités de code réutilisables que les autres développeurs mettent à votre disposition pour les utiliser dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="a5732-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="a5732-106">Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="a5732-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="a5732-107">Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="a5732-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="a5732-108">Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.</span><span class="sxs-lookup"><span data-stu-id="a5732-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="a5732-109">Le reste de cette rubrique vous guide tout au long du processus d’installation du package [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) dans un projet de plateforme Windows universelle (UWP, Universal Windows Platform) à l’aide de l’interface utilisateur du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="a5732-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="a5732-110">Il contient ensuite un exemple d’utilisation du package.</span><span class="sxs-lookup"><span data-stu-id="a5732-110">It then shows an example of using the package.</span></span> <span data-ttu-id="a5732-111">Vous utilisez un flux de travail similaire pour presque tous les packages NuGet que vous utilisez dans un projet.</span><span class="sxs-lookup"><span data-stu-id="a5732-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="a5732-112">Installer les prérequis</span><span class="sxs-lookup"><span data-stu-id="a5732-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="a5732-113">Créer un projet</span><span class="sxs-lookup"><span data-stu-id="a5732-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="a5732-114">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="a5732-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="a5732-115">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="a5732-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="a5732-116">**Commencez par nuget.org** : l’installation des packages à partir de nuget.org est un flux de travail courant grâce auquel les développeurs .NET peuvent rechercher des composants réutilisables dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="a5732-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="a5732-117">Vous pouvez toujours effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="a5732-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="a5732-118">Installer les prérequis</span><span class="sxs-lookup"><span data-stu-id="a5732-118">Install pre-requisites</span></span>

<span data-ttu-id="a5732-119">Ce didacticiel nécessite Visual Studio 2015 Update 3 avec les Outils pour les applications Windows universelles, ou Visual Studio 2017 avec la charge de travail de développement Plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="a5732-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="a5732-120">Si vous avez déjà installé Visual Studio, vous pouvez réexécuter le programme d’installation pour ajouter les outils UWP.</span><span class="sxs-lookup"><span data-stu-id="a5732-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="a5732-121">Vous pouvez installer l’édition Community gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a5732-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="a5732-122">Créer un projet</span><span class="sxs-lookup"><span data-stu-id="a5732-122">Create a project</span></span>

<span data-ttu-id="a5732-123">Pour installer un package NuGet, vous avez besoin d’un projet .NET dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5732-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="a5732-124">Pour cette procédure pas à pas, vous pouvez utiliser une application WPF (Windows Presentation Foundation) ou UWP simple :</span><span class="sxs-lookup"><span data-stu-id="a5732-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="a5732-125">Pour WPF (Windows 7+), choisissez **Fichier > Nouveau > Projet**, développez **Visual C#**, sélectionnez **Bureau classique Windows > Application WPF (.NET Framework)**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5732-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="a5732-126">Pour UWP (Windows 10), utilisez plutôt **Windows universel > Application vide (Application universelle)**.</span><span class="sxs-lookup"><span data-stu-id="a5732-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="a5732-127">À l’invite, acceptez les valeurs par défaut pour Version cible et Version minimale.</span><span class="sxs-lookup"><span data-stu-id="a5732-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="a5732-128">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="a5732-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="a5732-129">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** et choisissez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a5732-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="a5732-131">Choisissez « nuget.org » comme **Source du package**, sélectionnez l’onglet **Parcourir**, recherchez **Newtonsoft.Json**, sélectionnez-le dans la liste, puis sélectionnez **Installer** :</span><span class="sxs-lookup"><span data-stu-id="a5732-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Recherche du package Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="a5732-133">Si vous êtes invité à sélectionner un format de gestion de package, choisissez parmi PackageReference (recommandé) et `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="a5732-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Sélection d’un format de référence de package](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="a5732-135">Si vous êtes invité à vérifier les modifications, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5732-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="a5732-136">Cliquez avec le bouton droit sur la solution dans l’Explorateur de solutions, puis sélectionnez **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="a5732-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="a5732-137">Cette opération restaure tous les packages NuGet répertoriés sous **Références**.</span><span class="sxs-lookup"><span data-stu-id="a5732-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="a5732-138">Pour plus d’informations, consultez [Restauration des packages](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a5732-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="a5732-139">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="a5732-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="a5732-140">Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.</span><span class="sxs-lookup"><span data-stu-id="a5732-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="a5732-141">Ouvrez `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) et remplacez l’élément `Grid` existant par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a5732-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="a5732-142">Développez le nœud `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) dans l’Explorateur de solutions, ouvrez le fichier `.cs` et insérez le code suivant à l’intérieur de la classe `MainWindow` ou `MainPage`, après le constructeur :</span><span class="sxs-lookup"><span data-stu-id="a5732-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="a5732-143">Bien que vous ayez ajouté le package Newtonsoft.Json au projet, des tildes rouges s’affichent sous `JsonConvert`, car vous avez besoin d’une instruction `using`.</span><span class="sxs-lookup"><span data-stu-id="a5732-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="a5732-144">Placez le curseur sur le `JsonConvert` souligné pour faire apparaître l’ampoule et l’option **Afficher les corrections éventuelles** :</span><span class="sxs-lookup"><span data-stu-id="a5732-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Ampoule avec commande Afficher les corrections éventuelles](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="a5732-146">Cliquez sur **Afficher les corrections éventuelles** (ou l’ampoule) et sélectionnez la première correction suggérée, `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="a5732-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="a5732-147">Cela ajoute la ligne nécessaire en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="a5732-147">This adds the necessary line to the top of the file.</span></span>

    ![Ampoule permettant d’ajouter une instruction using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="a5732-149">Générez et exécutez l’application en appuyant sur F5 ou en sélectionnant **Déboguer > Démarrer le débogage** (UWP indiqué ici ; WPF est similaire) :</span><span class="sxs-lookup"><span data-stu-id="a5732-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Sortie initiale de l’application UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="a5732-151">Cliquez sur le bouton pour remplacer le contenu du TextBlock par du texte JSON :</span><span class="sxs-lookup"><span data-stu-id="a5732-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Sortie de l’application UWP après un clic sur le bouton](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="a5732-153">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="a5732-153">Related topics</span></span>

- [<span data-ttu-id="a5732-154">Vue d’ensemble et flux de travail de consommation de package</span><span class="sxs-lookup"><span data-stu-id="a5732-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="a5732-155">Recherche et sélection des packages</span><span class="sxs-lookup"><span data-stu-id="a5732-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="a5732-156">Configuration du comportement de NuGet</span><span class="sxs-lookup"><span data-stu-id="a5732-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
