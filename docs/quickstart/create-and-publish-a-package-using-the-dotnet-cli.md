---
title: Création et publication d’un package NuGet avec l’interface CLI dotnet
description: Ce didacticiel explique pas à pas comment créer et publier un package NuGet avec l’interface de ligne de commande (CLI) .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 4e96d9969c8b4570ee69501d6529986f891ea4dc
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842604"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="6a787-103">Démarrage rapide : Créer et publier un package (interface CLI dotnet)</span><span class="sxs-lookup"><span data-stu-id="6a787-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="6a787-104">La création d’un package NuGet à partir d’une bibliothèque de classes .NET est un processus simple, de même que sa publication sur nuget.org avec l’interface de ligne de commande (CLI) `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="6a787-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a787-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="6a787-105">Prerequisites</span></span>

1. <span data-ttu-id="6a787-106">Installez le [Kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/download/), qui comprend l’interface CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="6a787-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="6a787-107">À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.</span><span class="sxs-lookup"><span data-stu-id="6a787-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="6a787-108">[Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="6a787-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="6a787-109">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="6a787-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="6a787-110">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="6a787-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="6a787-111">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="6a787-111">Create a class library project</span></span>

<span data-ttu-id="6a787-112">Vous pouvez utiliser un projet de bibliothèque de classes .NET existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="6a787-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="6a787-113">Créez un dossier nommé `AppLogger` et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="6a787-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="6a787-114">Créez le projet à l’aide de la commande `dotnet new classlib`, qui donne le nom du dossier actif au projet.</span><span class="sxs-lookup"><span data-stu-id="6a787-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="6a787-115">Ajouter des métadonnées de package au fichier projet</span><span class="sxs-lookup"><span data-stu-id="6a787-115">Add package metadata to the project file</span></span>

<span data-ttu-id="6a787-116">Chaque package NuGet a besoin d’un manifeste décrivant son contenu et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="6a787-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="6a787-117">Dans un package final, il s’agit d’un fichier `.nuspec` généré à partir des propriétés de métadonnées NuGet incluses dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="6a787-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="6a787-118">Ouvrez votre fichier projet (`.csproj`) et ajoutez les propriétés minimales suivantes à l’intérieur de la balise `<PropertyGroup>` existante, en adaptant les valeurs :</span><span class="sxs-lookup"><span data-stu-id="6a787-118">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="6a787-119">Donnez au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="6a787-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="6a787-120">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="6a787-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="6a787-121">Ajoutez si vous le souhaitez certaines des propriétés facultatives décrites dans [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="6a787-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="6a787-122">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="6a787-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="6a787-123">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="6a787-123">Run the pack command</span></span>

<span data-ttu-id="6a787-124">Pour créer un package NuGet (fichier `.nupkg`) à partir du projet, exécutez la commande `dotnet pack`, qui génère également le projet automatiquement :</span><span class="sxs-lookup"><span data-stu-id="6a787-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="6a787-125">La sortie affiche le chemin d’accès du fichier `.nupkg` :</span><span class="sxs-lookup"><span data-stu-id="6a787-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="6a787-126">Générer automatiquement le package à la création</span><span class="sxs-lookup"><span data-stu-id="6a787-126">Automatically generate package on build</span></span>

<span data-ttu-id="6a787-127">Pour exécuter automatiquement `dotnet pack` pendant l’exécution de `dotnet build`, ajoutez la ligne suivante à votre fichier projet au sein de `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="6a787-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="6a787-128">Publier le package</span><span class="sxs-lookup"><span data-stu-id="6a787-128">Publish the package</span></span>

<span data-ttu-id="6a787-129">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de la commande `dotnet nuget push`, avec une clé API acquise sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6a787-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="6a787-130">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="6a787-130">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="6a787-131">Publier avec dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="6a787-131">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="6a787-132">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="6a787-132">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="6a787-133">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="6a787-133">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="6a787-134">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="6a787-134">Related topics</span></span>

- [<span data-ttu-id="6a787-135">Créer un package</span><span class="sxs-lookup"><span data-stu-id="6a787-135">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="6a787-136">Publier un package</span><span class="sxs-lookup"><span data-stu-id="6a787-136">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="6a787-137">Packages de préversion</span><span class="sxs-lookup"><span data-stu-id="6a787-137">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="6a787-138">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="6a787-138">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6a787-139">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="6a787-139">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="6a787-140">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="6a787-140">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="6a787-141">Création de packages de symboles</span><span class="sxs-lookup"><span data-stu-id="6a787-141">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="6a787-142">Signature de packages</span><span class="sxs-lookup"><span data-stu-id="6a787-142">Signing packages</span></span>](../create-packages/Sign-a-package.md)
