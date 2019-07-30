---
title: Installer et utiliser un package NuGet à l’aide de l’interface CLI dotnet
description: Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: ee456fd49675db37fee78dc14502a897d84a2b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342460"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="b41ee-103">Démarrage rapide : Installer et utiliser un package à l’aide de l’interface CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="b41ee-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="b41ee-104">Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="b41ee-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="b41ee-105">Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="b41ee-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="b41ee-106">Les packages sont installés dans un projet .NET Core à l’aide de la commande `dotnet add package`, comme décrit dans cet article pour le package courant [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="b41ee-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="b41ee-107">Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="b41ee-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="b41ee-108">Vous pourrez alors utiliser l’API du package.</span><span class="sxs-lookup"><span data-stu-id="b41ee-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="b41ee-109">**Prise en main de nuget.org** : Les développeurs .NET parcourent nutget.org à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="b41ee-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="b41ee-110">Vous pouvez effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b41ee-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b41ee-111">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b41ee-111">Prerequisites</span></span>

- <span data-ttu-id="b41ee-112">Le [kit SDK .NET Core](https://www.microsoft.com/net/download/), qui fournit l’outil en ligne de commande `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="b41ee-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="b41ee-113">À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.</span><span class="sxs-lookup"><span data-stu-id="b41ee-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="b41ee-114">Créer un projet</span><span class="sxs-lookup"><span data-stu-id="b41ee-114">Create a project</span></span>

<span data-ttu-id="b41ee-115">Les packages NuGet peuvent être installés dans tout type de projet .NET.</span><span class="sxs-lookup"><span data-stu-id="b41ee-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="b41ee-116">Pour cette procédure pas à pas, créez un projet de console .NET Core simple comme suit :</span><span class="sxs-lookup"><span data-stu-id="b41ee-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="b41ee-117">Créez un dossier pour le projet.</span><span class="sxs-lookup"><span data-stu-id="b41ee-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="b41ee-118">Créez le projet à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b41ee-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="b41ee-119">Utilisez `dotnet run` pour vérifier que l’application a été créée correctement.</span><span class="sxs-lookup"><span data-stu-id="b41ee-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="b41ee-120">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b41ee-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="b41ee-121">Utilisez la commande suivante pour installer le package `Newtonsoft.json` :</span><span class="sxs-lookup"><span data-stu-id="b41ee-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="b41ee-122">Une fois la commande terminée, ouvrez le fichier `.csproj` pour voir la référence ajoutée :</span><span class="sxs-lookup"><span data-stu-id="b41ee-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="b41ee-123">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="b41ee-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="b41ee-124">Ouvrez le fichier `Program.cs` et ajoutez la ligne suivante en haut du fichier :</span><span class="sxs-lookup"><span data-stu-id="b41ee-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="b41ee-125">Ajoutez le code suivant avant la ligne `class Program` :</span><span class="sxs-lookup"><span data-stu-id="b41ee-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="b41ee-126">Remplacez la fonction `Main` par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b41ee-126">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="b41ee-127">Générez et exécutez l’application à l’aide de la commande `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="b41ee-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="b41ee-128">La sortie doit être la représentation JSON de l’objet `Account` dans le code :</span><span class="sxs-lookup"><span data-stu-id="b41ee-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="b41ee-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b41ee-129">Next steps</span></span>

<span data-ttu-id="b41ee-130">Félicitations pour l’installation et l’utilisation de votre premier package NuGet !</span><span class="sxs-lookup"><span data-stu-id="b41ee-130">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b41ee-131">Installer et utiliser des packages à l’aide de l’interface CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="b41ee-131">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="b41ee-132">Pour explorer plus en détail ce que NuGet a à offrir, sélectionnez les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b41ee-132">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="b41ee-133">Vue d’ensemble et flux de travail de consommation de package</span><span class="sxs-lookup"><span data-stu-id="b41ee-133">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="b41ee-134">Recherche et sélection des packages</span><span class="sxs-lookup"><span data-stu-id="b41ee-134">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="b41ee-135">Références de package dans les fichiers projet</span><span class="sxs-lookup"><span data-stu-id="b41ee-135">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
