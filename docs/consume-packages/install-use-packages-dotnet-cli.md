---
title: Installer et gérer des packages NuGet à l’aide de l’interface CLI dotnet
description: Instructions d’utilisation de l’interface CLI dotnet pour gérer des packages NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825160"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="23d9b-103">Installer et gérer des packages à l’aide de l’interface CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="23d9b-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="23d9b-104">L’outil CLI facilite l’installation, la désinstallation et la mise à jour des packages NuGet dans les projets et solutions.</span><span class="sxs-lookup"><span data-stu-id="23d9b-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="23d9b-105">Il s’exécute sur Windows, Mac OS X et Linux.</span><span class="sxs-lookup"><span data-stu-id="23d9b-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="23d9b-106">Vous pouvez utiliser l’interface CLI dotnet dans votre projet .NET Core et .NET Standard (types de projets de style SDK) et dans tous les autres projets de style SDK (par exemple, un projet de style SDK qui cible le .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="23d9b-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="23d9b-107">Pour plus d’informations, consultez [Attribut Sdk](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="23d9b-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="23d9b-108">Cet article explique l’utilisation de base de quelques-unes des commandes de la CLI dotnet les plus courantes.</span><span class="sxs-lookup"><span data-stu-id="23d9b-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="23d9b-109">Pour la plupart de ces commandes, l’outil CLI recherche un fichier projet dans le répertoire actif, sauf si vous avez spécifié un fichier projet particulier dans la commande (le fichier projet est un commutateur facultatif).</span><span class="sxs-lookup"><span data-stu-id="23d9b-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="23d9b-110">Pour obtenir une liste complète des commandes et des arguments disponibles, consultez les [outils de l’interface de ligne de commande (CLI) de .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="23d9b-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23d9b-111">Prérequis</span><span class="sxs-lookup"><span data-stu-id="23d9b-111">Prerequisites</span></span>

- <span data-ttu-id="23d9b-112">Le [kit SDK .NET Core](https://www.microsoft.com/net/download/), qui fournit l’outil en ligne de commande `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="23d9b-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="23d9b-113">À compter de Visual Studio 2017, la CLI dotnet est installée automatiquement avec les charges de travail associées à NET Core.</span><span class="sxs-lookup"><span data-stu-id="23d9b-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="23d9b-114">Installer un package</span><span class="sxs-lookup"><span data-stu-id="23d9b-114">Install a package</span></span>

<span data-ttu-id="23d9b-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) ajoute une référence de package au fichier projet, puis exécute `dotnet restore` pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="23d9b-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="23d9b-116">Ouvrez une ligne de commande et accédez au répertoire contenant votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="23d9b-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="23d9b-117">Utilisez la commande suivante pour installer un package Nuget :</span><span class="sxs-lookup"><span data-stu-id="23d9b-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="23d9b-118">Par exemple, pour installer le package `Newtonsoft.Json`, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="23d9b-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="23d9b-119">Une fois que la commande est terminée, examinez le fichier projet pour vérifier que le package a été installé.</span><span class="sxs-lookup"><span data-stu-id="23d9b-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="23d9b-120">Vous pouvez ouvrir le fichier `.csproj` pour voir la référence ajoutée :</span><span class="sxs-lookup"><span data-stu-id="23d9b-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="23d9b-121">Installer une version particulière d’un package</span><span class="sxs-lookup"><span data-stu-id="23d9b-121">Install a specific version of a package</span></span>

<span data-ttu-id="23d9b-122">Si vous ne spécifiez pas de version, NuGet installe la dernière version disponible du package.</span><span class="sxs-lookup"><span data-stu-id="23d9b-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="23d9b-123">Vous pouvez également utiliser la commande [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) pour installer une version particulière d’un package Nuget :</span><span class="sxs-lookup"><span data-stu-id="23d9b-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="23d9b-124">Par exemple, pour ajouter la version 12.0.1 du package `Newtonsoft.Json`, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="23d9b-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="23d9b-125">Lister les références de package</span><span class="sxs-lookup"><span data-stu-id="23d9b-125">List package references</span></span>

<span data-ttu-id="23d9b-126">Vous pouvez lister les références de package pour votre projet en utilisant la commande [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="23d9b-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="23d9b-127">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="23d9b-127">Remove a package</span></span>

<span data-ttu-id="23d9b-128">Utilisez la commande [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) pour supprimer une référence de package dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="23d9b-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="23d9b-129">Par exemple, pour supprimer le package `Newtonsoft.Json`, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="23d9b-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="23d9b-130">Mettre à jour un package</span><span class="sxs-lookup"><span data-stu-id="23d9b-130">Update a package</span></span>

<span data-ttu-id="23d9b-131">NuGet installe la dernière version du package quand vous utilisez la commande `dotnet add package`, sauf si vous spécifiez une version particulière du package (commutateur `-v`).</span><span class="sxs-lookup"><span data-stu-id="23d9b-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="23d9b-132">Restaurer des packages</span><span class="sxs-lookup"><span data-stu-id="23d9b-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
