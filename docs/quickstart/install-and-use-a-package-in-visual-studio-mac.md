---
title: Installer et utiliser un package NuGet dans Visual Studio pour Mac
description: Didacticiel de procédure pas à pas sur le processus d’installation et d’utilisation d’un package NuGet dans un projet de Visual Studio pour Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238475"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="bccc4-103">Démarrage rapide : Installer et utiliser un package dans Visual Studio pour Mac</span><span class="sxs-lookup"><span data-stu-id="bccc4-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="bccc4-104">Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="bccc4-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="bccc4-105">Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="bccc4-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="bccc4-106">Les packages sont installés dans un projet Visual Studio pour Mac à l’aide du gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="bccc4-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="bccc4-107">Cet article présente le processus qui utilise le package [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) populaire et un projet de console .net core.</span><span class="sxs-lookup"><span data-stu-id="bccc4-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="bccc4-108">Le même processus s’applique à tout autre projet Xamarin ou .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bccc4-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="bccc4-109">Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="bccc4-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="bccc4-110">Une fois la référence effectuée, vous pouvez appeler le package par le biais de son API.</span><span class="sxs-lookup"><span data-stu-id="bccc4-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="bccc4-111">**Prise en main de nuget.org** : Les développeurs .NET parcourent *nutget.org* à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="bccc4-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="bccc4-112">Vous pouvez effectuer des recherches directement dans *nuget.org*, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.</span><span class="sxs-lookup"><span data-stu-id="bccc4-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="bccc4-113">Pour obtenir des informations générales, consultez [Rechercher et évaluer des packages NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bccc4-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bccc4-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="bccc4-114">Prerequisites</span></span>

- <span data-ttu-id="bccc4-115">Visual Studio 2019 pour Mac.</span><span class="sxs-lookup"><span data-stu-id="bccc4-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="bccc4-116">Vous pouvez installer l’édition Community 2019 gratuitement à partir de [visualstudio.com](https://www.visualstudio.com/), ou utiliser l’édition Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bccc4-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="bccc4-117">Si vous utilisez Visual Studio sur Windows, consultez [installer et utiliser un package dans Visual Studio (Windows uniquement)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="bccc4-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="bccc4-118">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="bccc4-118">Create a project</span></span>

<span data-ttu-id="bccc4-119">Les packages NuGet peuvent être installés dans n’importe quel projet .NET, à condition qu’ils prennent en charge la même version cible de .NET Framework que le projet.</span><span class="sxs-lookup"><span data-stu-id="bccc4-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="bccc4-120">Pour cette procédure pas à pas, utilisez une application console .NET Core simple.</span><span class="sxs-lookup"><span data-stu-id="bccc4-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="bccc4-121">Créez un projet dans Visual Studio pour Mac utilisant **fichier > nouvelle solution...** , sélectionnez le modèle **application console du > .net Core >** .</span><span class="sxs-lookup"><span data-stu-id="bccc4-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="bccc4-122">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bccc4-122">Click **Next**.</span></span> <span data-ttu-id="bccc4-123">Lorsque vous y êtes invité, acceptez les valeurs par défaut de la version **cible du .NET Framework** .</span><span class="sxs-lookup"><span data-stu-id="bccc4-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="bccc4-124">Visual Studio crée le projet qui s’ouvre dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="bccc4-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="bccc4-125">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="bccc4-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="bccc4-126">Pour installer le package, vous utilisez le gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="bccc4-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="bccc4-127">Quand vous installez un package, NuGet enregistre la dépendance dans votre fichier projet ou dans un `packages.config` fichier (en fonction du format du projet).</span><span class="sxs-lookup"><span data-stu-id="bccc4-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="bccc4-128">Pour plus d’informations, consultez [Vue d’ensemble et flux de consommation des packages](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="bccc4-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="bccc4-129">Gestionnaire de package NuGet</span><span class="sxs-lookup"><span data-stu-id="bccc4-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="bccc4-130">Dans Explorateur de solutions, cliquez avec le bouton droit sur **dépendances** , puis choisissez **Ajouter des packages...** .</span><span class="sxs-lookup"><span data-stu-id="bccc4-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Commande Gérer les packages NuGet pour les références de projet](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="bccc4-132">Choisissez « nuget.org » comme **source du package** dans le coin supérieur gauche de la boîte de dialogue et recherchez **Newtonsoft. JSON**, sélectionnez ce package dans la liste, puis sélectionnez **Ajouter des packages...** :</span><span class="sxs-lookup"><span data-stu-id="bccc4-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Recherche du package Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="bccc4-134">Si vous souhaitez plus d’informations sur le gestionnaire de package NuGet, consultez [installer et gérer des packages à l’aide de Visual Studio pour Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="bccc4-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="bccc4-135">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="bccc4-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="bccc4-136">Le package Newtonsoft.Json étant dans le projet, vous pouvez appeler sa méthode `JsonConvert.SerializeObject` pour convertir un objet en chaîne explicite.</span><span class="sxs-lookup"><span data-stu-id="bccc4-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="bccc4-137">Ouvrez le `Program.cs` fichier (situé dans le panneau solutions) et remplacez le contenu du fichier par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="bccc4-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="bccc4-138">Générez et exécutez l’application en sélectionnant **exécuter > démarrer le débogage**:</span><span class="sxs-lookup"><span data-stu-id="bccc4-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="bccc4-139">Une fois l’application exécutée, la sortie JSON sérialisée s’affiche dans la console :</span><span class="sxs-lookup"><span data-stu-id="bccc4-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Sortie de l’application console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="bccc4-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bccc4-141">Next steps</span></span>
<span data-ttu-id="bccc4-142">Félicitations pour l’installation et l’utilisation de votre premier package NuGet !</span><span class="sxs-lookup"><span data-stu-id="bccc4-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bccc4-143">Installer et gérer des packages à l’aide de Visual Studio pour Mac</span><span class="sxs-lookup"><span data-stu-id="bccc4-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="bccc4-144">Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bccc4-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="bccc4-145">Vue d’ensemble et flux de travail de consommation de package</span><span class="sxs-lookup"><span data-stu-id="bccc4-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="bccc4-146">Références de package dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="bccc4-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
