---
title: Installer et gérer les packages NuGet à l’aide de PowerShell dans Visual Studio
description: Instructions sur l’utilisation de la Console du Gestionnaire de Package NuGet dans Visual Studio pour travailler avec des packages.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426215"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a><span data-ttu-id="b958b-103">Installer et gérer des packages à l’aide de PowerShell dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b958b-103">Install and manage packages using PowerShell in Visual Studio</span></span>

<span data-ttu-id="b958b-104">La Console du Gestionnaire de Package NuGet vous permet d’utiliser [commandes NuGet PowerShell](../tools/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="b958b-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="b958b-105">L’utilisation de la console est nécessaire dans les cas où le Gestionnaire de packages UI ne fournit pas d’une façon d’effectuer une opération.</span><span class="sxs-lookup"><span data-stu-id="b958b-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="b958b-106">Pour utiliser `nuget.exe` commandes CLI dans la console, consultez [à l’aide de l’interface CLI de nuget.exe dans la console](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="b958b-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="b958b-107">La console est intégrée dans Visual Studio sur Windows.</span><span class="sxs-lookup"><span data-stu-id="b958b-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="b958b-108">Il n’est pas inclus avec Visual Studio pour Mac ou Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b958b-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="b958b-109">Rechercher et installer un package</span><span class="sxs-lookup"><span data-stu-id="b958b-109">Find and install a package</span></span>

<span data-ttu-id="b958b-110">Par exemple, la recherche et l’installation d’un package s’effectue en trois étapes simples :</span><span class="sxs-lookup"><span data-stu-id="b958b-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="b958b-111">Ouvrez le projet ou la solution dans Visual Studio, puis ouvrez la console à l’aide de la **Outils > Gestionnaire de Package NuGet > Console du Gestionnaire de Package** commande.</span><span class="sxs-lookup"><span data-stu-id="b958b-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="b958b-112">Recherchez le package que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="b958b-112">Find the package you want to install.</span></span> <span data-ttu-id="b958b-113">Si vous connaissez déjà cela, passez à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="b958b-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="b958b-114">Exécutez la commande d’installation :</span><span class="sxs-lookup"><span data-stu-id="b958b-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="b958b-115">Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées avec la [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b958b-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="b958b-116">Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et une projet/solution enregistrée et souvent accomplir plus de leurs commandes CLI équivalentes.</span><span class="sxs-lookup"><span data-stu-id="b958b-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="b958b-117">Par exemple, installation d’un package via la console ajoute une référence au projet n’est pas le cas de la commande CLI.</span><span class="sxs-lookup"><span data-stu-id="b958b-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="b958b-118">Pour cette raison, les développeurs qui travaillent dans Visual Studio en général, préfèrent à l’aide de la console à l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="b958b-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="b958b-119">De nombreuses opérations de console dépendent de disposer d’une solution ouverte dans Visual Studio avec un nom de chemin d’accès connus.</span><span class="sxs-lookup"><span data-stu-id="b958b-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="b958b-120">Si vous avez une solution non enregistrée, ou aucune solution, vous pouvez voir l’erreur, « Solution est pas ouvert ou non enregistrée.</span><span class="sxs-lookup"><span data-stu-id="b958b-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="b958b-121">Vérifiez que vous disposez d’une solution ouverte et enregistrée. »</span><span class="sxs-lookup"><span data-stu-id="b958b-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="b958b-122">Cela indique que la console ne peut pas déterminer le dossier de solution.</span><span class="sxs-lookup"><span data-stu-id="b958b-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="b958b-123">L’enregistrement d’une solution non enregistrée, ou en créant et en enregistrant une solution si vous n’en avez pas ouvert, devrait corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="b958b-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="b958b-124">Utiliser la console et les contrôles de la console</span><span class="sxs-lookup"><span data-stu-id="b958b-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="b958b-125">Ouvrez la console dans Visual Studio en utilisant la commande **Outils > Gestionnaire de Package NuGet > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="b958b-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="b958b-126">La console est une fenêtre de Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (voir [Personnaliser des dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="b958b-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="b958b-127">Par défaut, les commandes de la console fonctionnent par rapport à un projet et la source du package spécifique tel que défini dans le contrôle en haut de la fenêtre :</span><span class="sxs-lookup"><span data-stu-id="b958b-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Contrôles de la Console du Gestionnaire de package pour le projet et de la source du package](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="b958b-129">La sélection d’une source de package et/ou d’un projet différent(e) modifie les valeurs par défaut pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="b958b-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="b958b-130">Pour remplacer ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prend en charge les options `-Source` et `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="b958b-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="b958b-131">Pour gérer les sources de package, sélectionnez l’icône d’engrenage.</span><span class="sxs-lookup"><span data-stu-id="b958b-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="b958b-132">Il s’agit d’un raccourci vers la boîte de dialogue **Outils > Options > Gestionnaire de Package NuGet > Sources de Package**, comme décrit dans la page [Package Manager UI](package-manager-ui.md#package-sources).</span><span class="sxs-lookup"><span data-stu-id="b958b-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="b958b-133">En outre, le contrôle situé à droite du sélecteur de projet efface contenu de la console :</span><span class="sxs-lookup"><span data-stu-id="b958b-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paramètres de la Console du Gestionnaire de package et effacer les contrôles](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="b958b-135">Le bouton plus à droite interrompt une commande longue.</span><span class="sxs-lookup"><span data-stu-id="b958b-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="b958b-136">Par exemple, utilisez la commande `Get-Package -ListAvailable -PageSize 500` qui vous permet de répertorier les 500 premiers packages sur la source par défaut (par exemple nuget.org). Celle-ci peut prendre plusieurs minutes pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="b958b-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Contrôle d’arrêt de Console du Gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="b958b-138">Installer un package</span><span class="sxs-lookup"><span data-stu-id="b958b-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="b958b-139">Voir aussi [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="b958b-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="b958b-140">Installation d’un package dans la console effectue les mêmes étapes comme décrit sur [que se passe-t-il lorsqu’un package est installé](../concepts/package-installation-process.md), avec les ajouts suivants :</span><span class="sxs-lookup"><span data-stu-id="b958b-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="b958b-141">La Console affiche les termes du contrat de licence applicable dans sa fenêtre avec un contrat implicite.</span><span class="sxs-lookup"><span data-stu-id="b958b-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="b958b-142">Si vous n’acceptez pas les termes du contrat, vous devez désinstaller le package immédiatement.</span><span class="sxs-lookup"><span data-stu-id="b958b-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="b958b-143">Également une référence au package est ajoutée au fichier projet et apparaît dans **l’Explorateur de solutions** sous le **références** nœud, vous devez enregistrer le projet pour voir les modifications dans le fichier projet directement.</span><span class="sxs-lookup"><span data-stu-id="b958b-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="b958b-144">Désinstaller un package</span><span class="sxs-lookup"><span data-stu-id="b958b-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="b958b-145">Consultez la section [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="b958b-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="b958b-146">Utilisez [Get-Package](../tools/ps-ref-get-package.md) pour voir tous les packages actuellement installés dans le projet par défaut si vous avez besoin rechercher un identificateur.</span><span class="sxs-lookup"><span data-stu-id="b958b-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="b958b-147">La désinstallation d’un package effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="b958b-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="b958b-148">Supprime la référence au package dans le projet (et le format de gestion est en cours d’utilisation).</span><span class="sxs-lookup"><span data-stu-id="b958b-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="b958b-149">Références n’apparaissent plus dans **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="b958b-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="b958b-150">(Vous devrez peut-être régénérer le projet pour voir s’il est supprimé du dossier **Bin**.)</span><span class="sxs-lookup"><span data-stu-id="b958b-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="b958b-151">Annule les modifications apportées à `app.config` ou `web.config` lorsque le package a été installé.</span><span class="sxs-lookup"><span data-stu-id="b958b-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="b958b-152">Supprime les dépendances précédemment installées si aucun paquet restant n'utilise ces dépendances.</span><span class="sxs-lookup"><span data-stu-id="b958b-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="b958b-153">Mettre à jour un package</span><span class="sxs-lookup"><span data-stu-id="b958b-153">Updating a package</span></span>

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

<span data-ttu-id="b958b-154">Voir aussi [Obtenir un package](../tools/ps-ref-get-package.md) et [Mettre à jour un package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="b958b-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="b958b-155">Rechercher un package</span><span class="sxs-lookup"><span data-stu-id="b958b-155">Finding a package</span></span>

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

<span data-ttu-id="b958b-156">Voir aussi [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="b958b-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="b958b-157">Dans Visual Studio 2013 et versions antérieures, utilisez la commande [Get-Package](../tools/ps-ref-get-package.md).</span><span class="sxs-lookup"><span data-stu-id="b958b-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="b958b-158">Disponibilité de la console</span><span class="sxs-lookup"><span data-stu-id="b958b-158">Availability of the console</span></span>

<span data-ttu-id="b958b-159">À partir de Visual Studio 2017, NuGet et le Gestionnaire de Package NuGet sont automatiquement installés lorsque vous sélectionnez. Charges de travail liées NET ; Vous pouvez également l’installer individuellement en vérifiant la **composants individuels > Outils de Code > Gestionnaire de package NuGet** option dans le programme d’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b958b-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="b958b-160">En outre, si vous n'avez pas le Gestionnaire de package NuGet dans Visual Studio 2015 et versions antérieures, vérifiez **Outils > Extensions et mises à jour...** et recherchez l’extension du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="b958b-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="b958b-161">Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l’extension directement à partir de [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="b958b-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="b958b-162">La Console du Gestionnaire de Package n’est pas actuellement disponible avec Visual Studio pour Mac.</span><span class="sxs-lookup"><span data-stu-id="b958b-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="b958b-163">Toutefois, les commandes équivalentes, sont disponibles via le [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b958b-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="b958b-164">Visual Studio pour Mac a une interface utilisateur pour la gestion des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="b958b-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="b958b-165">Consultez [, y compris un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b958b-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="b958b-166">La Console du Gestionnaire de Package n’est pas incluse avec Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b958b-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="b958b-167">Etendre la Console du Gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="b958b-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="b958b-168">Certains packages installent les nouvelles commandes de la console.</span><span class="sxs-lookup"><span data-stu-id="b958b-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="b958b-169">Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold` illustré ci-dessous, qui génère les contrôleurs MVC ASP.NET et des vues :</span><span class="sxs-lookup"><span data-stu-id="b958b-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installation et l’utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="b958b-171">Configurer un profil de NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="b958b-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="b958b-172">Un profil PowerShell vous permet de rendre les commandes couramment utilisées disponibles partout où vous utilisez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b958b-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="b958b-173">NuGet prend en charge un profil NuGet spécifique qui se trouve généralement à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="b958b-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="b958b-174">Pour trouver le profil, tapez `$profile` dans la console :</span><span class="sxs-lookup"><span data-stu-id="b958b-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="b958b-175">Pour plus d’informations, reportez-vous à [Windows PowerShell profils](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="b958b-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="b958b-176">Utiliser l’interface CLI de nuget.exe dans la console</span><span class="sxs-lookup"><span data-stu-id="b958b-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="b958b-177">Pour rendre [ CLI`nuget.exe`](nuget-exe-cli-reference.md) disponible dans la Console du Gestionnaire de package, installez le package [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console :</span><span class="sxs-lookup"><span data-stu-id="b958b-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
