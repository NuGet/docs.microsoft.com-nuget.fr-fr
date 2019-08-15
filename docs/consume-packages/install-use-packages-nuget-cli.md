---
title: Gérer des packages NuGet à l’aide de l’interface CLI nuget.exe
description: Instructions d’utilisation de l’interface CLI nuget.exe pour gérer des packages NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9ef990c16cca62a1fbad25ff1582bfa543135fab
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860583"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="576e5-103">Gérer des packages à l’aide de l’interface CLI nuget.exe</span><span class="sxs-lookup"><span data-stu-id="576e5-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="576e5-104">L’outil CLI facilite la mise à jour et la restauration des packages NuGet dans les projets et solutions.</span><span class="sxs-lookup"><span data-stu-id="576e5-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="576e5-105">Cet outil fournit toutes les fonctionnalités NuGet sur Windows ainsi que la plupart des fonctionnalités sur Mac et Linux dans un environnement d’exécution Mono.</span><span class="sxs-lookup"><span data-stu-id="576e5-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="576e5-106">Vous pouvez utiliser l’interface CLI `nuget.exe` pour votre projet .NET Framework et les projets non-SDK-style (par exemple, un projet SDK-style ciblant les bibliothèques .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="576e5-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="576e5-107">Si vous utilisez un projet non-SDK-style qui a été migré vers `PackageReference`, utilisez l’interface CLI `dotnet` à la place.</span><span class="sxs-lookup"><span data-stu-id="576e5-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="576e5-108">L’interface CLI `nuget.exe` a besoin d’un fichier [packages.config](../reference/packages-config.md) pour référencer les packages.</span><span class="sxs-lookup"><span data-stu-id="576e5-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="576e5-109">Dans la plupart des scénarios, il est préférable de [migrer les projets non-SDK-style](../reference/migrate-packages-config-to-package-reference.md) qui utilisent `packages.config` vers PackageReference, et d’utiliser ensuite l’interface CLI `dotnet` au lieu de l’interface CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="576e5-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="576e5-110">La migration n’est actuellement pas possible pour les projets C++ et ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="576e5-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="576e5-111">Cet article explique l’utilisation de base de quelques-unes des commandes de la CLI `nuget.exe` les plus courantes.</span><span class="sxs-lookup"><span data-stu-id="576e5-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="576e5-112">Pour la plupart de ces commandes, l’outil CLI recherche un fichier projet dans le répertoire actif, sauf si vous avez spécifié un fichier projet particulier dans la commande.</span><span class="sxs-lookup"><span data-stu-id="576e5-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="576e5-113">Pour obtenir une liste complète des commandes et des arguments disponibles, consultez les [informations de référence sur l’interface CLI nuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="576e5-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="576e5-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="576e5-114">Prerequisites</span></span>

- <span data-ttu-id="576e5-115">Installez l’interface CLI `nuget.exe` en la téléchargeant sur [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) : enregistrez ce fichier `.exe` dans un dossier approprié et ajoutez ce dossier à votre variable d’environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="576e5-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="576e5-116">Installer un package</span><span class="sxs-lookup"><span data-stu-id="576e5-116">Install a package</span></span>

<span data-ttu-id="576e5-117">La commande [install](../reference/cli-reference/cli-ref-install.md) télécharge et installe un package dans un projet, par défaut dans le dossier actif, en utilisant les sources de packages spécifiées.</span><span class="sxs-lookup"><span data-stu-id="576e5-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="576e5-118">Installez les nouveaux packages dans le dossier *packages* du répertoire racine de votre projet.</span><span class="sxs-lookup"><span data-stu-id="576e5-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="576e5-119">La commande `install` ne modifie pas le fichier projet ni le fichier *packages.config*. Elle est similaire à la commande `restore` en ce sens qu’elle ajoute seulement les packages sur le disque, sans changer les dépendances du projet.</span><span class="sxs-lookup"><span data-stu-id="576e5-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="576e5-120">Pour ajouter une dépendance, soit vous ajoutez un package via l’interface utilisateur ou la console du Gestionnaire de package dans Visual Studio, soit vous modifiez *packages.config* et exécutez ensuite `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="576e5-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="576e5-121">Ouvrez une ligne de commande et accédez au répertoire contenant votre fichier projet.</span><span class="sxs-lookup"><span data-stu-id="576e5-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="576e5-122">Utilisez la commande suivante pour installer un package NuGet dans le dossier *packages*.</span><span class="sxs-lookup"><span data-stu-id="576e5-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="576e5-123">Pour installer le package `Newtonsoft.json` dans le dossier *packages*, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="576e5-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="576e5-124">Vous pouvez aussi utiliser la commande suivante si vous souhaitez installer un package NuGet à l’aide d’un fichier `packages.config` existant dans le dossier *packages*.</span><span class="sxs-lookup"><span data-stu-id="576e5-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="576e5-125">Cette commande n’ajoute pas le package aux dépendances de votre projet, elle l’installe localement.</span><span class="sxs-lookup"><span data-stu-id="576e5-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="576e5-126">Installer une version particulière d’un package</span><span class="sxs-lookup"><span data-stu-id="576e5-126">Install a specific version of a package</span></span>

<span data-ttu-id="576e5-127">Si vous ne spécifiez pas de version dans la commande [install](../reference/cli-reference/cli-ref-install.md), NuGet installe la dernière version disponible du package.</span><span class="sxs-lookup"><span data-stu-id="576e5-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="576e5-128">Vous pouvez toutefois installer une version particulière d’un package Nuget :</span><span class="sxs-lookup"><span data-stu-id="576e5-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="576e5-129">Par exemple, pour ajouter la version 12.0.1 du package `Newtonsoft.json`, utilisez cette commande :</span><span class="sxs-lookup"><span data-stu-id="576e5-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="576e5-130">Pour plus d’informations sur les limitations et le comportement de la commande `install`, consultez [Installer un package](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="576e5-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="576e5-131">Supprimer un package</span><span class="sxs-lookup"><span data-stu-id="576e5-131">Remove a package</span></span>

<span data-ttu-id="576e5-132">Pour supprimer un ou plusieurs packages, spécifiez les packages que vous souhaitez supprimer du dossier *packages*.</span><span class="sxs-lookup"><span data-stu-id="576e5-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="576e5-133">Pour réinstaller des packages supprimés, utilisez la commande `restore` ou `install`.</span><span class="sxs-lookup"><span data-stu-id="576e5-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="576e5-134">Lister les packages</span><span class="sxs-lookup"><span data-stu-id="576e5-134">List packages</span></span>

<span data-ttu-id="576e5-135">Vous pouvez lister les packages d’une source donnée à l’aide de la commande [list](../reference/cli-reference/cli-ref-list.md).</span><span class="sxs-lookup"><span data-stu-id="576e5-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="576e5-136">Utilisez l’option `-Source` pour limiter l’étendue de la recherche.</span><span class="sxs-lookup"><span data-stu-id="576e5-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="576e5-137">Par exemple, listez les packages contenus dans le dossier *packages*.</span><span class="sxs-lookup"><span data-stu-id="576e5-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="576e5-138">Si vous utilisez un terme de recherche, la recherche porte sur les noms des packages, les balises et les descriptions des packages.</span><span class="sxs-lookup"><span data-stu-id="576e5-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="576e5-139">Mettre à jour un seul package</span><span class="sxs-lookup"><span data-stu-id="576e5-139">Update an individual package</span></span>

<span data-ttu-id="576e5-140">NuGet installe la dernière version du package quand vous utilisez la commande `install`, sauf si vous spécifiez une version particulière du package.</span><span class="sxs-lookup"><span data-stu-id="576e5-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="576e5-141">Mettre à jour tous les packages</span><span class="sxs-lookup"><span data-stu-id="576e5-141">Update all packages</span></span>

<span data-ttu-id="576e5-142">Utilisez la commande [update](../reference/cli-reference/cli-ref-update.md) pour mettre à jour l’ensemble des packages.</span><span class="sxs-lookup"><span data-stu-id="576e5-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="576e5-143">Mettez à jour tous les packages dans un projet (en utilisant `packages.config`) avec leurs dernières versions disponibles.</span><span class="sxs-lookup"><span data-stu-id="576e5-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="576e5-144">Il est recommandé d’exécuter `restore` avant `update`.</span><span class="sxs-lookup"><span data-stu-id="576e5-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="576e5-145">Restaurer des packages</span><span class="sxs-lookup"><span data-stu-id="576e5-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]