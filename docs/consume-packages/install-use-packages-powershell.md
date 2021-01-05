---
title: Installer et gérer des packages NuGet à l’aide de la console Visual Studio
description: Instructions pour l’utilisation de la console du gestionnaire de package NuGet dans Visual Studio pour travailler avec des packages.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 31fa51bc017eaaf9306d5f267e5d4b0d7a15ec9c
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699836"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="8f066-103">Installer et gérer des packages avec la console du gestionnaire de package dans Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8f066-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="8f066-104">La console du gestionnaire de package NuGet vous permet d’utiliser des [commandes PowerShell NuGet](../reference/powershell-reference.md) pour rechercher, installer, désinstaller et mettre à jour des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f066-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="8f066-105">L’utilisation de la console est nécessaire dans les cas où l’interface utilisateur du gestionnaire de package n’offre aucun moyen d’effectuer une opération.</span><span class="sxs-lookup"><span data-stu-id="8f066-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="8f066-106">Pour utiliser les commandes CLI `nuget.exe` dans la console, consultez [Utilisation de l’interface CLI de nuget.exe dans la console](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="8f066-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="8f066-107">La console est intégrée dans Visual Studio sur Windows.</span><span class="sxs-lookup"><span data-stu-id="8f066-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="8f066-108">Elle n’est pas incluse dans Visual Studio pour Mac ou dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8f066-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="8f066-109">Les commandes répertoriées ici sont spécifiques à la console du gestionnaire de package dans Visual Studio, et diffèrent des [commandes du module Package Management](/powershell/module/packagemanagement/) qui sont disponibles dans un environnement PowerShell général.</span><span class="sxs-lookup"><span data-stu-id="8f066-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="8f066-110">Plus précisément, chaque environnement possède des commandes qui ne sont pas disponibles dans l’autre, et les commandes portant le même nom peuvent également différer dans leurs arguments spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8f066-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="8f066-111">Lorsque vous utilisez la console Package Management dans Visual Studio, les commandes et les arguments décrits dans cette rubrique s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="8f066-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="8f066-112">Rechercher et installer un package</span><span class="sxs-lookup"><span data-stu-id="8f066-112">Find and install a package</span></span>

<span data-ttu-id="8f066-113">Par exemple, la recherche et l’installation d’un package s’effectuent en trois étapes simples :</span><span class="sxs-lookup"><span data-stu-id="8f066-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="8f066-114">Ouvrez le projet/la solution dans Visual Studio, puis ouvrez la console à l’aide de la commande **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="8f066-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="8f066-115">Recherchez le package que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="8f066-115">Find the package you want to install.</span></span> <span data-ttu-id="8f066-116">Si vous le connaissez déjà ce cas, passez directement à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="8f066-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="8f066-117">Exécutez la commande d’installation :</span><span class="sxs-lookup"><span data-stu-id="8f066-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="8f066-118">Toutes les opérations qui sont disponibles dans la console peuvent également être effectuées à l’aide de l’[interface CLI NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8f066-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="8f066-119">Toutefois, les commandes de la console fonctionnent dans le contexte de Visual Studio et d’un projet/d’une solution enregistrés et accomplissent souvent plus que leurs commandes CLI équivalentes.</span><span class="sxs-lookup"><span data-stu-id="8f066-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="8f066-120">Par exemple, l’installation d’un package via la console ajoute une référence au projet, contrairement à la commande CLI.</span><span class="sxs-lookup"><span data-stu-id="8f066-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="8f066-121">Pour cette raison, les développeurs qui travaillent dans Visual Studio préfèrent généralement utiliser la console plutôt que l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="8f066-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="8f066-122">De nombreuses opérations de console dépendent d’une solution ouverte dans Visual Studio avec un nom de chemin connu.</span><span class="sxs-lookup"><span data-stu-id="8f066-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="8f066-123">Si votre solution est enregistrée ou que vous n’avez pas de solution, vous pouvez voir l’erreur « La solution n’est pas ouverte ou n’est pas enregistrée.</span><span class="sxs-lookup"><span data-stu-id="8f066-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="8f066-124">Vérifiez que vous disposez d’une solution ouverte et enregistrée. »</span><span class="sxs-lookup"><span data-stu-id="8f066-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="8f066-125">Ceci indique que la console ne peut pas déterminer le dossier de la solution.</span><span class="sxs-lookup"><span data-stu-id="8f066-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="8f066-126">L’enregistrement d’une solution non enregistrée, ou la création et l’enregistrement d’une solution si vous n’en avez pas une ouverte, devraient corriger l’erreur.</span><span class="sxs-lookup"><span data-stu-id="8f066-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="8f066-127">Ouverture de la console et des contrôles de la console</span><span class="sxs-lookup"><span data-stu-id="8f066-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="8f066-128">Ouvrez la console dans Visual Studio à l’aide de la commande **Outils > Gestionnaire de package NuGet > Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="8f066-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="8f066-129">La console est une fenêtre Visual Studio qui peut être organisée et positionnée comme vous le souhaitez (consultez [Personnaliser les dispositions de fenêtres dans Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="8f066-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="8f066-130">Par défaut, les commandes de la console fonctionnent sur une source de package et un projet spécifiques définis dans le contrôle en haut de la fenêtre :</span><span class="sxs-lookup"><span data-stu-id="8f066-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Contrôles de la console du gestionnaire de package pour la source et le projet du package](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="8f066-132">La sélection d’une autre source et/ou d’un autre projet de package modifie ces valeurs par défaut pour les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="8f066-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="8f066-133">Pour écraser ces paramètres sans modifier les valeurs par défaut, la plupart des commandes prennent en charge les options `-Source` et `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="8f066-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="8f066-134">Pour gérer les sources de packages, sélectionnez l’icône d’engrenage.</span><span class="sxs-lookup"><span data-stu-id="8f066-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="8f066-135">Il s’agit d’un raccourci vers la boîte de dialogue **Outils > Options > Gestionnaire de package NuGet > Sources des packages**, conformément à la description à la page [Interface utilisateur du gestionnaire de package](install-use-packages-visual-studio.md#package-sources).</span><span class="sxs-lookup"><span data-stu-id="8f066-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="8f066-136">Le contrôle situé à droite du sélecteur de projets efface également le contenu de la console :</span><span class="sxs-lookup"><span data-stu-id="8f066-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paramètres de la console du gestionnaire de package et contrôles d’effacement](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="8f066-138">Le bouton tout à droite interrompt une commande dont l’exécution dure longtemps.</span><span class="sxs-lookup"><span data-stu-id="8f066-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="8f066-139">Par exemple, l'exécution de listes `Get-Package -ListAvailable -PageSize 500` répertorie les 500 premiers packages sur la source par défaut (par exemple, nuget.org), ce qui peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="8f066-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Contrôle d’arrêt de la console du gestionnaire de package](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="8f066-141">Installer un package</span><span class="sxs-lookup"><span data-stu-id="8f066-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="8f066-142">Consultez [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f066-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="8f066-143">L’installation d’un package dans la console effectue les mêmes étapes que celles décrites dans [Processus d’installation d’un package](../concepts/package-installation-process.md), plus ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8f066-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="8f066-144">La console affiche les termes du contrat de licence applicables dans sa fenêtre et l’accord implicite.</span><span class="sxs-lookup"><span data-stu-id="8f066-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="8f066-145">Si vous n’acceptez pas les termes du contrat, vous devez désinstaller immédiatement le package.</span><span class="sxs-lookup"><span data-stu-id="8f066-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="8f066-146">Une référence au package est également ajoutée au fichier projet et s’affiche dans l’**Explorateur de solutions** sous le nœud **Références**. Vous devez enregistrer le projet pour voir les modifications directement dans le fichier projet.</span><span class="sxs-lookup"><span data-stu-id="8f066-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="8f066-147">Désinstaller un package</span><span class="sxs-lookup"><span data-stu-id="8f066-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="8f066-148">Consultez [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f066-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="8f066-149">Utilisez l’option [Get-Package](../reference/ps-reference/ps-ref-get-package.md) pour afficher tous les packages actuellement installés dans le projet par défaut si vous avez besoin de rechercher un identificateur.</span><span class="sxs-lookup"><span data-stu-id="8f066-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="8f066-150">La désinstallation d’un package effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8f066-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="8f066-151">Supprime les références au package provenant du projet (quel que soit le format de gestion utilisé).</span><span class="sxs-lookup"><span data-stu-id="8f066-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="8f066-152">Les références ne s’affichent plus dans l’**Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="8f066-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="8f066-153">(Vous devrez peut-être régénérer le projet pour le supprimer du dossier **Bin**.)</span><span class="sxs-lookup"><span data-stu-id="8f066-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="8f066-154">Annule toutes les modifications apportées à `app.config` ou à `web.config` lors de l’installation du package.</span><span class="sxs-lookup"><span data-stu-id="8f066-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="8f066-155">Supprime les dépendances précédemment installées si aucun package restant ne les utilise.</span><span class="sxs-lookup"><span data-stu-id="8f066-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="8f066-156">Mettre à jour un package</span><span class="sxs-lookup"><span data-stu-id="8f066-156">Update a package</span></span>

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

<span data-ttu-id="8f066-157">Consultez [Get-Package](../reference/ps-reference/ps-ref-get-package.md) et [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="8f066-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="8f066-158">Rechercher un package</span><span class="sxs-lookup"><span data-stu-id="8f066-158">Find a package</span></span>

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

<span data-ttu-id="8f066-159">Consultez [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f066-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="8f066-160">Dans Visual Studio 2013 et les versions antérieures, utilisez [Get-Package](../reference/ps-reference/ps-ref-get-package.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="8f066-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="8f066-161">Disponibilité de la console</span><span class="sxs-lookup"><span data-stu-id="8f066-161">Availability of the console</span></span>

<span data-ttu-id="8f066-162">À compter de Visual Studio 2017, NuGet et le gestionnaire de package NuGet sont automatiquement installés lorsque vous sélectionnez des charges de travail liées à .NET. Vous pouvez également les installer individuellement en cochant la case de l’option **Composants individuels > Outils de code > Gestionnaire de package NuGet** dans le programme d’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f066-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="8f066-163">Donc, si vous n’avez pas le gestionnaire de package NuGet dans Visual Studio 2015 et les versions antérieures, consultez **Outils > Extensions et mises à jour...** et recherchez l’extension pour le gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f066-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="8f066-164">Si vous ne parvenez pas à utiliser le programme d’installation des extensions dans Visual Studio, vous pouvez télécharger l’extension directement à partir de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .</span><span class="sxs-lookup"><span data-stu-id="8f066-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="8f066-165">La console du gestionnaire de package n’est actuellement pas disponible avec Visual Studio pour Mac.</span><span class="sxs-lookup"><span data-stu-id="8f066-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="8f066-166">Toutefois, les commandes équivalentes sont disponibles par le biais de l’interface [CLI NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8f066-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="8f066-167">Visual Studio pour Mac dispose d’une interface utilisateur pour la gestion des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f066-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="8f066-168">Consultez [Inclusion d’un package NuGet dans votre projet](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8f066-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="8f066-169">La console du gestionnaire de package n’est pas incluse dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8f066-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="8f066-170">Étendre la console du gestionnaire de package</span><span class="sxs-lookup"><span data-stu-id="8f066-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="8f066-171">Certains packages installent de nouvelles commandes pour la console.</span><span class="sxs-lookup"><span data-stu-id="8f066-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="8f066-172">Par exemple, `MvcScaffolding` crée des commandes telles que `Scaffold`, indiquée ci-dessous, qui génère des vues et des contrôleurs MVC ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="8f066-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installation et utilisation de MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="8f066-174">Configurer un profil PowerShell NuGet</span><span class="sxs-lookup"><span data-stu-id="8f066-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="8f066-175">Un profil PowerShell vous permet de mettre à disposition des commandes couramment utilisées partout où vous utilisez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f066-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="8f066-176">NuGet prend en charge un profil qui lui est spécifique et se trouve généralement à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="8f066-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="8f066-177">Pour rechercher le profil, tapez `$profile` dans la console :</span><span class="sxs-lookup"><span data-stu-id="8f066-177">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="8f066-178">Pour plus d’informations, consultez [Profils Windows PowerShell](/previous-versions//bb613488(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="8f066-178">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="8f066-179">Utiliser l’interface CLI nuget.exe dans la console</span><span class="sxs-lookup"><span data-stu-id="8f066-179">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="8f066-180">Pour rendre l' [ `nuget.exe` interface](../reference/nuget-exe-cli-reference.md) de ligne de commande disponible dans la console du gestionnaire de package, installez le package [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) à partir de la console :</span><span class="sxs-lookup"><span data-stu-id="8f066-180">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
