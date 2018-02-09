---
title: "Guide d’introduction à la création et à la publication de package NuGet avec l’interface CLI dotnet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Ce didacticiel explique pas à pas comment créer et publier un package NuGet avec l’interface de ligne de commande (CLI) .NET Core, dotnet."
keywords: "Création de package NuGet, publication de package NuGet, didacticiel NuGet, package NuGet de publication dotnet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c9f46cafafcdc238e43979d6f05521e19bf3d7f6
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="1f73f-104">Créer et publier un package</span><span class="sxs-lookup"><span data-stu-id="1f73f-104">Create and publish a package</span></span>

<span data-ttu-id="1f73f-105">La création d’un package NuGet à partir d’une bibliothèque de classes .NET est un processus simple, de même que sa publication sur nuget.org avec l’interface de ligne de commande (CLI) `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="1f73f-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="1f73f-106">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="1f73f-106">Pre-requisites</span></span>

1. <span data-ttu-id="1f73f-107">Installez le [Kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/download/), qui comprend l’interface CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="1f73f-107">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="1f73f-108">[Créez un compte gratuit sur nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si vous n’avez pas encore de compte.</span><span class="sxs-lookup"><span data-stu-id="1f73f-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="1f73f-109">La création d’un compte envoie un e-mail de confirmation.</span><span class="sxs-lookup"><span data-stu-id="1f73f-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="1f73f-110">Vous devez confirmer le compte avant de pouvoir charger un package.</span><span class="sxs-lookup"><span data-stu-id="1f73f-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="1f73f-111">Créer un projet de bibliothèque de classes</span><span class="sxs-lookup"><span data-stu-id="1f73f-111">Create a class library project</span></span>

<span data-ttu-id="1f73f-112">Vous pouvez utiliser un projet de bibliothèque de classes .NET existant pour le code à empaqueter, ou bien en créer un de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="1f73f-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="1f73f-113">Créez un dossier nommé `AppLogger` et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="1f73f-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="1f73f-114">Créez le projet à l’aide de la commande `dotnet new classlib`, qui donne le nom du dossier actif au projet.</span><span class="sxs-lookup"><span data-stu-id="1f73f-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="1f73f-115">Ajouter des métadonnées de package au fichier projet</span><span class="sxs-lookup"><span data-stu-id="1f73f-115">Add package metadata to the project file</span></span>

<span data-ttu-id="1f73f-116">Chaque package NuGet a besoin d’un manifeste décrivant son contenu et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="1f73f-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="1f73f-117">Dans un package final, il s’agit d’un fichier `.nuspec` généré à partir des propriétés de métadonnées NuGet incluses dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="1f73f-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="1f73f-118">Ouvrez votre fichier projet (`.csproj`) et ajoutez les propriétés minimales suivantes à l’intérieur de la balise de fin `<PropertyGroup>`, en adaptant les valeurs :</span><span class="sxs-lookup"><span data-stu-id="1f73f-118">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="1f73f-119">Donnez au package un identificateur unique sur nuget.org ou sur l’hôte que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="1f73f-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="1f73f-120">Dans le cadre de cette procédure pas à pas, nous vous recommandons d’inclure « Exemple » ou « Test » dans le nom, car l’étape de publication ultérieure rend le package visible publiquement (même s’il est peu probable que quelqu’un l’utilise vraiment).</span><span class="sxs-lookup"><span data-stu-id="1f73f-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="1f73f-121">Ajoutez si vous le souhaitez certaines des propriétés facultatives décrites dans [Propriétés de métadonnées NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="1f73f-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="1f73f-122">Dans le cas des packages destinés à une utilisation publique, faites particulièrement attention à la propriété **PackageTags**, car les balises aident les utilisateurs à trouver vos packages et à comprendre leur rôle.</span><span class="sxs-lookup"><span data-stu-id="1f73f-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="1f73f-123">Exécuter la commande pack</span><span class="sxs-lookup"><span data-stu-id="1f73f-123">Run the pack command</span></span>

<span data-ttu-id="1f73f-124">Pour générer un package NuGet (un fichier `.nupkg`) à partir du projet, exécutez la commande `dotnet pack` :</span><span class="sxs-lookup"><span data-stu-id="1f73f-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="1f73f-125">La sortie affiche le chemin d’accès du fichier `.nupkg` :</span><span class="sxs-lookup"><span data-stu-id="1f73f-125">The output will show the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

## <a name="publish-the-package"></a><span data-ttu-id="1f73f-126">Publier le package</span><span class="sxs-lookup"><span data-stu-id="1f73f-126">Publish the package</span></span>

<span data-ttu-id="1f73f-127">Maintenant que vous disposez d’un fichier `.nupkg`, publiez-le sur nuget.org à l’aide de la commande `dotnet nuget push`, avec une clé API acquise sur nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1f73f-127">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="1f73f-128">Obtenir une clé API</span><span class="sxs-lookup"><span data-stu-id="1f73f-128">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="1f73f-129">Publier avec dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="1f73f-129">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="1f73f-130">Erreurs de publication</span><span class="sxs-lookup"><span data-stu-id="1f73f-130">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]


### <a name="manage-the-published-package"></a><span data-ttu-id="1f73f-131">Gérer le package publié</span><span class="sxs-lookup"><span data-stu-id="1f73f-131">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="1f73f-132">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="1f73f-132">Related topics</span></span>

- [<span data-ttu-id="1f73f-133">Créer un package</span><span class="sxs-lookup"><span data-stu-id="1f73f-133">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="1f73f-134">Publier un package</span><span class="sxs-lookup"><span data-stu-id="1f73f-134">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="1f73f-135">Prendre en charge plusieurs frameworks cibles</span><span class="sxs-lookup"><span data-stu-id="1f73f-135">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="1f73f-136">Gestion des versions de package</span><span class="sxs-lookup"><span data-stu-id="1f73f-136">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="1f73f-137">Création de packages localisés</span><span class="sxs-lookup"><span data-stu-id="1f73f-137">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
