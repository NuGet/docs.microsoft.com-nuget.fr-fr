---
title: Guide de la Console Gestionnaire de Package NuGet | Documents Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
f1_keywords: vs.nuget.packagemanager.console
description: "Instructions pour à l’aide de la Console du Gestionnaire de Package NuGet dans Visual Studio pour l’utilisation de packages."
keywords: "Console de gestionnaire de package NuGet, powershell NuGet, gérer des packages NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b8f1df23d1a43412868c14e508ee5221d48dcc7c
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="51eb8-104">Console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="51eb8-104">Package Manager Console</span></span>

<span data-ttu-id="51eb8-105">La Console du Gestionnaire de Package NuGet est intégrée à Visual Studio sur Windows 2012 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="51eb8-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="51eb8-106">(Il n’est pas inclus dans Visual Studio pour Mac ou Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="51eb8-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="51eb8-107">La console vous permet d’utiliser [commandes NuGet PowerShell](../tools/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="51eb8-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="51eb8-108">L’utilisation de la console est nécessaire dans les cas où le Gestionnaire de Package UI ne fournit pas d’une façon d’effectuer une opération.</span><span class="sxs-lookup"><span data-stu-id="51eb8-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="51eb8-109">Par exemple, rechercher et installer un package s’effectue en trois étapes simples :</span><span class="sxs-lookup"><span data-stu-id="51eb8-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="51eb8-110">Ouvrez le projet ou la solution dans Visual Studio, puis ouvrez la console à l’aide de la **Outils > Gestionnaire de Package NuGet > Package Manager Console** commande.</span><span class="sxs-lookup"><span data-stu-id="51eb8-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="51eb8-111">Recherchez le package que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="51eb8-111">Find the package you want to install.</span></span> <span data-ttu-id="51eb8-112">Si vous connaissez déjà cela, passez à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="51eb8-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="51eb8-113">Exécutez la commande d’installation :</span><span class="sxs-lookup"><span data-stu-id="51eb8-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="51eb8-114">Dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="51eb8-114">In this topic:</span></span>

- [<span data-ttu-id="51eb8-115">Ouverture de la console</span><span class="sxs-lookup"><span data-stu-id="51eb8-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="51eb8-116">Installation d’un package</span><span class="sxs-lookup"><span data-stu-id="51eb8-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="51eb8-117">Désinstallation d’un package</span><span class="sxs-lookup"><span data-stu-id="51eb8-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="51eb8-118">Recherche d’un package</span><span class="sxs-lookup"><span data-stu-id="51eb8-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="51eb8-119">Un package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="51eb8-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="51eb8-120">Disponibilité de la console</span><span class="sxs-lookup"><span data-stu-id="51eb8-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="51eb8-121">Extension de la Console du Gestionnaire de Package</span><span class="sxs-lookup"><span data-stu-id="51eb8-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="51eb8-122">Configuration d’un profil de NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="51eb8-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="51eb8-123">Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées avec la [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="51eb8-124">Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et une projet/solution enregistrée et souvent accomplir plus de leurs commandes CLI équivalentes.</span><span class="sxs-lookup"><span data-stu-id="51eb8-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="51eb8-125">Par exemple, l’installation d’un package via la console ajoute une référence au projet n’est pas le cas de la commande CLI.</span><span class="sxs-lookup"><span data-stu-id="51eb8-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="51eb8-126">Pour cette raison, les développeurs qui travaillent dans Visual Studio en général, préfèrent à l’aide de la console pour l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="51eb8-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="51eb8-127">Nombre d’opérations console dépend de disposer d’une solution ouverte dans Visual Studio avec un nom de chemin d’accès connu.</span><span class="sxs-lookup"><span data-stu-id="51eb8-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="51eb8-128">Si vous avez une solution non enregistrée, ou aucune solution, vous pouvez voir l’erreur, « Solution est pas ouvert ou non enregistrée.</span><span class="sxs-lookup"><span data-stu-id="51eb8-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="51eb8-129">Vérifiez que vous avez une solution ouverte et enregistrée. »</span><span class="sxs-lookup"><span data-stu-id="51eb8-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="51eb8-130">Cela indique que la console ne peut pas déterminer le dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="51eb8-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="51eb8-131">L’enregistrement d’une solution non enregistrée, ou en créant et en enregistrant une solution si vous n’en avez pas ouvert, devrait corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="51eb8-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="51eb8-132">Ouverture de la console et les contrôles de la console</span><span class="sxs-lookup"><span data-stu-id="51eb8-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="51eb8-133">Ouvrez la console dans Visual Studio en utilisant le **Outils > Gestionnaire de Package NuGet > Package Manager Console** commande.</span><span class="sxs-lookup"><span data-stu-id="51eb8-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="51eb8-134">La console est une fenêtre de Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (voir [personnaliser des dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="51eb8-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="51eb8-135">Par défaut, les commandes de la console fonctionnent par rapport à un projet et la source du package spécifique défini dans le contrôle en haut de la fenêtre :</span><span class="sxs-lookup"><span data-stu-id="51eb8-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Contrôles de la Console du Gestionnaire de package pour le projet et de la source du package](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="51eb8-137">Sélection d’une source de package différent et/ou d’un projet modifie les valeurs par défaut pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="51eb8-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="51eb8-138">Moyen d’ignorer ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prend en charge `-Source` et `-ProjectName` options.</span><span class="sxs-lookup"><span data-stu-id="51eb8-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="51eb8-139">Pour gérer les sources de package, sélectionnez l’icône d’engrenage.</span><span class="sxs-lookup"><span data-stu-id="51eb8-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="51eb8-140">Il s’agit d’un raccourci vers le **Outils > Options > Gestionnaire de Package NuGet > Sources de Package** boîte de dialogue, comme décrit dans la [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span><span class="sxs-lookup"><span data-stu-id="51eb8-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="51eb8-141">En outre, le contrôle situé à droite du sélecteur de projet efface contenu de la console :</span><span class="sxs-lookup"><span data-stu-id="51eb8-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paramètres de la Console du Gestionnaire de package et effacer les contrôles](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="51eb8-143">Le bouton plus à droite interrompt une commande longue.</span><span class="sxs-lookup"><span data-stu-id="51eb8-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="51eb8-144">Par exemple, en cours d’exécution `Get-Package -ListAvailable -PageSize 500` répertorie les packages top 500 sur la source par défaut (par exemple nuget.org), ce qui peut prendre plusieurs minutes pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="51eb8-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Contrôle d’arrêt de Console du Gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="51eb8-146">Installation d’un package</span><span class="sxs-lookup"><span data-stu-id="51eb8-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="51eb8-147">Consultez [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="51eb8-148">Installation d’un package effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="51eb8-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="51eb8-149">Affiche les termes du contrat de licence applicable dans la fenêtre de console avec accord implicite.</span><span class="sxs-lookup"><span data-stu-id="51eb8-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="51eb8-150">Si vous n’acceptez pas les termes du contrat, vous devez désinstaller le package immédiatement.</span><span class="sxs-lookup"><span data-stu-id="51eb8-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="51eb8-151">Ajoute une référence au projet dans le format de la référence est en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="51eb8-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="51eb8-152">Références apparaissent par la suite dans l’Explorateur de solutions et le fichier de format de référence applicable.</span><span class="sxs-lookup"><span data-stu-id="51eb8-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="51eb8-153">Notez, toutefois, avec PackageReference, vous devez enregistrer le projet pour voir les modifications dans le fichier projet directement.</span><span class="sxs-lookup"><span data-stu-id="51eb8-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="51eb8-154">Met en cache le package :</span><span class="sxs-lookup"><span data-stu-id="51eb8-154">Caches the package:</span></span>
    - <span data-ttu-id="51eb8-155">PackageReference : package est mis en cache dans `%USERPROFILE%\.nuget\packages` et le verrouillage de fichier par exemple, `project.assets.json` est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="51eb8-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="51eb8-156">`packages.config`: crée un `packages` dossier à la racine de la solution et copie les fichiers de package dans un sous-dossier.</span><span class="sxs-lookup"><span data-stu-id="51eb8-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="51eb8-157">Le `package.config` fichier est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="51eb8-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="51eb8-158">Les mises à jour `app.config` et/ou `web.config` si le package utilise [source et configuration des transformations de fichiers](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="51eb8-159">Installe toutes les dépendances, si elle est déjà présent dans le projet.</span><span class="sxs-lookup"><span data-stu-id="51eb8-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="51eb8-160">Cela peut mettre à jour les versions de package dans le processus, comme décrit dans [résolution de dépendance](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="51eb8-161">Affiche le fichier Lisez-moi du package si elle est disponible, dans une fenêtre de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51eb8-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="51eb8-162">Un des principaux avantages de l’installation des packages avec le `Install-Package` commande dans la console est qui ajoute une référence au projet comme si vous avez utilisé le Gestionnaire de Package UI.</span><span class="sxs-lookup"><span data-stu-id="51eb8-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="51eb8-163">En revanche, le `nuget install` commande CLI télécharge le package uniquement et n’ajoute pas automatiquement une référence.</span><span class="sxs-lookup"><span data-stu-id="51eb8-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="51eb8-164">Désinstallation d’un package</span><span class="sxs-lookup"><span data-stu-id="51eb8-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="51eb8-165">Consultez [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="51eb8-166">Utilisez [Get-Package](../tools/ps-ref-get-package.md) pour voir tous les packages actuellement installés dans le projet par défaut si vous avez besoin rechercher un identificateur.</span><span class="sxs-lookup"><span data-stu-id="51eb8-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="51eb8-167">Désinstallation d’un package effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="51eb8-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="51eb8-168">Supprime les références au package du projet (et le format de la référence est en cours d’utilisation).</span><span class="sxs-lookup"><span data-stu-id="51eb8-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="51eb8-169">Les références n’apparaissent plus dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="51eb8-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="51eb8-170">(Vous devrez peut-être régénérer le projet pour voir qu’il est supprimé de la **Bin** dossier.)</span><span class="sxs-lookup"><span data-stu-id="51eb8-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="51eb8-171">Annule les modifications apportées à `app.config` ou `web.config` lorsque le package a été installé.</span><span class="sxs-lookup"><span data-stu-id="51eb8-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="51eb8-172">Dépendances supprime précédemment installés si aucun package restantes n’utilisent ces dépendances.</span><span class="sxs-lookup"><span data-stu-id="51eb8-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="51eb8-173">Comme `Install-Package`, le `Uninstall-Package` commande présente l’avantage de la gestion des références dans le projet, contrairement à la `nuget uninstall` commande CLI.</span><span class="sxs-lookup"><span data-stu-id="51eb8-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="51eb8-174">Un package de mise à jour</span><span class="sxs-lookup"><span data-stu-id="51eb8-174">Updating a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="51eb8-175">Consultez [Get-Package](../tools/ps-ref-get-package.md) et [Package de mise à jour](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="51eb8-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="51eb8-176">Recherche d’un package</span><span class="sxs-lookup"><span data-stu-id="51eb8-176">Finding a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="51eb8-177">Consultez [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="51eb8-178">Dans Visual Studio 2013 et versions antérieures, utilisez [Get-Package](../tools/ps-ref-get-package.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="51eb8-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="51eb8-179">Disponibilité de la console</span><span class="sxs-lookup"><span data-stu-id="51eb8-179">Availability of the console</span></span>

<span data-ttu-id="51eb8-180">Dans Visual Studio 2017, NuGet et le Gestionnaire de Package NuGet sont installés automatiquement lorsque vous sélectionnez. Charges de travail liées NET ; Vous pouvez également l’installer séparément en vérifiant la **des composants individuels > Code Outils > Gestionnaire de package NuGet** option dans le programme d’installation de Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="51eb8-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="51eb8-181">En outre, si vous êtes pas le Gestionnaire de Package NuGet dans Visual Studio 2015 et versions antérieures, vérifiez **Outils > Extensions et mises à jour...**  et recherchez l’extension du Gestionnaire de Package NuGet.</span><span class="sxs-lookup"><span data-stu-id="51eb8-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="51eb8-182">Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l’extension directement à partir de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="51eb8-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="51eb8-183">La Console du Gestionnaire de Package n’est pas actuellement disponible dans Visual Studio pour Mac.</span><span class="sxs-lookup"><span data-stu-id="51eb8-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="51eb8-184">Toutefois, les commandes équivalentes, sont disponibles via le [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="51eb8-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="51eb8-185">Visual Studio pour Mac possède une interface utilisateur pour la gestion des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="51eb8-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="51eb8-186">Consultez [package, y compris un NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="51eb8-186">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="51eb8-187">La Console du Gestionnaire de Package n’est pas incluse avec Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="51eb8-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="51eb8-188">Extension de la Console du Gestionnaire de Package</span><span class="sxs-lookup"><span data-stu-id="51eb8-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="51eb8-189">Certains packages installent de nouvelles commandes de la console.</span><span class="sxs-lookup"><span data-stu-id="51eb8-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="51eb8-190">Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold` illustré ci-dessous, qui génère les contrôleurs ASP.NET MVC et les vues :</span><span class="sxs-lookup"><span data-stu-id="51eb8-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installation et l’utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="51eb8-192">Configuration d’un profil de PowerShell NuGet</span><span class="sxs-lookup"><span data-stu-id="51eb8-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="51eb8-193">Un profil de PowerShell vous permet de rendre les commandes couramment utilisées disponible partout où vous utilisez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51eb8-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="51eb8-194">NuGet prend en charge un profil spécifique NuGet que se trouve généralement à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="51eb8-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="51eb8-195">Pour trouver le profil, tapez `$profile` dans la console :</span><span class="sxs-lookup"><span data-stu-id="51eb8-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="51eb8-196">Pour plus d’informations, reportez-vous à [les profils Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="51eb8-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
