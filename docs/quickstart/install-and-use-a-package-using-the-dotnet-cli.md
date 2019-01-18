---
title: Guide d’introduction à l’utilisation des packages NuGet via l’infrastructure CLI dotnet
description: Didacticiel décrivant la procédure pas à pas permettant d’installer et d’utiliser un package NuGet dans un projet .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 4b593cc215ad68629e5a93d1f17c90e53c0b4f4f
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324628"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="dacd6-103">Démarrage rapide : Installer et utiliser un package à l’aide de l’interface CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="dacd6-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="dacd6-104">Les packages NuGet contiennent du code réutilisable que les autres développeurs mettent à votre disposition pour l’utiliser dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="dacd6-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="dacd6-105">Pour des informations de base, consultez [Qu’est-ce que NuGet ?](../What-is-NuGet.md).</span><span class="sxs-lookup"><span data-stu-id="dacd6-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="dacd6-106">Les packages sont installés dans un projet .NET Core à l’aide de la commande `dotnet add package`, comme décrit dans cet article pour le package courant [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="dacd6-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="dacd6-107">Une fois le package installé, faites-y référence dans le code avec `using <namespace>`, où \<namespace\> est propre au package que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="dacd6-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="dacd6-108">Vous pourrez alors utiliser l’API du package.</span><span class="sxs-lookup"><span data-stu-id="dacd6-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="dacd6-109">**Prise en main de nuget.org** : Les développeurs .NET parcourent nutget.org à la recherche de composants qu’ils peuvent réutiliser dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="dacd6-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="dacd6-110">Vous pouvez effectuer des recherches directement dans nuget.org, ou rechercher et installer des packages dans Visual Studio comme illustré dans cet article.</span><span class="sxs-lookup"><span data-stu-id="dacd6-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dacd6-111">Prérequis</span><span class="sxs-lookup"><span data-stu-id="dacd6-111">Prerequisites</span></span>

- <span data-ttu-id="dacd6-112">Le [kit SDK .NET Core](https://www.microsoft.com/net/download/), qui fournit l’outil en ligne de commande `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="dacd6-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="dacd6-113">Créer un projet</span><span class="sxs-lookup"><span data-stu-id="dacd6-113">Create a project</span></span>

<span data-ttu-id="dacd6-114">Les packages NuGet peuvent être installés dans tout type de projet .NET.</span><span class="sxs-lookup"><span data-stu-id="dacd6-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="dacd6-115">Pour cette procédure pas à pas, créez un projet de console .NET Core simple comme suit :</span><span class="sxs-lookup"><span data-stu-id="dacd6-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="dacd6-116">Créez un dossier pour le projet.</span><span class="sxs-lookup"><span data-stu-id="dacd6-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="dacd6-117">Créez le projet à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dacd6-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="dacd6-118">Utilisez `dotnet run` pour vérifier que l’application a été créée correctement.</span><span class="sxs-lookup"><span data-stu-id="dacd6-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="dacd6-119">Ajouter le package NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="dacd6-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="dacd6-120">Utilisez la commande suivante pour installer le package `Newtonsoft.json` :</span><span class="sxs-lookup"><span data-stu-id="dacd6-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="dacd6-121">Une fois la commande terminée, ouvrez le fichier `.csproj` pour voir la référence ajoutée :</span><span class="sxs-lookup"><span data-stu-id="dacd6-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="dacd6-122">Utiliser l’API Newtonsoft.Json dans l’application</span><span class="sxs-lookup"><span data-stu-id="dacd6-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="dacd6-123">Ouvrez le fichier `Program.cs` et ajoutez la ligne suivante en haut du fichier :</span><span class="sxs-lookup"><span data-stu-id="dacd6-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="dacd6-124">Ajoutez le code suivant avant la ligne `class Program` :</span><span class="sxs-lookup"><span data-stu-id="dacd6-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="dacd6-125">Remplacez la fonction `Main` par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="dacd6-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="dacd6-126">Générez et exécutez l’application à l’aide de la commande `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="dacd6-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="dacd6-127">La sortie doit être la représentation JSON de l’objet `Account` dans le code :</span><span class="sxs-lookup"><span data-stu-id="dacd6-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="dacd6-128">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="dacd6-128">Related articles</span></span>

- [<span data-ttu-id="dacd6-129">Vue d’ensemble et flux de travail de consommation de package</span><span class="sxs-lookup"><span data-stu-id="dacd6-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="dacd6-130">Recherche et sélection des packages</span><span class="sxs-lookup"><span data-stu-id="dacd6-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="dacd6-131">Méthodes d’installation d’un package</span><span class="sxs-lookup"><span data-stu-id="dacd6-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="dacd6-132">Configuration du comportement de NuGet</span><span class="sxs-lookup"><span data-stu-id="dacd6-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
